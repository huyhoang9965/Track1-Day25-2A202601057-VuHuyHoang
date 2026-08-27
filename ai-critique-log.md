
# AI Critique Log — Day 25: AI Pricing · GTM · Evidence

**Học viên:** Vũ Huy Hoàng**Mã học viên:** 2A202601057**Sản phẩm:** Internova**Ngày thực hiện:** 27/08/2026

> Mục tiêu: sử dụng AI để phản biện các giả định về Cost/Job, Pricing và GTM của Internova; sau đó tự đánh giá từng đề xuất theo **Accept / Reject / Partial**. Quyết định cuối cùng vẫn do người làm bài chịu trách nhiệm.

---

# Prompt 1 — §4.7.1 Cost/Job Stress Test

## Input sử dụng

- **Product:** Internova — nền tảng AI/RAG hỗ trợ sinh viên trong quá trình thực tập.
- **1 completed job:** một yêu cầu hỗ trợ thực tập được AI giải quyết trọn vẹn bằng câu trả lời grounded/có nguồn, người dùng không cần hỏi lại và không phải chuyển cho staff.
- **Job attempts/tháng:** 200
- **Containment dùng trong pricing model:** 78%
- **Completed jobs/tháng:** 156
- **Cost/Job chưa overhead:** $0.1177
- **Fully-loaded Cost/Job:** $0.2459
- **Retry rate:** 8%
- **Internal QA:** 10%
- **Giá usage đề xuất:** $0.40/completed job
- **Gross Margin:** khoảng 70.6%
- **Breakeven containment để duy trì GM ≥60%:** khoảng 57.4%
- **HITL:** Variant A — Internova cung cấp software; Career Services xử lý các trường hợp cần escalation, trong khi Internova vẫn chịu chi phí QA/monitoring nội bộ.

## Kết quả phản biện

| Nhận xét phản biện                                                                                                          | Quyết định     | Lý do / Hành động                                                                                                                                          |
| ------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Containment 78% chưa nên được coi là kết quả của một frozen Eval ≥150 cases nếu chưa có snapshot đo tương ứng | **Accept**  | Giữ 78% làm**pricing assumption**. Internova đã có logging và observability để đo, nhưng không biến assumption thành measured evidence.     |
| Mẫu số Cost/Job phải là completed jobs, không phải toàn bộ attempts                                                     | **Accept**  | 200 attempts × 78% = 156 completed jobs. Đây là mẫu số đúng để tính Cost/Job.                                                                       |
| Retry 8% và QA 10% vẫn là các giả định cần được thay bằng telemetry thực tế khi có đủ dữ liệu                | **Accept**  | Không đặt retry/QA bằng 0 để làm mô hình đẹp. Giữ assumption hiện tại và cập nhật khi có dữ liệu vận hành.                               |
| Cost/Job $0.1177 thấp hơn fully-loaded Cost/Job $0.2459 khá nhiều                                                           | **Partial** | Gross Margin vẫn tính trên COGS trực tiếp, nhưng khi đánh giá profitability tổng thể phải theo dõi cả overhead, support, R&D và sales.          |
| HITL Variant A phù hợp với mô hình software B2B của Internova                                                             | **Accept**  | Career Services của khách hàng xử lý các escalation nghiệp vụ; Internova chịu QA, monitoring và technical support.                                   |
| Infra $0.02/job cần được kiểm tra lại khi traffic tăng                                                                   | **Accept**  | Chi phí database, vector search, embedding, Redis, storage và observability có thể tăng theo scale. Sau pilot cần phân bổ cloud bill theo usage thực. |
| Mô hình nhạy với containment hơn là chỉ nhạy với token price                                                           | **Accept**  | Nếu containment giảm mạnh, số completed jobs giảm và Cost/Job tăng. Giữ**57.4%** như financial guardrail để duy trì GM ≥60%.                |

## Kết luận Prompt 1

Mô hình Cost/Job hiện tại được **giữ nguyên** vì vẫn đáp ứng các guardrail tài chính của bài.

Tuy nhiên, cần phân biệt rõ:

- **78% containment là pricing assumption** trong financial model.
- Internova hiện đã có **job-level logging, groundedness tracking, source tracking và RAG Analytics** để hỗ trợ Eval.
- Không claim 78% là kết quả của một frozen ≥150-case evaluation nếu chưa có snapshot tương ứng.

Về vận hành, target containment nên duy trì **≥75%**, cao hơn đáng kể so với financial breakeven khoảng **57.4%**, để tạo vùng an toàn cho Gross Margin.

---

# Prompt 2 — §4.7.3 Channel Reality Check

## Input sử dụng

- **ARPU:** khoảng $57.48/tháng/tổ chức
- **Annual Contract Value:** khoảng $689.71/năm
- **Gross Margin:** khoảng 70.6%
- **CAC budget:** khoảng $730/khách
- **Sales-driven CAC stress test:** khoảng $32,000
- **CAC gap:** khoảng 43.8×
- **GTM hypothesis:** Partner-Led
- **Partner hypothesis:** TopCV Vietnam
- **Primary pilot surface:** VinUni Student Portal / LMS
- **Pain Moment:** 21:00–23:00, đặc biệt 24–48 giờ trước deadline thực tập.

## Kết quả phản biện

| Nhận xét phản biện                                                                             | Quyết định     | Lý do / Hành động                                                                                                                 |
| -------------------------------------------------------------------------------------------------- | ----------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Sales-Led không kinh tế ở mức ACV hiện tại                                                   | **Accept**  | CAC budget chỉ khoảng $730 trong khi stress-test CAC cho rep-driven sales có thể lên tới khoảng $32,000.                       |
| 0.87 deal/AE/ngày là quá cao với B2B education                                                 | **Accept**  | Procurement đại học thường có decision cycle dài; gần 1 hợp đồng/ngày không thực tế cho enterprise-style sales motion. |
| Partner-Led phù hợp hơn về economics nhưng chưa được chứng minh hoàn toàn              | **Accept**  | Đây vẫn là channel hypothesis cần được kiểm chứng bằng interaction thực tế với partner.                                 |
| Partner phải nhận được value rõ ràng, không chỉ đóng vai trò distribution              | **Accept**  | Internova phải giúp partner tăng engagement, chất lượng internship workflow hoặc giá trị cho sinh viên/doanh nghiệp.       |
| Pain Moment hiện xảy ra chủ yếu trong Student Portal/LMS, không phải trực tiếp trên TopCV | **Partial** | VinUni Portal/LMS là điểm nhúng tốt nhất cho pilot đầu; TopCV phù hợp hơn cho phase distribution/mở rộng.                |
| Partner-Led tạo dependency risk                                                                   | **Accept**  | Cần có falsification test rõ ràng và không phụ thuộc vô thời hạn vào một partner duy nhất.                              |
| PLG chưa phù hợp làm GTM motion chính                                                         | **Accept**  | End-user là sinh viên nhưng người trả tiền là tổ chức; student usage không tự chuyển thành B2B contract.                |

## Kết luận Prompt 2

Internova giữ **Partner-Led** là GTM motion chính trong giai đoạn đầu.

Partner hypothesis hiện tại là:

**TopCV Vietnam**

Tuy nhiên đây vẫn là **giả thuyết cần kiểm chứng**, không phải partnership đã được xác nhận.

Falsification test:

> Trong vòng 14 ngày phải tạo được ít nhất 1 cuộc trao đổi/meeting với partner tiềm năng. Nếu không đạt, Partner-Led chưa được chứng minh và cần điều chỉnh GTM hypothesis.

Đồng thời, **VinUni Student Portal / LMS** vẫn là điểm nhúng tốt nhất để kiểm chứng Pain Moment và product usage trước khi scale distribution qua partner.

---

# Tổng hợp quyết định sau AI Critique

| Hạng mục                                | Quyết định cuối cùng         |
| ----------------------------------------- | --------------------------------- |
| **Value Metric**                    | Hybrid                            |
| **Model suggestion**                | Outcome                           |
| **Attribution score**               | 10/10 theo self-assessment        |
| **Autonomy score**                  | 10/10 theo self-assessment        |
| **Platform pricing**                | 18 triệu VND/tổ chức/năm      |
| **Usage overage**                   | $0.40/completed job               |
| **Cost/Job**                        | $0.1177/job                       |
| **Fully-loaded Cost/Job**           | $0.2459/job                       |
| **Gross Margin**                    | khoảng 70.6%                     |
| **Containment trong pricing model** | 78% — pricing assumption         |
| **Financial guardrail**             | Containment ≥57.4% để GM ≥60% |
| **Operational target**              | Containment ≥75%                 |
| **GTM motion**                      | Partner-Led                       |
| **Partner hypothesis**              | TopCV Vietnam                     |
| **Pilot embed point**               | VinUni Student Portal / LMS       |
| **Peer / Stranger Test**            | PASS — ≤3 câu hỏi lại        |

---

# Evidence Pack Status

## 1. Eval / Observability Evidence — Rồi

Internova hiện đã có system-level evidence phục vụ đánh giá:

- job-level chat logs;
- answer status;
- confidence;
- sources;
- route intent/scope;
- groundedness status;
- RAG retrieval/reranking telemetry;
- no-answer rate;
- groundedness;
- faithfulness;
- answer relevance;
- pipeline latency.

Điều này cho phép truy vết một AI job từ request tới output và hỗ trợ việc chạy/freeze Eval sau này.

**Lưu ý:** containment 78% trong Pricing Model vẫn được giữ là **pricing assumption**, không được mô tả sai thành một frozen 150-case Eval result.

---

## 2. Risk Checklist — Rồi

Risk Checklist đã được rà lại dựa trên implementation thực tế của Internova.

### Hallucination

Internova sử dụng RAG, source-scoped retrieval và groundedness/evidence validation.

Nếu evidence không đủ hoặc semantic evidence validation gặp lỗi, pipeline áp dụng **fail-closed** thay vì coi câu trả lời là grounded.

### Personal Data / Privacy

Truy cập dữ liệu cá nhân được bảo vệ bởi semantic privacy gate.

Personal database chỉ được mở khi hệ thống xác định người dùng thực sự đang yêu cầu lấy dữ liệu được lưu trong tài khoản của chính họ.

Nếu intent classifier không chắc chắn hoặc gặp lỗi, hệ thống giữ personal DB đóng.

### Provider Data / Training

Internova sử dụng OpenAI API.

Theo chính sách của OpenAI, dữ liệu API/business không được dùng để train model mặc định trừ khi khách hàng chủ động opt-in.

### Delete / Vendor Exit

Internova đã có chức năng **permanent deletion** cho conversation ở cả frontend và backend.

Full self-service account export vẫn là một remediation cần hoàn thiện trước enterprise procurement; hiện có thể sử dụng authorized database export như contingency trong trường hợp migration/vendor exit.

---

## 3. Pre-Pilot Readiness Report — Rồi

Internova đã có đủ nền tảng kỹ thuật để đo một pilot:

- authenticated logging;
- groundedness/evidence validation;
- source tracking;
- RAG Analytics;
- privacy gate;
- delete flow;
- peer test đã PASS.

Report này xác nhận **pre-pilot readiness**, không giả vờ rằng Internova đã hoàn thành một external VinUni 4-week pilot với 300 attempts nếu chưa có outcome dataset tương ứng.

---

# Reflection

Qua hai AI critique, có thể thấy hai rủi ro chính của Internova là:

### 1. Pricing Risk

Cost/Job phụ thuộc đáng kể vào containment.

Nếu containment giảm, số completed jobs giảm và Cost/Job tăng. Vì vậy, containment cần được theo dõi như một KPI tài chính và vận hành, không chỉ là AI quality metric.

### 2. GTM Risk

ACV hiện tại chưa đủ cao để hỗ trợ một Sales-Led motion truyền thống có CAC lớn.

Do đó, Partner-Led hợp lý hơn về economics, nhưng partner hypothesis vẫn cần được kiểm chứng bằng hành động thực tế thay vì chỉ dựa vào spreadsheet.

### Quyết định cuối cùng

Internova không thay đổi số liệu chỉ để mô hình trông đẹp hơn.

Ưu tiên tiếp theo là:

1. tiếp tục freeze Eval/observability evidence thành dataset có version;
2. giữ containment cao hơn financial guardrail;
3. kiểm chứng Partner-Led bằng interaction thực tế;
4. chạy pilot trên điểm nhúng mà Pain Moment thực sự xảy ra;
5. chỉ scale khi unit economics và channel evidence cùng được chứng minh.
