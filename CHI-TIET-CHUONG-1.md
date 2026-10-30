# CHI TIẾT CHƯƠNG 1: KHÁM VẬT BA PHỦ

Mục đích: nội dung chi tiết từng nút chương 1, làm căn cứ viết code và tra ảnh art. Khớp sơ đồ nhánh trong SO-DO-COT-TRUYEN.md.
Trạng thái: ĐÃ DUYỆT TỔNG ngày 30/10/2026.

## QUYẾT ĐỊNH ĐÃ DUYỆT (30/10/2026)
1. Nút C1-03 được NGOẠI LỆ 4 lựa chọn (Đỗ, Tần, Vương, bỏ đi), không tách nút phụ.
2. Khóa tuyến diễn ra ngay tại C1-04, cuối chương 1.
3. Tên riêng đã duyệt: Thanh Thạch Trấn, Dẫn Khí Đan, linh thảo dị sắc.
4. Thêm trường save cotTruyenV1.
5. Chương 1 diễn ra từ ngày 1 đến khoảng ngày 90; cao trào trùng đợt dị tượng sẵn có V1.12 (60% ngày 86-90), không làm cơ chế mới.

## TRƯỜNG SAVE MỚI
cotTruyenV1: gói gồm phienBan (số 1), chuong (số chương hiện tại), nut (mã nút hiện tại), tuyen ("doat" hoặc "songsong" hoặc chưa có), the ("do" hoặc "tan" hoặc "vuong" hoặc "tanlap" hoặc chưa có), quanHeHanLap ("canhgiac" hoặc "thiencam" hoặc chưa có).
- Chỉ ghi khi có thay đổi. Hardcore chết là mất save vẫn theo luật cũ. Không đụng engine cũ, không thêm RNG mới.

## C1-MO "Buổi sáng ở Thanh Thạch Trấn" (ngày 1)
Điều kiện mở: bắt đầu game mới, sau khi chọn thân phận V1.5.
Ba biến thể văn bản, cùng đích:
- Tán tu: "Ba năm bôn ba, anh vẫn là tán tu không danh không phận, chưa có nổi một môn công pháp ra hồn. Sáng nay tỉnh dậy trong quán trọ tồi tàn, tiếng chuông tông môn vọng xuống từ Hoàng Phong Cốc xa xa."
- Thế gia: "Anh là con nhà buôn nhỏ ở Thanh Thạch Trấn. Cha mẹ sắm được một quyển dẫn khí quyết hạng thường, kỳ vọng anh bước vào con đường tu tiên."
- Tông môn: "Anh là đệ tử ngoại môn Hoàng Phong Cốc, hôm nay xuống núi lĩnh lệ phí hàng tháng."
Lựa chọn: không có, tự tiến tới C1-01.
Ảnh art: c1-mo--thi-tran.jpg (thị trấn nhỏ buổi sáng, núi mờ xa, thủy mặc).

## C1-01 "Tin ở chợ" (khoảng ngày 80)
Điều kiện mở: qua C1-MO.
Văn bản: "Chợ bỗng xôn xao: ba phủ Đỗ, Tần, Vương cùng mở cửa khảo vật, mời người hiền tài đến xem đồ. Lại nghe đồn mấy đêm nay trên trời có quang tượng lạ, ai cũng thấp thỏm."
Lựa chọn (đều tới C1-02, nan hoa hội tụ):
1. Đến phủ xem ngay.
2. Hỏi thăm kỹ trước: +2 uy tín; văn bản C1-04 thêm một câu dẫn về manh mối dị tượng.
3. Không màng, ở lại tu luyện: +50 EXP; đêm đó dị tượng xuất hiện, vẫn bị cuốn vào chuyện.
Ảnh art: c1-01--cho-truyen-tin.jpg (chợ, đám đông, bảng tin).

## C1-02 "Khám vật ba phủ" (ngày 81-85)
Điều kiện mở: qua C1-01.
Dùng nguyên trạng HD_V115: khảo sát theo thứ tự Đỗ, Tần, Vương; sổ kiến văn 0-3 chỉ trong phiên. Chỉ thêm lớp văn bản dẫn chuyện ngắn trước mỗi phủ.
Ảnh art: kiểm tra kho đã có ảnh ba phủ hay chưa; phủ nào thiếu sẽ tra thêm, phong cách đồng bộ bộ ảnh cảnh hiện có.

## C1-03 "Chọn chỗ đứng" (ngày 85)
Điều kiện mở: hoàn thành khám vật đủ ba phủ trong phiên.
Văn bản: "Khảo vật xong, cả ba phủ đều ngỏ ý giữ người tài ở lại."
Lựa chọn (NGOẠI LỆ 4 nút, đã duyệt):
1. Gia nhập họ Đỗ (Đan đạo): +100 điểm giaTocV114; tặng 3 viên Dẫn Khí Đan (đan bổ trợ tu luyện nhỏ).
2. Gia nhập họ Tần (Thương hội): +100 điểm giaTocV114; +50 linh thạch hạ.
3. Gia nhập họ Vương (Quyền quý): +100 điểm giaTocV114; +10 uy tín; được dẫn quen mặt người của tông môn.
4. Bỏ đi, tự thân lập nghiệp: +10 uy tín.
Cả bốn nhánh đều sang C1-04; ghi trường the tương ứng.
Ảnh art: kiểm tra ảnh sẵn có của ba phủ như mục C1-02.

## C1-04 "Đêm dị tượng" (ngày 86-90, đúng khung V1.12)
Điều kiện mở: qua C1-03 (mọi nhánh đều về đây).
Văn bản: "Quang tượng rực lên, một vết nứt linh khí hiện ở bãi đá ngoài trấn, trong đó một gốc linh thảo dị sắc phát huy. Bên vết nứt đã có một thanh niên áo vải dáng vẻ bình thường, ánh mắt tĩnh lặng, đang nhìn chăm chú." (Thanh niên là Hàn Lập, chưa nêu tên.)
Lựa chọn (điểm khóa tuyến, quy tắc (e)):
1. Lao vào giật linh thảo trước: + linh thảo dị sắc (tài nguyên, trị giá 30 linh thạch hạ); khóa tuyến ĐOẠT CƠ DUYÊN (tuyen = "doat"); Hàn Lập ghi nhớ mặt người chơi (quanHeHanLap = "canhgiac").
2. Lùi lại, nhường cho thanh niên: khóa tuyến SONG SONG (tuyen = "songsong"); hắn gật đầu cảm ơn rồi rời đi (quanHeHanLap = "thiencam"); +5 uy tín.
3. Bỏ qua linh thảo, chạy tới cứu người dân bị linh khí cuốn: khóa tuyến SONG SONG; +10 uy tín; chịu thương nhẹ (hardcore, nhưng không chết ở chương 1).
Ảnh art: c1-04--di-tuong.jpg (trời đêm quang tượng, vết nứt sáng); c1-04--han-lap.jpg (thanh niên áo vải lưng quay, không rõ mặt, thủy mặc).

## C1-KT "Kết chương 1" (khoảng ngày 90)
Văn bản tổng kết theo thế đã chọn và tuyến đã khóa; mở chương 2 theo hướng nhập Hoàng Phong Cốc, nơi người chơi gặp Hàn Lập trực tiếp (điểm (c) đã chốt).
Hệ quả: +150 EXP; ghi chương 2 vào cotTruyenV1.
Ảnh art: tùy biến theo thế, ưu tiên dùng ảnh cảnh sẵn có nếu khớp.

## DANH MỤC ẢNH ART CẦN TRA
1. c1-mo--thi-tran.jpg: thị trấn nhỏ buổi sáng, núi mờ xa, thủy mặc.
2. c1-01--cho-truyen-tin.jpg: chợ, đám đông, bảng tin.
3. Ảnh ba phủ: kiểm tra kho; thiếu thì tra thêm từng phủ.
4. c1-04--di-tuong.jpg: trời đêm quang tượng, vết nứt sáng.
5. c1-04--han-lap.jpg: thanh niên áo vải lưng quay, không rõ mặt.
Quy cách chung: JPEG 4:3, 1024x768, tối đa 250KB, thủy mặc, đặt theo cấu trúc thư mục art trong GHI-CHU-CONG-VIEC.md.

## CÔNG VIỆC TIẾP THEO
- Viết code module cốt truyện chương 1: module độc lập, ghi chú tiếng Việt, nút test trong khối tính năng, không sửa engine cũ.
- Tra ảnh art theo danh mục trên sau khi chốt bố cục từng cảnh.
