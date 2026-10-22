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

## 6. HỆ KINH TẾ
- Tiền tệ: linh thạch. 1 trung phẩm = 100 hạ phẩm. V1 hạ giới lưu hành chủ yếu hạ phẩm; trung phẩm xuất hiện từ tầm Trúc Cơ trở lên.
- Danh mục vật phẩm khoảng 350 loại, quản lý trong registry ITEMS thống nhất: mỗi vật có tên, phẩm cấp, công dụng, độc D (nếu là đan), giá tham chiếu.
- Giá cả do engine tính: giá cơ sở x hệ số vùng x hệ số cung cầu. Không định giá tay từng phiên. Cùng một nguyên liệu, vùng dư thì rẻ, vùng khan thì đắt: buôn tranh là nghề hợp pháp, nhưng đường xa có yêu thú và cướp.
- Nguồn thu của người chơi: lương theo chức vị (mục 7), bán đồ chế tác, làm nhiệm vụ, thưởng sự kiện, hái lượm (khan hiếm, điểm hái lượm có thể cạn).
- Nguồn chi: mua đan và nguyên liệu, công pháp, vũ khí pháp bảo, phù trận, thuê hoặc mua động phủ, hối lộ, chữa thương, giải độc.
- Khan hiếm là luật: nguyên liệu quý gắn với vùng nguy hiểm (Huyết Sắc Cấm Địa, lãnh thổ yêu thú). Sự kiện lớn (mỏ cạn, chiến tranh tông phái) làm giá biến động; ai có thông tin sớm thì có lợi thế thật (liên kết mục 16).
- Bảng giá chi tiết từng vật chốt ở M1 khi dựng registry ITEMS.

## 7. HỆ TÔNG MÔN VÀ CƠ CẤU QUYỀN LỰC
Người chơi nhập môn làm tạp dịch, chọn 1 trong 7 tông: Hoàng Phong Cốc, Yểm Nguyệt Tông, Hóa Đao Ổ, Thiên Khuyết Bảo, Cự Kiếm Môn, Thanh Hư Môn, Linh Thú Sơn. Mỗi tông có đặc trưng công pháp, phong cách ứng chiến và phe phái riêng (bảng chi tiết từng tông chốt ở M1).

### 7.1 Bảng chức vị, lương, khu vực
| Chức vị | Điều kiện | Lương/tháng | Quyền lợi chính |
|---|---|---|---|
| Tạp dịch | nhập môn | 2 hạ linh thạch | khu ở ngoại vi, tàng thư tầng 1 |
| Đệ tử ngoại môn | LK3 | 5 hạ + 1 Tụ Khí Đan | khu ngoại môn, tàng thư tầng 2 |
| Đệ tử nội môn | LK7 + 500 công lao | 20 hạ + 3 đan | khu nội môn, tàng thư tầng 3, được nhận nhiệm vụ tông |
| Đệ tử thân truyền | Trúc Cơ | 100 hạ (cộng thêm 1 trung/năm) | động phủ riêng, tàng thư tầng 4, ưu tiên danh ngạch bí cảnh |
| Trưởng lão | Kim Đan | 500 hạ | đỉnh riêng, được nhận đệ tử trực tiếp |
| Tông chủ | Nguyên Anh | - | quản toàn tông |

Mỗi bậc chức vị được vào khu vực tương ứng của tông; vào khu vượt bậc không có lý do là phạm luật tông.

### 7.2 Công lao
- Công lao là số nguyên, kiếm từ nhiệm vụ tông, sự kiện, chiến công.
- Chi dùng: đổi công pháp, vật tư, danh ngạch vào bí cảnh, điều kiện thăng chức vị.
- Công lao không đổi ra linh thạch trực tiếp. Hai đồng tiền tách bạch: linh thạch mua của cải, công lao mua địa vị.

### 7.3 Cấp trên và phe phái
- Mỗi đệ tử có cấp trên trực tiếp (quản sự đối với tạp dịch, trưởng lão đối với nội môn trở lên). Cấp trên quyết nhiệm vụ, đánh giá, có thể che chở hoặc gây khó dễ.
- Mỗi tông có 2-3 phe phái tranh chấp. Theo phe được ưu đãi (nhiệm vụ tốt, thăng tiến nhanh) nhưng bị ràng buộc (phải làm việc phe yêu cầu) và chịu liên đới khi phe thua. Đứng trung lập thì tự do nhưng khó thăng tiến.
- Cục diện phe phái thay đổi theo sự kiện (bầu quản sự, tông chủ bế quan, án oan án vu oán...).

### 7.4 Luật tông và chứng cứ
- Luật tông viết rõ các tội: giết đồng môn, trộm công pháp, tư thông Ma đạo, trộm mỏ... Xử phạt theo mức: trừ công lao, tước chức vị, phế tu vi, xử tử.
- Engine theo dõi chứng cứ thật: ai nhìn thấy việc gì, ai được nghe tin, dấu vết để lại. Bị tố mà chứng cứ mờ thì có khả năng thoát tội; vu oan cho người khác cũng là một đường chơi, nhưng bị lộ là vu oán thì phạm tội nặng.
- Phạm luật bí mật mà không để lại chứng cứ và không ai biết thì không bị phát hiện một cách máy móc.

### 7.5 Ma trận quan hệ 7 tông
- Bảng quan hệ tông với tông: đồng minh / hữu hảo / trung lập / cảnh giác / địch.
- Quan hệ thay đổi theo sự kiện lớn và cả hành vi cá nhân người chơi (giết đệ tử tông khác, giúp tông khác lập công...).
- Ảnh hưởng: giá mua bán giữa các vùng, nhiệm vụ liên tông, mời luận kiếm, chiến tranh tông phái.

### 7.6 Cống phẩm và thuế
- Quốc gia phàm phụ thuộc tông nộp cống phẩm (lương thực, quặng, tuyển người tài cho tông). Tông thu về và phân bổ lại qua lương và phát tài nguyên định kỳ.
- Đệ tử đóng góp theo chức vị: khai thác mỏ, canh gác, làm nhiệm vụ tông đều tính thành công lao.

### 7.7 Tài sản trọng yếu của tông
- Mỏ linh thạch: có phẩm cấp (hạ, trung), có thể CẠN theo khai thác. Mỏ là lợi ích chiến lược, nguyên nhân tranh đoạt giữa tông phái. Đi khai thác đổi công lao; trộm mỏ là tội trọng.
- Bí cảnh do tông kiểm soát danh ngạch: tiêu biểu là Huyết Sắc Cấm Địa, 30 năm mở một lần; danh ngạch chia theo chức vị, công lao và phe phái. Đây là cơ duyên đổi đời của hồi 2.
- Quốc gia phàm: vương triều phụ thuộc tông, quốc sư là cao thủ do tông cử. Việc triều chính phàm nhân tác động ngược lại tông (thuế nộp, khai mỏ, tuyển đệ tử).

### 7.8 Hệ sự kiện trong tông
- Định kỳ: Đại Khảo (thi đấu định hạng, thưởng phạt rõ), phát tài nguyên định kỳ, bầu quản sự, tông chủ bế quan (lúc phe phái nhúc nhích mạnh nhất).
- Đột phát: đệ tử mất tích, trộm công pháp (bạn cùng phòng có thể thành nghi phạm, hoặc chính là thủ phạm), mỏ bị tấn công, gián điệp Ma đạo tiềm nhập, luận kiếm khách quý.
- Hậu quả kéo dài: kết quả Đại Khảo đổi thứ hạng, bầu quản sự đổi thế lực phe lên xuống, xử oan người trong án gián điệp sinh oán hận âm thầm về sau.

## 8. HỆ ĐAN ĐỘC VÀ KHÁNG DƯỢC
- Thang độc D: 0-100, bước 0,1 (lưu nguyên 0-1000). Độc tích lũy theo từng loại đan, không trộn lẫn: mỗi loại đan có một cột D riêng.
- Bảng 9 đan phổ biến V1, mỗi đan có độ độc D cố định ghi trong thanh ghi hằng số CORE (giá trị D từng đan chốt ở M1 khi dựng bảng đan).
- Ngưỡng hiệu ứng của D: 30 suy yếu (giảm hệ số tu luyện và chiến đấu), 60 thương tổn nội tạng định kỳ, 90 nguy kịch, 100 tử vong.
- Ngoại lệ lúc D chạm 100: nếu cứu kịp lúc (đan giải độc xứng tầm hoặc NPC y thuật đủ cấp) thì sống sót nhưng D chỉ reset về 60, không về 0. Một lần chạm cửa tử là để lại di chứng.
- Kháng dược: mỗi loại đan có bộ đếm kháng riêng n (số viên đã dùng), hiệu quả giảm theo công thức 1/(1+0,02n). Càng dùng nhiều cùng một đan, càng về sau càng kém; buộc người chơi xen kẽ đan khác hoặc nghỉ xả kháng.
- Xả độc và xả kháng nhiều cách: ngừng dùng đan một thời gian (n giảm dần theo tháng), đan giải độc, tẩy tủy (mục 20), linh tuyền đặc biệt. Mỗi cách có chi phí và tốc độ riêng.
- Đan hỗ trợ tu luyện là con dao hai lưỡi: tăng tốc ngắn hạn nhưng tích độc D và kháng dược dài hạn. Đây là trục căng thẳng kinh điển của cả hệ.

## 9. HỆ TÂM CẢNH VÀ CHẤP NIỆM
- Tâm cảnh thang 0-100, khởi điểm 70. Lưu nguyên 0-1000, bước 0,1.
- Tâm cảnh chi phối: hệ số tu luyện TM = 0,8 + TC/250 (TC 100 ra 1,2, TC 50 ra 1,0); khả năng kháng Tâm Ma Kiếp; một số cửa ngộ công pháp yêu cầu tầm tâm cảnh.
- Bảng 8 chấp niệm: mỗi chấp niệm là một niềm tin hoặc ràng buộc cá nhân (tham sống sợ chết, hiếu thắng, tình nghĩa, báo thù...). Mỗi chấp niệm có hai cột: giữ thì tâm cảnh và hiệu ứng thay đổi thế nào, buông thì thế nào. Danh sách 8 chấp niệm cụ thể chốt ở M1.
- Chấp niệm là lựa chọn nhân vật, không có đáp án đúng: giữ chấp niệm thường giảm tâm cảnh nhưng đổi lại hiệu ứng thực chiến hoặc cơ hội nhất định; buông chấp niệm tăng tâm cảnh nhưng phải trả giá thật (mất ân nhân, mất danh dự, hao tài nguyên).
- Nút thắt vĩnh viễn: chấp niệm giữ qua biến cố ép buộc mà không buông sẽ thắt thành nút, trần tâm cảnh giảm còn 80 vĩnh viễn. Tâm Ma Kiếp không phải khuôn mẫu cố định: nội dung kiếp sinh từ đúng nút thắt thật của nhân vật (sợ chết gặp kiếp tử, hiếu thắng gặp kiếp nhục nhã).
- Chọn phương án thực dụng (lợi ích đặt trước đạo tâm) trong biến cố lớn: trừ 10 trần tâm cảnh vĩnh viễn mỗi lần, cộng dồn với nút thắt, không hoàn tác. Trần đã hạ không đan nào mua lại được: đây là con đường kiếp cứng nhất của hệ.
- Tâm cảnh hồi chậm (tĩnh tọa, danh thắng, tri kỷ, rượu) và sụp nhanh (thân hữu chết, phản bội, sát nhân lần đầu, đột phá thất bại). Biến động tâm cảnh lớn phát sự kiện qua đồng hồ CORE để các hệ khác nghe.

## 10. BỐN NGHỀ CHẾ TÁC: ĐAN DƯỢC, VŨ KHÍ PHÁP BẢO, PHÙ LỤC, TRẬN PHÁP
- Bốn nghề dùng chung khung kỹ năng: mỗi nghề có 5 bậc thợ (tập sự, thục luyện, tinh thông, đại thành, tông sư), nguyên liệu, thời gian chế tác theo phút, tỉ lệ hỏng.
- Tất định: kết quả chế tác do CORE roll từ seed và chỉ số; cùng trạng thái luôn ra cùng kết quả. Thất bại là mất nguyên liệu và thời gian, không hoàn vốn.
- Đan Dược: từ đan phàm (cầm máu, giải độc nhẹ) tới đan hỗ trợ đột phá. Một mẻ tốn nhiều canh; thất bại nặng có thể nổ lò (thương thế, cháy phòng luyện đan). Đan tốt gắn độc D theo mục 8.
- Vũ Khí Pháp Bảo: rèn từ quặng và nguyên liệu linh tính; pháp bảo có phẩm cấp, cần dưỡng luyện lâu dài (mục 21) mới lên cấp; hư hỏng phải sửa bằng nguyên liệu cùng loại.
- Phù Lục: bùa một lần dùng, tốn bút mực giấy linh khí; bùa mạnh bắt buộc giấy bút xứng tầm. Vẽ hỏng là mất nguyên liệu.
- Trận Pháp: bày từ trận kỳ, trận bàn, linh thạch làm mắt trận; dùng bảo vệ động phủ, bẫy địch, tụ linh khí. Trận có độ bền theo thời gian, trấn giữ lâu dài tốn chi phí duy trì.
- Chuyên sâu: chọn một nghề chính; nghề khác học được nhưng bị hệ số đa nghề giảm dần theo số nghề theo học (con số chốt M1). Cổng kiểm soát sức mạnh chế tác là nguyên liệu quý (mục 6, 14), không phải điểm kỹ năng: thợ giỏi không nguyên liệu vẫn vô dụng.

## 11. HỆ CHIẾN ĐẤU, THƯƠNG THẾ VÀ BẢNG CHỈ SỐ NHÂN VẬT
- Nguyên tắc: NPC và người chơi dùng chung một bảng chỉ số, cùng công thức. NPC không được cộng ẩn ngoài hợp đồng công khai.
- Bảng chỉ số 5 nhóm:
  A. Bẩm sinh: linh căn, thể chất bẩm sinh, ngộ tính, huyết mạch (V1 chỉ là modifier đơn giản).
  B. Thể chất rèn luyện: khí huyết, sức mạnh, thân pháp, kháng tính ngũ cảm.
  C. Công pháp: mỗi bộ có đặc trưng (công, thủ, thân, bổ trợ), bậc tu luyện công pháp quyết định hiệu lực.
  D. Trang bị: vũ khí pháp bảo, phù mang theo, trận đã bày, đan buff tạm thời.
  E. Lá bài tẩy ẩn: độc (mục 8), ma chiêu (mục 18), thủ đoạn bí mật, lợi dụng địa hình và biến động môi trường (mục 15).
- Trục thiết kế: đánh thắng cảnh giới cao hơn chỉ khả thi qua nhóm E và biến động môi trường, không bao giờ qua đấu chính diện C-D. Chênh cảnh giới trong đấu chính diện gần như tuyệt đối (triết lý mục 0). Đây là thế giới của độc, của mưu, không của đấu khí vũ lực.
- Chiến đấu theo lượt, engine tính hết: mỗi hiệp engine tính điểm hành động từ chỉ số, biến động và roll, ghi nhật ký; AI chỉ đọc kết quả và diễn đạt. Kết cục do engine: thắng, thua, bỏ chạy, đầu hàng, đồng quy.
- Thương thế có loại rõ: chảy máu, gãy xương, thương nội tạng, tẩu hỏa nhập ma. Thương nặng để lâu thành di chứng vĩnh viễn (giảm chỉ số vĩnh viễn). Chữa cần đan dược, y thuật NPC, thời gian nghỉ; tự chữa nguy hiểm cao.
- Chết trong chiến đấu là chết thật: mất save (mục 13).
## 12. HỆ NPC VÀ QUAN HỆ
- NPC dùng chung bảng chỉ số 5 nhóm A-E với người chơi (mục 11). Chỉ số sinh ra lúc tạo và lớn lên theo thời gian game: NPC tu luyện, đột phá, tranh đấu, chết. Không NPC đứng chờ người chơi.
- Mỗi NPC có: cảnh giới, công pháp, thể chất, ngộ tính, phe phái, chức vị, lịch trình theo canh (mục 4), quan hệ riêng với người chơi và NPC khác.
- Lịch trình theo canh: NPC xuất hiện đúng nơi đúng lúc (trưởng lão bế quan thì không gặp được).
- Cảm tình với người chơi là số nguyên, tích lũy từ hành vi (tặng quà, cứu giúp, cùng phe, hoàn thành nhiệm vụ; ngược lại là thất hứa, tranh giành, hại). Cảm tình chi phối: nhận nhiệm vụ hay không, bán rẻ hay đắt, tiết lộ tin hay giấu, che chở hay bán đứng.
- Quan hệ NPC với NPC: thù oán, ân nghĩa, phe phái tồn tại độc lập với người chơi; xen vào là bị cuốn theo cuộc chơi của họ.
- Cấp trên trực tiếp (mục 7.3) là NPC quan trọng nhất giai đoạn đầu: quyết định nhiệm vụ, đánh giá, che chở hoặc gây khó dễ.
- Hàn Lập là NPC đặc biệt: đúng timeline nguyên tác, xuất hiện đúng thời điểm lịch sử, mạnh lên đúng như truyện; cơ duyên của Hàn Lập không khả dụng cho người chơi (mục 0).

## 13. HỆ CHẾT CHÓC VÀ ĐẠO TIÊU
- Chết là mất save: toàn bộ tiến trình, vật phẩm, quan hệ bị xóa vĩnh viễn. Không hồi sinh, không đan cứu chết, không save thủ công.
- Nguyên nhân chết: thương thế quá nặng (mục 11), độc D chạm 100 không cứu kịp (mục 8), tẩu hỏa nhập ma khi đột phá thất bại (mục 5), bị giết, thọ nguyên hết (mục 20).
- NPC chết cũng là chết thật: kẻ thù đã giết không quay lại; oán hận có thể để lại cho người thân kẻ chết (mục 12, 22).
- Giết NPC để lại chứng cứ (mục 7.4) và nghiệp (mục 19): giết vô tội là nghiệp nặng, giết nơi đông người là tự đào hố.
- V1 không có chơi tiếp bằng hậu duệ: chết là kết thúc, chơi lại là nhân vật mới từ đầu.

## 14. HỆ KHÔNG GIAN VÀ MÊ CUNG CẤM ĐỊA
- Mê cung sinh từ seed thế giới qua RNG CORE: cùng seed cùng cấu trúc; sinh theo tầng khi vào, tất định.
- Không minimap miễn phí: phải tự ghi nhớ hoặc vẽ bằng giấy bút (vật phẩm); hết giấy mực là mất bản đồ. Lạc là lạc thật.
- Cấm địa có tầng: sâu hơn nguy hiểm hơn, nguyên liệu quý gắn tầng sâu (mục 6). Huyết Sắc Cấm Địa mở 30 năm một lần theo danh ngạch (mục 7.7) là cấm địa trung tâm hồi 2.
- Cơ quan bẫy do engine đặt, phát hiện qua hàm kiểm định chung CORE (mục 3): trượt là không thấy, trúng là trúng.
- Di chuyển giữa vùng tốn phút qua đồng hồ CORE; đường xa có yêu thú, cướp, thời tiết xấu (mục 15). V1 hạ giới không dịch chuyển tức thời.

## 15. HỆ BIẾN ĐỘNG MÔI TRƯỜNG
- Hệ số MT trong công thức chu thiên (mục 5): linh khí đậm tu nhanh, ô uế tạp loạn tu chậm. Giá trị từng vùng ghi trong thanh ghi hằng số CORE kèm chú thích nguồn duyệt.
- Chu kỳ ngày đêm, tháng, mùa: ảnh hưởng tu luyện (Thái Âm đêm x2 ngày x0,5), yêu thú (mục 23), tầm nhìn mê cung (mục 14).
- Biến động thiên nhiên theo seed nhưng tất định: bão, linh triều, điểm linh khí bùng nổ, yêu thú di trú đúng lịch sử seed; ai biết trước (mục 16) có lợi thế thật.
- Biến động nhân tạo: chiến tranh tông phái, mỏ cạn, khai quật thay đổi vĩnh viễn vùng đó (mục 6, 7.8).

## 16. HỆ THÔNG TIN VÀ TIN ĐỒN
- Tin là tài nguyên: tin đúng lúc đúng việc có giá trị thật (mua rẻ bán đắt mục 6, biết trước cấm địa mở, phe phái sắp đảo).
- Tin đồn có độ chính xác và độ tươi: có thể sai, quá hạn, bị xuyên tạc có chủ đích. Engine gắn nguồn gốc và thời điểm cho mỗi tin.
- Nguồn tin: nói chuyện NPC (phụ thuộc cảm tình, mục 12), tin đồn chợ phiên, mật báo trả tiền, quan sát, tàng thư tông.
- Tung tin giả là một đường chơi: yếu lòng tin và bằng chứng quyết định bị lật mặt hay không; lật mặt thì trả giá uy tín và quan hệ.

## 17. HỆ LINH ÁP VÀ CHÈN ÉP
- Linh áp là áp lực cảnh giới: chênh lớn cảnh giới gây tác động vật lý thật lên thân thể và tâm thần.
- Chênh 2 đại cảnh trở lên (Luyện Khí, Trúc Cơ, Kim Đan, Nguyên Anh, Hóa Thần) là tê liệt: không cưỡng lại bằng ý chí; chỉ thoát bằng tránh từ xa hoặc hóa giải bằng vật ngoài thân (trận pháp, phù, pháp bảo).
- Chênh 1 đại cảnh: áp lực rõ, giảm điểm hành động (mục 11), tâm cảnh non dễ hoảng loạn.
- Cùng đại cảnh: cảnh giới cao hơn chỉ tạo cảm giác nặng nề nhẹ, mang tính cảnh báo.
- Nguồn linh áp: tu giả cao cảnh, yêu thú cấp cao (mục 23), pháp bảo linh tính mạnh, một số vùng cấm địa chèn ép riêng.
- Chèn ép không gian: vùng không gian nặng nề lệch thường, hạn chế thân pháp, giảm hiệu quả công pháp; cửa ải tự nhiên chặn kẻ yếu.

## 18. HỆ MA CHIÊU VÀ BẪY
- Ma chiêu là đường tắt: học nhanh hơn chính đạo, mạnh sớm; cái giá là nghiệp (mục 19).
- Mỗi lần vận ma chiêu +1 nghiệp; luyện ma công +30; luyện sâu +100 (mục 19). Nghiệp tăng đẩy đạo tâm vào vùng ám đạm, nghiệp chướng, làm Tâm Ma Kiếp nguy hiểm hơn (mục 9).
- Ma chiêu để lại dấu vết: người có nhãn lực hoặc đồng ma đạo nhận ra; dùng nơi đông người là tự lộ.
- Bẫy do engine đặt: cấm địa, động phủ hoang, cổ mộ có cơ quan; phát hiện qua hàm kiểm định chung CORE, trượt là trúng, không roll may mắn lần hai.
- Bẫy do NPC đặt: NPC có mưu toan (giết người đo bảo, hãm hại) giăng bẫy cho người chơi hoặc NPC khác; người chơi cũng tự bày được (trận pháp mục 10).
- Cạm bẫy xã hội: dụ dỗ, lừa gạt, mượn dao giết người cũng là bẫy; engine ghi chứng cứ (mục 7.4) và nghiệp (mục 19) đầy đủ.

## 19. HỆ THIÊN ĐẠO VÀ TAI KIẾP (BẢNG NGHIỆP)
- Nghiệp là số nguyên -9999 đến +9999, khởi điểm 0. Lưu và tính trong CORE, mọi thay đổi ghi nhật ký.
- Bảng giá trị hành động (đã chốt): giết vô tội +50; cứu người -30; luyện ma công +30; mỗi lần vận ma chiêu +1; luyện ma công sâu +100; nghịch thiên kéo thọ +200. Mở rộng theo nội dung, mỗi giá trị mới phải được chủ game duyệt.
- Hệ số kiếp = 1 + N/2500 với N nghiệp dương (N +9999 ra 5,0). Nghiệp âm có sàn: kiếp không nhẹ hơn 60% độ khó chuẩn.
- Ngưỡng đạo tâm theo nghiệp: dưới 0 thanh minh; 0-250 vướng bụi; 250-750 ám đạm; 750-2000 nghiệp chướng; trên 2000 sát khí như thực. Chi phối cách NPC cảm nhận và cách engine mô tả nhân vật.
- 4 kiếp mốc: Trúc Cơ Tâm Ma Kiếp (sinh từ nút thắt thật, mục 9), Kim Đan Đan Kiếp, Nguyên Anh Lôi Kiếp, Hóa Thần Phong Hỏa Kiếp. Nghiệp cao làm kiếp mạnh qua hệ số; vượt kiếp không xóa nghiệp.
- Thiên đạo không thiện không ác: chỉ kết toán theo nghiệp, không thưởng người tốt máy móc, không trừng kẻ dữ không để lại chứng cứ. Tai kiếp là đòi nợ.
- Chuyển kiếp và trì hoãn kiếp (module hoãn, mục 28): mỗi chuyển kiếp +100 nghiệp, trì hoãn +10% độ khó lần kế tiếp, trước kiếp có thiên tượng báo trước. V1 chỉ cần lưu và cộng trừ nghiệp đúng.

### 14.1 Trữ Vật Đồ và Pháp Bảo Không Gian
- Túi trữ vật: chỉ chứa vật vô tri, không chứa sinh vật sống. V1 hai bậc: sơ cấp 1 khối lập phương, trung cấp 10 khối lập phương. Phải luyện hóa mới dùng được (mục 10). Gần như bắt buộc phải có: không túi thì sức mang theo giới hạn theo thể chất.
- Pháp bảo không gian bậc cao (dạng Tu Di, Tàng Trữ Giới): dung tích lớn hơn hẳn, vẫn thiên về chứa đồ; xuất hiện từ tầm Trúc Cơ trở lên, giá trị cực cao.
- Ngọc Cốt: pháp bảo không gian đặc biệt, bên trong là không gian ở được, sinh vật sống tồn tại được. V1 hạ giới duy nhất một kiện, gắn cơ duyên Tuyết Cơ: nàng trú ngụ bên trong, đi theo người chơi. Không chế tạo bằng nghề luyện khí, không mua được bằng linh thạch.
- Luật cân bằng hardcore: bên trong không chênh lệch thời gian với bên ngoài; người ở trong vẫn tiêu linh khí, thức ăn theo đồng hồ CORE; Ngọc Cốt bị hỏng hoặc bị đoạt thì sinh mạng bên trong bị đe dọa trực tiếp.
- Tuyết Cơ là NPC dùng chung bảng chỉ số 5 nhóm A-E (mục 11, 12); lai lịch, cảnh giới, thời điểm xuất hiện theo kịch bản 12 hồi, chốt khi viết arc-module.

