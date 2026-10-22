# KINH THÀNH GAME - HỒNG ĐỨC TU TIÊN LỘ V1

Tài liệu thiết kế tổng hợp, bản duyệt cuối trước khi code M1. Mọi con số trong file đã được chủ game duyệt qua bàn thảo từng hệ. Khi vá lỗi tuyệt đối không tự ý rút gọn hay bỏ tính năng đã duyệt; sửa bất kỳ con số nào phải được chủ game đồng ý.

## MỤC LỤC
0. Triết lý
1. Nguyên tắc kiến trúc và ghi chú code
2. Quy ước số liệu
3. Hệ Lõi Tính Toán (CORE)
4. Hệ Thời Gian
5. Hệ Tu Luyện
6. Hệ Kinh Tế
7. Hệ Tông Môn và Cơ Cấu Quyền Lực
8. Hệ Đan Độc và Kháng Dược
9. Hệ Tâm Cảnh và Chấp Niệm
10. Bốn nghề chế tác: Đan Dược, Vũ Khí Pháp Bảo, Phù Lục, Trận Pháp
11. Hệ Chiến Đấu, Thương Thế và Bảng Chỉ Số Nhân Vật
12. Hệ NPC và Quan Hệ
13. Hệ Chết Chóc và Đạo Tiêu
14. Hệ Không Gian và Mê Cung Cấm Địa
15. Hệ Biến Động Môi Trường
16. Hệ Thông Tin và Tin Đồn
17. Hệ Linh Áp và Chèn Ép
18. Hệ Ma Chiêu và Bẫy
19. Hệ Thiên Đạo và Tai Kiếp
20. Hệ Sinh Lý và Tẩy Tủy
21. Hệ Bảo Dưỡng và Khí Linh
22. Hệ Gia Tộc và Kế Thừa
23. Hệ Sinh Thái Yêu Tộc
24. Vai trò AI và hợp đồng AI-Engine
25. Cấu trúc 12 hồi và kiến trúc arc-module
26. Giao diện
27. Lộ trình M1-M4
28. Các hệ hoãn sang module Linh Giới trở lên

(Phần 1/5 gồm mục 0 đến mục 5. Các mục còn lại được bổ sung tiếp vào cùng file.)

## 0. TRIẾT LÝ
- Đồng nhân Phàm Nhân Tu Tiên: người chơi là nhân vật riêng, đi song song với Hàn Lập. Hàn Lập là NPC đặc biệt theo đúng timeline nguyên tác; cơ duyên của Hàn Lập không khả dụng cho người chơi.
- HARDCORE: chết là mất save. Tài nguyên khan hiếm, tu luyện chậm, đột phá thất bại có thể tàn phế. Không có chế độ dễ, không có nút an toàn.
- Tất định tuyệt đối: cùng input luôn ra cùng output. Mô hình "AI kể chuyện, engine quyết định": mọi con số do engine tính. AI chỉ được (1) dẫn truyện, mô tả, thoại NPC, (2) phiên dịch log khô thành văn phong nguyên tác. AI đề xuất sự kiện thì engine kiểm tra hợp lệ mới chạy. AI không chạm trực tiếp chỉ số, túi đồ, sinh mạng.
- Thế giới vận hành theo lợi ích, không cờ thiện ác. NPC dùng chung bảng chỉ số với người chơi, không được ưu tiên.
- Thưởng xảo quyệt, không thưởng liều lĩnh: chênh cảnh giới gần như tuyệt đối.

## 1. NGUYÊN TẮC KIẾN TRÚC VÀ GHI CHÚ CODE
- Mỗi hệ một module độc lập. Module không được đọc biến nội bộ của module khác: mọi giao tiếp qua hàm công khai có ghi chú hợp đồng (đầu vào, đầu ra, cam kết không đổi bất ngờ).
- Sự kiện đi qua đồng hồ CORE: hệ này phát sự kiện, hệ kia tự nghe và xử lý. Không hệ nào nhảy sang sửa ruột hệ khác.
- Đầu file index.html có MỤC LỤC MODULE: danh sách từng hệ, tên module code tương ứng, dòng bắt đầu.
- Mỗi module mở đầu bằng khối ghi chú thiết kế: tính năng đã duyệt, công thức, ngày duyệt, và dòng "tính năng đã qua kiểm thử - KHÔNG XÓA". Tính năng nhỏ bên trong cũng có ghi chú một dòng giải thích vì sao tồn tại.
- Mọi hằng số cân bằng đặt tên rõ ràng trong thanh ghi trung tâm, kèm chú thích nguồn duyệt. Không có con số ma chôn trong code.
- Mỗi hàm có biển tên: hệ sở hữu, đầu vào/đầu ra, hệ nào được phép gọi.
- Quy tắc vá lỗi: lỗi nằm trong một module thì chỉ sửa module đó, thay đổi nhỏ nhất có thể. Buộc phải chạm hai module thì tách hai thay đổi riêng, commit message ghi rõ từng bên đụng gì. Tuyệt đối không tái tạo toàn file, không rút gọn tính năng.
- Bộ test hồi quy: mỗi tính năng đã qua kiểm thử có một test tự động tương ứng; trước khi giao bản vá nào phải chạy toàn bộ test cũ, test cũ vỡ là phát hiện ngay chỗ đè nhau.
- Save có số phiên bản cấu trúc, dữ liệu chia theo module.
- Cuối file có LỊCH SỬ THAY ĐỔI: mỗi phiên bản ghi thêm/bỏ/sửa gì; bỏ cái gì phải nêu đích danh lý do và được chủ game đồng ý trước.

## 2. QUY ƯỚC SỐ LIỆU
- Toàn bộ nội bộ là số nguyên (fixed-point); thập phân chỉ là cách hiển thị. Lý do: số thực của máy tính cộng dồn bị lệch (0,1 cộng 0,2 khác 0,3), phá tính tất định và làm save cũ mở ra kết quả khác.
- Đơn vị nhỏ nhất từng loại: EXP 1/10000 điểm (ví dụ 123,4758 lưu thành nguyên 1234758); Đan Độc và Tâm Cảnh thang 0-100 bước 0,1 (lưu nguyên 0-1000); thời gian tính bằng phút, 1 ngày = 1440 phút; linh thạch nguyên theo hạ phẩm, 1 trung phẩm = 100 hạ phẩm; công lao, cảm tình NPC, số viên kháng dược đều nguyên.
- Nhân chia hệ số: hệ số lưu dạng phân số nguyên (1,5 = 3/2; 0,02 = 2/100), tính nhân trước chia sau rồi bỏ phần dư. Không bao giờ sinh dư số thập phân dài.
- Hiển thị qua một hàm format chung duy nhất: EXP hiện 2 chữ số lẻ, linh thạch hiện nguyên, thời gian hiện "Ngày 3 - canh Tý - tháng 2 - năm 1". Người chơi không bao giờ thấy số thô dài.
- Làm tròn chỉ xảy ra lúc hiển thị và lúc chốt (tiêu EXP để đột phá thì trừ đúng đơn vị nhỏ nhất, phần lẻ còn lại giữ tích lũy). Giữa chừng không làm tròn.

## 3. HỆ LÕI TÍNH TOÁN (CORE)
1. Số học fixed-point: mọi phép tính trong game bắt buộc đi qua đây.
2. RNG tất định một nguồn: cả game dùng MỘT bộ sinh số ngẫu nhiên duy nhất chạy theo seed thế giới; mọi lần roll ghi vào nhật ký engine (thời điểm, seed, kết quả). Cùng save luôn ra cùng kết quả; khi có bug mở log thấy chính xác chuỗi tính toán đã xảy ra.
3. Đồng hồ trung tâm: mọi hệ đăng ký sự kiện theo phút (đan xong lúc nào, deadline nhiệm vụ, kiếp đến ngày nào); time-skip là vòng lặp của CORE, không hệ nào tự đếm thời gian riêng.
4. Thanh ghi hệ số trung tâm: mọi hằng số cân bằng (độc D từng đan, hệ số thể chất, giá trị nghiệp...) tập trung một chỗ, mỗi hằng số có tên rõ và chú thích nguồn duyệt ngày nào.
5. Hàm kiểm định chung: một hàm check duy nhất (độ khó, chỉ số, biến động) dùng chung cho chiến đấu, độ kiếp, luyện đan thành bại, né đòn.
6. Format hiển thị chung.
Các hệ sở hữu công thức của mình nhưng bắt buộc gọi CORE khi tính, không tự chế phép tính riêng. AI chỉ đọc kết quả từ CORE, không bao giờ tự tính số.

## 4. HỆ THỜI GIAN
- 12 canh/ngày, 30 ngày/tháng, 12 tháng/năm. Đơn vị nhỏ nhất: phút.
- Hiển thị: "Ngày X - canh Y - tháng Z - năm N".
- Time-skip chỉ lặp lại hành động đã làm tại chính địa điểm đó; hết nguyên liệu hoặc hết linh thạch là DỪNG, không tự chuyển sang hành động khác.
- NPC có lịch trình theo canh (chi tiết mục 12).

## 5. HỆ TU LUYỆN
- Cảnh giới V1 hạ giới: Luyện Khí 13 tầng, Trúc Cơ, Kim Đan, Nguyên Anh, Hóa Thần.
- Linh căn, số ngày cần cho một chu thiên: thiên 1 / đơn 5 / song 12 / tam 25 / tạp ngũ 30 / tạp lục 36.
- 10 thể chất: Kiếm Đạo, Thần Lôi (x0,2), Mị Cốt, Thái Âm (đêm x2, ngày x0,5), Thuần Dương (ngược Thái Âm), Hỗn Nguyên (x1,5), Kim Cang Bất Hoại, Hấp Linh (x0,5), Băng Tâm Ngọc, Huyết Ma.
- Ngộ tính 1-10: ảnh hưởng tốc độ học công pháp và nghề chế tác (mức cân bằng chi tiết chốt ở M1).
- Công thức chu thiên: T = C_realm x LR x TH x TM x MT x DL, trong đó C_realm = hằng số tầng cảnh giới, LR = linh căn, TH = hệ số thể chất, TM = hệ số tâm cảnh (xem mục 9: 0,8 + tâm cảnh/250), MT = hệ số môi trường (mục 15), DL = hệ số đan và linh khí hỗ trợ.
- Mục tiêu cân bằng: tạp lục căn 25-40 năm để tới LK13; thiên linh căn 5-8 năm.
- Đột phá thất bại có hậu quả nặng theo cảnh: tẩu hỏa, thương nặng, tàn phế (chi tiết mục 11 và 19).
