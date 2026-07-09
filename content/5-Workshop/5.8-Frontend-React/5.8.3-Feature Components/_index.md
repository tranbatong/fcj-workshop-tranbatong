---
title : "Feature Components"
date : 2026-07-01
weight : 3
chapter : false
pre : " <b> 5.8.3. </b> "
---

To support the Dashboard, we have two critical components that allow users to interact deeply with their data.

#### Category Manager Interface
![Category Manager Interface](/images/5-Workshop/5.8-Frontend-React/category.png)

#### 1. Category Manager (src/components/CategoryManager.jsx)
Allows users to define custom expense categories (e.g., Fuel, Entertainment) and seamlessly sync them with DynamoDB.

```jsx
import React, { useState, useEffect } from "react";
import { Plus, Trash2, Tag } from "lucide-react";

export default function CategoryManager({ token, categories, setCategories, API_CATEGORIES }) {
  const [newCategory, setNewCategory] = useState("");
  const [isLoading, setIsLoading] = useState(false);

  const handleAddCategory = async () => {
    if (!newCategory.trim()) return;
    
    // Kiểm tra trùng lặp
    if (categories.includes(newCategory.trim())) {
      alert("Danh mục này đã tồn tại!");
      return;
    }

    const updatedCategories = [...categories, newCategory.trim()];
    await saveCategories(updatedCategories);
    setNewCategory("");
  };

  const handleDeleteCategory = async (catToDelete) => {
    if (!window.confirm(`Bạn có chắc muốn xóa danh mục "${catToDelete}"? Các hóa đơn cũ mang danh mục này sẽ giữ nguyên.`)) return;
    
    const updatedCategories = categories.filter(c => c !== catToDelete);
    await saveCategories(updatedCategories);
  };

  const saveCategories = async (updatedCategories) => {
    setIsLoading(true);
    try {
      const response = await fetch(API_CATEGORIES, {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: token,
        },
        body: JSON.stringify({ categories: updatedCategories }),
      });

      if (response.ok) {
        setCategories(updatedCategories);
      } else {
        alert("Lỗi khi lưu danh mục!");
      }
    } catch (err) {
      console.error(err);
      alert("Lỗi kết nối khi lưu danh mục");
    } finally {
      setIsLoading(false);
    }
  };

  return (
    <div className="bg-white p-6 rounded-lg shadow-sm border border-gray-100 h-full">
      <div className="flex items-center gap-3 mb-6">
        <div className="p-3 bg-blue-100 rounded-lg text-blue-600">
          <Tag className="w-6 h-6" />
        </div>
        <div>
          <h2 className="text-xl font-bold text-gray-800">Quản lý Danh mục</h2>
          <p className="text-gray-500 text-sm">Tạo và chỉnh sửa các danh mục chi tiêu của riêng bạn</p>
        </div>
      </div>

      <div className="flex gap-2 mb-8">
        <input
          type="text"
          value={newCategory}
          onChange={(e) => setNewCategory(e.target.value)}
          placeholder="Nhập tên danh mục mới (Vd: Xăng xe)"
          className="flex-1 px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
          onKeyPress={(e) => e.key === "Enter" && handleAddCategory()}
        />
        <button
          onClick={handleAddCategory}
          disabled={isLoading}
          className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 disabled:bg-gray-400 flex items-center gap-2"
        >
          <Plus className="w-5 h-5" /> Thêm
        </button>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {categories.map((cat, idx) => (
          <div key={idx} className="flex justify-between items-center bg-gray-50 px-4 py-3 rounded-lg border border-gray-100">
            <span className="font-medium text-gray-700">{cat}</span>
            <button
              onClick={() => handleDeleteCategory(cat)}
              className="text-red-500 hover:text-red-700 p-1 hover:bg-red-50 rounded"
              title="Xóa danh mục"
            >
              <Trash2 className="w-5 h-5" />
            </button>
          </div>
        ))}
      </div>
      
      {categories.length === 0 && (
        <div className="text-center text-gray-500 py-10">
          Chưa có danh mục nào. Hãy thêm danh mục đầu tiên của bạn!
        </div>
      )}
    </div>
  );
}

```
#### 2. Invoice Edit Modal (src/components/InvoiceEditModal.jsx)
A highly advanced UX/UI feature: It displays the original document (Image/PDF) side-by-side with the AI-extracted results. Users can visually compare and correct any AI misidentifications before saving.
```jsx
import React, { useState, useEffect } from 'react';
import { X, Save, FileText, Image as ImageIcon } from 'lucide-react';

export default function InvoiceEditModal({ invoice, isOpen, onClose, onSave, categories = [] }) {
  const [formData, setFormData] = useState({
    id: '',
    VendorName: '',
    InvoiceDate: '',
    TotalAmount: '',
    TaxID: '',
    Category: ''
  });
  const [isSaving, setIsSaving] = useState(false);
  const [error, setError] = useState('');

  // Load data khi mở modal
  useEffect(() => {
    if (invoice) {
      setFormData({
        id: invoice.id || '',
        VendorName: invoice.VendorName || '',
        InvoiceDate: invoice.InvoiceDate || '',
        TotalAmount: invoice.TotalAmount || '',
        TaxID: invoice.TaxID || '',
        Category: invoice.Category || ''
      });
    }
  }, [invoice]);

  if (!isOpen || !invoice) return null;

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setIsSaving(true);
    setError('');

    try {
      // Đảm bảo TotalAmount là số
      const payload = {
        ...formData,
        TotalAmount: parseFloat(formData.TotalAmount) || 0
      };

      await onSave(payload);
      // Đóng modal do parent component quản lý thông qua onSave thành công
    } catch (err) {
      setError(err.message || "Lỗi khi lưu dữ liệu");
    } finally {
      setIsSaving(false);
    }
  };

  return (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50 backdrop-blur-sm p-4">
      <div className="bg-white rounded-xl shadow-2xl w-full max-w-6xl max-h-[90vh] flex flex-col overflow-hidden">
        
        {/* Header Modal */}
        <div className="flex justify-between items-center p-4 border-b border-gray-200 bg-gray-50">
          <h2 className="text-xl font-bold text-gray-800 flex items-center">
            <FileText className="mr-2 text-blue-600" />
            Xác nhận & Chỉnh sửa Dữ liệu
          </h2>
          <button onClick={onClose} className="p-2 text-gray-500 hover:bg-gray-200 hover:text-red-500 rounded-full transition">
            <X size={20} />
          </button>
        </div>

        {/* Nội dung Side-by-side */}
        <div className="flex flex-col md:flex-row flex-1 overflow-hidden">
          
          {/* CỘT TRÁI: HIỂN THỊ ẢNH GỐC */}
          <div className="md:w-1/2 p-4 bg-gray-100 border-r border-gray-200 overflow-y-auto flex flex-col items-center justify-start">
            <div className="w-full flex justify-between items-center mb-2">
              <span className="text-sm font-semibold text-gray-600">Tài liệu gốc</span>
            </div>
            {invoice.imageUrl ? (
              <div className="w-full bg-white rounded-lg shadow-sm border border-gray-300 p-2 overflow-hidden flex items-center justify-center min-h-[400px]">
                {invoice.imageUrl.toLowerCase().includes('.pdf') ? (
                  <iframe 
                    src={invoice.imageUrl} 
                    className="w-full h-[600px] border-0 rounded"
                    title="PDF Viewer"
                  />
                ) : (
                  <img 
                    src={invoice.imageUrl} 
                    alt="Invoice Document" 
                    className="max-w-full h-auto object-contain max-h-[700px] rounded"
                  />
                )}
              </div>
            ) : (
              <div className="flex flex-col items-center justify-center w-full h-[400px] bg-white border-2 border-dashed border-gray-300 rounded-lg text-gray-400">
                <ImageIcon size={48} className="mb-2 opacity-50" />
                <p>Không có ảnh hiển thị</p>
                <p className="text-xs mt-1">Backend chưa trả về URL của ảnh</p>
              </div>
            )}
          </div>

          {/* CỘT PHẢI: FORM CHỈNH SỬA */}
          <div className="md:w-1/2 p-6 overflow-y-auto bg-white">
            <div className="mb-6">
              <h3 className="text-lg font-semibold text-gray-800 mb-1">Kết quả bóc tách AI</h3>
              <p className="text-sm text-gray-500">Vui lòng đối chiếu với ảnh gốc bên trái và sửa lại nếu AI nhận diện sai.</p>
            </div>

            {error && (
              <div className="mb-4 p-3 bg-red-50 text-red-700 rounded-lg text-sm border border-red-200">
                {error}
              </div>
            )}

            <form onSubmit={handleSubmit} className="space-y-5">
              
              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">Tên nhà cung cấp</label>
                <input
                  type="text"
                  name="VendorName"
                  value={formData.VendorName}
                  onChange={handleChange}
                  className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition"
                  placeholder="Nhập tên công ty..."
                />
              </div>

              <div className="grid grid-cols-2 gap-4">
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Ngày hóa đơn</label>
                  <input
                    type="text"
                    name="InvoiceDate"
                    value={formData.InvoiceDate}
                    onChange={handleChange}
                    className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition"
                    placeholder="DD/MM/YYYY"
                  />
                </div>
                <div>
                  <label className="block text-sm font-medium text-gray-700 mb-1">Mã số thuế</label>
                  <input
                    type="text"
                    name="TaxID"
                    value={formData.TaxID}
                    onChange={handleChange}
                    className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition"
                    placeholder="Nhập mã số thuế..."
                  />
                </div>
              </div>

              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">Tổng tiền (VNĐ)</label>
                <div className="relative">
                  <span className="absolute inset-y-0 left-0 pl-3 flex items-center text-gray-500">
                    ₫
                  </span>
                  <input
                    type="number"
                    name="TotalAmount"
                    value={formData.TotalAmount}
                    onChange={handleChange}
                    className="w-full pl-8 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition font-semibold text-blue-600"
                  />
                </div>
              </div>

              <div>
                <label className="block text-sm font-medium text-gray-700 mb-1">Danh mục chi tiêu</label>
                <select
                  name="Category"
                  value={formData.Category}
                  onChange={handleChange}
                  className="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none transition bg-white"
                >
                  <option value="Chưa phân loại">-- Chưa phân loại --</option>
                  {categories.map((cat, idx) => (
                    <option key={idx} value={cat}>{cat}</option>
                  ))}
                  {/* Nếu AI phân loại ra 1 danh mục chưa có trong list, ta vẫn giữ hiển thị nó */}
                  {formData.Category && formData.Category !== "Chưa phân loại" && !categories.includes(formData.Category) && (
                    <option value={formData.Category}>{formData.Category} (Từ AI)</option>
                  )}
                </select>
              </div>

              <div className="pt-6 mt-4 border-t border-gray-100 flex justify-end space-x-3">
                <button
                  type="button"
                  onClick={onClose}
                  className="px-5 py-2.5 text-sm font-medium text-gray-700 bg-white border border-gray-300 rounded-lg hover:bg-gray-50 transition"
                  disabled={isSaving}
                >
                  Hủy bỏ
                </button>
                <button
                  type="submit"
                  disabled={isSaving || !formData.id}
                  className="flex items-center justify-center px-5 py-2.5 text-sm font-medium text-white bg-blue-600 rounded-lg hover:bg-blue-700 shadow-md transition disabled:opacity-50 disabled:cursor-not-allowed"
                >
                  {isSaving ? (
                    <span className="flex items-center">
                      <svg className="animate-spin -ml-1 mr-2 h-4 w-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                        <circle className="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" strokeWidth="4"></circle>
                        <path className="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                      </svg>
                      Đang lưu...
                    </span>
                  ) : (
                    <span className="flex items-center">
                      <Save size={18} className="mr-2" />
                      Lưu thay đổi
                    </span>
                  )}
                </button>
              </div>

            </form>
          </div>
        </div>
      </div>
    </div>
  );
}
```