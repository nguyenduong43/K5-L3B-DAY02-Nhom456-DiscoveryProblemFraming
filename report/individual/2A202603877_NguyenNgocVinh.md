# Báo cáo cá nhân — 2A202603877_NguyenNgocVinh

> Đổi tên file theo quy tắc `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md` (MSSV trước, dấu `_`, họ tên viết liền không dấu). Sửa cả dòng tiêu đề phía trên cho khớp.
> Template chi tiết và prompt mẫu cho từng mục: [docs/01-worksheet.md](../../docs/01-worksheet.md).
> Mỗi thành viên một file trong `report/individual/` trên repo nhóm: copy template này thành file mới, điền, rồi commit bằng tài khoản GitHub của bạn. Không viết hộ người khác.

## 1. Thông tin học viên

- Họ tên:Nguyễn Ngọc Vinh
- MSSV:2A202603877
- Email trường (không bắt buộc, repo có thể để public):
- Tên nhóm: Nhom456
- Link repo nhóm: https://github.com/nguyenduong43/K5-L3B-DAY02-Nhom456-DiscoveryProblemFraming

---

## 2. Scan problem (CP1)

Lăng kính: **Lặp lại** · **Tốn thời gian** · **Cần đọc, tổng hợp nhiều thông tin** · **Pain từ người khác**.

| # | Lăng kính | Job Story: Khi… tôi muốn… để… | Ai chịu ảnh hưởng? | Dấu hiệu thật (thời gian, tần suất, số người, bằng chứng) |
|---:|---|---|---|---|
| 1 | Lặp lại | Khi kết thúc đợt benchmark GPU (CUDA/OpenMP), tôi muốn tự động gom số liệu execution time và Speedup thành bảng Markdown, để không phải nhập tay từng dòng log | Sinh viên nghiên cứu, DEV | 2–3 đợt test/tuần, mỗi lần mất 25 phút copy log terminal từ WSL/Colab |
| 2 | Cần đọc, tổng hợp | Khi cần tóm tắt các file tài liệu PDF/văn bản dung lượng lớn cho đồ án tốt nghiệp, tôi muốn phân tách và tổng hợp tự động theo MapReduce, để nắm nhanh nội dung chính mà không bỏ sót ý quan trọng | Thành viên nhóm đồ án, PM | Đọc tài liệu 50–100 trang mất 3–4 tiếng/lần, trung bình 2 lần/tuần |
| 3 | Tốn thời gian | Khi chuẩn bị cho các bài thi tiếng Anh B2 (APTIS/VSTEP), tôi muốn tổng hợp các dạng bài viết và nhận phản hồi ngữ pháp nhanh, để cải thiện điểm số đúng trọng tâm | Học viên luyện thi B2 | Mất 45 phút/bài viết để tra từ điển và kiểm tra cấu trúc, 3 bài/tuần |
| 4 | Pain từ người khác | Khi người dùng hệ thống spa (BestSpa) gặp lỗi trên trang live, tôi muốn tự động trích xuất log từ Nginx/PM2 và gửi về channel Slack, để team dev sửa lỗi ngay mà không cần ssh thủ công | Devops, Team Dev | Vận hành server bị trễ 15–30 phút mỗi lần tra log thủ công trên Ubuntu server |
| 5 | Lặp lại | Khi chuẩn bị họp standup nhóm 13 hằng tuần, tôi muốn tự động trích xuất các commit log từ GitHub Actions và công việc đã xong, để làm slide báo cáo cho giảng viên | Nhóm 13, Giảng viên | Mất 30 phút trước mỗi buổi họp thứ Hai |
| 6 | Cần đọc, tổng hợp | Khi tìm kiếm các hàm API trong backend Go (Gorilla Mux/GORM), tôi muốn tra nhanh cấu trúc DTO/Schema SQL tương ứng, để viết API frontend Next.js không bị lệch kiểu dữ liệu | Full-stack Dev | Mất 10–15 phút tìm trong các file repo backend, lặp lại 4–5 lần/ngày |
| 7 | | | | |
| 8 | | | | |

**Nếu có dùng AI để gợi ý thêm:** ý nào AI gợi ý mà bạn giữ lại, ý nào bỏ và vì sao.

- AI gợi ý: "Khi có lỗi GPU CUDA OOM (Out of Memory), tự động chỉnh sửa block/grid dimension và biên dịch lại code." → **Bỏ**: Vì việc tối chỉnh tham số CUDA phụ thuộc vào kiến trúc phần cứng (T4 vs RTX), AI dễ suy đoán vô căn cứ gây lỗi biên dịch nghiêm trọng.
- AI gợi ý: Ý #2 về việc tổng hợp văn bản dài dùng MapReduce LLM → **Giữ**: Đây đúng là bottleneck thực tế trong dự án tốt nghiệp SummarEase mà tôi đang phát triển.

---

## 3. Top 3 Problem Cards + quy trình nháp (CP2)

### Bảng chọn top 3

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---:|---|---|---|
| 1 | Tóm tắt văn bản dài cho đồ án (Problem #2) | Vấn đề cốt lõi của đồ án tốt nghiệp SummarEase, tốn nhiều thời gian đọc tài liệu | Chi phí gọi API LLM (Gemini/OpenAI) và giới hạn context window |
| 2 | Tổng hợp số liệu Benchmark GPU (Problem #1) | Quy trình lặp đi lặp lại nhiều lần trong môn Song song hóa | Định dạng log từ C++/CUDA không đồng nhất giữa các lần chạy |
| 3 | Trích xuất log sự cố Nginx/PM2 (Problem #4) | Ảnh hưởng trực tiếp đến quy trình CI/CD và vận hành server | Quyền riêng tư và bảo mật log hệ thống |

### Problem Card #1

| Trường | Nội dung |
|---|---|
| Job Story | Khi nhận được tài liệu nghiên cứu/báo cáo dài (>50 trang), tôi muốn có bản tóm tắt phân tầng MapReduce, để nắm bắt luận điểm chính dưới 10 phút |
| Actor | Sinh viên thực hiện đồ án tốt nghiệp, PM |
| Thời điểm / bối cảnh | Trước các buổi báo cáo tiến độ đồ án hoặc khi đọc tài liệu tham khảo mới |
| Quy trình hiện tại (3–7 bước) | 1. Tải PDF về local → 2. Đọc lướt Mục lục & Kết luận → 3. Đọc chi tiết từng chương → 4. Ghi chú tay vào Notion/Docs → 5. Tổng hợp lại thành slide/báo cáo ngắn |
| Bottleneck (bước nào, mất bao nhiêu phút) | Bước 3 & 4 (Đọc chi tiết & Ghi chú): Mất khoảng 180 phút/tài liệu |
| Impact (nếu không giải thì sao) | Trễ tiến độ làm tổng quan tài liệu (Literature Review), bỏ sót các công trình nghiên cứu liên quan |
| Success metric (baseline → target) | Thời gian đọc & tổng hợp từ 180 phút xuống 25 phút/tài liệu; giữ nguyên độ chính xác các ý chính |
| Phương án không dùng AI | Dùng từ khóa (Ctrl+F) trích xuất đoạn quan trọng + Đọc Executive Summary có sẵn |
| Giả thuyết về AI (nếu có) | Sử dụng MapReduce LLM architecture (chia nhỏ văn bản -> tóm tắt từng phần (Map) -> tổng hợp lại (Reduce)) |
| Cảm nhận nhanh | Workflow |

Quy trình nháp hiện tại:

```text
HIỆN TẠI — 180 phút

[1. Tải PDF: 5'] → [2. Đọc lướt Mục lục: 10'] → [3. Đọc chi tiết: 120'] ← BOTTLENECK
→ [4. Ghi chú Docs: 40'] ← BOTTLENECK → [5. Tổng hợp slide: 5']
```

### Problem Card #2

| Trường | Nội dung |
|---|---|
| Job Story | Khi kết thúc đợt test kernel CUDA (2D Convolution/LBM), tôi muốn tự động gom log execution time và Speedup thành bảng Markdown, để đưa vào báo cáo môn Lập trình song song mà không phải dán thủ công |
| Actor |Sinh viên nghiên cứu, Lập trình viên GPU & Parallel Computing |
| Thời điểm / bối cảnh |Sau mỗi đợt chạy script benchmark trên Google Colab (NVIDIA T4) hoặc môi trường WSL Ubuntu 24.0 |
| Quy trình hiện tại (3–7 bước) |1. Biên dịch và chạy binary C++/CUDA trên terminal → 2. Copy thủ công console log xuất ra → 3. Dán số liệu execution time vào Google Sheets → 4. Nhập công thức tính Speedup ($T_{seq}/T_{par}$) → 5. Format thành bảng Markdown |
| Bottleneck (bước nào, mất bao nhiêu phút) |Bước 3 & 4 (Dán số liệu & tính Speedup): Mất khoảng 15–20 phút/lần test do nhập thủ công và đối chiếu dữ liệu |
| Impact (nếu không giải thì sao) |Mất 25 phút/lần test (2–3 đợt/tuần); dễ nhầm lẫn số liệu giữa các phiên bản kernel khác nhau trong báo cáo nhóm 13 |
| Success metric (baseline → target) |Thời gian xử lý từ 25 phút xuống dưới 3 phút/báo cáo; đảm bảo 0% lỗi sai số liệu |
| Phương án không dùng AI |Viết Python script / Bash script dùng RegEx để parse log console và xuất thẳng ra file Markdown/CSV |
| Giả thuyết về AI (nếu có) |AI nhận diện console log không chuẩn hóa, tự động phân tích cấu trúc kernel và tổng hợp bảng so sánh |
| Cảm nhận nhanh | Rule |

Quy trình nháp hiện tại:

```text
[1. Chạy CUDA binary: 2'] → [2. Copy console log: 3'] → [3. Nhập số Sheets: 10'] ← BOTTLENECK
→ [4. Tính Speedup: 5'] ← BOTTLENECK → [5. Format Markdown: 5']
```

### Problem Card #3

| Trường | Nội dung |
|---|---|
| Job Story | Khi ứng dụng web bị lỗi runtime (panic/error) trên server live, tôi muốn tự động trích xuất đoạn stacktrace và nguyên nhân chính, để team dev sửa lỗi ngay mà không phải SSH tra log thủ công |
| Actor |Developer vận hành hệ thống / DevOps (RoamRoles, BestSpa) |
| Thời điểm / bối cảnh |Khi nhận báo lỗi từ khách hàng hoặc hệ thống ghi nhận lỗi 5xx trên server Nginx/PM2 (Ubuntu) |
| Quy trình hiện tại (3–7 bước) |1. SSH vào server Ubuntu → 2. Mở file log PM2/Nginx/Go API → 3. Grep timestamp thời điểm xảy ra lỗi → 4. Copy đoạn stacktrace về máy cá nhân → 5. Đọc phân tích tìm dòng code gây ra crash |
| Bottleneck (bước nào, mất bao nhiêu phút) |Bước 2 & 3 (Tìm và lọc file log): Mất 10–15 phút lật tìm giữa hàng ngàn dòng log server |
| Impact (nếu không giải thì sao) |Mất 20 phút/lần xử lý sự cố; gián đoạn dịch vụ web live, làm chậm quy trình xử lý bug |
| Success metric (baseline → target) |Thời gian trích xuất và phát hiện nguyên nhân từ 20 phút xuống dưới 3 phút/sự cố |
| Phương án không dùng AI |Cấu hình Grafana/Loki hoặc viết Bash script `grep -E "ERROR |
| Giả thuyết về AI (nếu có) |AI tự động phân tích log lỗi, đối chiếu với source code trên Git và gợi ý ngay dòng code bị crash |
| Cảm nhận nhanh | Workflow |

Quy trình nháp hiện tại:

```text
[1. SSH Server: 2'] → [2. Tìm file log: 3'] → [3. Grep timestamp log: 10'] ← BOTTLENECK
→ [4. Copy stacktrace: 2'] → [5. Phân tích nguyên nhân: 3']

```

### Card muốn pitch nhất

- Card số:1
- Vì sao:Vấn đề có tính thực tiễn cao, quy trình phức tạp (xử lý tài liệu lớn vượt context window của LLM thông thường), phù hợp áp dụng mô hình MapReduce
- Câu hỏi muốn nhóm phản biện:"Liệu phương pháp MapReduce có làm mất tính mạch lạc giữa các chương trong tài liệu dài không?"

### AI đã phản biện card thế nào

| Điểm yếu AI chỉ ra | Đồng ý? | Đã sửa gì |
|---|---|---|
|Metric thời gian 180 phút chỉ ước lượng |Đồng ý |Đã đo thực tế trong đợt làm báo cáo tổng quan tuần trước |
|Card #2 chọn AI là dư thừa vì RegEx/Script giải quyết hoàn hảo |Đồng ý | Chuyển Card #2 sang hướng "Rule/Script" không dùng AI|
|Chưa làm rõ Boundary cho Card #1: AI có được tự bịa các số liệu nghiên cứu không? |Đồng ý |Thêm boundary: AI không được đưa thông tin ngoài nội dung PDF gốc |

---

## 4. Tôi đã tham gia phần nào (CP3 → CP7)

| Hoạt động | Tôi đã làm gì? | Kết quả / ảnh hưởng tới bài nhóm |
|---|---|---|
| Pitch Problem Card |Pitch Card bài toán rà soát & ghép báo cáo nhóm sát deadline. |Được nhóm đánh giá cao về tính thực tế và đưa vào shortlist thảo luận. |
| Phản biện bài của bạn khác | Câu hỏi tôi đã đặt: "Nếu dùng AI tự động sửa bài của thành viên khác, làm sao đảm bảo AI không làm sai ý đồ nội dung của họ?" |Giúp nhóm nhận ra rủi ro về Boundary, không chọn phương án để AI tự động sửa bài. |
| Nhận phản biện | Câu hỏi tôi nhận được: "Nếu AI duyệt bài nhanh hơn nhưng bỏ sót mâu thuẫn số liệu thì sao?" | Tôi đã sửa gì: Bổ sung thêm metric "Phát hiện 100% mâu thuẫn số liệu" vào Success Metric v1. |
| Gom cluster / cây OST |Cùng nhóm phân loại các candidate bài toán thành 3 Cluster chính và xây dựng cây Opportunity Solution Tree (OST). |Loại bỏ các "Solution đội lốt Opportunity" (như Chatbot AI tự động làm báo cáo). |
| Chọn candidate problem |Cùng nhóm chấm điểm 3 candidate theo 7 tiêu chí trong bảng shortlist. |Thống nhất chọn bài toán Rà soát mâu thuẫn số liệu & lệch cấu trúc khi ghép báo cáo nhóm. |
| Kiểm chứng / research |Tìm hiểu các giải pháp đối chiếu ngữ cảnh văn bản hiện có (Prompts rà soát Cross-check, các tool lật lỗi format). |Xác định được khoảng trống: các tool hiện tại chưa kiểm tra được mâu thuẫn ngữ cảnh/số liệu giữa nhiều người viết. |
| Quy trình nhóm |Đóng góp xây dựng sơ đồ To-Be, xác định rõ bước nào AI kiểm tra ngữ cảnh và bước nào nhóm trưởng duyệt bài. |Thiết lập ranh giới rõ ràng: AI chỉ đưa ra danh sách cảnh báo, con người kiểm duyệt trước khi merge. |
| Problem Statement |Phản biện Problem Statement v0 và trực tiếp cập nhật lên phiên bản v1. |Thu hẹp chính xác Actor và bổ sung tiêu chí độ chính xác mâu thuẫn số liệu vào Success Metric. |
| Mức can thiệp AI |Chủ trì phân tích Ma trận Mơ hồ × Phức tạp, so sánh 4 mức No AI/Rule/Workflow/Agent, điền AI Canvas & 2 câu hỏi PAIR. |Chốt chọn mức Workflow (kết hợp Script + LLM), giúp nhóm tránh sa đà làm Agent quá phức tạp và tốn chi phí. |
| Quyết định |Chủ trì đánh giá 4 rủi ro Cagan (Value, Usability, Feasibility, Viability), xây dựng điều kiện Pilot 2 tuần & Ngưỡng dừng. |Đưa ra quyết định Go kèm ngưỡng dừng rõ ràng: dừng pilot nếu lỗi bỏ sót mâu thuẫn > 20% hoặc cảnh báo giả > 50%. |

---

## 5. Dùng AI

| Checkpoint | Tôi dùng AI để làm gì? | AI hữu ích ở đâu? | AI sai hoặc hời hợt ở đâu? | Tôi sửa gì bằng nhận định của mình? |
|---|---|---|---|---|
| CP1 Scan |Prompt AI gợi ý thêm các vấn đề lặp lại/tốn thời gian theo góc nhìn của một sinh viên CNTT/Dev. |Gợi ý thêm được ý về rủi ro trích xuất log server vận hành. |Gợi ý ý quá xa thực tế và nguy hiểm: "Tự động sửa bug CUDA khi bị OOM". |Loại bỏ các ý AI gợi ý không khả thi; chỉ giữ lại 6 ý có quy trình thủ công và số phút đo được thật. |
| CP2 Problem Card |Đóng vai PM hoài nghi để tự phản biện 3 Problem Cards cá nhân. |Chỉ ra rất đúng điểm yếu ở Card #2 (GPU Benchmark) là dùng Script Python/RegEx 5 phút là xong, dùng AI là thừa thãi. |Đánh giá hời hợt rủi ro trích xuất text từ các file PDF scanned (dạng ảnh). |Chuyển Card #2 sang mức Rule/Script, bổ sung thêm bước OCR xử lý file PDF dạng ảnh cho Card #1. |
| CP4 Research | | | | |
| CP5 Quy trình | | | | |
| CP5–6 Problem Statement | | | | |
| CP6 Mức can thiệp / quyết định | | | | |

---

## 6. Reflection (CP7)

Trả lời bằng trải nghiệm thật của bạn, tối thiểu 200 từ cho các câu 6.1–6.6 (không tính 6.7, câu này được chấm riêng ở tiêu chí C5). **Không dùng AI để viết thay.**

**6.1. Tôi học được gì khi nghe top 3 problems của các bạn khác?**
-Tôi học được việc khả năng sáng tạo và áp dụng tốt được vào đời sống, giải quyết những vấn đề mà có thể tối ưu chi phí và thời gian bằng AI được.
**6.2. Nhóm có lúc nào bị "solution-first" (nghĩ giải pháp trước khi hiểu vấn đề) không? Lúc đó nhóm nhận ra và xử lý thế nào?**
-Không
**6.3. Tôi có đổi ý sau khi bị phản biện không? Kể một lần cụ thể.**
-Có, khi tôi bị hỏi về vấn đề có thứ đá thay thế được cái AI này của tôi rồi thì tôi đã thay đổi hướng tiếp cận cái vấn đề theo hướng khác
**6.4. Kết quả kiểm chứng (phỏng vấn/survey/research) có làm tôi bất ngờ không? Điều gì?**
-Không
**6.5. Điều khó nhất khi viết Problem Statement là gì?**
-Điều khó nhất là tách biệt hoàn toàn vấn đề ra khỏi giải pháp  và thiết lập một ranh giới thực sự rõ ràng.
**6.6. Nếu làm lại, tôi sẽ đổi gì? Tôi sẽ phản biện nhóm mạnh hơn ở điểm nào?**
-Tôi sẽ thay đổi về việc tôi sẽ không chỉ hỏi chung chung về "thời gian đọc tài liệu", tôi sẽ chuẩn bị sẵn một bản tóm tắt mẫu do AI tạo ra để đưa trực tiếp cho người được phỏng vấn đọc thử. Tôi sẽ phản biện nhóm quyết liệt hơn khi có các ý tưởng muốn dựng "AI Agent tự do" để tóm tắt tài liệu. Tôi sẽ ép nhóm phải phân tích kỹ Ma trận Độ mơ hồ × Độ phức tạp ngay từ đầu để thấy rằng một Workflow định sẵn các nấc xử lý (Pre-process -> Map -> Reduce) mới là lựa chọn an toàn
**6.7. Hiểu bài:** giải thích bằng 5–8 câu, không nhìn tài liệu, chuỗi *problem → quy trình → metric → boundary → mức can thiệp AI → quyết định* của bài nhóm mình.
Bài toán xuất phát từ problem thực tế của sinh viên khi mất đến 180 phút để đọc và ghi chú thủ công một tài liệu nghiên cứu/PDF dài 50–100 trang cho đồ án tốt nghiệp. Để giải quyết, nhóm xây dựng quy trình mới chuyển đổi từ 5 bước thủ công sang pipeline tự động hóa: nhận file PDF, tự động chia nhỏ (chunking), gọi AI tóm tắt phân tầng và sinh viên kiểm duyệt bản nháp. Metric mục tiêu của giải pháp là giảm tổng thời gian tổng hợp từ 180 phút xuống dưới 25 phút, đồng thời giữ tỉ lệ bịa đặt thông tin (hallucination) ở mức 0%. Nhóm thiết lập boundary rất chặt chẽ: AI tuyệt đối không tự bịa thông tin ngoài file PDF và bắt buộc phải có con người kiểm duyệt (Human-in-the-loop) chứ AI không tự gửi báo cáo. Vì các nấc xử lý đã cố định nhưng nội dung đầu ra có độ mơ hồ ngôn ngữ cao, nhóm chọn mức can thiệp AI là Workflow (kết hợp script lập trình Python xử lý file + LLM ở bước Map/Reduce) thay vì dựng Agent phức tạp. Đánh giá qua 4 rủi ro sản phẩm cho thấy feasibility và value rất rõ ràng, dẫn đến quyết định Go để triển khai bản pilot 2 tuần kèm ngưỡng dừng cụ thể nếu tỉ lệ sai sót vượt quá 15%.
---

## 7. Tài liệu tham khảo

1. **Teresa Torres**, *Continuous Discovery Habits: Discover Products That Create Customer Value and Business Value*, Product Discovery Group, 2021. *(Khung Opportunity Solution Tree - OST & Interview Snapshot)*
2. **Rob Fitzpatrick**, *The Mom Test: How to talk to customers & find out if everyone is lying to you when everyone else is lying to you*, Founder Centric, 2013. *(Phương pháp phỏng vấn kiểm chứng nỗi đau người dùng)*
3. **Marty Cagan**, *Inspired: How to Create Tech Products Customers Love*, O'Reilly Media, 2017. *(Khung đánh giá 4 Rủi ro Sản phẩm: Value, Usability, Feasibility, Viability)*
4. **Jeff Gothelf & Josh Seiden**, *Lean UX: Designing Great Products with Agile Teams*, O'Reilly Media, 2021. *(Phương pháp xây dựng Problem Statement & Hypothesis-driven design)*
