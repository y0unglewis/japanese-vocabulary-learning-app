# Japanese Vocabulary Learning App

**Nhóm:** 19  
**Đồ án môn học:** Lập trình di động  
**Đề tài:** Xây dựng ứng dụng hỗ trợ học và ôn tập từ vựng tiếng Nhật

Ứng dụng Android hỗ trợ học và ôn tập từ vựng tiếng Nhật (dự kiến JLPT N5–N4) thông qua **Vocabulary**, **Flashcard**, **Quiz** và **Learning Progress**. Dự án ưu tiên hoạt động **offline-first**, phù hợp với phạm vi đồ án môn học.

> **Trạng thái:** Planning & UI/UX Design — đang thiết kế giao diện trên Figma. Các chức năng bên dưới là **dự kiến**, chưa được xác nhận là đã hoàn thành.

## Chức năng dự kiến

| Chức năng | Mô tả |
|---|---|
| **Vocabulary** | Xem danh sách và chi tiết từ vựng; tìm kiếm, lọc theo cấp độ. |
| **Flashcard** | Học từ vựng qua thẻ hai mặt. |
| **Quiz** | Ôn tập bằng câu hỏi trắc nghiệm và xem kết quả. |
| **Learning Progress** | Theo dõi kết quả và tiến độ học tập trên thiết bị. |
| **Favorites** | Đánh dấu và xem lại những từ cần ôn tập. |
| **Settings** | Thiết lập cơ bản cho trải nghiệm học tập. |

**Phạm vi hiện tại:** ưu tiên lưu trữ dữ liệu cục bộ. Việc có cần tài khoản đăng nhập thực sự, đồng bộ đám mây hoặc backend sẽ được nhóm xem xét sau.

## Công nghệ sử dụng

| Thành phần | Công nghệ |
|---|---|
| Ngôn ngữ | Java |
| Giao diện | XML |
| IDE | Android Studio |
| Lưu trữ cục bộ | **SQLite** (`SQLiteOpenHelper`, `SQLiteDatabase`) |
| Nền tảng | Android |
| Thiết kế | Figma |
| Quản lý mã nguồn | Git & GitHub |

## UI/UX — Figma

**Trạng thái:** In Progress.

Nhóm đang thiết kế các màn hình dự kiến như Splash/Onboarding, Home, Vocabulary List/Detail, Flashcard, Quiz/Result, Favorites, Progress, Settings và các màn hình hỗ trợ khác.

- **Figma:** https://www.figma.com/design/CRrZn0BlXLxURrJ57E6MS3/japanese-vocabulary-learning-app?node-id=0-1
- Ảnh chụp giao diện và luồng điều hướng sẽ được cập nhật sau khi nhóm thống nhất thiết kế.

## Phân công thiết kế Figma hiện tại

| Người phụ trách | Màn hình | Tình trạng |
|---|---|---|
| **Nguyễn Thị Như Ý** | 01–05, 24 (Splash, Onboarding, Home, Settings) | Đang làm |
| **Thái Duy Cường** | 06–09, 22–23 (Level, Lesson, Vocabulary, Favorites) | Chưa làm |
| **Phạm Thành Long** | 10–14, 20 (Flashcard, Progress) | Chưa làm |
| **Huỳnh Tấn Trung** | 15–19, 21 (Quiz, Quiz History) | Chưa làm |

## Định hướng triển khai dữ liệu

- **Database:** SQLite lưu trực tiếp trên thiết bị Android, không cần server để sử dụng chức năng học offline.
- **Truy cập dữ liệu:** tạo `DatabaseHelper` kế thừa `SQLiteOpenHelper`; tổ chức các phương thức truy vấn riêng cho các module.
- **Bảng dữ liệu dự kiến:** `lessons`, `vocabulary`, `favorites`, `learning_progress`, `quiz_history` (chưa chốt cột và quan hệ).
- **Dữ liệu dùng chung:** Vocabulary, Flashcard, Quiz và Progress sử dụng cùng một database; không tạo nhiều database trùng lặp theo từng thành viên.
- **An toàn dữ liệu:** sử dụng `?`/selection arguments cho truy vấn có đầu vào người dùng; chạy truy vấn nhiều dữ liệu trên background thread.

## Getting Started

### Yêu cầu

- Android Studio
- Android SDK
- Git
- Android Emulator hoặc thiết bị Android thật
- JDK tương thích với Android Gradle Plugin của dự án

### Clone repository

```bash
git clone https://github.com/y0unglewis/japanese-vocabulary-learning-app.git
cd japanese-vocabulary-learning-app
```

### Mở dự án

1. Mở Android Studio và chọn **Open**.
2. Chọn thư mục repository vừa clone.
3. Nếu repository đã có dự án Android, chờ Gradle Sync và cài SDK theo yêu cầu.
4. Chọn emulator hoặc điện thoại Android để chạy ứng dụng.

> Hướng dẫn build/run sẽ được kiểm chứng và cập nhật theo cấu trúc mã nguồn thực tế. Repo đang trong giai đoạn chuẩn bị nên không cam kết hiện đã có bản ứng dụng chạy hoàn chỉnh.

## Git Workflow

| Branch | Mục đích |
|---|---|
| `main` | Phiên bản ổn định |
| `develop` | Tích hợp và kiểm thử |
| `feature/*` | Phát triển tính năng hoặc tài liệu |
| `fix/*` | Sửa lỗi |

**Quy ước nhóm:** Mỗi thay đổi được thực hiện trên nhánh riêng (`feature/*` hoặc `fix/*`), sau đó mở **Pull Request (PR) vào `develop`**. PR cần ít nhất **1 approval** trước khi merge. Khi phiên bản trên `develop` đã được kiểm thử ổn định, tạo **PR từ `develop` vào `main`**. Không push trực tiếp lên `main` hoặc `develop` trong quy trình làm việc thông thường.

### 1. Tạo nhánh làm việc

Sau khi clone repository và mở terminal tại thư mục dự án:

```bash
git switch develop
git pull origin develop
git switch -c feature/ten-chuc-nang
```

Đổi `ten-chuc-nang` thành phần đang làm, ví dụ `feature/flashcard`, `feature/quiz` hoặc `feature/update-readme`. Nếu sửa lỗi, đặt tên nhánh như `fix/quiz-scoring`.

### 2. Commit và push code

Sau khi thay đổi file:

```bash
git status
git add .
git commit -m "feat: add flashcard screen"
git push -u origin feature/ten-chuc-nang
```

Thay `feature/ten-chuc-nang` bằng **đúng tên nhánh đang làm**. Các lần cập nhật tiếp theo trên cùng nhánh chỉ cần `git push`.

### 3. Tạo Pull Request

1. Vào tab **Pull requests** trên GitHub và chọn **New pull request**.
2. Chọn **base: `develop`** và **compare: `feature/ten-chuc-nang`** (hoặc nhánh `fix/*`).
3. Ghi rõ chức năng đã làm, phần cần kiểm thử và ảnh chụp giao diện nếu có.
4. Nhờ thành viên khác review; sau khi PR có đủ approval và không có xung đột, tiến hành merge.
5. Cập nhật `develop` trước khi bắt đầu công việc tiếp theo:

```bash
git switch develop
git pull origin develop
```

### 4. Đưa phiên bản ổn định lên `main`

Khi nhóm đã tích hợp và kiểm thử trên `develop`, tạo PR với **base: `main`** và **compare: `develop`**. Review và merge theo Rulesets của repository.

## Project Status

**Planning / UI-UX Design (In Progress)**
