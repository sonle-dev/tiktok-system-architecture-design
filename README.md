BẢN THIẾT KẾ KIẾN TRÚC: KIẾN TRÚC HÓA MẠNG XÃ HỘI TIKTOK

1. Cách 1: Phân tách theo Khả năng kinh doanh (Decomposition by Business Capability)
   Phương pháp này phân chia hệ thống theo các đơn vị và năng lực kinh doanh chức năng (Top-down), mỗi module là một dịch vụ độc lập chịu trách nhiệm trọn vẹn cho một mảng hoạt động của nền tảng:

- 1. Video & Content Management Service (Quản lý Nội dung Video):

Trách nhiệm: Tiếp nhận video tải lên từ người dùng, quản lý metadata (tiêu đề, hashtag, âm thanh đính kèm), lưu trữ thông tin video và kiểm soát trạng thái hiển thị (công khai, bạn bè, riêng tư).

Ranh giới: Không xử lý logic phân phối video lên bảng tin người dùng.

- 2. User & Social Graph Service (Quản lý Người dùng & Mạng lưới xã hội):

Trách nhiệm: Quản lý hồ sơ cá nhân (profile), thiết lập quan hệ bạn bè (Followers / Following), chặn người dùng (Block list) và danh sách liên hệ.

Ranh giới: Không quản lý tương tác chi tiết trên từng video.

- 3. Engagement & Interaction Service (Quản lý Tương tác & Cộng đồng):

Trách nhiệm: Xử lý toàn bộ các hành động tương tác thời gian thực của người dùng trên video: Thả tim (Like), Bình luận (Comment theo luồng), Chia sẻ (Share), Lưu video yêu thích (Bookmark).

Ranh giới: Không lưu trữ file video gốc hay can thiệp vào tài khoản thanh toán.

- 4. Feed & Recommendation Service (Dịch vụ Bảng tin & Gợi ý nội dung):

Trách nhiệm: Tạo và cung cấp luồng video vô tận trên trang "Dành cho bạn" (For You Page - FYP) và trang "Đang Follow" theo thời gian thực dựa trên sở thích và hành vi của người dùng.

Ranh giới: Đọc dữ liệu từ Video Service và Engagement Service để tính toán điểm số hiển thị, không trực tiếp lưu trữ video.

- 5. Advertising & Monetization Service (Quản lý Quảng cáo & Kiếm tiền):

Trách nhiệm: Quản lý các chiến dịch quảng cáo của nhãn hàng (In-Feed Ads, TopView Ads), đấu thầu vị trí hiển thị (Ad Bidding), xen kẽ quảng cáo vào luồng FYP và đo lường tỷ lệ chuyển đổi (CTR, Impression).

Ranh giới: Tách biệt với luồng video tự nhiên (organic content) của người dùng thông thường.

- 6. Live Streaming & Virtual Gifting Service (Phát trực tiếp & Quà tặng ảo):

Trách nhiệm: Quản lý phiên phát sóng trực tiếp (Livestream), phòng chat trực tiếp, cơ chế nạp xu và tặng quà ảo (Virtual Gifts) cho Creator theo thời gian thực.

Ranh giới: Sử dụng giao thức truyền thông độ trễ thấp (WebRTC, RTMP), tách biệt khỏi hạ tầng video ngắn tĩnh.

2. Cách 2: Phân tách theo Sub-domain (Domain-Driven Design)
   Cách tiếp cận này nhìn nhận hệ thống qua lăng kính giá trị chiến lược và mức độ quan trọng đối với sự sống còn của doanh nghiệp:

- 1. Core Domain (Miền cốt lõi - Vũ khí tạo nên vị thế độc tôn của TikTok)
   Tập trung nguồn lực tinh hoa nhất để nghiên cứu và tự phát triển (In-house R&D), tạo ra khoảng cách cạnh tranh mà đối thủ không thể sao chép dễ dàng:

For You Recommendation Algorithm (Thuật toán gợi ý cá nhân hóa FYP):

Trọng tâm giá trị của TikTok. Sử dụng mô hình học máy xử lý dữ liệu hành vi theo thời gian thực (thời gian dừng xem, tỷ lệ xem lại, tốc độ lướt qua) để liên tục điều chỉnh luồng nội dung gây nghiện cho người xem.

Content Moderation & Safety AI (AI Kiểm duyệt nội dung tự động):

Với hàng triệu video tải lên mỗi giờ, hệ thống Computer Vision và NLP xử lý nhận diện tức thì các nội dung vi phạm bản quyền, bạo lực, nhạy cảm để giữ nền tảng an toàn và tuân thủ pháp lý toàn cầu.

- 2. Supporting Domain (Miền hỗ trợ - Cần thiết cho vận hành nhưng không tạo đột phá)
   Các chức năng mang tính chất bổ trợ cho nghiệp vụ mạng xã hội. Thường được tự xây dựng để tương thích với hệ thống nội bộ nhưng áp dụng các mô hình kỹ thuật quen thuộc:

Social Interaction (Hệ thống Bình luận, Thả tim, Chia sẻ):

Cần thiết để giữ tính kết nối xã hội nhưng đây là các tính năng tiêu chuẩn của mọi mạng xã hội, không phải là lý do duy nhất khiến người dùng tải TikTok.

Creator Portal & Analytics (Bảng phân tích số liệu cho nhà sáng tạo):

Cung cấp thống kê lượt xem, nhân khẩu học người xem cho kênh. Được tùy biến theo tiêu chuẩn đo lường của TikTok.

- 3. Generic Domain (Miền phổ quát - Tiêu chuẩn hóa, có thể dùng giải pháp ngoài hoặc mã nguồn mở)
   Các dịch vụ nền tảng không tạo ra lợi thế cạnh tranh độc quyền. Doanh nghiệp nên tận dụng thư viện có sẵn, giải pháp đám mây hoặc công cụ chuẩn công nghiệp:

Video Transcoding & Encoding (Mã hóa và nén video):

Chuyển đổi video tải lên thành nhiều định dạng độ phân giải (360p, 720p, 1080p, H.264, H.265). Sử dụng các bộ công cụ chuẩn như FFmpeg, AWS Elemental MediaConvert hoặc giải pháp chuyên dụng từ hạ tầng đám mây.

Media Storage & CDN Distribution (Lưu trữ và mạng phân phối nội dung):

Hệ thống lưu trữ đối tượng (Object Storage như AWS S3) kết hợp mạng phân phối nội dung toàn cầu (Cloudflare, Akamai, Fastly) để phân phối video nhanh tới rìa người dùng.

Identity & Authentication (Xác thực và phân quyền):

Đăng nhập bằng số điện thoại, Gmail, Facebook, Apple ID theo chuẩn OAuth2/OpenID Connect.

3. So sánh: Cách chia nào giúp team phát triển nhanh hơn?
   Đánh giá theo từng góc độ phát triển:
   Cách 1 (Business Capability) giúp phát triển nhanh ở quy mô TỔ CHỨC TEAM:

Lý do: Cách chia này ánh xạ trực tiếp 1-1 với cơ cấu phòng ban và đội ngũ kỹ thuật (Team Video, Team Ads, Team LiveStream).

Lợi thế: Các team làm việc độc lập, sở hữu trọn vẹn vòng đời của service từ database đến API, triển khai CI/CD riêng rẽ mà không dẫm chân lên nhau, giúp mở rộng số lượng kỹ sư (scale nhân sự) và đẩy nhanh tiến độ bàn giao tính năng ở giai đoạn phát triển diện rộng.

Cách 2 (Sub-domain) giúp phát triển nhanh ở quy mô CHIẾN LƯỢC SẢN PHẨM & TẬP TRUNG TÀI NGUYÊN:

Lý do: Giúp lãnh đạo kỹ thuật xác định rõ cái gì cần tự code và cái gì nên mua ngoài/dùng mã nguồn mở.

Lợi thế: Bằng cách dùng ngay các giải pháp có sẵn cho Generic Domain (như CDN, Auth, Video Transcoder), đội ngũ tiết kiệm được hàng ngàn giờ kỹ thuật vô ích để dồn 100% nhân lực vào Core Domain (Thuật toán gợi ý). Điều này giúp sản phẩm đạt được lợi thế cạnh tranh vượt trội nhanh nhất khi ra mắt thị trường.

Nhận định tổng kết:
Để tối ưu tốc độ, cách tiếp cận chuẩn mực nhất trong thực tế là kết hợp cả hai:
Sử dụng Sub-domain (DDD) ở cấp độ chiến lược để quyết định Build vs Buy (tập trung tự làm Core, mua Generic), sau đó dùng Business Capability để tổ chức các nhóm phát triển độc lập (Stream-aligned teams) triển khai các dịch vụ tương ứng.