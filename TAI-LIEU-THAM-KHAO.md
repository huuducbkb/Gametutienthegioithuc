# TÀI LIỆU THAM KHẢO XÂY LẠI GAME

Ngày ghi nhận: 31/10/2026. Chủ kho quyết định thiết kế lại game hoàn toàn từ đầu. Bản cũ, mã và tài liệu sau đây là tư liệu tham khảo, không bắt buộc giữ nguyên engine cũ. Dừng hướng chèn module V2.0 vào file cũ và bỏ bản nháp HD_V20. Bản V1.15 trên main tiếp tục chạy bình thường; v116-staging giữ nguyên làm lưu trữ. Quyết định mới này thay các kế hoạch cũ nếu có mâu thuẫn.

## A. TỔNG QUAN

HỒNG ĐỨC TU TIÊN LỘ là game đồng nhân thế giới Phàm Nhân Tu Tiên của Vong Ngữ. Bản cũ là một file index.html chạy GitHub Pages tại https://huuducbkb.github.io/Gametutienthegioithuc/. Hardcore: nhân vật chết thì mất bản lưu. Thẩm mỹ giấy dó, mực tàu, thủy mặc; chủ kho không thích hình vector. Thiết kế mobile-first, khung tham chiếu 414 x 896 cho iPhone 11; kiểm tra giả lập không thay thế nghiệm thu máy thật.

Lịch sử V1.0 đến V1.16 xem GHI-CHU-CONG-VIEC.md và lịch sử mã; V1.15 đã phát hành, V1.16 chỉ trên nhánh lưu trữ. Quy tắc phiên bản: mỗi 10 bản vá tăng số lớn.

## B. THÔNG SỐ ENGINE CŨ

Đối chiếu index.html ghim 41e1b485 trên v116-staging, SHA-256 1143226e8c3a3105013118db057736525dbccb6006b349f70e675bb98dee105c. Đây là mô tả tham khảo, không bắt buộc giữ nguyên khi làm mới.

- Combat V04: điểm hành động mỗi hiệp = bỏ dư của (2 + thân pháp chia nguyên 25) nhân hệ số SL, rồi trừ linh áp và 1 điểm nếu thương nặng, tối thiểu 0. Công thức rút gọn 2 + TP/25 x SL được cung cấp thiếu ngoặc, chia nguyên và các khoản trừ; code là căn cứ. Linh áp phạt bên thấp hơn theo chênh đại cảnh, không phạt chênh tầng.
- Trúng: d100 + chính xác - né >= 60; code kẹp ngưỡng roll 6 đến 96, tương ứng xác suất trúng 95% đến 5%. Chí mạng roll riêng, ngưỡng 95 trừ phần cộng chí mạng của vũ khí, sát thương nhân 3/2; mô tả chỉ d100 >= 95 bỏ sót thưởng vũ khí.
- Luyện Khí có 13 tầng; ngưỡng lên tầng k là 1500 x k x k điểm EXP. Mỗi phiên hoàn tất tăng tối đa một tầng. EXP lưu theo tỉ lệ 1/10000; thanh tài nguyên dùng fixed-point và quy đổi riêng. Các thang như tâm cảnh và độc được kẹp trong khoảng 0 đến 1000, không coi đây là đơn vị lưu chung cho mọi thanh: code có THANH = 1440 và TOI_DA_THANH = 144000.
- 1 linh thạch trung bằng 100 linh thạch hạ. Uy tín có ngưỡng 0, 20, 60, 150, 300. Ba gia tộc Đỗ, Tần, Vương có các ngưỡng hiển thị 0, 500, 1500, 3500, 7000, trần 10000 điểm, hệ số 1.00, 1.10, 1.25, 1.40, 1.60; code lưu điểm gia tộc theo đơn vị 100.
- Thân phận Tán tu, Thế gia, Tông môn; giá bán đan tại Tông Môn tương ứng 95%, 100%, 105% giá cơ sở; các hệ số thân phận này không áp dụng trực tiếp cho kênh Phường Thị. Giá Phường Thị theo Xuân, Hạ, Thu, Đông là 100%, 90%, 110%, 120%; Tông Môn không chịu hệ số mùa này.
- Thời tiết có bốn trạng thái mỗi mùa, chọn theo seed; dị tượng có 60% cơ hội trong mỗi mùa, cửa sổ ngày 86 đến 90 của mùa. Lịch 360 ngày, bốn mùa, mỗi ngày 1440 phút. Code tuổi thọ lại tính năm 365 ngày, không đồng nhất với lịch 360 ngày.
- Tám hệ Kim, Mộc, Thủy, Hỏa, Thổ, Lôi, Băng, Phong. Dùng vũ khí vượt cấp hao linh lực gấp 2 và uy lực còn 70% khi đủ điều kiện.
- Bảy tông: Hoàng Phong Cốc, Yểm Nguyệt Tông, Hóa Đao Ổ, Thiên Khuyết Bảo, Cự Kiếm Môn, Thanh Hư Môn, Linh Thú Sơn.
- Registry cảnh V1.13 có ma, ten, loai, anh, moTa, nut, cha, biDanh. Yêu cầu gọi trường cuối là alias nhưng code thật dùng biDanh; không nhầm tên trường.
- Nhịp chiến đấu tự động 1150 ms; hiệu ứng bay số có bộ hẹn 1500 ms. Giao diện cũ có năm tab Nhân Vật, Tông Môn, Luyện Công, Thế Giới, Cài Đặt; Thế Giới có năm cửa. Lời tựa dùng Dancing Script 600, WOFF2 subset. Khi kiểm thử nhúng iframe sandbox opaque để cô lập, không coi môi trường đó là engine sản xuất. Năm nút chiến đấu có cơ chế khóa theo điều kiện; số nút không đồng nghĩa năm hành động engine độc lập.

## C. CỐT TRUYỆN

### Thế giới và hai tuyến

Hàn Lập là thiên mệnh chi tử, không bao giờ chết: người chơi có thể đánh bại nhưng không thể giết. Nếu cơ duyên của Hàn Lập bị đoạt, cơ duyên khác tự bù để truyện gốc không sụp. Người chơi là phàm nhân trong cùng thế giới, không thay thế nhân vật chính. Hai tuyến hình thành từ hành động: đoạt cơ duyên, thu hoạch lớn và rủi ro lớn, đối địch Hàn Lập; hoặc song song, không cướp cơ duyên, tự tìm đường riêng, an toàn hơn nhưng chậm hơn.

Game bắt đầu khi Hàn Lập đã nhập Hoàng Phong Cốc vài năm và còn thấp tầng; cả hai cùng lớn dần. Bảy tông khớp bảy phái gốc, Hoàng Phong Cốc gắn với Hàn Lập. Cao trào cuối giai đoạn là Ma Đạo Lục Tông xâm lược bảy phái. Trùm cuối về sau là Cổ Hoặc Kim, đạo tổ pháp tắc thời gian; người chơi cùng Hàn Lập là chìa khóa đánh bại hắn. Khung trận cuối Tiên giới chưa thiết kế chi tiết. Mỗi chương dự kiến 5 đến 8 nút chốt; nhánh hội tụ, không phân tầng vô hạn.

### Chương 1: Thanh Thạch Trấn, ngày 1 đến khoảng 90

Thanh Thạch Trấn nằm dưới chân Hoàng Phong Cốc. Sáu nút và hệ quả đã duyệt trong CHI-TIET-CHUONG-1.md:

1. C1-MO, ngày 1: sau khi chọn thân phận, ba biến thể cùng đích. Tán tu thức trong quán trọ nghèo; Thế gia là con nhà buôn có dẫn khí quyết; Tông môn là đệ tử ngoại môn xuống núi lĩnh lệ phí. Không có lựa chọn, tiếp tới C1-01.
2. C1-01, khoảng ngày 80: chợ loan tin ba phủ khảo vật và trời có quang tượng. Đến xem ngay; hỏi kỹ được +2 uy tín và manh mối dị tượng; ở lại tu luyện được +50 EXP. Cả ba hội tụ C1-02.
3. C1-02, ngày 81 đến 85 theo tài liệu: khám Đỗ, Tần, Vương đúng thứ tự bằng phiên HD_V115, sổ kiến văn 0 đến 3 chỉ tồn tại trong phiên, tải lại mất tiến độ. Code V1.16 mở từ ngày 81 trở đi, không đặt cận trên ngày 85; đây là khác biệt cần cân nhắc khi làm mới.
4. C1-03, ngày 85: sau khi đủ ba phủ, ngoại lệ bốn lựa chọn. Đỗ +100 điểm gia tộc và 3 Dẫn Khí Đan; Tần +100 và 50 linh thạch hạ; Vương +100 và 10 uy tín, được dẫn quen người tông môn; tự lập +10 uy tín. Ghi thế tương ứng, cả bốn hội tụ C1-04. Code mở từ ngày 85 trở đi, không chỉ đúng ngày 85.
5. C1-04, ngày 86 đến 90: linh thảo dị sắc ở vết nứt ngoài trấn, Hàn Lập xuất hiện trực tiếp dưới dạng thanh niên áo vải chưa nêu tên. Giật linh thảo được một linh thảo, giá trị tham khảo 30 linh thạch hạ, khóa tuyến đoạt và quan hệ cảnh giác; nhường khóa song song, +5 uy tín, quan hệ thiện cảm; cứu dân khóa song song, +10 uy tín và thương nhẹ, không chết ở chương 1. Code cho mở trong cửa sổ này khi không có dị tượng mùa hoặc từ ngày bắt đầu dị tượng nếu có; không phải điều kiện bắt buộc dị tượng xuất hiện.
6. C1-KT, khoảng ngày 90: tổng kết theo thế và tuyến, +150 EXP, mở chương 2 hướng tới Hoàng Phong Cốc, nơi người chơi gặp Hàn Lập. Code mở từ ngày 90 trở đi.

Save cũ cotTruyenV1 gồm phienBan, chuong, nut, tuyen, the, quanHeHanLap; vatPhamCotTruyenV116 chứa danKhi và linhThao. Các giá trị tuyến doat, songsong; thế do, tan, vuong, tanlap; quan hệ canhgiac, thiencam hoặc chưa có. Save này là tham khảo, không áp đặt vào game mới.

### Ảnh và mỹ thuật

Ba ảnh phủ đã có: art/canh/do-thi--phu.jpg, art/canh/tan-thi--phu.jpg, art/canh/vuong-thi--phu.jpg. Bốn ảnh chương 1 cần làm hoặc tra: c1-mo--thi-tran.jpg, c1-01--cho-truyen-tin.jpg, c1-04--di-tuong.jpg, c1-04--han-lap.jpg. Cảnh lần lượt là thị trấn sáng sớm, chợ đưa tin, dị tượng đêm và thanh niên áo vải quay lưng không rõ mặt. Dùng thủy mặc trên nền giấy dó, JPEG 4:3, 1024 x 768, dưới 250 KB mỗi ảnh.

## D. THIẾT KẾ V2.0 AI DẪN CHUYỆN ĐÃ DUYỆT

Lấy hướng thiết kế đã duyệt làm nền cho game mới, không tiếp tục bản nháp cũ. Game truyện tương tác văn bản kiểu cũ: đoạn văn liền mạch, lựa chọn đánh số dạng dòng chữ, ô nhập hành động tự do, nút GỬI và khung SYSTEM LOGS. Đọc là chính; khi có chiến đấu hay tu luyện, gọi màn combat tham khảo HD_V04 hoặc màn luyện công kèm ảnh, xong quay về đọc.

Luật cứng: engine tính trước mọi con số và trạng thái như trúng đòn, sát thương, EXP, linh thạch, uy tín, thương tích và chết sống; AI chỉ diễn đạt lời văn và lựa chọn dựa trên kết quả đó, không được tự quyết kết quả. AI trả JSON có cấu trúc; bịa số hoặc thưởng thì từ chối, thử lại và dùng văn bản fallback nếu vẫn không hợp lệ. Hardcore xóa save theo engine, AI không cứu được. Phần thưởng lớn như đan, linh thạch, uy tín, khóa tuyến chỉ tại nút chốt; gõ tự do không xin thêm được.

Hai ô Gemini và OpenRouter, mỗi ô nhận nhiều key ngăn bằng <>. Key chỉ lưu localStorage trên máy người chơi, tuyệt đối không đưa lên repo. Xoay key khi lỗi, hết hạn hoặc hết hạn mức; hết key nhà cung cấp này thì chuyển nhà cung cấp kia; hết cả hai hoặc mất mạng thì dùng văn bản chốt sẵn. Không có key vẫn chơi trọn vẹn.

Bài học HD_V20: bộ lọc danh sách từ cấm không đủ, kiểm thử đối kháng từng lọt câu bịa thưởng một phần bằng chữ. Thiết kế đóng mặc định: chỉ chấp nhận trường JSON đã biết; từ chối trường lạ và phần thưởng ngoài danh sách cho phép. Không để lời văn trở thành nguồn sự thật cho số liệu; cần đối chiếu chặt nội dung diễn đạt với kết quả engine, vì chỉ kiểm tra tên trường không tự chứng minh văn bản không bịa.

## E. QUY TẮC CODE VÀ QUY TRÌNH

- Tách module thành khối độc lập, ghi chú thiết kế tiếng Việt; MỤC LỤC MODULE ở đầu file, LỊCH SỬ THAY ĐỔI cuối file. Vá đúng module, không tái tạo toàn bộ file khi vá; không xóa tính năng đã duyệt.
- Dùng event bus và số liệu fixed-point; nhân trước, chia sau, bỏ dư theo quy tắc. Cùng seed cho cùng kết quả. Tự động chạy hồi quy seed cố định, nút test từng tính năng đặt trong chính khối tính năng và nút test tổng trong Cài Đặt. Tôn trọng reduced-motion; nhịp tham khảo 1150 ms.
- Chỉ dùng chữ Latin có dấu và ký hiệu cần thiết; không CJK, Cyrillic hoặc emoji. Mỗi 10 bản vá tăng số lớn.
- Mọi commit lên main phải có card duyệt trước, bot không tự duyệt. Với task này chỉ một commit tài liệu gồm hai tệp, không sửa index.html, không đụng v116-staging, không PR, merge hoặc xóa nhánh.
- Phương pháp tham khảo: chỉnh qua trang edit GitHub, dán bằng DataTransfer, đọc lại CodeMirror; phục vụ bản ghim qua raw.githack và kiểm thử trong iframe 414 x 896 khi làm game. Chỉ báo số test có trong báo cáo thực tế.
- Tránh nhầm: sandbox PASS không phải hồi quy engine thật; iframe quá hạn tải là lỗi runner, chưa chứng minh lỗi game; commit staging chưa phải phát hành live. Không khẳng định kết quả hoặc số lượng test khi chưa có bằng chứng.

## F. DANH MỤC NGUỒN

- Ghi chú và lịch sử: https://github.com/huuducbkb/Gametutienthegioithuc/blob/main/GHI-CHU-CONG-VIEC.md
- Sơ đồ cốt truyện: https://github.com/huuducbkb/Gametutienthegioithuc/blob/main/SO-DO-COT-TRUYEN.md
- Chi tiết chương 1: https://github.com/huuducbkb/Gametutienthegioithuc/blob/main/CHI-TIET-CHUONG-1.md
- index.html main, bản V1.15 live: https://github.com/huuducbkb/Gametutienthegioithuc/blob/main/index.html
- index.html v116-staging, bản cũ đầy đủ nhất có module chương 1: https://github.com/huuducbkb/Gametutienthegioithuc/blob/v116-staging/index.html
- Bản code ghim để đối chiếu: https://github.com/huuducbkb/Gametutienthegioithuc/blob/41e1b485/index.html
