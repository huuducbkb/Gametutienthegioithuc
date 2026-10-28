# HỒNG ĐỨC TU TIÊN LỘ V1 - GHI CHÚ CÔNG VIỆC

File theo dõi công việc do Boba ghi và cập nhật sau mỗi bản, để chủ kho tiện theo dõi trên GitHub. Bản ghi chú chi tiết đầy đủ nằm trong Google Docs của chủ kho; file này là bản tóm tắt thường trực.

## HIỆN TRẠNG (cập nhật 27/10/2026)
- Bản hiện hành: V1.10, commit ec448f1d394ec2f0fa595f65482dfc59432c9e80, nhánh v05-thu
- Link chơi ghim SHA: https://raw.githack.com/huuducbkb/Gametutienthegioithuc/ec448f1d394ec2f0fa595f65482dfc59432c9e80/index.html
- Nghiệm thu iPhone: V1.4 đến V1.10 vẫn còn nợ; chưa nghiệm thu iPhone vật lý V1.10
- Nhánh staging v19-staging-20261027: chủ kho quyết xóa chiều 27/10/2026 (nội dung đã có trong commit phát hành)

## QUY TẮC LÀM VIỆC
1. Phát hành: chủ kho duyệt qua approval card trước mỗi commit phát hành. Commit candidate lên nhánh staging để test raw là được phép; CẤM commit phát hành lên v05-thu trước khi duyệt. Mỗi bản một commit trực tiếp, chỉ index.html, không PR/merge, không chạm main/art/tài liệu.
2. Code: module độc lập, ghi chú thiết kế tiếng Việt ngay trong module; MỤC LỤC MODULE đầu file; LỊCH SỬ THAY ĐỔI cuối file; vá đúng module, không tái tạo file, không rút gọn tính năng đã duyệt; CJK/Cyrillic/emoji = 0; nhịp 1150ms; same seed = same kết quả; fixed-point nhân trước chia sau bỏ dư.
3. Test: hồi quy seed cố định, khung 414x896, chạy trước mỗi phát hành; mục tiêu 0 FAIL.
4. NÚT TEST (chốt chiều 27/10/2026): mỗi phần/hệ mới làm đều có một nút test thử riêng; có một nút test tổng chạy toàn bộ game, đặt trong tab Cài Đặt. Các nút này là công cụ admin để chủ kho kiểm tra game; khi game hoàn tất có thể bỏ đi hoặc ẩn, nên code thiết kế gọn để sau này bỏ/ẩn dễ.
5. Ghi chú: Google Docs ghi chi tiết sau mỗi bản; file này trên GitHub cập nhật song song để theo dõi nhanh.

## LỊCH SỬ PHÁT HÀNH (tóm tắt, mới nhất trước)
- V1.11 (28/10/2026, LIVE trên v05-thu, commit b0a7a8ad8505aebc9f1e474b4476c6b8a087f3a6): message "V1.11: Uy tín tông môn và Danh vọng giang hồ"; chỉ sửa index.html. index.html: 913.743 byte UTF-8, SHA-256 f53c4979df1deff7cf0264fb9da542d0e31ff905d301fca8bb2b968b2750c757, khớp đúng candidate staging 37cca35dff6ed8594c7a2e2217043316a3408a2c. Chuẩn test mới: 1387 PASS / 0 FAIL (26 bộ cũ 1265 + HD_V111_TEST 122). Nội dung: hệ Uy tín tông môn và Danh vọng giang hồ (module HD_V111) theo 7 điểm thiết kế chủ kho đã chốt all A: uy tín từ chu thiên/luyện đan/hiến đan có trần; danh vọng từ bán Phường Thị/đấu giá thành công; lời hẹn tự nguyện thưởng phạt 5/10/15/20, hạn 30 ngày; ngưỡng bậc 0/20/60/150/300; fixed-point 100, sàn 0, trần 10.000; seed miền riêng; save thêm danhTiengV111 (save cũ bắt đầu 0); UI đầy đủ Tông Môn và tóm tắt Nhân Vật; nút "Test HD_V111" trong khối Công cụ admin tab Cài Đặt. Sự cố phát hành: commit phát hành đầu e5a5240 sai nội dung do lỗi thao tác editor của Boba (raw 884.321 byte, thiếu module HD_V111, chỉ thêm 35 dòng đầu V1.10); đã sửa bằng đúng MỘT commit b0a7a8ad theo ngoại lệ A chủ kho duyệt sáng 28/10/2026; không reset/rewrite lịch sử; lịch sử phát hành V1.11 gồm 2 commit. Nhánh staging v111-staging-20261027 được giữ nguyên. Chưa nghiệm thu iPhone vật lý. Link chơi ghim SHA: https://raw.githack.com/huuducbkb/Gametutienthegioithuc/b0a7a8ad8505aebc9f1e474b4476c6b8a087f3a6/index.html
- V1.10 (27/10/2026, commit ec448f1d): thêm module HD_V110 "Công cụ admin" trong tab Cài Đặt: 26 nút test riêng (Test V02 đến Test V093, Test HD_V10, Test HD_V1, Test V11 đến Test V18, Test HD_V110) và nút "Test tổng toàn bộ game" chạy tuần tự 26 bộ; hai nhóm thu gọn "Legacy V02-V093" và "V1.0-V1.8"; cờ chung HD_V110.bat bật/ẩn cả khối, không lưu vào save. Mỗi bộ chạy trong iframe cô lập có storage riêng, lưu cờ HD_V1.bat, datBat(false) trước chạy, khôi phục trong finally; V09 nền riêng; không đổi ca test, kỳ vọng, engine, save, RNG, seed. Kết quả: 1265 PASS / 0 FAIL. Mốc 1105 là mốc cố định thời V1.5: 537 (V02-V093) + 197 (HD_V10) + 53 (HD_V1) + 318 (V11 27 + V12 59 + V13 55 + V14 91 + V15 86). Từ V1.6, V16/V17/V18 báo riêng (59+25+40=124), nên 25 bộ cũ hiện có 1229; thêm HD_V110_TEST mới 36 ca thành 1265. Không thay ca hay kỳ vọng bộ cũ; V09 giữ kỳ vọng TN 14. Số ca từng bộ, đều 0 FAIL: V02 94; V03 58; V04 92; V05 28; V06 40; V07 21; V071 11; V072 17; V08 27; V081 13; V082 14; V09 41; V091 20; V092 44; V093 17; HD_V10 197; HD_V1 53; V11 27; V12 59; V13 55; V14 91; V15 86; V16 59; V17 25; V18 40; HD_V110 36. Kiểm tra kèm: 36 script parse hợp lệ; CJK/Cyrillic/emoji = 0; 24 JPG nguyên đường dẫn và blob SHA; khối admin đo 414x896 không tràn ngang, không chồng nút, 5 nav hit-test đạt; save/localStorage/cờ chính không đổi sau khi chạy tổng; reduced-motion và nhịp 1150ms giữ nguyên. Chưa nghiệm thu iPhone vật lý. Parent V1.9: 13e2cabb67ee070babf959ff3c904152233b5980; message phát hành: "V1.10: khoi nut test tung he va test tong trong tab Cai Dat"; index.html: 877.084 byte UTF-8, SHA-256 f9e02ebaf4ad705117e22a3bf937277a60b6417dd1bf717cfaef35cfabc18f77.
- V1.9 (27/10/2026, commit 13e2cabb): vá bộ chạy hồi quy cũ chế độ tương thích HD_V1; sáu nút hồi quy cũ và đường gọi HD_V09.kiemThu giờ tắt HD_V1 trước test, khôi phục trong finally; kỳ vọng TN 14 giữ nguyên; legacy 1105 PASS / 0 FAIL.
- V1.8 (27/10/2026, commit ceb92f7e): sửa nút Xem thử/Dừng xem thử thành điều hướng; idle không đè nav, active cách nav 12px.
- V1.7 (26/10/2026, commit 6bd12841): thêm tranh nền phòng đấu giá (art/phien-dau-gia-dan-v17-q73.jpg).
- V1.6 (26/10/2026, commit ba47371): giá mùa Xuân/Hạ/Thu/Đông 100/90/110/120%, Tông Môn +5%/0%/-5%, đấu giá đan seed cố định ngày 30,60..., một API quyết toán.
- V1.5 (26/10/2026, commit 38957cf3): Việt hóa toàn bộ có dấu; hệ thân phận Tán tu/Đệ tử thế gia/Đệ tử tông môn; hai kênh bán đan.
- V1.4 (26/10/2026, commit 92c77a66): mở lò đan và kinh tế tông môn; 29 loại đan luyện được, quay phẩm 50/30/15/5.
- V1.3 (25/10/2026): tab Thế Giới 5 cửa placeholder; lịch 360 ngày 4 mùa; "Năm Hồng Đức thứ nhất".
- V1.0: TN thành thanh tài nguyên; vũ khí 4 bậc; luyện đan 10 TN/mẻ; HUD Linh Lực đỏ khi dưới 20%.
- V0.10: 13 tầng/đại cảnh; EXP 1500 x k^2; bảng chỉ số và tỷ lệ đột phá, tẩy tủy, trần linh lực, thọ nguyên.
- V0.9/V0.9.1: hệ đan dược hai trục 30 bản gốc 102 biến thể, độc tích lũ, kháng dược, phẩm chất bốn cấp; bố cục GUI mực tàu.
- V1.1, V1.2, V0.4 và các bản nền khác: chi tiết trong Google Docs.

## VIỆC ĐANG NỢ / TRỌNG
- Nghiệm thu iPhone vật lý V1.4 đến V1.10 vẫn còn nợ.
- Lộ trình tiếp theo: V1.11 = uy tín tông môn + danh vọng giang hồ; V1.12 = thời tiết + dị tượng mùa cuối; phương án B (NPC đồng đại timeline seed) tính sau.
- Nhãn "CHƯA KHAI MỞ" tab Tông Môn: chủ kho chưa có ý tưởng (27/10/2026).
- Hướng đã chốt: A (V0.10), B (Thần Niệm), D (gameplay); bỏ C.

## LINK
- Repo: https://github.com/huuducbkb/Gametutienthegioithuc
- Commit V1.10: https://github.com/huuducbkb/Gametutienthegioithuc/commit/ec448f1d394ec2f0fa595f65482dfc59432c9e80
- Bản raw V1.10: https://raw.githubusercontent.com/huuducbkb/Gametutienthegioithuc/ec448f1d394ec2f0fa595f65482dfc59432c9e80/index.html
