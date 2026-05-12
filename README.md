# BÀI TẬP VỀ NHÀ 03 - HỆ QUẢN TRỊ CSDL

# ĐỀ TÀI: HỆ THỐNG QUẢN LÝ CẦM ĐỒ

 

---

 

## Thông tin sinh viên

 

Họ và tên:  Nguyễn Văn

Mã số sinh viên: K235480106077
 
Lớp: K59KMT.K01 - Kỹ thuật Máy tính
 
Trường: Đại học Kỹ thuật Công nghiệp Thái Nguyên (TNUT)

Giảng viên hướng dẫn: Thầy Đỗ Duy Cốp

 

---

 

# 1. Mô tả bài toán

 

Hệ thống quản lý cầm đồ dùng để quản lý:

- khách hàng

- hợp đồng vay tiền

- tài sản thế chấp

- thanh toán công nợ

- thanh lý tài sản

 

Mỗi khách hàng có thể có nhiều hợp đồng khác nhau. Một hợp đồng

có thể cầm cố nhiều tài sản.

 

Hệ thống hỗ trợ:

- tính lãi đơn

- tính lãi kép

- trả góp

- quản lý nợ xấu

- lưu lịch sử giao dịch

 

---

 

# 2. Quy trình hoạt động của hệ thống

 

                Khách

hàng 

                   ↓ 

                Tạo hợp

đồng 

                   ↓ 

                Thêm

tài sản 

                   ↓ 

            Tính lãi

theo ngày 

                   ↓ 

            Khách trả

tiền 

                   ↓ 

            Ghi log

thanh toán 

                   ↓ 

            Cập nhật

dư nợ 

                   ↓ 

            Quá hạn hợp

đồng 

                   ↓ 

            Thanh lý

tài sản 

 

---

 

# 3. Thiết kế cơ sở dữ liệu

TẠO database

<img width="1568" height="820" alt="Screenshot 2026-05-12 214247" src="https://github.com/user-attachments/assets/20f4b6de-0a5c-4958-98fc-409caaa32a38" />

 
## Tạo bảng dữ liệu

 <img width="1564" height="838" alt="Screenshot 2026-05-12 220624" src="https://github.com/user-attachments/assets/446dd5f1-6756-4e51-bf0c-6f87732431de" />

Hệ thống sử dụng các bảng:

- KhachHang

- HopDong

- TaiSan

- ThanhToan

- HopDong_TaiSan
<img width="1567" height="807" alt="Screenshot 2026-05-12 220946" src="https://github.com/user-attachments/assets/e054acd6-9692-43b5-876b-3ebbf2b92b77" />

tạo dữ liệu

<img width="1203" height="775" alt="Screenshot 2026-05-12 221059" src="https://github.com/user-attachments/assets/8b747af9-0ac3-4f56-aef7-c84d4c7f6264" />


 

## 3.1 Bảng KhachHang

 

Bảng dùng để lưu thông tin khách hàng.

 

| Tên cột | Ý nghĩa |

|---|---|

| CustomerID | Mã khách hàng |

| FullName | Họ tên |

| Phone | Số điện thoại |

| CCCD | CCCD |

| Address | Địa chỉ |


---

 

## 3.2 Bảng HopDong

 

Bảng quản lý hợp đồng vay tiền.

 

| Tên cột | Ý nghĩa |

|---|---|

| ContractID | Mã hợp đồng |

| CustomerID | Mã khách |

| LoanAmount | Tiền vay |

| RemainingDebt | Dư nợ |

| Deadline1 | Hạn lãi đơn |

| Deadline2 | Hạn thanh lý |

| Status | Trạng thái |

 <img width="1196" height="763" alt="Screenshot 2026-05-12 221206" src="https://github.com/user-attachments/assets/3a6fc841-e9bc-4ec8-94d2-460c73eb9b72" />




---

 

## 3.3 Bảng TaiSan

 

Bảng quản lý tài sản cầm cố.

 

| Tên cột | Ý nghĩa |

|---|---|

| AssetID | Mã tài sản |

| AssetName | Tên tài sản |

| AssetValue | Giá trị tài sản |

| AssetStatus | Trạng thái |

| IsSold | Đã thanh lý |

<img width="1581" height="825" alt="Screenshot 2026-05-12 221444" src="https://github.com/user-attachments/assets/f6011723-cf25-4565-bfa8-e3fdfdd6f8da" />


---

 

# 4. Quan hệ dữ liệu

 

- Một khách hàng có nhiều hợp đồng.

- Một hợp đồng có nhiều tài sản.

- Một hợp đồng có nhiều lần thanh toán.

 

### Sơ đồ logic

 

KhachHang 1 --- N HopDong 

 

HopDong 1 --- N ThanhToan 

 

HopDong N --- N TaiSan 

<img width="1196" height="828" alt="Screenshot 2026-05-12 221326" src="https://github.com/user-attachments/assets/7d797317-db5f-44bb-b588-230a94d19386" />


---

 

# 5. Logic tính lãi

 

Trong hệ thống quản lý cầm đồ, việc tính lãi đóng vai trò rất

quan trọng trong quản lý công nợ khách hàng.

 

Hệ thống sử dụng hai hình thức tính lãi gồm:

- lãi đơn

- lãi kép

 

---

 

## 5.1 Lãi đơn

 

Trước thời hạn Deadline1 hệ thống sử dụng lãi đơn để tính tiền

lãi theo số ngày vay thực tế.

 

Công thức tính:

 

TienLai = (TienGoc / 1000000) * 5000 * SoNgayVay

 

Trong đó:

 

- TienGoc là số tiền khách vay

- SoNgayVay là số ngày vay thực tế

 

Ví dụ:

 

Nếu khách vay:

- 5.000.000 VNĐ

- trong 10 ngày

 

thì tiền lãi sẽ là:

 

(5.000.000 / 1.000.000) * 5000 * 10 = 250.000 VNĐ

 

Điều này giúp hệ thống dễ dàng tính công nợ theo ngày.


---
 

## 5.2 Lãi kép

 

Sau khi vượt quá Deadline1, hợp đồng được xem là quá hạn và

hệ thống chuyển sang lãi kép nhằm tăng công nợ theo thời gian.

 

Công thức tính:

 

A = P(1 + r)^n

 

Trong đó:

 

- P là tổng tiền gốc và lãi đơn

- r là lãi suất quá hạn

- n là số ngày quá hạn

 

Lãi kép giúp:

- tăng công nợ theo thời gian

- hỗ trợ quản lý nợ xấu

- giảm tình trạng khách hàng chậm thanh toán

 

Hệ thống sử dụng Function:

- fn_CalcMoneyContract

 

để tự động tính tổng công nợ của khách hàng.

Sau Deadline1 hệ thống chuyển sang lãi kép.
<img width="969" height="739" alt="Screenshot 2026-05-12 221636" src="https://github.com/user-attachments/assets/fca5ec51-423c-435d-9a0f-ed229b59e853" />

---

# 6. Event tạo hợp đồng

 

Procedure:

- sp_CreateContract

 

Procedure dùng để:

- thêm khách hàng

- tạo hợp đồng

- thêm tài sản

- liên kết tài sản với hợp đồng
<img width="1562" height="864" alt="Screenshot 2026-05-12 221754" src="https://github.com/user-attachments/assets/77e9fdde-0b6c-4272-abcb-376f43d1f2a5" />
 


---

 

# 7. Event thanh toán

 

Procedure:

- sp_Payment

 

Hệ thống sẽ:

- tính tổng nợ

- trừ số tiền khách trả

- cập nhật dư nợ

- lưu log thanh toán

 

Nếu trả hết:

- cập nhật trạng thái “Đã thanh toán”

 

Nếu chưa trả hết:

- cập nhật trạng thái “Đang trả góp”
<img width="1556" height="840" alt="Screenshot 2026-05-12 221843" src="https://github.com/user-attachments/assets/52a01945-c5f5-4cc5-8f18-31025d084dbb" />


*Hình ảnh minh họa quá trình thực thi procedure sp_Payment để

xử lý thanh toán cho hợp đồng cầm đồ.*

 

Hệ thống thực hiện:

- tính tổng công nợ

- ghi nhận số tiền khách thanh toán

- cập nhật dư nợ còn lại
<img width="1554" height="832" alt="Screenshot 2026-05-12 221934" src="https://github.com/user-attachments/assets/6adf5719-24f0-493b-841c-53a6d4c1e4e3" />

*Hình ảnh minh họa dữ liệu lịch sử thanh toán của khách hàng

sau khi procedure được thực thi.*

 

Hệ thống lưu:

- mã thanh toán

- số tiền thanh toán

- ngày thanh toán

- người thu tiền

 

<img width="1556" height="827" alt="Screenshot 2026-05-12 222201" src="https://github.com/user-attachments/assets/552dd7b4-f8f4-428a-9596-5526c7fd6e6d" />


*Hình ảnh minh họa quá trình cập nhật dư nợ và trạng thái hợp

đồng sau khi khách hàng thanh toán.*

 

Sau khi thanh toán:

- RemainingDebt được giảm xuống

- Status được cập nhật phù hợp với trạng thái thanh toán thực

tế

 

Nếu khách chưa trả hết:

- trạng thái sẽ là “Đang trả góp”

 

Nếu khách đã trả đủ:

- trạng thái sẽ là “Đã thanh toán”

Dữ liệu này giúp theo dõi lịch sử giao dịch và quản lý công

nợ chính xác hơn.

---

 

# 8. Event quá hạn hợp đồng

 

Trigger:

 

TRG_QuaHan

 

Trigger được sử dụng để tự động cập nhật trạng thái hợp đồng

khi khách hàng quá thời hạn thanh toán.

 

Hệ thống sẽ:

 

kiểm tra thời hạn thanh toán Deadline1

xác định hợp đồng quá hạn

tự động cập nhật trạng thái hợp đồng thành:

“Quá hạn”

 

Điều này giúp hệ thống:

 

quản lý công nợ chính xác

theo dõi khách hàng nợ xấu

hỗ trợ thanh lý tài sản khi cần thiết

*Ghi chú : TẠO TRIGGER*
<img width="1562" height="827" alt="Screenshot 2026-05-12 222303" src="https://github.com/user-attachments/assets/ae8cda00-36b8-4194-94cc-ccc3c3d88911" />

*Hình ảnh minh họa quá trình cập nhật thời hạn thanh toán của

hợp đồng để kiểm tra trigger quá hạn.*

 

Hệ thống sẽ kiểm tra:

- thời gian thanh toán

- trạng thái hợp đồng

- điều kiện quá hạn
<img width="1194" height="830" alt="Screenshot 2026-05-12 222353" src="https://github.com/user-attachments/assets/e4783be1-e541-41d8-bb66-fd8f580ad1ef" />


*Hình ảnh minh họa kết quả sau khi trigger TRG_QuaHan được

kích hoạt.*

Khi hợp đồng vượt quá thời hạn thanh toán:

- trạng thái hợp đồng sẽ tự động chuyển thành “Quá hạn”

Điều này giúp hệ thống tự động quản lý các hợp đồng nợ xấu

hiệu quả hơn.

---

# 9. Query nợ xấu

Query được sử dụng để hiển thị danh sách khách hàng đang có

hợp đồng quá hạn.

 

Hệ thống sẽ hiển thị:

 

tên khách hàng

số điện thoại

số ngày quá hạn

tổng công nợ hiện tại

 

Điều kiện:

 

hợp đồng vượt quá Deadline1

khách hàng chưa hoàn tất thanh toán

 

Query này giúp:

 

quản lý khách hàng nợ xấu

theo dõi công nợ

hỗ trợ xử lý thanh toán và thanh lý tài sản

 

<img width="1198" height="831" alt="Screenshot 2026-05-12 222524" src="https://github.com/user-attachments/assets/003aabdb-a18a-489c-bb8e-b90c669787c7" />

*Hình ảnh minh họa kết quả truy vấn danh sách khách hàng có

hợp đồng quá hạn thanh toán.*

Hệ thống sẽ hiển thị:

- thông tin khách hàng

- số ngày quá hạn

- tổng công nợ hiện tại

Query này giúp theo dõi các hợp đồng nợ xấu và hỗ trợ quản

lý công nợ hiệu quả hơn.
---
 # 10. Trigger thanh lý


## Trigger thanh lý
 
Tự động chuyển:

- Đã thanh lý

→ Đã bán thanh lý
<img width="922" height="627" alt="Screenshot 2026-05-12 222647" src="https://github.com/user-attachments/assets/6372fc9a-f781-421d-8cab-8b3048739f7d" />


Hình ảnh minh họa kết quả sau khi trigger TRG_QuaHan được

kích hoạt.

Khi hợp đồng vượt quá thời hạn thanh toán:

- trạng thái hợp đồng sẽ tự động chuyển từ “Đang vay” sang

“Quá hạn”

Điều này giúp hệ thống quản lý các hợp đồng nợ xấu hiệu quả

hơn.

---

# 11. Event quản lý thanh lý tài sản

Hệ thống sử dụng Trigger để tự động quản lý trạng thái hợp đồng

và tài sản cầm cố khi hợp đồng bị quá hạn hoặc thanh lý.

Các chức năng chính gồm:


- tự động chuyển trạng thái hợp đồng sang “Quá hạn”

- tự động chuyển trạng thái tài sản sang “Sẵn sàng thanh lý”

- tự động chuyển trạng thái tài sản sang “Đã bán thanh lý”

Điều này giúp:

- quản lý tài sản cầm cố hiệu quả hơn

- giảm thao tác thủ công

- hỗ trợ xử lý nợ xấu chính xác hơn

Ngoài ra hệ thống còn hỗ trợ theo dõi:

- tình trạng hợp đồng

- trạng thái tài sản

- quá trình thanh lý tài sản trong cửa hàng cầm đồ
 
---
 
# 12. Kết luận
 
Hệ thống quản lý cầm đồ được xây dựng bằng SQL Server nhằm hỗ

trợ quản lý khách hàng, hợp đồng vay tiền, tài sản cầm cố và công nợ trong cửa

hàng cầm đồ.

Trong quá trình thực hiện bài tập đã xây dựng được:

- cơ sở dữ liệu quan hệ

- Function tính lãi

- Procedure xử lý thanh toán

- Trigger quản lý trạng thái hợp đồng và tài sản

- Query theo dõi khách hàng nợ xấu

 Thông qua bài tập này giúp:
 - hiểu rõ hơn về thiết kế cơ sở dữ liệu

- sử dụng Function, Procedure, Trigger và Query trong SQL

Server

- xây dựng được luồng xử lý dữ liệu theo mô hình thực tế

Hệ thống giúp:

- giảm thao tác thủ công

- quản lý dữ liệu hiệu quả hơn

- hỗ trợ theo dõi công nợ và tài sản chính xác hơn.
