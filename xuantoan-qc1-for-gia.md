# Phiếu QC 1 — Road v1.0 (lượt kiểm tự động và sơ bộ bằng ảnh)

> Đây là phiếu kiểm chéo có hai phần: đã xác minh được bằng manifest/XML/ảnh, và các mục còn phụ thuộc xác nhận trực tiếp trên CVAT. Không dùng cảnh báo lint hoặc suy đoán thay cho xác nhận bằng mắt.

Lô được kiểm (học viên): gia  
Người kiểm (học viên): xuantoan  
Ngày: 2026-11-21  
Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `gia-front.zip` + `gia-fisheye.zip`, revision 1  
Số ảnh kiểm: 6 (không lấy ảnh thêm)  
Mẫu đã chọn: A05, A06, A07, B03, B06, B08  
Số nhãn trong mẫu (shape + tag): 80 (56 shape + 24 tag)

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi / trạng thái | Mức |
| --- | --- | ---: | --- | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 ảnh | 0; camera và đủ bốn tag khớp trong mẫu | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 ảnh | 4 ứng viên từ lint; chưa xác nhận bằng mắt | nặng |
| QC1-03 position | sai thuộc tính / thừa | 4 lane trong B03, B06, B08 | 0 theo thuộc tính XML; B06/B08 dùng `other` | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-06 style, color, kind | sai thuộc tính | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | Chưa kiểm bằng mắt | Chưa kết luận | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | Chưa kiểm bằng mắt | Chưa kết luận | chính |
| QC1-12 file | lỗi file | 2 ZIP + manifest | 0 lỗi cấu trúc; hash/bytes khớp, ZIP chỉ có `annotations.xml` | nhẹ / nặng |

## Danh sách lỗi / ứng viên cần xác nhận

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A05 | lane | nặng, chưa xác nhận | Lint báo thiếu cả L1 và R1 vì ảnh không có lane; cần xác nhận ảnh có vạch nhìn thấy hay không. |
| 2 | QC1-02 | A06 | lane | nặng, chưa xác nhận | Lint báo thiếu R1; cần xác nhận vạch phải có và nhìn thấy trong ảnh. |
| 3 | QC1-02 | A07 | lane | nặng, chưa xác nhận | Lint báo thiếu L1; cần xác nhận vạch phải có và nhìn thấy trong ảnh. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh có thấy được L1 và/hoặc R1 không? Nếu không thấy, xác nhận miễn QC1-02. | Chưa có |
| A06 | R1 có nhìn thấy và cần gán trong ảnh này không? | Chưa có |
| A07 | L1 có nhìn thấy và cần gán trong ảnh này không? | Chưa có |

## Quyết định

Lỗi nặng đã xác nhận: 0  
Ứng viên lỗi nặng chờ xác nhận: 4  
Lỗi chính đã xác nhận: chưa thống kê  
Tỉ lệ lỗi chính: chưa tính; cần hoàn tất kiểm bằng mắt trên mẫu 80 nhãn  
Lỗi nhẹ: 0 đã xác nhận  
Ca chờ lead: 3 ảnh  

Quyết định: **Hold (tạm thời)**  
Lý do: còn câu hỏi về tính nhìn thấy của vạch ở A05, A06 và A07. Theo thang QC1, Hold chỉ dùng khi cần lead giải đáp ca mơ hồ. Chưa dùng các cảnh báo lint làm kết luận cuối cùng.

## Phạm vi và giới hạn kiểm

- Đã kiểm manifest Gia: revision 1, 16 ảnh front + 12 ảnh fisheye, đủ tag theo manifest; SHA-256 và dung lượng của hai ZIP khớp manifest.
- Đã kiểm ZIP mở được và chỉ chứa `annotations.xml`, không kèm ảnh.
- `road_check lint` trên toàn bộ bài Gia báo 6 cảnh báo, đều là QC1-02: A05 thiếu L1/R1, A06 thiếu R1, A07 thiếu L1, A12 thiếu R1, A14 thiếu R1. Ba ảnh trong mẫu QC được ghi ở trên; A12 và A14 ngoài mẫu 6 ảnh.
- Chưa xác nhận các hình học/thuộc tính bằng cách so trực tiếp với ảnh cho tất cả mục QC1-04 đến QC1-11. Không coi việc lint không báo lỗi là bằng chứng các mục đó đúng.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
