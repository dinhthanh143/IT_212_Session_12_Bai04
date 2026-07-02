# BẢNG TEST CASE - API ĐĂNG KÝ eKYC
## Module: POST /api/v1/ekyc/register

---

## 1. Positive Test Cases

| ID | Mô tả | Trường | Giá trị nhập | Kỳ vọng | Loại |
|----|-------|--------|-------------|----------|------|
| TC-P-01 | Tất cả trường hợp lệ | fullName | Nguyễn Văn An | 201 - Đăng ký thành công | Positive |
| | | phone | 0987654321 | | |
| | | email | nguyenvanan@email.com | | |
| | | citizenId | 001202012345 | | |
| TC-P-02 | Tên có dấu tiếng Việt | fullName | Trần Thị Mai Hương | 201 - Đăng ký thành công | Positive |
| | | phone | 0912345678 | | |
| | | email | huong.tran@gmail.com | | |
| | | citizenId | 002203012346 | | |
| TC-P-03 | Tên tối thiểu 2 từ | fullName | Lê Vân | 201 - Đăng ký thành công | Positive |
| | | phone | 0356789123 | | |
| | | email | levan@abc.com | | |
| | | citizenId | 003204015678 | | |
| TC-P-04 | SĐT đầu số 03 | phone | 0312345678 | 201 - Đăng ký thành công | Positive |
| TC-P-05 | SĐT đầu số 05 | phone | 0512345678 | 201 - Đăng ký thành công | Positive |
| TC-P-06 | SĐT đầu số 07 | phone | 0712345678 | 201 - Đăng ký thành công | Positive |
| TC-P-07 | SĐT đầu số 08 | phone | 0812345678 | 201 - Đăng ký thành công | Positive |
| TC-P-08 | SĐT đầu số 09 | phone | 0912345678 | 201 - Đăng ký thành công | Positive |
| TC-P-09 | CitizenId đúng 12 số | citizenId | 001302012345 | 201 - Đăng ký thành công | Positive |
| TC-P-10 | Email có dấu + | email | test+ekyc@bank.com | 201 - Đăng ký thành công | Positive |

---

## 2. Negative Test Cases

### 2.1. Trường để trống (Empty/Null)

| ID | Mô tả | Trường | Giá trị nhập | Kỳ vọng | Loại |
|----|-------|--------|-------------|----------|------|
| TC-N-01 | fullName để trống | fullName | (empty) | 400 - "Họ và tên không được để trống" | Negative |
| TC-N-02 | phone để trống | phone | (empty) | 400 - "Số điện thoại không được để trống" | Negative |
| TC-N-03 | email để trống | email | (empty) | 400 - "Email không được để trống" | Negative |
| TC-N-04 | citizenId để trống | citizenId | (empty) | 400 - "Số CCCD không được để trống" | Negative |
| TC-N-05 | Tất cả để trống | all | (empty) | 400 - Validation error (4 lỗi) | Negative |

### 2.2. Sai định dạng (Format Error)

| ID | Mô tả | Trường | Giá trị nhập | Kỳ vọng | Loại |
|----|-------|--------|-------------|----------|------|
| TC-N-06 | Email không có @ | email | nguyenvangmail.com | 400 - "Email không đúng định dạng" | Negative |
| TC-N-07 | Email không có domain | email | nguyenvan@ | 400 - "Email không đúng định dạng" | Negative |
| TC-N-08 | Email multiple @ | email | test@@test.com | 400 - "Email không đúng định dạng" | Negative |
| TC-N-09 | SĐT đầu số 02 (không VN) | phone | 0212345678 | 400 - "Số điện thoại không đúng định dạng VN" | Negative |
| TC-N-10 | SĐT đầu số 04 (không VN) | phone | 0412345678 | 400 - "Số điện thoại không đúng định dạng VN" | Negative |
| TC-N-11 | SĐT đầu số 06 (không VN) | phone | 0612345678 | 400 - "Số điện thoại không đúng định dạng VN" | Negative |
| TC-N-12 | SĐT có chứa chữ | phone | 09123a5678 | 400 - "Số điện thoại không đúng định dạng VN" | Negative |
| TC-N-13 | SĐT 9 số | phone | 091234567 | 400 - "Số điện thoại không đúng định dạng VN" | Negative |
| TC-N-14 | SĐT 11 số | phone | 09123456789 | 400 - "Số điện thoại không đúng định dạng VN" | Negative |
| TC-N-15 | CitizenId có chữ | citizenId | 00120201234A | 400 - "Số CCCD phải gồm đúng 12 chữ số" | Negative |
| TC-N-16 | CitizenId 11 số | citizenId | 00120201234 | 400 - "Số CCCD phải gồm đúng 12 chữ số" | Negative |
| TC-N-17 | CitizenId 13 số | citizenId | 0012020123456 | 400 - "Số CCCD phải gồm đúng 12 chữ số" | Negative |
| TC-N-18 | CitizenId toàn số 0 | citizenId | 000000000000 | 400 - "Số CCCD phải gồm đúng 12 chữ số" | Negative |

### 2.3. Trùng lặp (Duplicate)

| ID | Mô tả | Trường | Giá trị nhập | Kỳ vọng | Loại |
|----|-------|--------|-------------|----------|------|
| TC-N-19 | citizenId đã tồn tại | citizenId | (đã có trong DB) | 409 - "Số CCCD đã được đăng ký trong hệ thống" | Negative |
| TC-N-20 | phone đã tồn tại | phone | (đã có trong DB) | 409 - "Số điện thoại đã được đăng ký" | Negative |
| TC-N-21 | email đã tồn tại | email | (đã có trong DB) | 409 - "Email đã được đăng ký" | Negative |

---

## 3. Boundary Test Cases

| ID | Mô tả | Trường | Giá trị nhập | Kỳ vọng | Loại |
|----|-------|--------|-------------|----------|------|
| TC-B-01 | fullName 1 ký tự (dưới min) | fullName | A | 400 - "Họ và tên phải từ 2-100 ký tự" | Boundary |
| TC-B-02 | fullName 2 ký tự (min) | fullName | Lê A | 201 - Đăng ký thành công | Boundary |
| TC-B-03 | fullName 100 ký tự (max) | fullName | (100 ký tự chữ cái và khoảng trắng) | 201 - Đăng ký thành công | Boundary |
| TC-B-04 | fullName 101 ký tự (quá max) | fullName | (101 ký tự) | 400 - "Họ và tên phải từ 2-100 ký tự" | Boundary |
| TC-B-05 | fullName có số (không hợp lệ) | fullName | Nguyễn Văn 123 | 400 - Validation error | Boundary |
| TC-B-06 | fullName có ký tự đặc biệt | fullName | Nguyễn Văn @! | 400 - Validation error | Boundary |
| TC-B-07 | fullName tiếng Việt có dấu max | fullName | (100 ký tự tiếng Việt) | 201 - Đăng ký thành công | Boundary |
| TC-B-08 | email 1 ký tự trước @ | email | a@b.c | 201 - Đăng ký thành công | Boundary |
| TC-B-09 | email 100 ký tự (max) | email | (100 ký tự) | 201 - Đăng ký thành công | Boundary |
| TC-B-10 | email 101 ký tự (quá max) | email | (101 ký tự) | 400 - "Email không được quá 100 ký tự" | Boundary |
| TC-B-11 | phone 10 số (đúng) | phone | 0912345678 | 201 - Đăng ký thành công | Boundary |
| TC-B-12 | phone 9 số | phone | 091234567 | 400 - "Số điện thoại không đúng định dạng VN" | Boundary |
| TC-B-13 | phone 11 số | phone | 09123456789 | 400 - "Số điện thoại không đúng định dạng VN" | Boundary |

---

## Summary

| Loại | Số lượng |
|------|----------|
| Positive TC | 10 |
| Negative TC (Empty) | 5 |
| Negative TC (Format) | 13 |
| Negative TC (Duplicate) | 3 |
| Boundary TC | 13 |
| **Tổng** | **44** |
