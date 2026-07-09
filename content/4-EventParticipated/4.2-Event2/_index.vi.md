---
title: "Báo cáo sự kiện: AI Innovations & Cloud Foundations"
date: 2026-06-29
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

### Mục Đích Của Sự Kiện

- Cập nhật xu hướng thiết kế hệ thống tích hợp AI, đặc biệt là kiến trúc Multi-Agent và quản lý ngữ cảnh.
- Hiểu rõ bản chất kỹ thuật và cách tối ưu hóa các tham số của mô hình ngôn ngữ lớn (LLM).
- Chia sẻ giải pháp tối ưu chi phí và bảo mật hạ tầng mạng trên môi trường Cloud.
- Đúc kết kinh nghiệm thực chiến từ các cuộc thi Hackathon và quá trình phát triển sản phẩm thực tế.

### Danh Sách Diễn Giả

- **Vy Lam** - Senior Business Systems Analyst, VPBank
- **Duc Dao** - Solution Architect, Cloud Kinetics
- **Team VIB** - Đội thi tham gia sự kiện Lotus Hacks 2026
- **Nguyen Tuan Thinh** - DevOps Engineer
- **Tinh Truong** - Platform Engineer, GoTymeX
- **Pham Ng Hai Anh** - G-AsiaPacific Vietnam, AWS Community Builder

### Nội Dung Nổi Bật

#### Kiến Trúc Multi-Agent Cho Doanh Nghiệp

- Hệ thống chấm điểm tín dụng startup truyền thống thường thiếu dữ liệu lịch sử.
- Giải pháp Multi-Agent hoạt động như một hội đồng ảo với các Agent chuyên biệt (Financial Analyst, Risk Assessor...).
- Kết quả giúp giảm 95% thời gian và chi phí xử lý, tăng cường khả năng kiểm tra chéo và bảo mật so với Single Agent.

#### Bản Chất Phi Tất Định Của LLM

- Cài đặt Temperature = 0 không đảm bảo kết quả giống hệt nhau do sai số làm tròn siêu nhỏ trong các phép toán trên GPU.
- Khuyến nghị sử dụng Temperature = 0.1 để tránh vòng lặp.
- Nên kết hợp phương pháp chạy nhiều lần để bầu chọn kết quả và ép buộc đầu ra theo cấu trúc định dạng JSON.

#### Bài Học Từ Hackathon Lotus Hacks

- Quá trình 36 giờ xây dựng công cụ UTMorpho (Sketch2App) biến bản vẽ thành code giao diện.
- Những thách thức lớn bao gồm giới hạn Token của API, sự phình to phạm vi dự án và lỗi sinh code tràn lan từ AI.
- Bài học cốt lõi là duy trì sự đồng bộ trong nhóm và ưu tiên hoàn thiện giá trị cốt lõi trước.

#### Xây Dựng Nền Tảng Hạ Tầng Với CloudFront

- Nỗi lo về chi phí do lưu lượng tăng đột biến hoặc tấn công DDoS có thể được giải quyết qua mạng lưới Edge toàn cầu.
- Miễn phí hoàn toàn chi phí truyền tải dữ liệu (DTO) từ AWS Origins.
- Cung cấp tính năng Origin Cloaking qua Origin Access Control (OAC) để giấu kín máy chủ gốc khỏi mạng internet công cộng.

#### Tầm Quan Trọng Của Ngữ Cảnh Trong AI

- AI trả lời sai thường do ngữ cảnh được cung cấp quá kém hoặc nhiễu dữ liệu.
- Việc nhồi nhét tài liệu không liên quan gây tốn kém token và giảm độ chính xác.
- Xu hướng tương lai là chuyển từ các câu lệnh đơn lẻ sang hệ thống bộ nhớ ngữ cảnh để cá nhân hóa hiệu quả.

#### Ứng Dụng Amazon Q và Tự Động Kiểm Toán

- Amazon Q đóng vai trò trợ lý thống nhất, giúp tạo biên bản cuộc họp, lên lịch và truy xuất dữ liệu từ hơn 40 nguồn.
- Đảm bảo tuân thủ bảo mật và phân quyền (RBAC) khi doanh nghiệp áp dụng AI.
- Kết hợp GenAI để thực hiện kiểm toán bảo mật hạ tầng tự động trên các hệ thống đám mây.

### Những Gì Học Được

#### Tư Duy Kỹ Thuật Lõi

- Chấp nhận tính xác suất tự nhiên của các mô hình AI và chủ động xây dựng cơ chế xử lý lỗi, xác thực cấu trúc đầu ra.
- Hiểu được sự khác biệt giữa việc nhồi nhét dữ liệu thô và việc xây dựng một hệ thống ngữ cảnh có bộ nhớ hiệu quả.

#### Thiết Kế Hệ Thống

- Nắm bắt mô hình Multi-Agent để giải quyết các bài toán nghiệp vụ phức tạp đòi hỏi sự minh bạch và đối chiếu chéo.
- Hiểu rõ cách triển khai lớp bảo vệ hạ tầng ở mức Edge thay vì chỉ tập trung vào máy chủ ứng dụng nội bộ.

#### Chiến Lược Triển Khai

- Tránh tình trạng nhồi nhét quá nhiều tính năng (Scope Creep) trong giai đoạn đầu của dự án.
- Tận dụng các dịch vụ có sẵn như Lambda@Edge và CloudFront để xử lý failover linh hoạt.

### Ứng Dụng Vào Công Việc

- Cấu hình bắt buộc định dạng trả về JSON cho các luồng xử lý AI tích hợp trong các API backend để dễ dàng bóc tách dữ liệu và lưu trữ vào MongoDB.
- Áp dụng cơ chế Origin Access Control (OAC) kết hợp cùng kiến trúc mạng hiện tại để ẩn hoàn toàn các máy chủ chạy Spring Boot và Node.js khỏi internet, tăng cường bảo mật hệ thống.
- Thử nghiệm việc chia nhỏ logic xử lý phức tạp theo hướng Multi-Agent cho các module chẩn đoán hoặc phân tích, thay vì để một luồng xử lý duy nhất đảm nhiệm.
- Tận dụng Amazon Q để tự động hóa việc viết document và khởi tạo cấu trúc cho các kịch bản kiểm thử, tích hợp thẳng vào quy trình CI/CD trên GitHub Actions nhằm rút ngắn thời gian phát triển.

### Trải Nghiệm Trong Event

Tham gia sự kiện giúp tôi mở rộng góc nhìn từ việc chỉ viết code ứng dụng sang cách tư duy thiết kế hệ thống và tích hợp AI một cách bài bản. Một số trải nghiệm nổi bật:

#### Đào sâu về bản chất kỹ thuật của AI

- Các phiên trình bày không chỉ dừng lại ở mức độ ứng dụng mà còn đi sâu vào bản chất phần cứng, giải thích lý do tại sao LLM không mang tính tất định hoàn toàn, giúp tôi có cách thiết lập tham số thực tế hơn.

#### Tiếp cận kiến trúc hạ tầng hiện đại

- Hiểu rõ hơn về các kỹ thuật ẩn danh máy chủ gốc và kiểm soát luồng dữ liệu trên đám mây, một yếu tố cực kỳ quan trọng khi triển khai các hệ thống yêu cầu tính sẵn sàng cao và bảo mật chặt chẽ.

#### Học hỏi từ những bài toán thực tế

- Kinh nghiệm thực chiến từ đội thi Hackathon là minh chứng rõ ràng nhất cho việc giới hạn tính năng và quản lý rủi ro khi sử dụng API của bên thứ ba trong điều kiện áp lực thời gian.
- Cách tiếp cận hệ thống Multi-Agent của ngành ngân hàng mang lại nguồn cảm hứng lớn để tái cấu trúc lại các luồng xử lý dữ liệu truyền thống.

#### Bài học rút ra

- Không có một giải pháp công nghệ nào hoàn hảo tuyệt đối; việc hiểu rõ giới hạn của AI (như token limits, non-determinism) giúp xây dựng phần mềm vững chắc hơn.
- Việc tối ưu hóa chi phí hạ tầng cần được tính toán ngay từ khâu thiết kế mạng lưới Edge, thay vì chỉ tối ưu ở mức code ứng dụng.

> Sự kiện đã mang lại cho tôi những kiến thức chuyên sâu về cả AI và Cloud, đồng thời cung cấp các hướng dẫn thực tiễn để nâng cấp kiến trúc hệ thống, cải thiện khả năng mở rộng và độ an toàn cho các ứng dụng thực tế.
