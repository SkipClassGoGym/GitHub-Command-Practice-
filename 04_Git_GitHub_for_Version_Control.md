# Buổi 04 – Git & GitHub for Version Control

> **AIO2025 – Module 1 – Advanced (T5+T7)**
> Giảng viên: Nguyễn Thái Hà (Ph.D) · Supporter (STA): Nguyễn Đăng Nhã · Ngày: 14/06/2025 (Thứ 7)
> Nguồn: transcript buổi học + slide `[slide]_github_for_version_control_v03.pdf`

---

## Mục lục

0. [Mở đầu & bối cảnh](#0-mở-đầu--bối-cảnh)
1. [Phần 1 – Hệ thống quản lý phiên bản (VCS) & Git](#phần-1--hệ-thống-quản-lý-phiên-bản-vcs--git)
2. [Phần 2 – Quy trình làm việc Git cơ bản](#phần-2--quy-trình-làm-việc-git-cơ-bản)
3. [Phần 3 – Quản lý nhánh và lịch sử](#phần-3--quản-lý-nhánh-và-lịch-sử)
4. [Phần 4 – Cộng tác qua GitHub](#phần-4--cộng-tác-qua-github)
5. [Phần 5 – Tùy chỉnh & mở rộng Git](#phần-5--tùy-chỉnh--mở-rộng-git)
6. [Kahoot – Câu hỏi ôn tập](#6-kahoot--câu-hỏi-ôn-tập)
7. [Bài tập thực hành (Hands-on)](#7-bài-tập-thực-hành-hands-on)
8. [Cheat sheet – ~10 lệnh dùng nhiều nhất](#8-cheat-sheet--10-lệnh-dùng-nhiều-nhất)
9. [Tài liệu tham khảo](#9-tài-liệu-tham-khảo)

---

## 0. Mở đầu & bối cảnh

### 0.1. Khảo sát nhanh
- Khoảng 170 học viên tham dự, chỉ khoảng 16 bạn đã có kinh nghiệm với Git, nên **phần lớn là người mới**. Giảng viên đi chậm và tập trung vào việc *hiểu bản chất*.

### 0.2. Vấn đề khi chưa dùng Git
Khi làm nhóm mà chia sẻ code qua email, Zalo hay Google Drive thì:
- Có 5–6 phiên bản khác nhau, không biết bản nào là bản cuối.
- Ai đó vô tình xóa một đoạn quan trọng, **không biết ai xóa** và **không khôi phục được**.

**Git giống như một "cỗ máy thời gian" cho code**: xem lại toàn bộ lịch sử, biết *ai* sửa, sửa *cái gì*, *khi nào* và *như thế nào*.

### 0.3. Roadmap học Data Science (nhắc lại)
Roadmap có 3 trục:

| Trục | Nội dung chính |
|---|---|
| **Tools & Programming** | Excel, Python, Data Visualization, SQL, Cloud (AWS/Azure), Databricks. *Code Management*: Coding Methodology, **Git & GitHub**, Unix/Linux, CI/CD |
| **Machine Learning** | Thống kê, quản lý dự án ML, Supervised/Unsupervised, Feature Engineering, Time Series, NLP, Optimization, A/B Testing, XAI (SHAP, LIME) |
| **Business & Communication** | Logical thinking, Business writing, Data storytelling, Presentation, Case study, Stakeholder communication |

**3 dự án thực tế** (dựa trên các dự án giảng viên đã làm ở công ty tư vấn chiến lược):
1. Sales Forecasting & Demand Prediction, có áp dụng **XAI** để giải thích kết quả mô hình cho bên business.
2. Công cụ tối ưu hóa phân bổ hàng hóa cho chuỗi cửa hàng thời trang.
3. Customer Segmentation cho chiến lược Marketing (Unsupervised Learning).

> Git/GitHub ít được dạy ở trường đại học nhưng là kỹ năng **bắt buộc (must-have, không phải nice-to-have)** khi đi làm. Hầu hết công ty công nghệ đều dùng Git, GitLab hoặc công cụ tương tự. Hầu hết thư viện open source cũng nằm trên GitHub.

### 0.4. Mục tiêu buổi học (Learning Objectives)
1. **Hiểu rõ Git & GitHub**: khái niệm VCS và cách Git hoạt động.
2. **Thành thạo quy trình làm việc**: quản lý mã nguồn, nhánh, hợp tác.
3. **Cộng tác hiệu quả**: Fork, Pull Request, CI/CD, pre-commit (công cụ "gác cổng" kiểm tra PEP8, format, linting trước khi public code).
4. **Tùy chỉnh & mở rộng**: cấu hình nâng cao, Git Hooks, tự động hóa.

### 0.5. Hình ảnh liên tưởng: Git và GitHub là gì?
Khi brainstorm, học viên đưa ra các hình ảnh: nhật ký, backup dữ liệu, folder chung, Google Drive, log theo dõi. Giảng viên chọn hình ảnh sau:

| | Liên tưởng | Vai trò |
|---|---|---|
| **Git** | 📷 **Máy chụp ảnh** | Mỗi khi hoàn thành một phần việc, Git "chụp ảnh" toàn bộ dự án và cất vào **album**. Ảnh không bao giờ mất, có thể xem lại bất kỳ lúc nào |
| **GitHub** | ☁️ **Google Photos dành cho lập trình viên** | Backup album lên cloud, chia sẻ với bạn bè/đồng nghiệp, bình luận/góp ý, có thể public cho cả thế giới xem |

> Git là **công cụ** quản lý code. GitHub là **nơi lưu trữ** code online. Ngoài GitHub còn có GitLab, Bitbucket. Công ty của giảng viên dùng GitLab nhiều hơn; cách dùng gần như giống hệt GitHub.

---

## Phần 1 – Hệ thống quản lý phiên bản (VCS) & Git

### 1.1. Khái niệm VCS
**Version Control System (VCS)** là hệ thống theo dõi và lưu lại mọi thay đổi của tập tin theo thời gian. Nó giống như một **người thư ký tận tâm** ghi lại:
- **Who**: ai thay đổi
- **What**: thay đổi gì
- **When**: khi nào
- **Why**: tại sao (ghi chú/message)

**Ví dụ viết tiểu thuyết**: mỗi ngày viết thêm vài trang, có hôm xóa đoạn, đổi cốt truyện, thêm nhân vật. Nếu cốt truyện hôm nay chưa ổn thì cần quay lại bản hôm qua. VCS giúp làm việc đó.

**Lợi ích của VCS:**
- Khôi phục phiên bản cũ khi có lỗi. Nút "Undo" của Word chỉ quay lại thao tác gần nhất, còn VCS quay lại được **bất kỳ thời điểm nào**.
- So sánh sự khác biệt giữa các phiên bản (ảnh chụp ở thời điểm A với thời điểm B).
- Biết rõ ai thay đổi, thay đổi gì, khi nào.
- Bảo vệ dữ liệu (máy hỏng thì code vẫn còn trên cloud) và hỗ trợ làm việc nhóm.

### 1.2. Ba loại VCS

| Loại | Cách hoạt động | Ví dụ | Nhược điểm |
|---|---|---|---|
| **Local VCS** | Lưu các version ngay trên máy cá nhân, giống *nhật ký cá nhân* | – | **Mất máy là mất toàn bộ code** |
| **Centralized VCS (CVCS)** – hệ thống *tập trung* | Một **Shared Repository** trên máy chủ trung tâm. Dev phải *checkout* bản sao, commit và luôn kết nối server, giống *thư viện trung tâm* phải đến mượn sách | **CVS** (thập niên 1990), **Subversion (SVN)** | **Server hỏng thì cả team ngừng việc** ("thư viện đóng cửa thì không mượn được sách") |
| **Distributed VCS (DVCS)** – hệ thống *phân tán* | **Mỗi người có bản sao đầy đủ** (một "thư viện mini" riêng, có Version Database riêng), khi có mạng thì đồng bộ với nhau | **Git**, **Mercurial** (cả hai ra đời khoảng 2005; Facebook/Meta từng dùng Mercurial) | Khắc phục được cả hai nhược điểm trên |

**Ưu điểm của DVCS:**
- **An toàn**: không sợ mất máy, vì ai cũng có bản đầy đủ.
- **Linh hoạt**: làm việc offline ở đâu cũng được, chỉ cần internet khi muốn đồng bộ.

> Hiện có khoảng **100 triệu developer** dùng Git.

### 1.3. Lược sử Git
- **Bối cảnh (2005)**: đội phát triển **Linux** (dự án rất lớn, khoảng 10–20 triệu dòng code, hàng nghìn developer) dùng công cụ **BitKeeper**. Do **tranh chấp bản quyền** giữa nhóm Linux và công ty BitKeeper, nhóm không được dùng công cụ này nữa.
- Chuyển sang công cụ khác thì không có gì đảm bảo chuyện cũ không lặp lại. **Linus Torvalds** (cha đẻ của Linux) quyết định: *"nếu không có công cụ nào phù hợp thì tự tạo ra một cái"*.
- Chỉ trong **vài tháng**, Git ra đời, trở thành công cụ chính thức của Linux, rồi được cộng đồng mã nguồn mở dùng rộng rãi.
- **Mục tiêu thiết kế**:
  - **Nhanh**: xử lý được dự án cỡ Linux.
  - **Đơn giản, dễ dùng**: hàng nghìn dev phải dùng được.
  - **Dễ phân nhánh**.
  - **Phân tán**: không phụ thuộc máy chủ trung tâm.

### 1.4. Nguyên lý hoạt động của Git, mẹo nhớ **"SSO"**

| Chữ | Nguyên lý | Giải thích |
|---|---|---|
| **S** | **Snapshot thay vì Diff** | Các VCS cũ chỉ lưu *phần thay đổi* (diff). Git lưu **bản chụp toàn bộ dự án** mỗi lần commit. Thoạt nghe thì có vẻ lãng phí, nhưng **file nào không đổi thì Git chỉ tạo liên kết (link) tới bản chụp cũ**, nên vẫn tiết kiệm dung lượng, nhanh, ít lỗi và dễ khôi phục. *Ví dụ khu vườn*: diff chỉ ghi "cây A cao thêm 2 cm"; Git chụp cả khu vườn, nhưng cây nào không đổi thì chỉ trỏ tới ảnh cũ |
| **S** | **Toàn vẹn dữ liệu với SHA-1** | SHA-1 là hàm băm. Mọi thứ trong Git (mỗi commit) có một **mã định danh 40 ký tự**, giống *số CMND/CCCD*, không bao giờ trùng. Nội dung thay đổi thì mã hash thay đổi hoàn toàn, giúp phát hiện dữ liệu hỏng và quay lại đúng thời điểm theo mã. Không cần nhớ mã, xem bằng `git log` |
| **O** | **Offline-first** | Hầu hết thao tác (commit, xem lịch sử, tạo/gộp nhánh) đều chạy **trên máy local**, không cần mạng. Ngồi quán cà phê không có wifi vẫn làm việc được. **Chỉ cần internet khi push/pull** để chia sẻ code |

### 1.5. Cài đặt Git

| Hệ điều hành | Lệnh / cách cài |
|---|---|
| Linux (Debian/Ubuntu) | `sudo apt install git` |
| Linux (Fedora/RHEL) | `sudo dnf install git` |
| macOS | `xcode-select --install`, Homebrew (`brew install git`) hoặc tải từ git-scm.com |
| Windows | Tải từ **git-scm.com** hoặc `choco install git` |

Kiểm tra phiên bản:
```bash
git --version
```

### 1.6. Cấu hình cơ bản
Đầu tiên cần khai báo "định danh" (tên, email) để Git biết ai là người commit:
```bash
git config --global user.name "Tên Của Bạn"
git config --global user.email "email@example.com"
git config --global core.editor "code --wait"   # editor mặc định là VS Code (có thể dùng vim, nano...)
git config --global color.ui auto

git config --list          # xem lại toàn bộ cấu hình
```
- Cấu hình global được lưu trong **một file text**: `~/.gitconfig` (file ẩn trong thư mục home). Có thể mở trực tiếp, ví dụ `code ~/.gitconfig`.

### 1.7. Alias, lệnh tắt
Mỗi ngày phải gõ đi gõ lại `git status`, `git add`, `git commit`... Alias giúp gõ nhanh hơn và đỡ phải nhớ những lệnh dài:
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
```
- Giảng viên dùng `git st`, `git ci` (commit), `git co`... Giữ tiền tố `git` để vẫn phân biệt được với các lệnh khác của hệ điều hành. Có người còn đặt alias ngắn hơn nữa; tùy sở thích.
- Lệnh xem log đẹp rất dài (`git log --graph --pretty=format:...`), nên đặt thành `git lg` (xem Phần 5).

### 1.8. Hỗ trợ & trợ giúp
- **Tài liệu chính thức**: git-scm.com.
- **Trợ giúp ngay trong terminal**: `git help`, `git --help`, `man git-<lệnh>` (ví dụ `man git-init`).
- **Cộng đồng**: Stack Overflow (giờ ít dùng hơn vì đã có ChatGPT và các công cụ AI), GitHub Discussions, các diễn đàn Git.
- **Sách "Pro Git"** (Scott Chacon), miễn phí tại git-scm.com/book. Giảng viên khuyên: *"muốn Git pro thì đọc cuốn này và thực hành"*.
- Trong công việc thực tế chỉ cần nhớ khoảng **5–10 lệnh**; lệnh nào chưa biết thì hỏi AI hoặc tra `git help`.

### ✅ Tổng kết Phần 1
- **VCS** giúp theo dõi và kiểm soát thay đổi của mã nguồn.
- **Git** do Linus Torvalds tạo năm 2005, là hệ thống **phân tán (DVCS)**.
- Git lưu **snapshot** thay vì diff, dùng SHA-1 và hoạt động theo kiểu offline-first (**SSO**).
- Cài đặt dễ trên mọi nền tảng; cấu hình bằng `git config`.
- Tài liệu phong phú, có trợ giúp ngay trong dòng lệnh, cộng đồng lớn.

> 💡 **Mindset học Git**: lúc đầu thấy *confused* là **hoàn toàn bình thường**, giống học lái xe (phanh, ga, xi-nhan, gạt mưa). Hãy **hiểu nguyên lý (tại sao)** trước khi học *làm thế nào*, rồi **thực hành thật nhiều**. Biết lý thuyết mà không ra đường thì không bao giờ lái giỏi.

---

## Phần 2 – Quy trình làm việc Git cơ bản

### 2.1. Bức tranh tổng quan: "3 khu vực + Remote"
Giảng viên vẽ sơ đồ và dùng hình ảnh **sân khấu / truyền hình**:

```
   MÁY LOCAL (Developer A)                                       ONLINE
┌──────────────────┐  git add  ┌─────────────┐ git commit ┌────────────┐  git push   ┌───────────────────┐
│ Working Directory│ ────────▶ │ Staging Area│ ─────────▶ │ Local Repo │ ──────────▶ │ Remote Repository │
│  (Hậu trường /   │           │ (Cánh gà)   │            │ (Sân khấu) │ ◀────────── │ (Truyền hình / TV)│
│  phòng trang điểm)│          └─────────────┘            └────────────┘  git pull   │   GitHub/GitLab   │
└──────────────────┘                                                                └───────────────────┘
        ▲  git status: kiểm tra trạng thái         git log: xem lịch sử                   │ git clone
        └─────────────────────────────────────────────────────────────────────────────────┘ (lần đầu)
```

| Khu vực | Liên tưởng | Ý nghĩa |
|---|---|---|
| **Working Directory** | Hậu trường / phòng trang điểm | Thư mục (workspace) đang làm việc |
| **Staging Area** | Cánh gà | Nơi "chuẩn bị" những thay đổi sẽ được lưu. Ví dụ đội bóng: **đăng ký danh sách cầu thủ ra sân** |
| **Local Repository** | Sân khấu | Lịch sử commit trong thư mục `.git` |
| **Remote Repository** | Truyền hình | Bản online trên GitHub để chia sẻ cho mọi người |

- `git clone` chỉ dùng **lần đầu** để tải repo về. Sau đó, muốn lấy thay đổi của người khác thì dùng **`git pull`**, không clone lại.
- Developer B, C, D đều có cấu trúc giống hệt trên máy của họ, vì Git là hệ thống phân tán.

### 2.2. Khởi tạo & sao chép repository
**Repository (repo)**: hiểu đơn giản là một *folder* (trên máy hoặc trên GitHub) kèm *cuốn nhật ký* lưu lịch sử của code.

**Cách 1: khởi tạo repo mới ở local rồi liên kết với GitHub**
```bash
mkdir <new_project_name>
cd <new_project_name>
git init                 # tạo thư mục ẩn .git/ để Git lưu dữ liệu và theo dõi dự án
ls -a                    # -a: hiện cả file ẩn, sẽ thấy .git
```

**Cách 2: clone repo có sẵn** (thường nhanh hơn, giảng viên hay dùng cách này)
```bash
git clone https://github.com/username/repository.git          # HTTPS
git clone git@github.com:username/repository.git              # SSH
git clone https://github.com/username/repository.git <new_name>  # đổi tên thư mục
```
- `git clone` tải về **toàn bộ lịch sử** và tạo thư mục trùng tên repo.
- **HTTPS và SSH**: HTTPS chỉ cần đăng nhập tài khoản hoặc token, dùng được trong hầu hết trường hợp. **SSH** dùng *cặp khóa* (giống chìa khóa), kết nối **bảo mật hơn**. Ngoài ra có thể *Download ZIP* nếu chỉ muốn xem code.

**Tạo repo trên GitHub** (nút **New**):
- **Repository name**, **Description** (giới thiệu ngắn).
- **Public**: ai trên internet cũng xem được. Ví dụ: repo dự án cá nhân để share lên LinkedIn khi xin việc. **Private**: chỉ mình hoặc những người được cấp quyền xem/sửa (dự án công ty).
- **README**: file mô tả dự án.
- **.gitignore**: những file không muốn đưa lên (API key OpenAI, `.env`, `__pycache__`, `.DS_Store` của Mac...).
- **License**: rất quan trọng nhưng hay bị bỏ qua.
  - **MIT**: ai cũng được dùng thoải mái, kể cả cho mục đích thương mại.
  - **BSD** và các license khác: có điều kiện riêng, cần tìm hiểu kỹ.
  - ⚠️ Dùng code của người khác cho **công ty hoặc mục đích thương mại** mà không kiểm tra license là **rất nguy hiểm**.

> 💡 **Mẹo**: trên trang repo GitHub, **nhấn phím `.`** để mở giao diện VS Code online (github.dev) xem code ngay trên trình duyệt.

**Demo trên lớp** (làm theo gợi ý của GitHub):
```bash
echo "# demo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main                                   # đổi tên nhánh master thành main
git remote add origin https://github.com/<user>/<repo>.git
git push -u origin main
```
Refresh trang GitHub sẽ thấy file README.md vừa tạo.

### 2.3. Bốn trạng thái của file

```
 Untracked ──git add──▶ Staged ──git commit──▶ Committed
                          ▲                        │
                          │ git add                │ chỉnh sửa sau khi commit
                       Modified ◀──────────────────┘
```

| Trạng thái | Mô tả | Hiển thị trong `git status` | Hành động tiếp |
|---|---|---|---|
| **Untracked** | File mới, Git chưa theo dõi. Giống *cầu thủ mới chưa đăng ký ra sân* | `Untracked files:` | `git add` |
| **Modified** | Đã thay đổi so với lần commit trước, chưa stage | `Changes not staged for commit:` | `git add` |
| **Staged** | Đã vào vùng chuẩn bị, sẵn sàng commit. Giống *diễn viên đã trang điểm xong, đứng ở cánh gà* | `Changes to be committed:` | `git commit` |
| **Committed** | Đã được lưu an toàn vào lịch sử | Không hiển thị | Không cần làm gì |

**Thao tác cơ bản:**
```bash
git status                       # xem trạng thái
git add ten-file.txt             # stage một file
git add .                        # stage tất cả file đã thay đổi
git commit -m "Mô tả ngắn về thay đổi"   # -m = message, nên viết tiếng Anh, rõ nghĩa
git push -u origin main          # lần đầu: liên kết (set upstream) với remote
git push                         # các lần sau
```

**Demo trên lớp**:
1. `touch sample.txt` và thêm nội dung, file ở trạng thái **Untracked**.
2. `git add sample.txt` chuyển sang **Staged**.
3. `git commit -m "add sample text file"` chuyển sang **Committed**.
4. `git push` đưa lên GitHub.
5. Sửa file (`echo "second line" >> sample.txt`), file thành **Modified**, rồi lặp lại add, commit, push.

**`.gitignore`**: liệt kê file/thư mục Git sẽ bỏ qua, thường gồm file log và dữ liệu tạm, thư mục build, file cấu hình cá nhân (`.env`), thư mục thư viện (`node_modules`, `vendor`).
```gitignore
# Bỏ qua thư mục build
/build/
# Bỏ qua tất cả file .log
*.log
# Bỏ qua file cấu hình cụ thể
config.ini
.env
```

### 2.4. Xem lịch sử commit: `git log`
Hiển thị mã hash (40 ký tự SHA-1), tác giả, thời gian và message của từng commit.

| Lệnh | Tác dụng |
|---|---|
| `git log` | Lịch sử đầy đủ (dài) |
| `git log --oneline` | Mỗi commit một dòng, chỉ **7 ký tự đầu** của hash. Ngắn gọn nhưng thiếu thông tin tác giả/thời gian |
| `git log -p` | Hiện **diff** (sự khác biệt) của mỗi commit |
| `git log --stat` | Số file và số dòng thay đổi mỗi commit |
| `git log --since="2 weeks ago"` | Lọc commit trong 2 tuần gần đây |
| `git log --author="Tên"` | Lọc theo người tạo, hữu ích khi làm team (ví dụ `--author="dangnha"`) |
| `git log --oneline --graph --all` | Lịch sử **dạng đồ thị** cho tất cả nhánh |

- Giảng viên tạo alias **`git lg`**: vẫn một dòng/commit nhưng có thêm thời gian, tác giả, nhánh, tag.
- Đồ thị commit **đọc từ dưới lên** (commit cũ ở dưới).
- `git show <hash>` để xem chi tiết một commit.

### 2.5. Hoàn tác thay đổi

| Tình huống | Lệnh | Mô tả |
|---|---|---|
| Đã sửa file nhưng **chưa stage** | `git restore <file>` | Khôi phục file về trạng thái của commit trước |
| Đã **stage** nhưng muốn bỏ stage | `git restore --staged <file>` | Đưa file từ Staged về Modified/Untracked ("đưa diễn viên từ cánh gà về phòng trang điểm") |
| Muốn **sửa commit gần nhất** | `git commit --amend` | Sửa message hoặc thêm file vào commit cuối. Không kèm `-m` thì mở editor để sửa |
| Muốn **hoàn tác một commit** | `git revert <commit-hash>` | Tạo **commit mới** đảo ngược thay đổi, không xóa lịch sử |

- ⚠️ **`git restore` xóa hoàn toàn thay đổi chưa commit và không khôi phục được.** Giảng viên ít dùng `restore`, mà dùng cách an toàn hơn là **stash**:
  ```bash
  git stash        # cất tạm các thay đổi
  git stash pop    # lấy lại thay đổi đã cất
  ```
- **`git reset`** quay lại phiên bản trước nhưng **ảnh hưởng lịch sử commit**, cần cẩn trọng. Có 3 chế độ `--soft`, `--mixed` (mặc định), `--hard`; riêng `--hard` **xóa hết** thay đổi phía sau commit đích.
- **Commit message phải có ý nghĩa**: "first commit" hay "update" không giúp ai hiểu gì khi xem lại. Demo trên lớp: dùng `--amend` đổi "update text file" thành "update user information".

**Công cụ hỗ trợ trong VS Code / Cursor:**
- **GitLens** (extension): có **Commit Graph** trực quan hóa lịch sử và nhánh, xem tag, có thể undo commit ngay trên giao diện.
- **Source Control** (có sẵn trong VS Code): stage, commit (nhập message), push bằng nút bấm. Có thể cài thêm extension **Git Graph**.

### 2.6. Làm việc với Remote Repository
Remote repository là bản lưu trữ dự án trên máy chủ (GitHub, GitLab, Bitbucket), dùng để cộng tác và đồng bộ.

```bash
# Quản lý remote
git remote -v                                                   # xem danh sách remote
git remote add origin https://github.com/username/repository.git  # thêm remote
git remote remove <name>                                        # xóa remote

# Đẩy thay đổi lên
git push origin main
git push --force-with-lease      # force push an toàn hơn --force

# Kéo thay đổi về
git pull origin main
git pull --rebase

# Kiểm soát chi tiết hơn: pull = fetch + merge
git fetch            # tải thay đổi về nhưng CHƯA gộp vào code local
git fetch --all
git merge origin/main
```
- **`origin`** chỉ là **tên quy ước** cho remote mặc định; có thể đặt tên khác như `upstream`, `production`.
- **`fetch`** chỉ kéo thông tin về để xem khác biệt, chưa gộp. **`pull`** làm cả fetch lẫn merge trong một bước nên tiện hơn.
- **Luồng làm việc nhóm**: Dev A `remote add`, `add`, `commit`, `push` (Version 3) lên Online Repo; Dev B, C, D `pull` về để có Version 3 rồi tiếp tục phát triển.

### 2.7. Tagging, đánh dấu phiên bản
Tag giống một **milestone**, đánh dấu các điểm quan trọng trong lịch sử (thường là bản phát hành), giúp đặt tên cho commit để dễ tham chiếu.

| Loại | Đặc điểm | Lệnh |
|---|---|---|
| **Annotated tag** | Tag đầy đủ: người tạo, ngày tạo, message. **Khuyên dùng** cho release | `git tag -a v1.0 -m "Version 1.0 - Phát hành chính thức"` |
| **Lightweight tag** | Chỉ là con trỏ tới commit, không có thông tin thêm. Dùng tạm thời/cá nhân | `git tag v1.0-beta` |

```bash
git push origin v1.0      # ⚠️ git push mặc định KHÔNG đẩy tag
git push origin --tags    # đẩy tất cả tag
git show v1.0             # xem nội dung tag
git tag                   # liệt kê tag
git tag -l "v1.*"         # tìm tag theo mẫu
```
- **Ví dụ thực tế trong ML**: tag `baseline` khi có mô hình cơ bản, rồi tag mới khi chuyển sang XGBoost/LightGBM. Giảng viên hay tạo tag **trước mỗi lần báo cáo khách hàng**.
- Tag trên GitHub cho phép **tải code tại đúng thời điểm đó** (ví dụ để deploy ở nơi khác).
- Nếu không push tag thì trên GitHub sẽ không thấy tag.

### ✅ Tổng kết Phần 2
| Chủ đề | Lệnh |
|---|---|
| Khởi tạo / sao chép | `git init`, `git clone` |
| Theo dõi & lưu | `git add`, `git commit` |
| Lịch sử & hoàn tác | `git log`, `git restore`, `git commit --amend`, `git revert` |
| Remote | `git push`, `git pull` |
| Đánh dấu phiên bản | `git tag` |

> **Khoảng 10 lệnh này cộng với kiến thức về branch là đủ cho khoảng 80% công việc hằng ngày.**

---

## Phần 3 – Quản lý nhánh và lịch sử

### 3.1. Khái niệm nhánh (Branch)
- **Nhánh là con trỏ** đến một commit cụ thể. Khi tạo commit mới, con trỏ tự động dịch theo. Vì nhánh chỉ là một file nhỏ chứa mã SHA-1 nên tạo và xóa nhánh **rất nhanh**.
- **Phát triển song song**: mỗi nhánh là một môi trường riêng để phát triển tính năng, sửa lỗi hay thử nghiệm mà **không ảnh hưởng code chính**. Nhiều người làm đồng thời mà không xung đột.
- **Lịch sử phân nhánh**: lịch sử Git giống một cái cây; các nhánh sau đó được **merge** hoặc **rebase** lại thành một lịch sử thống nhất.
- Git tự tạo nhánh **`master`** hoặc **`main`** (chỉ là tên gọi) khi `git init`. Đây là nhánh chính chứa bản ổn định.

**Tại sao nhánh quan trọng?** Nếu A, B, C cùng commit thẳng lên `main` thì nhánh sẽ rất lộn xộn và giải quyết conflict rất mệt. Ý tưởng: **mỗi người hoặc mỗi feature một nhánh riêng**, làm xong mới gộp về.

> ⚠️ **Quy tắc khi đi làm**: **không bao giờ commit trực tiếp lên `main`**. Nhánh `main` phải luôn ở trạng thái **deployable** (sẵn sàng đưa vào sử dụng). Làm việc cá nhân thì thoải mái hơn.

### 3.2. Tạo, chuyển và gộp nhánh
```bash
git branch                      # liệt kê nhánh, dấu * là nhánh hiện tại

# Tạo rồi chuyển nhánh (2 bước)
git branch feature/login
git checkout feature/login

# Tạo và chuyển cùng lúc (1 bước)
git checkout -b feature/login

# Gộp nhánh vào main
git checkout main
git merge feature/login
```
- **Đặt tên nhánh** theo quy tắc của team, ví dụ `feature/<tên>`, `fix-login-bug`.
- Trên nhánh mới, mọi commit **chỉ ảnh hưởng nhánh đó**, `main` giữ nguyên.
- Lần đầu push nhánh mới cần set upstream: `git push -u origin feature/login`. Các lần sau chỉ cần `git push`.

**Hai cách gộp nhánh (demo trên lớp):**
1. **`git merge` trực tiếp ở local**: nhanh, phù hợp khi làm một mình. Ít dùng khi làm team.
2. **Pull Request (PR) trên GitHub**: **dùng nhiều nhất khi đi làm**.
   - Push nhánh lên, GitHub hiện gợi ý **"Compare & pull request"**.
   - Viết **title** và **mô tả** (Markdown; nhiều công ty có template PR riêng).
   - **Reviewer** (thường là team leader) kiểm tra: feature có đúng yêu cầu không, có thêm thứ linh tinh không, code đã clean và đúng chuẩn chưa.
   - Đạt yêu cầu thì merge. Có ba lựa chọn:
     - **Create a merge commit**: giữ nguyên lịch sử các commit.
     - **Squash and merge**: gom nhiều commit của cùng một nhiệm vụ thành **1 commit** cho gọn.
     - **Rebase and merge**.
   - Sau khi merge: `git checkout main` rồi `git pull` để cập nhật local.

### 3.3. Giải quyết xung đột (Conflict)
- **Khi nào xảy ra**: hai nhánh **cùng sửa một dòng** (hoặc cùng vùng) trong cùng một file, rồi merge với nhau.
- **Ví dụ**: trong `model.py`, anh A thêm *Linear Regression*, anh B thêm *XGBoost* vào cùng chỗ. Lúc merge phải chọn **A, B hoặc cả hai**.
- Git đánh dấu vùng xung đột trong file (phía trên là bản hiện tại, phía dưới là bản đang merge). VS Code có nút *Accept Current / Incoming / Both*.
- **Quy trình**: sửa file theo lựa chọn, rồi:
  ```bash
  git add .
  git commit
  ```
- *"Gọi là quy trình cho oai, thực ra chỉ là hai người cùng sửa thì phải chọn một version."* Video giải bài tập 2 của STA Nhã (từ khoảng phút 46) có demo chi tiết.

### 3.4. Quản lý nhánh

| Mục đích | Lệnh |
|---|---|
| Nhánh local | `git branch` |
| Nhánh remote-tracking | `git branch -r` |
| Tất cả nhánh (local + remote) | `git branch -a` |
| Chi tiết trạng thái theo dõi remote | `git branch -vv` |
| Xóa nhánh **đã merge** | `git branch -d feature/login` |
| Xóa nhánh **chưa merge** (cẩn trọng) | `git branch -D feature/login` |
| Xóa nhánh trên remote | `git push origin --delete feature/login` |
| Đổi tên nhánh chỉ định | `git branch -m ten-cu ten-moi` |
| Đổi tên nhánh hiện tại | `git branch -m ten-moi` |
| Cập nhật tên mới lên remote | `git push origin :ten-cu ten-moi` |
| Nhánh không có lịch sử chung | `git checkout --orphan ten-nhanh-moi` (bắt đầu lại từ đầu nhưng giữ mã nguồn) |

> 💡 **Kinh nghiệm đi làm**: mỗi feature một nhánh, nên dự án có thể có hàng trăm nhánh và repo rất lộn xộn. Công ty lớn thường yêu cầu **xóa nhánh sau khi đã merge xong**, vì thay đổi và lịch sử commit đã nằm trong `main`, không còn lý do giữ nhánh cũ.

### 3.5. Nhánh remote
- **Remote-tracking branch**: tham chiếu đến trạng thái nhánh trên remote, dạng `<remote>/<branch>` (ví dụ `origin/main`). Không sửa trực tiếp được; chúng tự cập nhật khi giao tiếp với remote.
- `git fetch` cập nhật mọi remote-tracking branch mà **không thay đổi nhánh local**.

```bash
# Thiết lập theo dõi
git branch --track branch-name origin/branch-name
git branch -u origin/dev-feature        # đổi nhánh remote mà nhánh local đang theo dõi

# Tạo nhánh local từ nhánh remote
git fetch origin
git checkout -b mybranch origin/feature-x
git checkout feature-x                  # rút gọn: Git tự tạo nhánh local và thiết lập theo dõi

# Push nhánh mới lần đầu
git push -u origin feature-branch
```
- Khi clone, Git tự thiết lập `main` theo dõi `origin/main`, nên `git pull` và `git push` không cần chỉ định nhánh.

### 3.6. Rebase và Merge

```
Merge  (có "thế giới song song"):          Rebase (lịch sử "đứng thẳng"):
A ─ B ─ C ─────── M   (main)               A ─ B ─ C ─ D' ─ E'   (feature)
     \           /
      D ─── E ──┘    (feature)
```
- **Merge**: tạo **merge commit**, giữ nguyên lịch sử rẽ nhánh.
- **Rebase**: "gỡ" tạm các commit của feature (D, E), áp dụng các commit mới của main, rồi **áp lại** D, E lên trên (thành D', E'). Kết quả là lịch sử **tuyến tính**, gọn và dễ đọc.

```bash
git checkout feature-branch
git rebase main

git rebase -i HEAD~3       # rebase tương tác: sửa, gộp (squash), xóa 3 commit gần nhất
git rebase --continue      # tiếp tục sau khi giải quyết conflict
git rebase --abort         # hủy rebase
```
> ⚠️ **Không rebase các nhánh đã chia sẻ công khai.** Rebase **viết lại lịch sử** nên có thể gây rắc rối cho người khác. Chỉ rebase nhánh local hoặc nhánh bạn làm một mình.

Theo giảng viên: merge dùng nhiều trong Pull Request; rebase dùng để giữ lịch sử tuyến tính. *Chỉ cần nắm hình ảnh "song song" và "thẳng hàng" là đủ.*

### 3.7. Các workflow và mô hình nhánh phổ biến
Mô hình nhánh là quy ước giúp team làm việc nhất quán. Chọn mô hình dựa trên quy mô dự án, số thành viên, chu kỳ phát hành, văn hóa team, CI/CD và yêu cầu kinh doanh. **Có thể bắt đầu đơn giản với GitHub Flow**; quan trọng nhất là mọi người đều hiểu và tuân thủ mô hình đã chọn.

#### GitFlow (Vincent Driessen, 2010)
Phù hợp với dự án có **chu kỳ phát hành rõ ràng**, nhưng có thể quá phức tạp với dự án nhỏ hoặc dự án triển khai liên tục.

| Nhánh | Tạo từ | Vai trò | Merge về |
|---|---|---|---|
| **main** | – | Code sẵn sàng triển khai; mỗi commit được gắn **tag phiên bản** | – |
| **develop** | main | Nhánh tích hợp các tính năng đã xong nhưng chưa phát hành | – |
| **feature/\*** | develop | Mỗi tính năng một nhánh | develop |
| **release/\*** | develop | Chuẩn bị phát hành: **chỉ sửa lỗi, không thêm tính năng** | main **và** develop |
| **hotfix/\*** | main | Sửa lỗi khẩn cấp trên production | main **và** develop |

```
Master  ──●───────────────●────────●──     (V0.1, V0.2, V1.0)
Hotfix          └──●──┘
Release              ┌──●──┐
Develop ──●────●────●─────●────●──
Feature     └──●──●─┘   └──●──┘
```

#### Các workflow hiện đại
| Workflow | Đặc điểm | Phù hợp |
|---|---|---|
| **Trunk-based Development** | Commit trực tiếp vào `main` (trunk) hoặc qua nhánh tính năng **ngắn hạn**; dùng **feature flags**; bắt buộc có CI | DevOps, triển khai nhiều lần mỗi ngày |
| **GitHub Flow** | 1) Tạo nhánh từ main, 2) commit và push thường xuyên, 3) mở PR để review, 4) merge khi pass kiểm tra và được approve, 5) **deploy ngay** sau merge | Web/app có chu kỳ phát hành liên tục |
| **GitLab Flow** | GitHub Flow kết hợp **nhánh môi trường** (staging, pre-production, production); thay đổi đi từ main sang môi trường test rồi production; có hai biến thể (nhánh môi trường hoặc nhánh phát hành) | Nhiều môi trường/phiên bản; đơn giản hơn GitFlow |

Giảng viên gợi ý: team nhỏ dùng mô hình đơn giản (main + các nhánh feature, xong thì merge về main).

### ✅ Tổng kết Phần 3
- **Branch**: khái niệm, cách tạo, chuyển, gộp, quản lý nhánh local và remote.
- **Rebase & lịch sử**: tái cấu trúc lịch sử commit cho gọn.
- **Mô hình nhánh**: GitFlow và các workflow Trunk-based, GitHub Flow, GitLab Flow.
- **Hợp tác**: chọn mô hình theo quy mô và văn hóa team.

---

## Phần 4 – Cộng tác qua GitHub
> Trên lớp giảng viên chỉ nói lướt (Pull Request đã demo ở Phần 3). Phần này chủ yếu dựa theo slide; học viên tự đọc thêm.

### 4.1. Thiết lập tài khoản & bảo mật
- **Đăng ký** tại github.com. Chọn username cẩn thận vì nó xuất hiện trong URL dự án. Xác minh email.
- **Xác thực**: hỗ trợ HTTPS và SSH; **nên dùng SSH** vì bảo mật hơn và không phải nhập mật khẩu liên tục:
  ```bash
  ssh-keygen -t ed25519 -C "email@example.com"
  # sau đó thêm public key vào GitHub: Settings > SSH and GPG keys
  ```
- **Hồ sơ cá nhân**: ảnh đại diện, thông tin liên hệ.
- **Bảo mật**: bật **2FA** (ứng dụng, SMS hoặc khóa vật lý); kiểm soát quyền của ứng dụng bên thứ ba trong *Settings > Applications*.

### 4.2. Quy trình Fork & Pull Request (đóng góp open source)
1. **Fork**: nhấn nút *Fork* (góc trên phải) để tạo bản sao repo về tài khoản của bạn.
2. **Clone về local** và thiết lập `upstream` trỏ về repo gốc:
   ```bash
   git clone https://github.com/<username-cua-ban>/<ten-repo>.git
   cd <ten-repo>
   git remote add upstream https://github.com/<owner-goc>/<ten-repo>.git
   ```
3. **Tạo nhánh chủ đề**: `git checkout -b fix-login-bug` (tên mô tả ngắn gọn).
4. **Commit và push lên fork của bạn**:
   ```bash
   git add .
   git commit -m "Mô tả ngắn gọn về thay đổi"
   git push origin fix-login-bug
   ```
5. **Tạo Pull Request**: vào repo gốc, chọn *New pull request*. Nguồn là nhánh của bạn, đích là nhánh chính của repo gốc. Viết tiêu đề và mô tả rồi chọn *Create pull request*.
6. **Thảo luận và cập nhật**: chủ repo review và có thể yêu cầu sửa. Bạn commit và push thêm, PR **tự động cập nhật**. Được chấp thuận thì PR được merge.

### 4.3. Quản lý repository trên GitHub
- **Tạo và cấu hình**: nút "+" chọn *New repository*. Thêm **collaborator** trong *Settings* để cấp quyền commit.
- **Tài liệu**: `README.md` (mô tả dự án), `CONTRIBUTING.md` (hướng dẫn đóng góp), `CODE_OF_CONDUCT.md` (quy tắc ứng xử).
- **Mẫu Issue/PR** đặt trong thư mục `.github/`. Mẫu Issue để phân loại lỗi và yêu cầu; mẫu PR mô tả thay đổi, cách kiểm tra và checklist chất lượng.
- **Bảo vệ nhánh**: *Settings > Branches*. Bật bảo vệ nhánh chính để bắt buộc review, bắt buộc pass CI/CD và **chặn push trực tiếp**.

### 4.4. Organization & Teams
- **Organization**: quản lý nhiều repo và người dùng dưới một tài khoản (công ty hoặc dự án lớn). Tạo bằng "+" và *New organization*, chọn gói (Teams/Enterprise). Chuyển repo cá nhân vào bằng *Settings > Transfer ownership*.
- **Teams**: *Teams > New team*, thêm thành viên, cấp quyền repo:
  - **Read**: xem và clone
  - **Write**: push
  - **Admin**: quản lý cài đặt
  - Team có thể lồng nhau; thành viên kế thừa quyền từ team cha.
- **Audit log** (GitHub Enterprise, *Settings > Audit log*): ghi lại ai làm gì, lúc nào, thay đổi quyền, truy cập repo; xuất được để phân tích.
- **Security alerts & Dependabot**: phát hiện và khắc phục lỗ hổng trong dependencies.

### 4.5. Mẹo làm việc hiệu quả
1. **Draft Pull Request**: nhận phản hồi sớm cho code đang làm dở mà không làm mất thời gian reviewer (chọn *Create draft pull request*).
2. **Review checklist**: coding standard, test coverage, hiệu suất, bảo mật. Đưa vào template PR để mọi người tự kiểm tra trước.
3. **Đồng bộ fork thường xuyên** với upstream:
   ```bash
   git remote add upstream https://github.com/original/repo.git
   git fetch upstream
   git checkout main
   git merge upstream/main
   git push origin main
   ```

### 4.6. GitHub Desktop
Ứng dụng giao diện đồ họa (GUI) cho người mới hoặc người không thích terminal: theo dõi thay đổi trực quan, quản lý nhánh, xử lý conflict dễ dàng, tích hợp sẵn GitHub.com.
Cách dùng: tải tại desktop.github.com, đăng nhập, clone hoặc tạo repo, commit, push.

### ✅ Tổng kết Phần 4
Tài khoản và bảo mật (2FA, SSH) · Fork & Pull Request · Quản lý repo (README, license, issue template, GitHub Pages) · Organization & Teams · GitHub Desktop.

---

## Phần 5 – Tùy chỉnh & mở rộng Git
> Trên lớp giảng viên chỉ nhắc lại alias và cấu hình đã nói ở Phần 1; phần còn lại học viên tự đọc slide.

### 5.1. Cấu hình nâng cao (`.gitconfig`)
```bash
# Đặt tên nhánh mặc định khi git init (từ Git 2.28): đổi master thành main
git config --global init.defaultBranch main

# Mẫu commit message
git config --global commit.template ~/.gitmessage.txt
```
Ví dụ `~/.gitmessage.txt`:
```
# Tiêu đề: Tóm tắt ngắn gọn (< 50 ký tự)
# Nội dung: Giải thích thay đổi và lý do
# (Tối đa 72 ký tự/dòng)
# Issue liên quan: #123
```
```bash
# Dùng VS Code làm công cụ merge/diff
git config --global merge.tool vscode
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
git config --global mergetool.vscode.cmd "code --wait $MERGED"

# Proxy (mạng doanh nghiệp)
git config --global http.proxy  http://proxy.example.com:8080
git config --global https.proxy https://proxy.example.com:8080

# Lưu thông tin đăng nhập
git config --global credential.helper store                    # lưu vĩnh viễn
git config --global credential.helper cache                    # lưu tạm trong bộ nhớ
git config --global credential.helper 'cache --timeout=3600'   # lưu theo số giây
```

### 5.2. Git Attributes (`.gitattributes`)
Quy định cách Git xử lý từng loại file. Cú pháp: `pattern attr1 attr2 ...`
```gitattributes
# Chuẩn hóa line endings
* text=auto
*.txt text
*.md  text
*.bat text eol=crlf      # CRLF khi checkout (Windows)
*.sh  text eol=lf        # luôn giữ LF

# File binary (giữ nguyên nội dung, không diff/merge theo dòng)
*.png binary
*.jpg binary
*.zip binary

# Chiến lược merge
config.xml        merge=ours     # giữ bản local khi merge
generated-code.js merge=theirs   # dùng bản từ nhánh đang merge

# Clean/Smudge filters
*.c    filter=indent
*.java filter=keyword
```
- Giúp giải quyết khác biệt **CRLF (Windows)** và **LF (Unix/Mac)**, tránh các "thay đổi" không cần thiết.
- **Clean** chạy khi *thêm file vào repo*; **smudge** chạy khi *lấy file ra* (checkout). Filter khai báo trong `.gitconfig`:
  ```ini
  [filter "indent"]
      clean = indent
      smudge = cat
  ```

### 5.3. Git Hooks, tự động hóa
- Là script **tự động chạy** tại các thời điểm cụ thể trong quy trình Git, lưu trong `.git/hooks/` (file thực thi không đuôi). Muốn dùng thì bỏ đuôi `.sample` của file mẫu và chạy `chmod +x`.

| Client-side (máy dev) | Khi nào chạy |
|---|---|
| `pre-commit` | Trước commit: kiểm tra code, chạy test, lint (liên quan **pre-commit**/PEP8 đã nhắc ở phần mục tiêu) |
| `prepare-commit-msg` | Trước khi soạn commit message |
| `commit-msg` | Kiểm tra định dạng commit message |
| `post-commit` | Sau commit (thường để thông báo) |
| `pre-push` | Trước khi push lên remote |

| Server-side (máy chủ) | Khi nào chạy |
|---|---|
| `pre-receive` | Khi server nhận yêu cầu push |
| `update` | Giống pre-receive nhưng chạy riêng cho từng nhánh/ref |
| `post-receive` | Sau khi push xong, thường dùng để kích hoạt **CI/CD** |

Server-side hooks thực thi quy định hiệu quả vì người dùng **không thể bỏ qua**, nhưng cần quyền truy cập máy chủ để cài.

### 5.4. Alias & Scripts
Alias cơ bản trong `~/.gitconfig`:
```ini
[alias]
    st = status
    co = checkout
    br = branch -v
    cm = commit -m
    l = log --oneline --graph --decorate
    unstage = restore --staged
    last = log -1 HEAD
    visual = !gitk
```
Alias nâng cao (tiền tố `!` cho phép chạy shell command hoặc định nghĩa hàm):
```ini
[alias]
    # Tạo nhánh mới và chuyển sang
    nb = "!f() { git checkout -b $1; }; f"
    # Xóa tất cả nhánh đã merge vào nhánh hiện tại
    cleanup = "!git branch --merged | grep -v '\\*' | xargs -n 1 git branch -d"
    # Cập nhật nhánh hiện tại từ upstream
    sync = "!f() { git pull upstream $(git rev-parse --abbrev-ref HEAD); }; f"
    # Log đẹp (kiểu git lg giảng viên dùng)
    graph = "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

### ✅ Tổng kết Phần 5
`.gitconfig` (tùy chỉnh sâu) · `.gitattributes` (xử lý theo loại file) · Git Hooks (tự động kiểm tra trước/sau commit, push) · Alias & Scripts (tối ưu thao tác hằng ngày).

---

## 6. Kahoot – Câu hỏi ôn tập
STA Nhã tổ chức Kahoot (mỗi câu 30–45 giây).

| # | Câu hỏi | Đáp án đúng | Giải thích |
|---|---|---|---|
| 1 | Lệnh kết nối repo local với repo online? | **`git remote add origin <url>`** | `git clone` là tải repo về; `git push origin main` là đẩy code; `git pull origin` là kéo code mới về. Các lệnh liên quan đến remote đều có chữ `remote` (`remote add`, `remote remove`...) |
| 2 | Lấy thông tin **tất cả các branch** từ remote về local mà **không hợp nhất**? | **`git fetch origin`** | `git pull` kéo code **và merge** vào nhánh đang đứng. Clone mặc định chỉ checkout nhánh main; muốn biết các nhánh khác thì `fetch`. `git clone <url> --a` là lệnh không hợp lệ |
| 3 | Khôi phục file về trạng thái trước khi chỉnh sửa (chưa commit, chưa add)? | **`git restore <file>`** | `git rebase <branch>` dùng để gộp lịch sử; `git rebase --abort` hủy một lần rebase; `git reset --hard <id>` quay về commit cũ và **xóa hết** lịch sử phía sau (cẩn thận; ngoài ra còn `--soft` và `--mixed`) |
| 4 | Thứ tự khởi tạo và đẩy code lên remote: (1) add, (2) init, (3) remote add origin, (4) commit, (5) push | **2 → 3 → 1 → 4 → 5** *(và 2 → 1 → 4 → 3 → 5 cũng đúng)* | add và commit diễn ra ở local nên có thể làm trước hay sau khi `remote add`; chỉ cần `remote add` trước `push`. Câu này hóa ra có 2 đáp án đúng |
| 5 | Lệnh tạo branch mới **và chuyển sang ngay**? | **`git checkout -b <branch>`** | `git branch <name>` chỉ tạo, vẫn đứng ở nhánh cũ; `git switch <name>` (không có `-c`) chỉ chuyển sang nhánh đã có; `git branch -m` là đổi tên nhánh |
| 6 | File tạo ở `main`, **chưa add, chưa commit**, khi checkout sang nhánh khác thì sao? | **File vẫn còn ở đó, vẫn untracked** | Git chưa theo dõi file nên checkout không đụng tới nó. Nếu file đã add và commit ở main thì khi sang nhánh không có commit đó, file sẽ "biến mất" |

---

## 7. Bài tập thực hành (Hands-on)
> **Không bắt buộc nộp, không chấm điểm**, nhưng rất nên làm vì đây là kỹ năng must-have. *Làm được cả 3 bài thì đủ tự tin đi làm.*
> Lời giải: **video khoảng 2 tiếng của STA Nhã**, hướng dẫn từng bước (link gửi trong chat của buổi học). Phần merge conflict và rebase ở bài 2 bắt đầu từ khoảng **phút 46** của video.
> Bạn nào đã quen Git thì nên tự làm trước rồi mới xem video để đối chiếu. Trong lúc làm có thể hỏi ChatGPT.

### Bài 1 – Git cơ bản
| Phần | Nhiệm vụ |
|---|---|
| **1. Cài đặt & cấu hình** | Cài Git; cấu hình tên/email bằng `git config`; tạo alias cho `status` và `log`; kiểm tra bằng `git config --list` |
| **2. Tạo repo** | Tạo thư mục `git-practice`; `git init`; tạo `README.md` giới thiệu; `git status`; stage và commit |
| **3. Commit & lịch sử** | Tạo `read_data.py` rồi commit; sửa README rồi commit; xem `git log` và `git log --oneline`; `git show` xem chi tiết commit |
| **4. Hoàn tác** | Sửa `read_data.py` rồi `git restore`; thêm nội dung, stage rồi `git restore --staged`; commit rồi `git commit --amend` để sửa message |

### Bài 2 – Phân nhánh
| Phần | Nhiệm vụ |
|---|---|
| **1. Phân nhánh cơ bản** | `git branch feature-a` → `git checkout feature-a` → tạo và commit `feature-a.txt` → quay lại main quan sát khác biệt → thử `git checkout -b` |
| **2. Merge & conflict** | Ở main: commit `common.txt` với nội dung "Dòng 1: Nội dung từ main". Ở feature-a: commit `common.txt` với nội dung khác. Quay về main và `git merge feature-a`, sửa conflict để giữ cả hai nội dung, rồi `git add` + `git commit` |
| **3. Rebase** | Tạo `feature-b` từ main, 2–3 commit; quay lại main thêm 1–2 commit; ở feature-b chạy `git rebase main` (gặp conflict thì sửa rồi `git rebase --continue`); xem `git log --graph --oneline` và so sánh với kiểu merge |
| **4. Mô phỏng GitFlow** | Repo `gitflow-practice`; tạo `develop` từ main; commit trên `feature/login`, rồi `git merge --no-ff feature/login` vào develop; sửa lỗi trên `release/v1.0`, merge vào **main và develop**, tạo tag `v1.0`; hotfix tạo từ main, sửa xong merge về cả main và develop |

### Bài 3 – Cộng tác GitHub
| Phần | Nhiệm vụ |
|---|---|
| **1. Fork & Clone** | Tìm một dự án open source nhỏ, Fork, clone về, thêm remote `upstream`, kiểm tra bằng `git remote -v` |
| **2. Pull Request** | Tạo nhánh mới; sửa nhỏ (lỗi chính tả, tài liệu, comment); commit và push lên fork; tạo PR vào repo gốc kèm mô tả chi tiết |
| **3. Code Review** | Tìm một PR đang mở; đọc thay đổi; comment vào từng dòng; viết review tổng thể (Approve / Comment / Request Changes); review chéo PR với bạn học |
| **4. Quản lý dự án** | Tạo repo "dự án cá nhân"; viết README chi tiết (mô tả, cài đặt); `CONTRIBUTING.md`; Issue templates (bug, feature); tạo vài Issue mẫu; thử bật **GitHub Pages** |

> Giảng viên chia sẻ thêm một **repo mẫu** của dự án trong chuỗi bài học (cấu trúc thư mục docs, notebooks, source code, README, file environment, `.gitignore`, license) để hình dung sản phẩm khi đi làm trông như thế nào.

---

## 8. Cheat sheet – ~10 lệnh dùng nhiều nhất
> *"Khoảng 10 lệnh này cộng với branching là đủ cho khoảng 80% công việc."*

| # | Lệnh | Dùng khi |
|---|---|---|
| 1 | `git init` | Khởi tạo repo mới (lần đầu) |
| 2 | `git clone <url>` | Tải repo có sẵn về máy (lần đầu) |
| 3 | `git status` | Xem trạng thái file |
| 4 | `git add <file>` / `git add .` | Đưa thay đổi vào staging |
| 5 | `git commit -m "msg"` | Lưu snapshot vào lịch sử |
| 6 | `git log` (`--oneline --graph --all`) | Xem lịch sử |
| 7 | `git restore` / `git restore --staged` | Hoàn tác thay đổi chưa commit / bỏ stage |
| 8 | `git commit --amend` / `git revert <hash>` | Sửa commit cuối / hoàn tác một commit |
| 9 | `git push` / `git pull` | Đẩy lên / kéo về remote |
| 10 | `git tag -a v1.0 -m "..."` | Đánh dấu phiên bản |
| + | `git branch`, `git checkout -b`, `git merge`, `git rebase` | Làm việc với nhánh |
| + | `git remote add origin <url>`, `git fetch` | Kết nối remote / lấy thông tin mà không merge |
| + | `git stash` / `git stash pop` | Cất tạm thay đổi (an toàn hơn restore) |

**Quy trình hằng ngày:**
```bash
git checkout main && git pull           # cập nhật code mới nhất
git checkout -b feature/<ten>           # tạo nhánh cho tính năng
# ... code ...
git status
git add .
git commit -m "Add <feature>"
git push -u origin feature/<ten>        # rồi mở Pull Request trên GitHub
# sau khi PR được merge:
git checkout main && git pull
git branch -d feature/<ten>             # dọn nhánh đã merge
```

---

## 9. Tài liệu tham khảo

| Nhóm | Tài nguyên |
|---|---|
| **Tài liệu chính thức** | Pro Git Book: https://git-scm.com/book/en/v2 · Git docs: https://git-scm.com/doc · GitHub docs: https://docs.github.com · GitHub Guides: https://guides.github.com |
| **Khóa học online** | Atlassian Tutorials: https://www.atlassian.com/git/tutorials · GitHub Learning Lab: https://lab.github.com · Codecademy: https://www.codecademy.com/learn/learn-git |
| **Blog** | https://www.atlassian.com/blog/git · https://www.git-tower.com/blog · https://github.blog |
| **GUI** | GitKraken · Sourcetree · GitHub Desktop (https://desktop.github.com) · VS Code + Git Extensions (GitLens, Git Graph) |
| **CLI** | GitHub CLI (https://cli.github.com) · Lazygit · tig · diff-so-fancy |
| **Tiện ích mở rộng** | Git Flow (gitflow-avh) · Git LFS (https://git-lfs.github.com) · Husky (Git hooks cho JS) · Conventional Commits (https://www.conventionalcommits.org) |

---

### 📌 Thông điệp cuối buổi
- Git là **must-have**. Hãy học ngay từ khi còn đi học, đừng đợi vào công ty mới học.
- Ban đầu thấy confused là bình thường. Hãy **nắm bức tranh tổng quan** (Working Directory, Staging, Local Repo, Remote) và khoảng 10 lệnh chính, rồi **thực hành thật nhiều** để quen tay, giống như học lái xe.
- Buổi sau (thứ 7): **Unix/Linux for Data Science**, sẽ học chi tiết các lệnh terminal (`mkdir`, `cd`, `ls -a`, `touch`, `echo`...) đã dùng trong buổi này.
