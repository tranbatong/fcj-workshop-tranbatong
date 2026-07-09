---
title : "Landing Page & Authentication"
date : 2026-07-01
weight : 1
chapter : false
pre : " <b> 5.8.1. </b> "
---

Our system opens with a modern Landing Page and a secure user authentication flow using Amazon Cognito.
#### Landing Page Interface
![Landing Page Interface](/images/5-Workshop/5.8-Frontend-React/landing-page.png)
#### Register Interface
![Landing Page Interface](/images/5-Workshop/5.8-Frontend-React/register.png)
#### Email verification Interface
![Email verification Interface](/images/5-Workshop/5.8-Frontend-React/email-verification.png)
#### Login Interface
![Landing Page Interface](/images/5-Workshop/5.8-Frontend-React/login.png)
#### DataUpload Interface
![DataUpload Interface](/images/5-Workshop/5.8-Frontend-React/data-upload.png)


#### 1. Landing Page (src/components/LandingPage.jsx)
A welcoming interface with smooth animations that highlights the core features of IDPCloud.

```jsx
import React from 'react';
import { ArrowRight, FileText, Zap, Shield } from 'lucide-react';

const LandingPage = ({ onGetStarted }) => {
  return (
    <div className="min-h-screen bg-gradient-to-b from-gray-50 to-white text-gray-900 font-sans selection:bg-blue-200">
      {/* Navbar */}
      <nav className="container mx-auto px-6 py-6 flex justify-between items-center">
        <div className="text-3xl font-black tracking-tight text-blue-700">
          IDP<span className="text-orange-500">Cloud</span>
        </div>
        <div className="space-x-4">
          <button
            onClick={onGetStarted}
            className="px-6 py-2.5 text-blue-700 font-semibold hover:bg-blue-50 rounded-full transition"
          >
            Đăng nhập
          </button>
          <button
            onClick={onGetStarted}
            className="px-6 py-2.5 bg-blue-600 text-white font-semibold rounded-full hover:bg-blue-700 transition shadow-lg hover:shadow-blue-500/30 transform hover:-translate-y-0.5"
          >
            Bắt đầu miễn phí
          </button>
        </div>
      </nav>

      {/* Hero Section */}
      <section className="container mx-auto px-6 pt-20 pb-28 text-center">
        <div className="inline-flex items-center space-x-2 bg-blue-50 text-blue-700 px-4 py-2 rounded-full mb-8 font-medium text-sm border border-blue-100">
          <span className="relative flex h-3 w-3">
            <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-blue-400 opacity-75"></span>
            <span className="relative inline-flex rounded-full h-3 w-3 bg-blue-500"></span>
          </span>
          <span>Nền tảng xử lý tài liệu AI số 1</span>
        </div>
        
        <h1 className="text-5xl md:text-7xl font-extrabold tracking-tight mb-8 text-slate-900 leading-tight">
          Số hóa tài liệu <br className="hidden md:block" />
          <span className="text-transparent bg-clip-text bg-gradient-to-r from-blue-600 to-cyan-500">
            thông minh & tốc độ
          </span>
        </h1>
        
        <p className="text-xl md:text-2xl text-slate-600 mb-12 max-w-3xl mx-auto leading-relaxed">
          Tự động bóc tách dữ liệu từ hóa đơn, hợp đồng và chứng từ với sức mạnh của AI. Tiết kiệm 90% thời gian nhập liệu thủ công của bạn.
        </p>
        
        <div className="flex flex-col sm:flex-row justify-center items-center space-y-4 sm:space-y-0 sm:space-x-6">
          <button
            onClick={onGetStarted}
            className="flex items-center px-8 py-4 bg-gradient-to-r from-blue-600 to-blue-700 text-white font-bold rounded-full text-lg hover:from-blue-700 hover:to-blue-800 transition-all shadow-xl hover:shadow-blue-600/30 transform hover:-translate-y-1"
          >
            Trải nghiệm ngay
            <ArrowRight className="ml-2 group-hover:translate-x-1 transition-transform" size={24} />
          </button>
        </div>

        {/* Mockup Preview */}
        <div className="mt-20 mx-auto max-w-5xl relative">
          <div className="absolute inset-0 bg-gradient-to-t from-white via-transparent to-transparent z-10 h-full w-full pointer-events-none"></div>
          <div className="bg-white rounded-2xl shadow-2xl border border-gray-200 overflow-hidden transform transition hover:scale-[1.01] duration-500">
            <div className="bg-gray-100 border-b border-gray-200 p-4 flex items-center space-x-2">
              <div className="w-3 h-3 rounded-full bg-red-400"></div>
              <div className="w-3 h-3 rounded-full bg-yellow-400"></div>
              <div className="w-3 h-3 rounded-full bg-green-400"></div>
            </div>
            <div className="p-8 bg-slate-50/50">
              <div className="grid grid-cols-1 md:grid-cols-3 gap-6 opacity-80">
                <div className="h-40 bg-white rounded-xl border border-gray-100 shadow-sm animate-pulse"></div>
                <div className="h-40 bg-white rounded-xl border border-gray-100 shadow-sm animate-pulse delay-75"></div>
                <div className="h-40 bg-white rounded-xl border border-gray-100 shadow-sm animate-pulse delay-150"></div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Features Section */}
      <section className="bg-slate-50 py-24 border-t border-gray-200">
        <div className="container mx-auto px-6">
          <div className="text-center mb-16">
            <h2 className="text-3xl md:text-4xl font-bold text-slate-900 mb-4">
              Tại sao doanh nghiệp chọn IDPCloud?
            </h2>
            <p className="text-lg text-slate-600">
              Nâng cao hiệu suất với các công cụ tự động hóa toàn diện
            </p>
          </div>

          <div className="grid md:grid-cols-3 gap-10 max-w-6xl mx-auto">
            <div className="bg-white p-8 rounded-3xl border border-gray-100 hover:shadow-xl transition-all duration-300 hover:-translate-y-2 group">
              <div className="bg-blue-50 w-16 h-16 flex items-center justify-center rounded-2xl mb-8 text-blue-600 group-hover:scale-110 transition-transform">
                <Zap size={32} />
              </div>
              <h3 className="text-xl font-bold mb-4 text-slate-800">Xử lý chớp nhoáng</h3>
              <p className="text-slate-600 leading-relaxed">
                Hệ thống AI xử lý hàng ngàn hóa đơn mỗi phút. Từ lúc tải lên S3 đến lúc có dữ liệu chuẩn hóa chỉ mất chưa tới vài giây.
              </p>
            </div>
            
            <div className="bg-white p-8 rounded-3xl border border-gray-100 hover:shadow-xl transition-all duration-300 hover:-translate-y-2 group">
              <div className="bg-orange-50 w-16 h-16 flex items-center justify-center rounded-2xl mb-8 text-orange-600 group-hover:scale-110 transition-transform">
                <Shield size={32} />
              </div>
              <h3 className="text-xl font-bold mb-4 text-slate-800">Bảo mật AWS S3</h3>
              <p className="text-slate-600 leading-relaxed">
                Tài liệu của bạn được lưu trữ an toàn tuyệt đối trên hạ tầng Cloud của Amazon, đảm bảo tính riêng tư và bảo mật cấp doanh nghiệp.
              </p>
            </div>

            <div className="bg-white p-8 rounded-3xl border border-gray-100 hover:shadow-xl transition-all duration-300 hover:-translate-y-2 group">
              <div className="bg-cyan-50 w-16 h-16 flex items-center justify-center rounded-2xl mb-8 text-cyan-600 group-hover:scale-110 transition-transform">
                <FileText size={32} />
              </div>
              <h3 className="text-xl font-bold mb-4 text-slate-800">Quản lý trực quan</h3>
              <p className="text-slate-600 leading-relaxed">
                Theo dõi chi tiêu, quản lý danh mục và lịch sử hóa đơn một cách minh bạch với Dashboard thống kê chuyên nghiệp.
              </p>
            </div>
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-white border-t border-gray-200 py-12">
        <div className="container mx-auto px-6 flex flex-col md:flex-row justify-between items-center text-slate-500 text-sm">
          <div className="flex items-center space-x-2 mb-4 md:mb-0">
            <span className="font-bold text-lg text-slate-800">IDPCloud</span>
            <span>&copy; {new Date().getFullYear()}</span>
          </div>
          <div className="flex space-x-6">
            <a href="#" className="hover:text-blue-600 transition">Điều khoản sử dụng</a>
            <a href="#" className="hover:text-blue-600 transition">Chính sách bảo mật</a>
            <a href="#" className="hover:text-blue-600 transition">Liên hệ</a>
          </div>
        </div>
      </footer>
    </div>
  );
};

export default LandingPage;

```
### 2. Login & Authentication Component (src/components/Login.jsx)
This component handles the entire user lifecycle: Login, Registration, OTP Email Verification, and First-time Password Updates.
```jsx
import React, { useState } from "react";
import {
  AuthenticationDetails,
  CognitoUser,
  CognitoUserAttribute,
} from "amazon-cognito-identity-js";
import { userPool } from "../cognitoConfig";

export default function Login({ onLoginSuccess }) {
  // login | register | verify | newPassword
  const [authMode, setAuthMode] = useState("login");

  // States dùng chung
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");
  const [error, setError] = useState("");
  const [successMsg, setSuccessMsg] = useState("");
  const [isLoading, setIsLoading] = useState(false);

  // States cho Đăng ký & Đổi mật khẩu
  const [name, setName] = useState("");
  const [verificationCode, setVerificationCode] = useState("");
  const [cognitoUserObj, setCognitoUserObj] = useState(null);

  // 1. LUỒNG ĐĂNG NHẬP (LOGIN)
  const handleLoginSubmit = (e) => {
    e.preventDefault();
    if (!username || !password) {
      setError("Vui lòng nhập đầy đủ tài khoản và mật khẩu!");
      return;
    }

    setIsLoading(true);
    setError("");
    setSuccessMsg("");

    const authenticationData = { Username: username, Password: password };
    const authenticationDetails = new AuthenticationDetails(authenticationData);
    const userData = { Username: username, Pool: userPool };
    const cognitoUser = new CognitoUser(userData);

    cognitoUser.authenticateUser(authenticationDetails, {
      onSuccess: (result) => {
        setIsLoading(false);
        const idToken = result.getIdToken().getJwtToken();
        onLoginSuccess(idToken);
      },
      onFailure: (err) => {
        setIsLoading(false);
        console.error(err);
        if (err.code === "UserNotConfirmedException") {
          setError("Tài khoản chưa được xác thực. Vui lòng nhập mã OTP.");
          setAuthMode("verify");
        } else {
          setError(err.message || "Đăng nhập thất bại, vui lòng kiểm tra lại!");
        }
      },
      newPasswordRequired: (userAttributes, requiredAttributes) => {
        setIsLoading(false);
        setAuthMode("newPassword");
        setCognitoUserObj(cognitoUser);
      },
    });
  };

  // 2. LUỒNG ĐỔI MẬT KHẨU LẦN ĐẦU (DO ADMIN TẠO)
  const handleNewPasswordSubmit = (e) => {
    e.preventDefault();
    if (!password || !name) {
      setError("Vui lòng nhập đầy đủ Họ tên và Mật khẩu mới!");
      return;
    }

    setIsLoading(true);
    setError("");

    const requiredAttributes = { name: name };

    cognitoUserObj.completeNewPasswordChallenge(
      password, // Dùng chung state password cho mật khẩu mới
      requiredAttributes,
      {
        onSuccess: (result) => {
          setIsLoading(false);
          const idToken = result.getIdToken().getJwtToken();
          onLoginSuccess(idToken);
        },
        onFailure: (err) => {
          setIsLoading(false);
          setError("Đổi mật khẩu thất bại: " + err.message);
        },
      }
    );
  };

  // 3. LUỒNG ĐĂNG KÝ (REGISTER)
  const handleRegisterSubmit = (e) => {
    e.preventDefault();
    if (!username || !password || !name) {
      setError("Vui lòng điền đầy đủ thông tin!");
      return;
    }

    setIsLoading(true);
    setError("");
    setSuccessMsg("");

    const attributeList = [
      new CognitoUserAttribute({ Name: "email", Value: username }),
      new CognitoUserAttribute({ Name: "name", Value: name }),
    ];

    userPool.signUp(username, password, attributeList, null, (err, result) => {
      setIsLoading(false);
      if (err) {
        setError(err.message || "Đăng ký thất bại!");
        return;
      }
      setSuccessMsg("Đăng ký thành công! Vui lòng kiểm tra email để lấy mã OTP.");
      setAuthMode("verify"); // Chuyển sang màn hình nhập OTP
    });
  };

  // 4. LUỒNG XÁC THỰC OTP (VERIFY)
  const handleVerifySubmit = (e) => {
    e.preventDefault();
    if (!username || !verificationCode) {
      setError("Vui lòng nhập Email và mã OTP!");
      return;
    }

    setIsLoading(true);
    setError("");

    const userData = { Username: username, Pool: userPool };
    const cognitoUser = new CognitoUser(userData);

    cognitoUser.confirmRegistration(verificationCode, true, (err, result) => {
      setIsLoading(false);
      if (err) {
        setError(err.message || "Xác thực thất bại!");
        return;
      }
      setSuccessMsg("Xác thực thành công! Bạn đã có thể đăng nhập.");
      setAuthMode("login");
      setPassword(""); // Xóa password để người dùng nhập lại cho an toàn
    });
  };

  // HÀM RENDER GIAO DIỆN THEO authMode
  const renderForm = () => {
    if (authMode === "newPassword") {
      return (
        <form onSubmit={handleNewPasswordSubmit} className="space-y-4">
          <p className="text-center text-orange-600 mb-4 text-sm font-medium">
            Đây là lần đăng nhập đầu tiên. Vui lòng bổ sung thông tin!
          </p>
          <div>
            <label className="block text-sm font-medium text-gray-700">Họ và tên</label>
            <input
              type="text"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              value={name}
              onChange={(e) => setName(e.target.value)}
            />
          </div>
          <div>
            <label className="block text-sm font-medium text-gray-700">Mật khẩu mới</label>
            <input
              type="password"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
          </div>
          <button
            type="submit"
            disabled={isLoading}
            className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-orange-600 hover:bg-orange-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-orange-500 disabled:bg-orange-300"
          >
            {isLoading ? "Đang cập nhật..." : "Xác nhận thông tin"}
          </button>
        </form>
      );
    }

    if (authMode === "register") {
      return (
        <form onSubmit={handleRegisterSubmit} className="space-y-4">
          <p className="text-center text-gray-500 mb-6 text-sm">Tạo tài khoản mới</p>
          <div>
            <label className="block text-sm font-medium text-gray-700">Họ và tên</label>
            <input
              type="text"
              placeholder="VD: Nguyễn Văn A"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              value={name}
              onChange={(e) => setName(e.target.value)}
            />
          </div>
          <div>
            <label className="block text-sm font-medium text-gray-700">Email</label>
            <input
              type="email"
              placeholder="Nhập email của bạn"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
            />
          </div>
          <div>
            <label className="block text-sm font-medium text-gray-700">Mật khẩu</label>
            <input
              type="password"
              placeholder="Chữ hoa, thường, số và ký tự đặc biệt"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
            />
          </div>
          <button
            type="submit"
            disabled={isLoading}
            className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-green-600 hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500 disabled:bg-green-300"
          >
            {isLoading ? "Đang xử lý..." : "Đăng ký ngay"}
          </button>
          <div className="text-center mt-4">
            <span className="text-sm text-gray-600">Đã có tài khoản? </span>
            <button
              type="button"
              onClick={() => { setAuthMode("login"); setError(""); setSuccessMsg(""); }}
              className="text-sm text-blue-600 hover:underline"
            >
              Đăng nhập
            </button>
          </div>
        </form>
      );
    }

    if (authMode === "verify") {
      return (
        <form onSubmit={handleVerifySubmit} className="space-y-4">
          <p className="text-center text-gray-500 mb-6 text-sm">
            Nhập mã OTP gồm 6 chữ số đã được gửi đến Email của bạn.
          </p>
          <div>
            <label className="block text-sm font-medium text-gray-700">Email</label>
            <input
              type="email"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 bg-gray-50"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
            />
          </div>
          <div>
            <label className="block text-sm font-medium text-gray-700">Mã OTP</label>
            <input
              type="text"
              placeholder="123456"
              className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
              value={verificationCode}
              onChange={(e) => setVerificationCode(e.target.value)}
            />
          </div>
          <button
            type="submit"
            disabled={isLoading}
            className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 disabled:bg-indigo-300"
          >
            {isLoading ? "Đang xác thực..." : "Xác thực Email"}
          </button>
          <div className="text-center mt-4">
            <button
              type="button"
              onClick={() => { setAuthMode("login"); setError(""); setSuccessMsg(""); }}
              className="text-sm text-blue-600 hover:underline"
            >
              Quay lại Đăng nhập
            </button>
          </div>
        </form>
      );
    }

    // Default: login
    return (
      <form onSubmit={handleLoginSubmit} className="space-y-4">
        <p className="text-center text-gray-500 mb-6 text-sm">
          Vui lòng đăng nhập để sử dụng dịch vụ
        </p>
        <div>
          <label className="block text-sm font-medium text-gray-700">Tài khoản (Email)</label>
          <input
            type="text"
            className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
            value={username}
            onChange={(e) => setUsername(e.target.value)}
          />
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700">Mật khẩu</label>
          <input
            type="password"
            className="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
          />
        </div>
        <button
          type="submit"
          disabled={isLoading}
          className="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500 disabled:bg-blue-300"
        >
          {isLoading ? "Đang xác thực..." : "Đăng nhập"}
        </button>
        <div className="text-center mt-4">
          <span className="text-sm text-gray-600">Chưa có tài khoản? </span>
          <button
            type="button"
            onClick={() => { setAuthMode("register"); setError(""); setSuccessMsg(""); }}
            className="text-sm text-blue-600 hover:underline font-medium"
          >
            Đăng ký ngay
          </button>
        </div>
      </form>
    );
  };

  return (
    <div className="min-h-screen flex items-center justify-center bg-gray-100 px-4">
      <div className="max-w-md w-full bg-white rounded-lg shadow-md p-8">
        <h2 className="text-2xl font-bold text-center text-blue-600 mb-6">
          Hệ thống IDP Serverless
        </h2>

        {error && (
          <div className="bg-red-50 border border-red-200 text-red-600 px-4 py-3 rounded mb-4 text-sm text-center">
            {error}
          </div>
        )}

        {successMsg && (
          <div className="bg-green-50 border border-green-200 text-green-700 px-4 py-3 rounded mb-4 text-sm text-center">
            {successMsg}
          </div>
        )}

        {renderForm()}
      </div>
    </div>
  );
}

```