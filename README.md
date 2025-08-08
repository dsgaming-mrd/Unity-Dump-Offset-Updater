
# Unity Dump Offset Updater – By DS Gaming (Mr D)

Tool dùng để tự động phân tích `dump.cs` từ game Unity (Il2Cpp) và sinh ra file header `.h` chứa các offset `fields`, `methods` phục vụ cho cheat/mod game.

---

## 🧪 Hướng dẫn sử dụng (Demo)


### 📁 Chuẩn bị:

1. File `dump.cs` từ Il2CppDumper → đặt tại:

```

dump/dump.cs

```

---

2. Tạo file `config.json`:

```json
{
	"file_path": "dump/dump.cs",
	"output_file": "DarkOffsets.h",
	"offset_type": "VA",
	"obfuscate": true,
	"avoid_dup": true
}
```

-  `file_path`: Đường dẫn đến file `dump.cs` (xuất từ Il2CppDumper)
-  `output_file`: Tên file `.h` sẽ được xuất ra chứa các offset
-  `offset_type`: Loại offset cần lấy, gồm:
-  `"RVA"` – Relative Virtual Address
-  `"Offset"` – Offset gốc
-  `"VA"` – Virtual Address (thường dùng)
-  `obfuscate`: Nếu là `true`, offset sẽ được mã hoá dạng `ENCRYPTOFFSET("...")`, nếu `false` thì giữ nguyên offset
-  `avoid_dup`: Nếu là `true`, sẽ in ra biến offset chống trùng lặp dạng `_class_field` và `_class_method`, nếu `false` sẽ giữ nguyên là  `class_field` và `class_method`

---

3. Tạo file `function.json`:

```json
{
	"UnityEngine": {
		"Camera": {
			"fields": ["onPreCull"],
			"methods": [
				{ "name": "get_main", "args": 0 }
			]
		}
	}
}

```
- Cấu trúc: `{ "Namespace": { "Class": { "fields": [...], "methods": [...] }}}`
-  `fields`: Danh sách tên biến cần lấy offset
-  `methods`: Mỗi method gồm `name` (tên hàm) và `args` (số lượng tham số)

---

### ▶️ Cách chạy:


**Click vào tệp `.exe`:**

```bash

Tool.exe

```

---

### 📤 Kết quả:

Tool sẽ tạo ra file:

```

DarkOffsets.h (Tên có thể thay đổi trong config.json)

```

Chứa các dòng:

```cpp

uint64_t _class_field = ENCRYPTOFFSET("0x123");
uint64_t _class_method = ENCRYPTOFFSET("0x12345678");

```
---
  
Tool Created By DS Gaming - Mr D
---
Ủng hộ tôi bằng cách mua hack: [**Tại đây**](https://shopdsgm.vn)

Web Tool miễn phí: [**Tại đây**](https://tool.shopdsgm.vn)