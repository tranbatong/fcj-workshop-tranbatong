---
title : "Bảng điều khiển (Dashboard)"
date : 2026-07-01
weight : 2
chapter : false
pre : " <b> 5.8.2. </b> "
---

Trái tim của ứng dụng Frontend là trang Dashboard. Tại đây, hệ thống sẽ kết nối với các API Gateway (`/invoices`, `/budget`, `/categories`, `/payments`) để vẽ biểu đồ thống kê bằng Recharts và quản lý lịch sử hóa đơn.

#### Dashboard Interface
![Dashboard Interface](/images/5-Workshop/5.8-Frontend-React/dashboard.png)

#### Dashboard Core (`src/components/Dashboard.jsx`)
Component này xử lý logic tính toán ngân sách, cảnh báo vượt mức chi tiêu, lọc công nợ và xuất dữ liệu ra file CSV.

*(Lưu ý: Đảm bảo bạn đã thay thế các đường link API_INVOICES, API_BUDGET... bằng Invoke URL thực tế của AWS API Gateway).*

```jsx
import React, { useState, useEffect } from "react";
import {
  BarChart,
  Bar,
  XAxis,
  YAxis,
  Tooltip,
  ResponsiveContainer,
  PieChart,
  Pie,
  Cell,
  Legend,
} from "recharts";
import { Edit, Search, Download } from "lucide-react";
import InvoiceEditModal from "./InvoiceEditModal";
import CategoryManager from "./CategoryManager";

const COLORS = ["#0088FE", "#00C49F", "#FFBB28", "#FF8042", "#8884d8"];

export default function Dashboard({ token, activeTab = "budget" }) {
  const [invoices, setInvoices] = useState([]);
  const [stats, setStats] = useState({ monthly: [], vendors: [] });
  // States cho tính năng Ngân sách (Budget)
  const [budget, setBudget] = useState(0);
  const [isEditingBudget, setIsEditingBudget] = useState(false);
  const [categories, setCategories] = useState([]);
  const [isLoading, setIsLoading] = useState(false);
  const [budgetInput, setBudgetInput] = useState("");

  // States cho tính năng Edit
  const [isModalOpen, setIsModalOpen] = useState(false);
  const [selectedInvoice, setSelectedInvoice] = useState(null);

  // States cho tính năng Tìm kiếm
  const [searchTerm, setSearchTerm] = useState("");
  const [error, setError] = useState("");

  // KIỂM TRA LẠI CHÍNH XÁC LINK API CỦA BẠN:
  const API_INVOICES =
    "https://xb9xtht5w1.execute-api.us-east-1.amazonaws.com/dev/invoices";
  const API_BUDGET = 
    "https://xb9xtht5w1.execute-api.us-east-1.amazonaws.com/dev/budget";
  const API_CATEGORIES = 
    "https://xb9xtht5w1.execute-api.us-east-1.amazonaws.com/dev/categories";
  const API_PAYMENTS = 
    "https://xb9xtht5w1.execute-api.us-east-1.amazonaws.com/dev/payments";

  useEffect(() => {
    fetchData();
  }, []);

  // TỰ ĐỘNG TÍNH TOÁN STATS MỖI KHI INVOICES THAY ĐỔI
  useEffect(() => {
    if (!invoices || invoices.length === 0) {
      setStats({ monthly: [], vendors: [] });
      return;
    }

    const monthlyMap = {};
    const categoryMap = {};

    invoices.forEach((inv) => {
      const categoryName = inv.Category || "Chưa phân loại";
      const amount = Number(inv.TotalAmount) || 0;

      // Cộng dồn theo category
      if (!categoryMap[categoryName]) categoryMap[categoryName] = 0;
      categoryMap[categoryName] += amount;

      // Cộng dồn theo tháng (Parse YYYY-MM)
      let monthKey = "Khác";
      if (inv.InvoiceDate && inv.InvoiceDate !== "N/A") {
        const matchDDMMYYYY = inv.InvoiceDate.match(/(\d{2})[\/\-](\d{2})[\/\-](\d{4})/);
        const matchYYYYMMDD = inv.InvoiceDate.match(/(\d{4})[\/\-](\d{2})[\/\-](\d{2})/);
        if (matchDDMMYYYY) monthKey = `${matchDDMMYYYY[3]}-${matchDDMMYYYY[2]}`;
        else if (matchYYYYMMDD) monthKey = `${matchYYYYMMDD[1]}-${matchYYYYMMDD[2]}`;
        else monthKey = inv.InvoiceDate.substring(0, 7); // Fallback
      }

      if (!monthlyMap[monthKey]) monthlyMap[monthKey] = 0;
      monthlyMap[monthKey] += amount;
    });

    const categoryArray = Object.keys(categoryMap).map((k) => ({ name: k, total: categoryMap[k] }));
    const monthlyArray = Object.keys(monthlyMap).map((k) => ({ month: k, total: monthlyMap[k] }));
    
    // Sắp xếp tháng tăng dần
    monthlyArray.sort((a, b) => a.month.localeCompare(b.month));

    setStats({ monthly: monthlyArray, categories: categoryArray });
  }, [invoices]);

  const fetchData = async () => {
    setIsLoading(true);
    try {
      const resInvoices = await fetch(API_INVOICES, { headers: { Authorization: token } });

      if (!resInvoices.ok)
        throw new Error("Không thể tải dữ liệu hóa đơn từ server.");

      const rawInvoices = await resInvoices.json();

      // Lột bỏ lớp vỏ bọc bên ngoài của API Gateway, ép kiểu chuỗi bên trong thành JSON
      const dataInvoices = rawInvoices.body
        ? JSON.parse(rawInvoices.body)
        : rawInvoices;
        
      let parsedInvoices = Array.isArray(dataInvoices) ? dataInvoices : [];

      // Gọi API lấy Công nợ (Payments)
      try {
        const resPayments = await fetch(API_PAYMENTS, { headers: { Authorization: token } });
        if (resPayments.ok) {
          const rawPayments = await resPayments.json();
          const dataPayments = rawPayments.body ? JSON.parse(rawPayments.body) : rawPayments;
          const paymentsDict = dataPayments.payments || {};
          
          // Merge dữ liệu payment vào invoices
          parsedInvoices = parsedInvoices.map(inv => ({
            ...inv,
            paymentStatus: paymentsDict[inv.id]?.status || "PAID", // Fallback là PAID nếu k có
            dueDate: paymentsDict[inv.id]?.dueDate || ""
          }));
        }
      } catch (errPayments) {
        console.error("Lỗi khi tải dữ liệu công nợ:", errPayments);
      }
      
      setInvoices(parsedInvoices);

      // Gọi API lấy Ngân sách (Budget)
      try {
        const resBudget = await fetch(API_BUDGET, { headers: { Authorization: token } });
        if (resBudget.ok) {
          const rawBudget = await resBudget.json();
          const dataBudget = rawBudget.body ? JSON.parse(rawBudget.body) : rawBudget;
          setBudget(dataBudget.monthlyBudget || 0);
        }
      } catch (errBudget) {
        console.error("Lỗi khi tải ngân sách:", errBudget);
      }

      // Gọi API lấy Danh mục (Categories)
      try {
        const resCategories = await fetch(API_CATEGORIES, { headers: { Authorization: token } });
        if (resCategories.ok) {
          const rawCategories = await resCategories.json();
          const dataCategories = rawCategories.body ? JSON.parse(rawCategories.body) : rawCategories;
          setCategories(dataCategories.categories || []);
        }
      } catch (errCat) {
        console.error("Lỗi khi tải danh mục:", errCat);
      }

    } catch (err) {
      console.error(err);
      setError("Có lỗi xảy ra: " + err.message);
    } finally {
      setIsLoading(false);
    }
  };

  const handleSaveBudget = async () => {
    try {
      const newBudget = Number(budgetInput);
      const response = await fetch(API_BUDGET, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: token,
        },
        body: JSON.stringify({ monthlyBudget: newBudget }),
      });

      if (response.ok) {
        setBudget(newBudget);
        setIsEditingBudget(false);
      } else {
        alert("Lỗi khi lưu ngân sách lên máy chủ!");
      }
    } catch (error) {
      console.error(error);
      alert("Lỗi kết nối khi lưu ngân sách");
    }
  };

  const handleEditClick = (invoice) => {
    setSelectedInvoice(invoice);
    setIsModalOpen(true);
  };

  const handleUpdateInvoice = async (updatedData) => {
    try {
      const response = await fetch(API_INVOICES, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: token,
        },
        body: JSON.stringify(updatedData),
      });

      if (!response.ok) {
        let errorMsg = "Lỗi khi cập nhật dữ liệu với Backend";
        try {
           const errData = await response.json();
           if (errData.error) errorMsg = `Lỗi Backend: ${errData.error}`;
        } catch(e) {}
        throw new Error(errorMsg);
      }

      // Cập nhật lại UI sau khi thành công (không cần fetch lại toàn bộ để tối ưu)
      setInvoices((prev) =>
        prev.map((inv) => (inv.id === updatedData.id ? { ...inv, ...updatedData } : inv))
      );
      
      // Bạn có thể cân nhắc gọi lại fetchData() nếu muốn update cả biểu đồ
      // fetchData(); 

    } catch (error) {
      console.error(error);
      throw error; // Ném lỗi ra để Modal bắt được và hiển thị
    }
  };

  const handleTogglePaymentStatus = async (invoiceId, currentStatus) => {
    const newStatus = currentStatus === "PAID" ? "UNPAID" : "PAID";
    
    // Cập nhật giao diện trước cho mượt (Optimistic UI update)
    setInvoices(prev => prev.map(inv => 
      inv.id === invoiceId ? { ...inv, paymentStatus: newStatus } : inv
    ));

    try {
      const response = await fetch(API_PAYMENTS, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: token,
        },
        body: JSON.stringify({ invoiceId, status: newStatus }),
      });

      if (!response.ok) {
        throw new Error("Lỗi cập nhật trạng thái");
      }
    } catch (error) {
      console.error(error);
      alert("Không thể cập nhật trạng thái thanh toán. Vui lòng thử lại!");
      // Rollback lại nếu lỗi
      setInvoices(prev => prev.map(inv => 
        inv.id === invoiceId ? { ...inv, paymentStatus: currentStatus } : inv
      ));
    }
  };

  const handleExportCSV = () => {
    if (!filteredInvoices || filteredInvoices.length === 0) return;
    
    // Tạo header cho CSV
    const headers = ["Nhà cung cấp", "Ngày HĐ", "Tổng tiền", "Mã số thuế"];
    
    // Map dữ liệu thành các dòng CSV
    const csvRows = filteredInvoices.map(inv => {
      return `"${inv.VendorName || ''}","${inv.InvoiceDate || ''}","${inv.TotalAmount || 0}","${inv.TaxID || ''}"`;
    });
    
    // Gộp header và dữ liệu
    const csvString = [headers.join(","), ...csvRows].join("\n");
    
    // Thêm BOM để Excel đọc được tiếng Việt có dấu
    const bom = "\uFEFF";
    const blob = new Blob([bom + csvString], { type: "text/csv;charset=utf-8;" });
    const url = URL.createObjectURL(blob);
    
    // Tạo thẻ a ẩn để trigger download
    const link = document.createElement("a");
    link.href = url;
    link.setAttribute("download", `bao-cao-hoa-don-${new Date().getTime()}.csv`);
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };

  const filteredInvoices = invoices.filter((inv) => {
    if (activeTab === "unpaid" && inv.paymentStatus !== "UNPAID") return false;
    
    const term = searchTerm.toLowerCase();
    return (
      (inv.VendorName || "").toLowerCase().includes(term) ||
      (inv.TaxID || "").toLowerCase().includes(term)
    );
  });

  if (isLoading)
    return (
      <div className="flex justify-center items-center h-full">
        <div className="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-600"></div>
      </div>
    );
  if (error)
    return (
      <div className="text-red-500 p-4 bg-red-50 rounded border border-red-200">
        {error}
      </div>
    );

  return (
    <div className="space-y-6">
      
      {activeTab === "categories" && (
        <CategoryManager 
          token={token} 
          categories={categories} 
          setCategories={setCategories} 
          API_CATEGORIES={API_CATEGORIES} 
        />
      )}

      {activeTab === "budget" && (
        <>
          <h2 className="text-2xl font-bold text-gray-800">Thống kê & Ngân sách</h2>

          {/* Thẻ Quản lý Ngân sách */}
      <div className="bg-white p-6 rounded-lg shadow-sm border border-gray-100">
        <div className="flex justify-between items-center mb-4">
          <h3 className="text-lg font-semibold text-gray-700">Ngân sách Tháng {new Date().toISOString().substring(0, 7)}</h3>
          {!isEditingBudget ? (
            <button 
              onClick={() => { setBudgetInput(budget || ""); setIsEditingBudget(true); }} 
              className="text-blue-600 hover:text-blue-800 text-sm font-medium transition"
            >
              Cài đặt ngân sách
            </button>
          ) : (
            <div className="flex items-center space-x-2">
              <input 
                type="number" 
                value={budgetInput} 
                onChange={e => setBudgetInput(e.target.value)} 
                className="border border-gray-300 rounded-md px-3 py-1.5 text-sm w-40 focus:ring-2 focus:ring-blue-500 outline-none" 
                placeholder="VD: 10000000" 
              />
              <button 
                onClick={handleSaveBudget} 
                className="bg-blue-600 text-white px-4 py-1.5 rounded-md text-sm hover:bg-blue-700 transition"
              >
                Lưu
              </button>
              <button 
                onClick={() => setIsEditingBudget(false)} 
                className="text-gray-500 text-sm hover:text-gray-700 font-medium px-2"
              >
                Hủy
              </button>
            </div>
          )}
        </div>
        
        {budget > 0 ? (() => {
          // Logic tính toán Progress Bar trực tiếp trong render để lấy số liệu mới nhất
          const currentMonthStr = new Date().toISOString().substring(0, 7);
          let currentSpent = 0;
          if (stats && stats.monthly) {
            const currentMonthData = stats.monthly.find(m => m.month === currentMonthStr);
            if (currentMonthData) currentSpent = currentMonthData.total;
          }
          
          const budgetPercentage = (currentSpent / budget) * 100;
          let progressColor = "bg-green-500";
          if (budgetPercentage >= 80 && budgetPercentage < 100) progressColor = "bg-yellow-500";
          else if (budgetPercentage >= 100) progressColor = "bg-red-500";

          return (
            <div>
              <div className="flex justify-between text-sm mb-2">
                <span className="font-medium text-gray-700">
                  Đã tiêu: <span className={budgetPercentage >= 100 ? "text-red-600 font-bold" : ""}>
                    {new Intl.NumberFormat("vi-VN", { style: "currency", currency: "VND" }).format(currentSpent)}
                  </span>
                </span>
                <span className="text-gray-500 font-medium">
                  Ngân sách: {new Intl.NumberFormat("vi-VN", { style: "currency", currency: "VND" }).format(budget)}
                </span>
              </div>
              <div className="w-full bg-gray-200 rounded-full h-3 overflow-hidden">
                <div 
                  className={`h-3 rounded-full transition-all duration-1000 ease-in-out ${progressColor}`} 
                  style={{ width: `${Math.min(budgetPercentage, 100)}%` }}
                ></div>
              </div>
              {budgetPercentage >= 100 && (
                <p className="text-red-600 text-sm mt-3 font-semibold flex items-center">
                  <span className="mr-1">⚠️</span> Cảnh báo: Bạn đã vượt quá ngân sách của tháng này!
                </p>
              )}
              {budgetPercentage >= 80 && budgetPercentage < 100 && (
                <p className="text-yellow-600 text-sm mt-3 font-semibold flex items-center">
                  <span className="mr-1">⚠️</span> Chú ý: Bạn sắp chạm ngưỡng ngân sách của tháng!
                </p>
              )}
            </div>
          );
        })() : (
          <div className="bg-blue-50 border border-blue-100 rounded-lg p-4 text-center">
            <p className="text-sm text-blue-800 font-medium">Bạn chưa cài đặt ngân sách cho tháng này.</p>
            <p className="text-xs text-blue-600 mt-1">Bấm "Cài đặt ngân sách" ở góc trên bên phải để bắt đầu kiểm soát chi tiêu của bạn!</p>
          </div>
        )}
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
        {/* Biểu đồ Cột */}
        <div className="bg-white p-6 rounded-lg shadow-sm border border-gray-100">
          <h3 className="text-lg font-semibold text-gray-700 mb-4">
            Chi phí theo tháng
          </h3>
          <div className="h-72">
            <ResponsiveContainer width="100%" height="100%">
              {/* Sử dụng optional chaining ?. để an toàn tuyệt đối */}
              <BarChart data={stats?.monthly || []}>
                <XAxis dataKey="month" />
                <YAxis
                  tickFormatter={(value) => `${(value / 1000000).toFixed(1)}M`}
                />
                <Tooltip
                  formatter={(value) =>
                    new Intl.NumberFormat("vi-VN", {
                      style: "currency",
                      currency: "VND",
                    }).format(value)
                  }
                />
                <Bar dataKey="total" fill="#3b82f6" radius={[4, 4, 0, 0]} />
              </BarChart>
            </ResponsiveContainer>
          </div>
        </div>

        {/* Biểu đồ Tròn */}
        <div className="bg-white p-6 rounded-lg shadow-sm border border-gray-100">
          <h3 className="text-lg font-semibold text-gray-700 mb-4">
            Tỷ trọng theo Danh mục
          </h3>
          <div className="h-72">
            <ResponsiveContainer width="100%" height="100%">
              <PieChart>
                <Pie
                  data={stats?.categories || []}
                  dataKey="total"
                  nameKey="name"
                  cx="50%"
                  cy="50%"
                  outerRadius={100}
                  label
                >
                  {(stats?.categories || []).map((entry, index) => (
                    <Cell
                      key={`cell-${index}`}
                      fill={COLORS[index % COLORS.length]}
                    />
                  ))}
                </Pie>
                <Tooltip
                  formatter={(value) =>
                    new Intl.NumberFormat("vi-VN", {
                      style: "currency",
                      currency: "VND",
                    }).format(value)
                  }
                />
                <Legend />
              </PieChart>
            </ResponsiveContainer>
          </div>
        </div>
      </div>
        </>
      )}

      {/* Bảng Dữ Liệu */}
      {(activeTab === "history" || activeTab === "unpaid") && (() => {
        // Lọc danh sách hóa đơn sắp đến hạn (UNPAID và còn <= 3 ngày)
        const upcomingInvoices = invoices.filter(inv => {
          if (inv.paymentStatus !== "UNPAID" || !inv.dueDate) return false;
          const dueTime = new Date(inv.dueDate).getTime();
          const nowTime = new Date().getTime();
          const diffDays = Math.ceil((dueTime - nowTime) / (1000 * 60 * 60 * 24));
          return diffDays <= 3;
        });

        return (
        <>
          <h2 className="text-2xl font-bold text-gray-800 mb-4">
            {activeTab === "unpaid" ? "Công nợ chưa thanh toán" : "Lịch sử hóa đơn"}
          </h2>
          
          {upcomingInvoices.length > 0 && (
            <div className="bg-red-50 border border-red-200 rounded-lg p-4 mb-6 shadow-sm">
              <h3 className="text-red-700 font-bold flex items-center mb-2">
                <span className="mr-2">⚠️</span> Cảnh báo: {upcomingInvoices.length} hóa đơn sắp đến hạn hoặc đã quá hạn!
              </h3>
              <ul className="list-disc pl-8 text-sm text-red-600 space-y-1">
                {upcomingInvoices.map(inv => (
                  <li key={inv.id}>
                    <strong>{inv.VendorName || "Chưa xác định"}</strong> - {new Intl.NumberFormat("vi-VN", { style: "currency", currency: "VND" }).format(inv.TotalAmount || 0)} - Hạn: <span className="font-bold underline">{inv.dueDate}</span>
                  </li>
                ))}
              </ul>
            </div>
          )}

          <div className="bg-white rounded-lg shadow-sm border border-gray-100 overflow-hidden">
            <div className="p-4 border-b border-gray-100 bg-gray-50 flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
              <div>
                <h3 className="text-lg font-semibold text-gray-700">
                  Lịch sử hóa đơn đã xử lý
                </h3>
                <span className="text-sm text-gray-500">
                  Hiển thị: {filteredInvoices.length} / {invoices.length} hóa đơn
                </span>
              </div>
              
              <div className="flex items-center space-x-3 w-full sm:w-auto">
                <div className="relative w-full sm:w-64">
                  <span className="absolute inset-y-0 left-0 pl-3 flex items-center text-gray-400">
                    <Search size={16} />
                  </span>
                  <input
                    type="text"
                    value={searchTerm}
                    onChange={(e) => setSearchTerm(e.target.value)}
                    placeholder="Tìm tên NCC hoặc MST..."
                    className="w-full pl-9 pr-4 py-2 text-sm border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition"
                  />
                </div>
                
                <button
                  onClick={handleExportCSV}
                  className="flex items-center space-x-2 bg-green-600 hover:bg-green-700 text-white px-4 py-2 rounded-lg text-sm font-medium transition shadow-sm whitespace-nowrap"
                >
                  <Download size={16} />
                  <span className="hidden sm:inline">Xuất CSV</span>
                </button>
              </div>
            </div>
            <div className="overflow-x-auto">
              <table className="w-full text-left text-sm text-gray-600">
                <thead className="bg-gray-50 text-gray-700 uppercase">
                  <tr>
                    <th className="px-6 py-3">Nhà cung cấp</th>
                    <th className="px-6 py-3">Ngày HĐ</th>
                    <th className="px-6 py-3">Tổng tiền</th>
                    <th className="px-6 py-3">Danh mục</th>
                    <th className="px-6 py-3 text-center">Hạn thanh toán</th>
                    <th className="px-6 py-3 text-center">Trạng thái TT</th>
                    <th className="px-6 py-3 text-center">Hành động</th>
                  </tr>
                </thead>
                <tbody>
                  {!filteredInvoices || filteredInvoices.length === 0 ? (
                    <tr>
                      <td colSpan="6" className="text-center py-8 text-gray-500">
                        {invoices.length === 0 
                          ? "Chưa có dữ liệu hoặc API trả về lỗi" 
                          : "Không tìm thấy hóa đơn nào phù hợp với từ khóa tìm kiếm."}
                      </td>
                    </tr>
                  ) : (
                    filteredInvoices.map((inv, idx) => (
                      <tr
                        key={idx}
                        className="border-b border-gray-50 hover:bg-gray-50 transition"
                      >
                        <td className="px-6 py-4 font-medium text-gray-900">
                          {inv.VendorName || "N/A"}
                          <div className="text-xs text-gray-500 font-normal mt-1">MST: {inv.TaxID || "N/A"}</div>
                        </td>
                        <td className="px-6 py-4">{inv.InvoiceDate || "N/A"}</td>
                        <td className="px-6 py-4 font-semibold text-blue-600">
                          {new Intl.NumberFormat("vi-VN", {
                            style: "currency",
                            currency: "VND",
                          }).format(inv.TotalAmount || 0)}
                        </td>
                        <td className="px-6 py-4 text-center">
                          <span className="bg-blue-100 text-blue-800 text-xs font-medium px-2.5 py-0.5 rounded">
                            {inv.Category || "Chưa phân loại"}
                          </span>
                        </td>
                        <td className="px-6 py-4 text-center font-medium text-gray-600">
                          {inv.dueDate || "N/A"}
                        </td>
                        <td className="px-6 py-4 text-center">
                          <button
                            onClick={() => handleTogglePaymentStatus(inv.id, inv.paymentStatus)}
                            className={`px-3 py-1 rounded-full text-xs font-bold border transition ${
                              inv.paymentStatus === "PAID" 
                                ? "bg-green-100 text-green-700 border-green-300 hover:bg-green-200" 
                                : "bg-red-100 text-red-700 border-red-300 hover:bg-red-200"
                            }`}
                          >
                            {inv.paymentStatus === "PAID" ? "Đã thanh toán" : "Chưa thanh toán"}
                          </button>
                        </td>
                        <td className="px-6 py-4 text-center">
                          <button
                            onClick={() => handleEditClick(inv)}
                            className="text-blue-600 hover:text-blue-800 hover:bg-blue-50 p-2 rounded-full transition flex items-center justify-center mx-auto"
                            title="Xem và Chỉnh sửa"
                          >
                            <Edit size={18} />
                          </button>
                        </td>
                      </tr>
                    ))
                  )}
                </tbody>
              </table>
            </div>
          </div>
        </>
      )})()}

      <InvoiceEditModal
        invoice={selectedInvoice}
        isOpen={isModalOpen}
        onClose={() => setIsModalOpen(false)}
        onSave={handleUpdateInvoice}
        token={token}
        categories={categories}
      />
    </div>
  );
}

```