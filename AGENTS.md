3. Skills và quy trình làm việc

Bộ kỹ năng Superpowers đã được cài đặt toàn cục. Sử dụng skill using-superpowers để xác định quy trình phù hợp và chỉ tải các skill thực sự cần thiết.

Đối với những thay đổi liên quan đến Java/Spring Boot, sử dụng java-spring-best-practices làm hướng dẫn về ngôn ngữ và framework, kết hợp với quy trình Superpowers phù hợp.

Đối với những thay đổi liên quan đến React/Next.js, chỉ sử dụng vercel-react-best-practices khi frontend thực tế của dự án sử dụng React/Next.js. Việc cài đặt skill không đồng nghĩa với việc đã quyết định công nghệ frontend.

Khi phát triển một tính năng: tìm hiểu nghiệp vụ đã được phê duyệt, lập kế hoạch nếu thay đổi không đơn giản, triển khai thành những phần nhỏ có thể kiểm chứng, chạy kiểm thử và rà soát kết quả.

Khi sửa lỗi: phải tái hiện lỗi và xác định nguyên nhân trước khi sửa code; sau đó xác minh lỗi đã được khắc phục.

Trước khi tuyên bố hoàn thành: phải có bằng chứng kiểm chứng bằng cách thực thi thực tế, không chỉ dựa vào nhận định.

Công nghệ hoặc mẫu thiết kế mà skill khuyến nghị không được tự động thay thế thiết kế hiện tại hoặc thay đổi phiên bản dependency.

## 4. Testing Strategy và Quality Gates bắt buộc

- Áp dụng [Testing Strategy & Test Data](../nghiepvu/08-kiem-thu/chung/testing-strategy.md), [Test Case Standard](../nghiepvu/08-kiem-thu/chung/test-case-standard.md), [Quality Gates & Agent Workflow](../nghiepvu/08-kiem-thu/chung/quality-gates.md); với đồng bộ units dùng [bộ ca Slice A](../nghiepvu/08-kiem-thu/daotao/slice-a-test-cases.md). Máy/CI thiếu bộ tài liệu phải lấy đúng bản đã duyệt trước khi code.
- Trước code: xác định nguồn yêu cầu, ID test cases, expected results, acceptance criteria, gate liên quan, fixture và phần thật/mock. Không tự đặt nghiệp vụ hoặc thay Q01–Q08/contract/schema.
- Dùng `test-driven-development` khi phát triển feature/bugfix; `systematic-debugging` khi gặp lỗi; `verification-before-completion` trước khi tuyên bố hoàn thành. Task tài liệu chỉ cần gate tài liệu phù hợp.
- Không tuyên bố PASS nếu chưa chạy. Phân biệt Unit/mock, MockMvc, integration SQL Server thật, HTTP thật và hai backend MVP chạy thật; `contextLoads()` không chứng minh nghiệp vụ/DB/API đúng.
- Chỉ chạy setup/cleanup trên DB test đã xác minh đích và quyền sở hữu; không dùng dữ liệu nhạy cảm, không log key/token. Hạ tầng chưa thiết lập phải ghi rõ, không báo lệnh dự kiến là đã chạy.
- Không skip/disable/xóa assertion hoặc sửa test/expected chỉ để xanh; nếu test sai phải có căn cứ và lý do review. Kiểm số test thực sự chạy, fail/error/skip và report mới; zero test không đạt gate cần test.
- Bàn giao kèm lệnh/cwd, phiên bản, số ca/report/evidence, phạm vi thật–mock; bắt buộc nêu FAIL, BLOCKED, NOT VERIFIED và giới hạn. Chỉ kết luận hoàn thành khi các gate liên quan đạt; nghiệm thu slice cần thành viên khác kiểm độc lập.
## 5. API Design & Contract-First bắt buộc

- Trước khi tạo hoặc chỉnh sửa API, phải đọc API Conventions,
  API Catalog và API Contract hiện hành của chức năng liên quan.
- Thiết kế và triển khai API theo Contract-First; không tự tạo
  endpoint, DTO, request/response, error code hoặc quy tắc
  authorization trái với contract đã duyệt.
- Tuân thủ quy ước URL, HTTP Method, naming, validation,
  status code, ProblemDetail, security và versioning đã chốt.
- Phân biệt API Contract đã phê duyệt với các đề xuất chưa chốt.
  Khi thiếu hoặc mâu thuẫn contract, phải báo rõ trước khi code.
- Khi thay đổi API, phải đánh giá tác động đến provider,
  consumer, OpenAPI, API Catalog và test cases liên quan.
- Thực hiện Contract/API/Security/Integration Test theo
  Testing Strategy và Quality Gates hiện hành.
- Không tuyên bố API hoàn thành nếu chưa đáp ứng các
  acceptance criteria và quality gates liên quan.


## 6. Kiến trúc và phạm vi cộng tác chung — 09/11/2026

- Đọc [Kiến trúc CTSV và quy tắc cộng tác](../nghiepvu/01-thiet-ke/kien-truc-va-quy-tac-cong-tac.md) trước khi lập plan/code. Nhóm4người cùng một CTSV; ba repo ctsv/daotao/taichinh độc lập, Organization không là repo cha.
- CTSV là Modular Monolith: một Spring Boot backend, một React frontend chung; Auth/Foundation/Shared là tài nguyên chung trong ctsv_db, không thuộc riêng MGHP. SIS/Kế toán là backend riêng, không tự thêm application Auth hoặc frontend SIS/Kế toán.
- Phạm vi Codex tại repo này: backend Kế toán/Tài chính và tích hợp MGHP được giao; không tạo frontend hoặc nghiệp vụ module CTSV khác. Không tự tạo task, API, bảng, skeleton, code hoặc UI của SHCN/DRL/Học bổng; chỉ nhắc để xác định ranh giới/ảnh hưởng tích hợp.
- Nếu cần thay đổi Auth/Foundation/Shared hoặc contract chung ngoài task: nêu lý do/phạm vi ảnh hưởng, xin xác nhận và phối hợp owner liên quan; không tự gán owner hoặc sửa module người khác để test xanh.
- Package theo module trước, layer sau; dùng public interface/application service thay repository/entity nội bộ xuyên module; không phụ thuộc vòng. Migration CTSV dùng một Flyway history/version duy nhất, phối hợp trước merge theo nguồn chuẩn.
- Feature branch ngắn, main ổn định, PR thường xuyên; Codex không tự commit/push/tạo PR/merge/đổi cấu hình GitHub/deploy khi chưa có lệnh trực tiếp. Không push main.
- Người dùng trực tiếp cài công cụ, thiết lập SQL Server test/kết nối và kiểm môi trường P00; Codex chỉ hướng dẫn/kiểm khi được yêu cầu. Không tự kết nối SQL hoặc xin credential trong task tài liệu. Không dùng báo cáo thiết kế làm runtime PASS.
