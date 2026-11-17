# SO SÁNH TRADE-OFF PROMPTING NÂNG CAO (LOGIC & CHUỖI)

## Bước 1: Đề xuất 2 prompt mẫu

### Giải pháp 1: Prompt đơn giản

Bạn là nhân viên chăm sóc khách hàng.
Hãy phân tích tin nhắn, xác định ý định,
trích xuất sản phẩm, số lượng, đơn giá và tính tổng tiền.
Nếu thiếu dữ liệu, hãy thông báo.
Trả kết quả dưới dạng bảng.


### Giải pháp 2: Prompt chi tiết


Bạn là chuyên viên xử lý đơn hàng.

1. CoT: Phân tích lần lượt ý định, sản phẩm,
số lượng, đơn giá và tính tổng tiền.

2. Prompt Chaining: Chia thành 3 giai đoạn:
phân loại, trích xuất dữ liệu, tính toán và kiểm tra.

3. Rolling Summary: Nếu hội thoại bị gián đoạn,
tóm tắt dữ liệu đã xác nhận để tiếp tục xử lý.

4. Ràng buộc: Không tự suy đoán, dữ liệu thiếu
ghi null, dữ liệu sai phải báo lỗi.

5. Output: Trả kết quả dạng JSON gồm ý định,
sản phẩm, số lượng, đơn giá, tổng tiền và trạng thái.


## Bước 2: Bảng so sánh Trade-off
| Tiêu chí |  Giải pháp 1 | Giải pháp 2 
| :-: | :-: | :-: | 
| Độ dễ hiểu | Cao | Trung bình | 
| Tốn token | Ít | Nhiều hơn
| Tốc độ xử lý | Nhanh | Chậm hơn
| Chain-of-Thought | Cơ bản | Rõ ràng
| Prompt Chaining | Không có | Có 3 giai đoạn
| Rolling Summary | Không có | Có
    

## Bước 3: Lựa chọn và chạy thử

### 1. Lựa chọn phương án

**Chọn Giải pháp 2.**

Lý do: Kết hợp CoT, Prompt Chaining và Rolling Summary, giúp xử lý tuần tự, hạn chế lỗi và duy trì ngữ cảnh.

### 2. Chạy thử

**Input:**

Đặt 2 áo giá 150.000đ/chiếc và 1 quần giá 200.000đ.

**Output:**

```
{
  "intent": "Đặt hàng",
  "products": [
    {
      "name": "Áo",
      "quantity": 2,
      "subtotal": 300000
    },
    {
      "name": "Quần",
      "quantity": 1,
      "subtotal": 200000
    }
  ],
  "total": 500000,
  "status": "Thành công"
}
```

### 3. Kết luận

Giải pháp 2 tối ưu hơn nhờ độ chính xác cao, kiểm soát lỗi tốt và phù hợp với xử lý đơn hàng thực tế.
