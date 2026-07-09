---
title: "Báo cáo sự kiện: FCAJ Community Day - June 2026"
date: 2026-06-15
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch Sự kiện

Sự kiện "FCAJ Community Day - June 2026" là một diễn đàn công nghệ chuyên sâu, tập trung vào việc ứng dụng Trí tuệ Nhân tạo (AI) vào các hoạt động vận hành doanh nghiệp (Operations), từ hạ tầng Cloud, hỗ trợ khách hàng bằng giọng nói (Voice AI), quy trình DevOps, cho đến quản trị nhân sự (HR) và bảo mật hệ thống. Sự kiện mang tính thực tiễn cao với nhiều bài trình bày từ các chuyên gia đang trực tiếp làm việc tại các doanh nghiệp và startup công nghệ lớn.

### Mục Đích Của Sự Kiện
Sự kiện FCAJ Community Day là một hoạt động được tổ chức hàng tháng nhằm tạo không gian kết nối cộng đồng. Mục đích cốt lõi là để các diễn giả đến từ nhiều doanh nghiệp khác nhau chia sẻ những kiến thức, kinh nghiệm, trải nghiệm và góc nhìn thực tế nhất xuất phát từ môi trường làm việc doanh nghiệp. Sự kiện được tổ chức song song dưới hình thức offline (tại tầng 26 và 36) và livestream trên YouTube để tiếp cận đông đảo khán giả.

### Danh Sách Diễn Giả
Sự kiện quy tụ nhiều diễn giả từ các doanh nghiệp và tổ chức công nghệ khác nhau:
- **Anh Steve Trần**: Founder của Cloud Thinker.
- **Anh Hiếu Nghị**: Đại diện từ Renova Cloud.
- **Anh Kiệt**: Đến từ AWS Study Builder Group.
- **Anh Trung**: Founder & CEO của startup R AI (REI).
- **Chị Bảo & Anh Nguyên Nguyễn**: Cloud Engineer đến từ Cloud Kinetics.
- **Anh Trường (WEN) & Chị Minh Anh**: Team Solution từ Noventis.
- **Anh Toàn Nguyễn**: AWS Security Builder.

### Nội Dung Nổi Bật
Sự kiện được chia thành 4 chủ đề công nghệ vô cùng thiết thực:

#### 1. Định hướng nghề nghiệp & AI trong Cloud Operations
Anh Steve Trần chia sẻ về hành trình từ một sinh viên đến Founder, đồng thời nhấn mạnh việc AI đang thay đổi nhu cầu tuyển dụng. Các công cụ AI hiện nay hỗ trợ đắc lực trong việc xử lý kiến trúc hệ thống phức tạp, tối ưu hóa chi phí (FinOps) và tự động hóa bảo mật (Security). Anh cũng thảo luận sâu về sự ưu việt của kiến trúc Single-agent so với Multi-agent trong việc tối ưu cost và performance khi giải quyết các tác vụ hạ tầng.

#### 2. Voice AI Agent (AI Giọng nói)
Khai thác tiềm năng của Voice AI tại Việt Nam. Anh Trung (R AI) giải thích lý do không dùng mô hình Speech-to-Speech trực tiếp cho tiếng Việt mà dùng kiến trúc chuyển đổi: Giọng nói -> Văn bản (Text) -> LLM -> Văn bản -> Giọng nói nhằm kiểm soát chặt chẽ nội dung AI phát ngôn và hỗ trợ tính năng "tool calling" (ví dụ: tự động khóa thẻ ngân hàng). Các vấn đề ngữ cảnh tiếng Việt như phân biệt giới tính, cách xưng hô, giọng vùng miền và kỹ năng "ngắt lời" cũng được đào sâu.

#### 3. DevOps AI Agent
Nhóm Cloud Kinetics giới thiệu giải pháp dùng AI làm trợ lý phân tích lỗi hệ thống. Thay vì kỹ sư phải lặn lội tìm log ở nhiều nơi, DevOps AI Agent tự động tổng hợp, điều tra nguyên nhân gốc rễ (Root Cause Analysis) và đề xuất phương án khắc phục (Mitigation plan). Điều này giúp giảm thiểu đáng kể thời gian xử lý sự cố (MTTR) nhưng quyền quyết định cuối cùng vẫn thuộc về con người.

#### 4. Amazon Quick (Amazon Q) cho Doanh nghiệp & Bảo mật
- **Ứng dụng cho HR**: Giải quyết vấn đề đọc CV thủ công, cảm tính và rủi ro bảo mật dữ liệu. Công cụ AI có thể tự động trích xuất thông tin, đối chiếu CV với JD, chấm điểm kỹ năng và tạo báo cáo nhân sự chi tiết.
- **Bảo mật kết nối**: Để đảm bảo an toàn dữ liệu, anh Toàn Nguyễn trình bày kiến trúc kết nối AI với các server bên thứ ba (MCP Server) thông qua VPC Connection và Private Subnet, giúp dữ liệu nội bộ không bị phơi nhiễm ra Internet public.

### Những Gì Học Được

- **Sự dịch chuyển của Job Market**: AI không hoàn toàn thay thế con người, đặc biệt là trong các môi trường vận hành sản xuất (production) quan trọng. Tuy nhiên, thị trường sẽ ngừng tuyển dụng diện rộng các vị trí cấp thấp, mà chuyển sang tìm kiếm những kỹ sư senior thực sự giỏi, hoặc những người biết sử dụng AI thành thạo để tăng hiệu suất.
- **Tư duy giải quyết vấn đề bằng AI**: Khi xây dựng AI, không phải cứ dùng công nghệ mới nhất là tốt. Ví dụ, với tiếng Việt (low-resource language), việc chia nhỏ model (chuyển thành Text để xử lý bằng LLM) lại mang đến độ chính xác và khả năng tùy biến cao hơn.
- **Bảo mật là yếu tố sống còn**: Việc áp dụng AI vào doanh nghiệp lớn không chỉ là "AI làm được gì", mà còn là "AI có kết nối an toàn không". Thiết lập các VPC Private để bảo vệ luồng dữ liệu là kiến thức hạ tầng vô cùng quan trọng.

### Trải nghiệm trong event
Sự kiện mang lại một trải nghiệm học hỏi tuyệt vời và rất thực tế. Không khí diễn ra vô cùng sôi nổi với sự kết hợp giữa offline và nền tảng livestream. Các diễn giả không chỉ trình bày lý thuyết mà còn có những màn "Live Demo" trực tiếp, như demo hỏi đáp sản phẩm Apple bằng Voice Agent, hoặc demo AI xử lý khi hệ thống e-commerce bị tấn công DDoS. Mặc dù đôi lúc có các sự cố kỹ thuật nhỏ về micro hay dây cắm máy chiếu, nhưng điều đó càng làm tăng tính "thực tế" và gần gũi của sự kiện. Các phần Q&A và đố vui tặng quà (cà phê, đồ lưu niệm) cũng giúp kéo gần khoảng cách giữa những chuyên gia đi trước và các bạn sinh viên/nhân sự trẻ.
