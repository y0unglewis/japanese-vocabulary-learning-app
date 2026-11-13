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

Dự án sử dụng Git và GitHub để quản lý mã nguồn, phân chia công việc và tích hợp các chức năng do từng thành viên phát triển.

### 1. Quy ước Branch

| Branch | Mục đích |
|---|---|
| `main` | Chứa phiên bản ổn định của ứng dụng |
| `develop` | Tích hợp và kiểm thử code từ các thành viên |
| `feature/*` | Phát triển chức năng mới |
| `fix/*` | Sửa lỗi |

**Quy tắc làm việc:**

- Mỗi thành viên phải tạo **branch riêng từ `develop`** trước khi bắt đầu code.
- Không làm việc hoặc push trực tiếp lên `main` và `develop`.
- Sau khi hoàn thành, push code lên branch cá nhân và tạo **Pull Request (PR) vào `develop`**.
- PR cần được review và có ít nhất **1 approval** trước khi merge.
- Chỉ đưa code từ `develop` lên `main` thông qua PR sau khi đã tích hợp và kiểm thử ổn định.

### 2. Clone repository (lần đầu)

```bash
git clone https://github.com/y0unglewis/japanese-vocabulary-learning-app.git

cd japanese-vocabulary-learning-app
```

### 3. Tạo branch riêng trước khi code

Đảm bảo branch `develop` đã được cập nhật:

```bash
git switch develop
git pull origin develop
```

Tạo branch mới:

```bash
git switch -c feature/feature-name
```

Thay `feature-name` bằng tên chức năng phụ trách.

**Ví dụ:**

- `feature/home`
- `feature/vocabulary`
- `feature/flashcard`
- `feature/quiz`
- `fix/quiz-scoring`

### 4. Commit và Push code

Sau khi hoàn thành một phần công việc, kiểm tra các file đã thay đổi:

```bash
git status
```

Thêm và commit:

```bash
git add .
git commit -m "feat: implement flashcard screen"
```

Push lên branch riêng:

```bash
git push -u origin feature/flashcard
```

**Lưu ý:** Thay `feature/flashcard` bằng tên branch đang làm việc. Những lần push tiếp theo trên cùng branch chỉ cần chạy:

```bash
git push
```

### 5. Tạo Pull Request vào `develop`

Sau khi push code thành công:

1. Mở repository trên GitHub.
2. Vào **Pull requests** → **New pull request**.
3. Chọn:
   - **Base:** `develop`
   - **Compare:** branch cá nhân (`feature/*` hoặc `fix/*`).
4. Đặt tiêu đề và mô tả những thay đổi đã thực hiện.
5. Chọn **Create pull request**.
6. Chờ thành viên khác review và approve.
7. Khi PR đáp ứng yêu cầu review và không có xung đột, tiến hành merge vào `develop`.

**Lưu ý:** `git push` chỉ đưa code lên branch cá nhân. Code chỉ được tích hợp vào `develop` sau khi PR được merge.

### 6. Bắt đầu công việc tiếp theo

Sau khi PR đã được merge, cập nhật branch `develop`:

```bash
git switch develop
git pull origin develop
```

Tạo branch mới cho công việc tiếp theo:

```bash
git switch -c feature/next-feature
```

Không tiếp tục phát triển chức năng mới trên branch cũ đã merge.

### 7. Merge `develop` vào `main`

Khi các chức năng đã được tích hợp và kiểm thử ổn định:

1. Vào **Pull requests** → **New pull request**.
2. Chọn **Base: `main`** và **Compare: `develop`**.
3. Review những thay đổi trước khi merge.
4. Merge PR khi đáp ứng các yêu cầu của repository.

`main` được sử dụng để lưu trữ phiên bản ổn định của đồ án.

### 8. Quy ước Commit Message

Sử dụng commit message ngắn gọn, mô tả đúng nội dung thay đổi.

| Prefix | Mục đích | Ví dụ |
|---|---|---|
| `feat:` | Thêm chức năng | `feat: add quiz screen` |
| `fix:` | Sửa lỗi | `fix: correct quiz score` |
| `docs:` | Cập nhật tài liệu | `docs: update README` |
| `style:` | Chỉnh giao diện/định dạng | `style: adjust home layout` |
| `refactor:` | Cải thiện code | `refactor: simplify database helper` |

**Không commit** các file cấu hình cá nhân của IDE, file build, mật khẩu hoặc thông tin nhạy cảm.

## Project Status

**Planning / UI-UX Design (In Progress)**
