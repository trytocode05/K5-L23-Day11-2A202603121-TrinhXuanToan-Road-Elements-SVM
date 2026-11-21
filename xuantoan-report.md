# Báo cáo cá nhân — Ngày 11 (bản nháp)

Họ tên: Trịnh Xuân Toàn  
Mã học viên: 2A202603121  
Phiên bản CVAT (Help → About): **Chưa ghi trong export; cần bạn tra trực tiếp Help → About**  
Guideline: Road v1.0  
Lần nộp (`revision` trong manifest): 1  
Thời điểm export (theo manifest, UTC): 2026-11-20 17:00:16 UTC (2026-11-21 00:00:16, giờ Việt Nam)  
Số lần nộp lại sau Rework: **Cần xác nhận**

## 1. Kiểm project

| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có trong metadata của XML export | Chưa có ảnh chụp tab Labels để xác nhận project CVAT trực tiếp. |
| Thuộc tính và giá trị | Có trong metadata của XML export | Cần đối chiếu tab Labels và sửa lỗi thuộc tính nếu lint/QC phát hiện. |
| 4 tag ảnh | Có trên 28/28 ảnh trong XML export | Camera tag được tách thành front/fisheye đúng theo tên ảnh. |

Cách kết thúc polyline trên bản CVAT này: **Cần bạn xác nhận**.  
Cách đặt tag ảnh trên bản CVAT này: **Cần bạn xác nhận thao tác thực tế**.

## 2. Số lượng đã gán

Số shape được đếm từ hai ZIP hiện tại; task front/fisheye gồm cả ảnh bắt buộc và ảnh thêm.

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 33 | 0 | 8 | 21 | 22 | 14 |
| front-extra (đã làm 4 / 4) | 4 | 11 | 0 | 5 | 9 | 5 | 10 |
| fisheye | 8 | 12 | 0 | 12 | 11 | 3 | 5 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 0 | 5 | 3 | 0 | 0 |

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| **Cần bạn bổ sung** | | | | Không thể suy ra các ca bạn đã cân nhắc chỉ từ XML. |

## 4. Phiếu QC 1 nhận được

Bạn kiểm lô của tôi: **Chưa có thông tin trong package nhận được**  
Quyết định nhận được: **Chưa có phiếu QC cho bài xuantoan trong `Downloads.zip`**.

| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| Chưa có dữ liệu | — | — | — |

`Downloads.zip` chứa submission `gia` để xuantoan kiểm chéo, không chứa phiếu phản hồi kiểm bài xuantoan. Bản nháp phiếu kiểm Gia nằm tại `xuantoan-qc1-for-gia.md`.

## 5. Kiểm file export

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | ---: | ---: | --- |
| `xuantoan-front.zip` | Có | A01: 8 / 8 | A02: 6 / 6 | Có (`front`) |
| `xuantoan-fisheye.zip` | Có | B01: 2 / 2 | B02: 5 / 5 | Có (`fisheye_front`) |

Đã xác minh SHA-256 và dung lượng hai ZIP khớp `xuantoan-manifest.json`; ZIP chỉ chứa `annotations.xml`, không kèm ảnh.

## 6. Ảnh chụp màn hình

**Chưa có ảnh chụp trong các tệp hiện tại.** Cần chèn bốn ảnh thật từ CVAT:

1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
4. Một đoạn XML có `<polyline label="lane">`.

## 7. Tự đánh giá

Kiểm tra lint hiện tại trên bài xuantoan báo 36 cảnh báo: 19 nặng, 15 chính, 2 nhẹ. Trong đó có các gợi ý thiếu L1/R1, lane cùng position, hướng vẽ polyline, edge_zone, cùng vài điểm lặp. Đây là cảnh báo tự động, cần đối chiếu với ảnh trước khi kết luận và sửa.

- Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: **Cần bạn xác nhận sau khi rà và sửa bài.**
- Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: **Chưa thể điền vì chưa có xác nhận lỗi nào đã được sửa.** Ví dụ để bạn hoàn thiện: thiếu L1/R1 có thể khiến model học rằng vị trí đó không có ranh làn; polyline lệch tâm có thể làm đích dự đoán của model lệch khỏi vạch thật.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi (A01, R1) | không có làn | 153.9 | 202.5 | 251.6 | 298.3 |
| x của bạn kia (A01, R1) | không có làn | 657.7 | 602.0 | 544.0 | 486.6 |

1. R1 ở A01 hiện kết thúc khoảng y=500. Nếu rút ngắn đầu xa khoảng 40 px theo chiều ảnh, y=520 có thể thành “không có làn”; trong các hàng mẫu 720/680/640/600/560, chưa hàng nào nhất thiết đổi. Cần xác nhận cách hiểu “dừng sớm 40 px” theo slide của lớp.
2. Hai polyline R1 lệch nhau khoảng 503.8 px tại y=680 và 188.3 px tại y=560. Hàng gần xe hơn thường quan trọng hơn cho LKA; theo tọa độ ảnh, y=680 gần xe hơn y=560. Cần đối chiếu slide 25 của lớp trước khi chốt nhận xét.
3. Với polyline đơn giản chỉ cắt mỗi hàng một lần, đảo thứ tự điểm không đổi giao điểm x hình học. Tuy vậy, `road_check` kiểm tra chiều gần-ra-xa; với polyline có nhiều đoạn cắt cùng một hàng, script `rowanchor` cũng lấy giao điểm đầu tiên theo thứ tự điểm nên có thể chọn giao điểm khác.
