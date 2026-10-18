# [Thực hành] Chuyển đổi CSS có sẵn sang SASS theo chuẩn

## Cấu trúc thư mục dự án
```text
sass-conversion/
├── styles.css                   ← File CSS gốc ban đầu (trước khi chuyển đổi)
├── main.scss                    ← File SCSS gốc tổng hợp tất cả partials
├── abstracts/
│   ├── _variables.scss          ← Biến SASS ($primary-color, $text-color, ...)
│   └── _mixins.scss             ← Mixins tái sử dụng (button-style, box-shadow)
├── base/
│   └── _global.scss             ← Style toàn cục (body font, color, background)
├── layout/
│   └── _container.scss          ← Bố cục container trang
└── components/
    ├── _buttons.scss            ← Component Button (dùng mixin button-style)
    └── _cards.scss              ← Component Card (dùng mixin box-shadow)
```

## Quá trình chuyển đổi

| Bước | Từ CSS truyền thống | Sang SCSS chuẩn |
|------|---------------------|-----------------|
| 1 | Giá trị màu lặp lại: `#333`, `#f4f4f4`... | Biến SASS: `$text-color`, `$background-color`... |
| 2 | Code `button` lặp padding/border-radius | Mixin `@mixin button-style($bg-color)` |
| 3 | Code `box-shadow` lặp ở nhiều nơi | Mixin `@mixin box-shadow` |
| 4 | Tất cả trong 1 file duy nhất | Tách thành các **partials** (`_*.scss`) theo chức năng |
| 5 | Không có cấu trúc rõ ràng | Tổ chức theo **7-1 pattern**: `abstracts/`, `base/`, `layout/`, `components/` |

## Lợi ích của SASS so với CSS
- ✔ **Biến (Variables):** Thay đổi 1 nơi, áp dụng toàn bộ dự án.
- ✔ **Mixins:** Tái sử dụng code, giảm trùng lặp.
- ✔ **Partials:** Tổ chức code theo chức năng, dễ bảo trì.
- ✔ **Import:** Gom tất cả vào `main.scss`, biên dịch ra 1 file CSS duy nhất.

## Cách biên dịch SCSS ra CSS
Cài đặt Node.js Sass:
```bash
npm install -g sass
```
Biên dịch:
```bash
sass main.scss output.css
```
Hoặc watch (tự động biên dịch khi có thay đổi):
```bash
sass --watch main.scss:output.css
```
