# BaiTapNhom_LTNC

## 🚀 TEMPLATE FOR A MAZE PROBLEM  
**Presented by Group 15 - LTNC**  

---
## ✅ Members:
- 👤 **Nguyen Quang Huy** - `24022803` (Representative)
- 👤 Vu Manh Hung - `24022796`
- 👤 Phan Van Thai Hung - `24022798`
- 👤 Trịnh Thị Vân - `24022842`
- 👤 Hoà Tùng Dương - `24022780`

---
## 🎯 **Problem given:**
Tìm đường đi ngắn nhất trong mê cung có chướng ngại vật.

### **📌 Đề bài:**
- Cho mê cung `NxN`, một số ô có chướng ngại vật.
- Tìm đường đi ngắn nhất từ **(0,0)** tới **(N-1,N-1)**.

### **🔍 Gợi ý:**
- 🔄 Đệ quy thử đi 4 hướng (lên, xuống, trái, phải).
- ❌ Nếu ra ngoài biên hoặc gặp chướng ngại vật, bỏ qua.
- 🎯 Nếu đến đích, cập nhật độ dài ngắn nhất.
- 📌 Kết hợp memo hóa để tránh tính trùng.

---
## 📊 **Demonstration & Analysis**

### **📌 Tính chất:**
Bài toán bản chất là tìm **đường đi ngắn nhất trên đồ thị không trọng số**, mỗi bước đi có chi phí **1**.

### **📌 Các trường hợp cần xử lý:**
- ✅ **TH1:** Có đường đi đến đích → **tìm đường đi ngắn nhất**.
- ❌ **TH2:** Không có đường đi → **bị chặn hoàn toàn**.
- 🔲 **TH3:** Mê cung trống → **đường đi tối thiểu**.

---
## ⚙ **Algorithm**

### **💡 Ý tưởng:**
- Bắt đầu từ **(0,0)**, dùng **đệ quy** để thử tất cả các đường đi có thể đến **(N-1,N-1)** qua 4 hướng.
- 📌 **Lưu trữ (memo) độ dài đường đi ngắn nhất** tới mỗi ô để tránh tính trùng.
- ✅ **Đánh dấu (visited) cho mỗi ô đã đi qua**.
- 🎯 **In ra đường đi có số bước nhỏ nhất khi đến đích (N-1,N-1).**

### **📌 Phân tích thuật toán:**
**1️⃣ Khởi tạo:**  
- 🏗 **Tạo ma trận memo `NxN`**, tất cả các phần tử có giá trị là **INF (1 tỷ)**.
- ❌ **Gán giá trị `False` cho mảng `visited`** (các ô chưa được đi qua).

**2️⃣ Kiểm tra ô hợp lệ:**  
- ✅ Tạo hàm **`isValid(x, y, maze)`**:
  - 📏 **Kiểm tra (x, y) trong biên**: `0 <= x < N && 0 <= y < N`
  - 🛑 **Kiểm tra ô trống**: `maze[x][y] == 0`
  - 🔄 **Kiểm tra đã đi qua chưa**: `!visited[x][y]`

**3️⃣ Đệ quy tìm đường đi ngắn nhất:**  
- 🔄 Hàm **`findShortestPath(maze, x, y, step)`**:
  - **B1:** Nếu `(x, y)` không hợp lệ **→ trả về INF**.
  - **B2:** Nếu `(x, y) == (N-1, N-1)`, **trả về `steps`**.
  - **B3:** Nếu `memo[x][y]` đã có giá trị nhỏ hơn hoặc bằng `steps`, **trả về memo[x][y]`**.
  - **B4:** Thử **4 hướng**:
    - 🔄 **Tính `(newX, newY)` từ `(x, y)` theo 4 hướng**.
    - 📌 **Gọi đệ quy** `findShortestPath(maze, newX, newY, step + 1)`.
    - 🔽 **Lấy giá trị nhỏ nhất bằng `minPath` từ 4 kết quả**.
    - 🚀 **Bỏ đánh dấu `visited` để thử hướng khác**.
  - **B5:** Lưu `minPath` vào `memo[x][y]` và **trả về**.

**🎯 Kết quả:**
- Gọi `findShortestPath(maze, 0, 0, 0)` từ **(0,0) với `steps = 0`**.
- Nếu kết quả là **INF** → ❌ Không có đường đi.
- Nếu là **số cụ thể**, đó là **độ dài đường đi ngắn nhất**.

### **⏳ Độ phức tạp:**
- **Thời gian:** 🕒 `O(N²)` – **mỗi ô chỉ tính toán 1 lần nhờ memoization**.
- **Không gian:** 🏗 `O(N²)` – **lưu ma trận memo, cộng thêm `O(N²)` cho ngăn xếp đệ quy**.

---
## 💻 **Code**
🔗 GitHub: [Click here](https://github.com/NguyenHuy1804/demo/blob/main/ShortestPath_demo.cpp)

---
## 🧪 **Test Cases**

### **🔹 Test 1:**
```
Nhap kich thuoc me cung N: 4
Nhap me cung (0: trong, 1: chuong ngai vat):
4
0 0 0 0
1 1 0 1
0 0 0 0
0 1 1 0
```
### **🔹 Test 2:**
```
Nhap kich thuoc me cung N: 3
Nhap me cung (0: trong, 1: chuong ngai vat):
3
0 0 1
1 1 0
0 0 0
```
### **🔹 Test 3:**
```
Nhap kich thuoc me cung N: 3
Nhap me cung (0: trong, 1: chuong ngai vat):
3
0 0 0
0 0 0
0 0 0
```

---
## ✅ **Advantages & Disadvantages**

### **✅ Advantages:**
- 🚀 **Tối ưu bằng memoization** để tránh tính toán trùng.
- 📝 **Đơn giản, dễ hiểu** với chỉ **1 hàm `findShortestPath`**.
- 🔍 **Xử lý đầy đủ các trường hợp** (có đường đi, không có đường đi, mê cung trống).
- 🔄 **Dùng giá trị `INF`** giúp dễ dàng xử lý trường hợp không có đường đi.

### **❌ Disadvantages:**
- 📌 **Nguy cơ tràn ngăn xếp do gọi đệ quy quá sâu**.
- 🔄 **DFS chưa tối ưu** vì có thể đi vào đường cụt trước khi tìm thấy đường ngắn nhất.
- 🚀 **Cải thiện:** Dùng **BFS (Breadth-First Search)** thay vì DFS.

