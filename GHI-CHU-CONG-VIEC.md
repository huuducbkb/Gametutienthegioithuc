# HỒNG ĐỨC TU TIÊN LỘ V1 - GHI CHÚ CÔNG VIỆC

File theo dõi công việc do Boba ghi và cập nhật sau mỗi bản, để chủ kho tiện theo dõi trên GitHub. Bản ghi chú chi tiết đầy đủ nằm trong Google Docs của chủ kho; file này là bản tóm tắt thường trực.

## HIỆN TRẠNG (cập nhật 27/10/2026)
- Bản hiện hành: V1.9, commit 13e2cabb67ee070babf959ff3c904152233b5980, nhánh v05-thu
- Link chơi ghim SHA: https://raw.githack.com/huuducbkb/Gametutienthegioithuc/13e2cabb67ee070babf959ff3c904152233b5980/index.html
- Nghiệm thu iPhone: V1.4 đến V1.8 chủ kho xác nhận xong ngày 27/10/2026; V1.9 chủ kho xác nhận OK chiều 27/10/2026
- Nhánh staging v19-staging-20261027: chủ kho quyết xóa chiều 27/10/2026 (nội dung đã có trong commit phát hành)

## QUY TẮC LÀM VIỆC
1. Phát hành: chủ kho duyệt qua approval card trước mỗi commit phát hành. Commit candidate lên nhánh staging để test raw là được phép; CẤM commit phát hành lên v05-thu trước khi duyệt. Mỗi bản một commit trực tiếp, chỉ index.html, không PR/merge, không chạm main/art/tài liệu.
2. Code: module độc lập, ghi chú thiết kế tiếng Việt ngay trong module; MỤC LỤC MODULE đầu file; LỊCH SỬ THAY ĐỔI cuối file; vá đúng module, không tái tạo file, không rút gọn tính năng đã duyệt; CJK/Cyrillic/emoji = 0; nhịp 1150ms; same seed = same kết quả; fixed-point nhân trước chia sau bỏ dư.
3. Test: hồi quy seed cố định, khung 414x896, chạy trước mỗi phát hành; mục tiêu 0 FAIL.
4. NÚT TEST (chốt chiều 27/10/2026): mỗi phần/hệ mới làm đều có một nút test thử riêng; có một nút test tổng chạy toàn bộ game, đặt trong tab Cài Đặt. Các nút này là công cụ admin để chủ kho kiểm tra game; khi game hoàn tất có thể bỏ đi hoặc ẩn, nên code thiết kế gọn để sau này bỏ/ẩn dễ.
5. Ghi chú: Google Docs ghi chi tiết sau mỗi bản; file này trên GitHub cập nhật song song để theo dõi nhanh.

## LỊCH SỬ PHÁT HÀNH (tóm tắt, mới nhất trước)
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
- Nhãn "CHƯA KHAI MỞ" tab Tông Môn: để ngỏ, chủ kho chưa có ý tưởng (27/10/2026).
- Lộ trình dài hạn đã bàn: NPC đồng đại timeline seed; uy tín tông môn + danh vọng giang hồ; thời tiết + dị tượng mùa cuối; thế gia defer.
- Hướng đã chốt: A (V0.10), B (Thần Niệm), D (gameplay); bỏ C.

## LINK
- Repo: https://github.com/huuducbkb/Gametutienthegioithuc
- Commit V1.9: https://github.com/huuducbkb/Gametutienthegioithuc/commit/13e2cabb67ee070babf959ff3c904152233b5980
- Bản raw V1.9: https://raw.githubusercontent.com/huuducbkb/Gametutienthegioithuc/13e2cabb67ee070babf959ff3c904152233b5980/index.html
