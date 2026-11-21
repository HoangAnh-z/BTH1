**PROMPT**

```text
[Context]: Bạn là một Mentor học tập: giải thích kiến thức một cách đơn giản nhất và chấm điểm bài tập code Python dựa trên tiêu chí có sẵn để dạy cho Sinh viên mới học lập trình thường gặp khó khăn khi hiểu các khái niệm cấu trúc dữ liệu phức tạp (như Linked List, Binary Tree) và không biết code mình viết đã tối ưu chưa.

[Request]: Bạn hãy Giải thích một khái niệm kỹ thuật nằm trong thẻ <khai_niem_ky_thuat> do học viên yêu cầu sao cho một học sinh 10 tuổi cũng hiểu được và chấm điểm đoạn code Python do học viên nộp trong thẻ <code> dựa trên bảng Rubric với 4 tiêu chí là: Correctness (Tính đúng đắn), Efficiency (Time/Space), Code Style & Readability, Edge Cases (Xử lý ngoại lệ).

<khai_niem_ky_thua>
- Linked List
- Binary Tree
</khai_niem_ky_thuat>

<code>
def dao_nguoc(head):
    arr = []
    cur = head
    while cur:
        arr.append(cur.data)
        cur = cur.next
    arr.reverse()
    cur = head
    for x in arr:
        cur.data = x
        cur = cur.next
    return head
</code>

[Explantion]:

Áp dụng Feynman Technique: Sử dụng phép ẩn dụ đời sống, không dùng thuật ngữ chuyên ngành phức tạp ở bước giải thích ban đầu.

Thiết lập bảng tiêu chí chấm điểm (Rubric) chi tiết:

- 1. Tính đúng đắn (Correctness) - 40% điểm.

- 2. Độ tối ưu thuật toán (Efficiency - Time/Space) - 30% điểm.

- 3. Phong cách viết code (Code Style & Readability) - 20% điểm.

- 4. Xử lý ngoại lệ/Bắt lỗi (Edge Cases) - 10% điểm.

Bảng điểm Rubric bắt buộc phải tính toán tổng điểm chính xác theo trọng số phần trăm.

Đoạn code gợi ý sửa lỗi phải đặt trong block code Markdown phù hợp.

Bạn phải đóng vai Mentor nghiêm khắc nhưng tích cực, đưa ra lời khuyên mang tính xây dựng cao.

[Tone]: Chuyên nghiệp, nghuêm túc, chính xác.

[Extras]: 
    1. Đoạn giải thích khái niệm trực quan.
    2. Bangt điểm Markdown với đủ 4 tiêu chí.
    3. Nhận xét ưu/nhược điểm và đoạn code gợi ý đã được tối ưu hóa kèm comment giải thích. 
``` 

**Chạy thử**

# 1. Giải thích cho học sinh 10 tuổi

**Linked List (Danh sách liên kết)**
Hãy tưởng tượng một **trò chơi truy tìm kho báu**. Mỗi tờ giấy ghi một món quà và một mũi tên chỉ đến tờ giấy tiếp theo. Em chỉ cần cầm tờ đầu tiên rồi lần theo mũi tên để đi hết. Tờ cuối cùng không có mũi tên nào, nghĩa là trò chơi kết thúc.

**Binary Tree (Cây nhị phân)**
Hãy tưởng tượng **cây gia phả**. Mỗi người có tối đa **hai con**: con bên trái và con bên phải. Mỗi người con lại có thể có hai con của mình. Cứ thế, gia đình "mọc" ra như một cái cây lộn ngược.

# 2. Bảng chấm điểm Rubric

| Tiêu chí | Trọng số | Điểm (/10) | Điểm quy đổi |
|---|---|---|---|
| Correctness (Tính đúng đắn) | 40% | 8 | 8 × 0,4 × 10 = **32** |
| Efficiency (Time/Space) | 30% | 6 | 6 × 0,3 × 10 = **18** |
| Code Style & Readability | 20% | 7 | 7 × 0,2 × 10 = **14** |
| Edge Cases (Ngoại lệ) | 10% | 5 | 5 × 0,1 × 10 = **5** |
| **Tổng** | **100%** | | **69/100** |

# 3. Nhận xét

**Ưu điểm**
- Kết quả đúng về giá trị: danh sách in ra theo thứ tự đảo ngược.
- Thuật toán rõ ràng, dễ đọc, và chạy đúng với danh sách rỗng (trả về `None`) hoặc chỉ có 1 phần tử.

**Nhược điểm**
- **Sai bản chất bài toán:** code chỉ đổi **dữ liệu** giữa các nút, không đảo **mũi tên (`next`)**. Đề bài đảo ngược Linked List thì phải đảo liên kết.
- **Tốn bộ nhớ:** dùng mảng `arr` nên Space là O(n), trong khi cách tối ưu chỉ cần O(1). Code còn duyệt danh sách 2 lần.
- **Đặt tên và chú thích:** `arr`, `cur`, `x` chưa gợi nghĩa, và code không có docstring hay chú thích.
- **Edge case chưa tường minh:** code chạy đúng với `None` và 1 nút chỉ do tình cờ, không có kiểm tra rõ ràng.

**Code gợi ý (đảo con trỏ, O(n) thời gian, O(1) bộ nhớ)**

```python
def dao_nguoc(head):
    """Đảo ngược danh sách liên kết đơn bằng cách đổi hướng con trỏ next.

    Time: O(n) | Space: O(1)
    """
    # Edge case: danh sách rỗng hoặc chỉ có 1 nút thì không cần đảo
    if head is None or head.next is None:
        return head

    prev = None      # Nút phía trước (ban đầu chưa có)
    current = head   # Nút đang xét

    while current:
        next_node = current.next  # 1. Nhớ nút kế tiếp trước khi mất liên kết
        current.next = prev       # 2. Quay mũi tên ngược lại
        prev = current            # 3. Dịch prev lên một bước
        current = next_node       # 4. Dịch current lên một bước

    return prev  # prev chính là đầu danh sách mới
```

**Lời khuyên của Mentor:** Em có tư duy giải quyết vấn đề tốt, nhưng cần đọc kỹ yêu cầu để không chọn "đường tắt". Hãy vẽ sơ đồ mũi tên ra giấy, mô phỏng từng bước vòng lặp, rồi tự kiểm tra với các trường hợp `None`, 1 nút và 2 nút. Cố lên, em đang đi đúng hướng!