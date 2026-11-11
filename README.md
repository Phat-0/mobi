# Ứng dụng hỗ trợ tuyển dụng và tìm việc làm

**Bộ chuẩn đã duyệt — phiên bản 1.0, ngày 12/11/2026.**

- Kho mã: https://github.com/Phat-0/mobi
- Yêu cầu môn học: https://ceb.net.vn/flutter/requirement.html
- Mục tiêu: ứng viên tìm và ứng tuyển việc; doanh nghiệp mua lượt, đăng tuyển và xét hồ sơ; quản trị viên quản lý hệ thống.
- Đây là yêu cầu triển khai, không phải danh sách chức năng đã hoàn thành.

## 1. Công nghệ và ngôn ngữ

| Thành phần | Chuẩn |
|---|---|
| Điện thoại | Flutter/Dart, ưu tiên Android |
| Lưu cục bộ | SQLite |
| Máy chủ | C# ASP.NET Core 10, REST API |
| Dữ liệu chính | SQL Server |
| Quản lý mã | GitHub |

Không tự thay công nghệ bắt buộc bằng PostgreSQL, Supabase, Firebase hoặc nền tảng khác. SQL Server MCP kết nối sau; ứng dụng vẫn dùng SQL Server. Thư viện chính, phiên bản và kiến trúc phải thống nhất; thay đổi lớn cần người dùng duyệt.

**Tiếng Việt:** giao diện, lỗi, tài liệu và báo cáo dùng tiếng Việt có dấu. Thành phần tự đặt tên dùng tiếng Việt không dấu: thư mục `ung-dung`, tập tin `tin_tuyen_dung.dart`, lớp `TinTuyenDung`, biến `soLuotConLai`, hàm `guiHoSo()`, bảng/cột `tin_tuyen_dung`/`so_luot_con_lai`, đường dẫn `/api/v1/tin-tuyen-dung`. Một khái niệm dùng một tên; viết tắt phải giải thích. Giữ từ khóa, tên công nghệ, thư viện và tên bắt buộc như README.md. Mã trạng thái không dấu ánh xạ sang nhãn có dấu. Tiền hiển thị 100.000đ, ngày dạng 12/11/2026; lưu thời gian UTC và hiển thị giờ Việt Nam.

## 2. Tài khoản, quyền và doanh nghiệp

| Đối tượng | Quyền |
|---|---|
| Khách | Xem, tìm, lọc việc; xem doanh nghiệp và dịch vụ |
| Ứng viên | Hồ sơ, CV, lưu việc, ứng tuyển, rút và theo dõi kết quả |
| Nhà tuyển dụng | Doanh nghiệp theo quyền; mua lượt, quản lý tin và xét hồ sơ |
| Quản trị viên | Tài khoản, vai trò, danh mục, doanh nghiệp, tin, dịch vụ, đơn và thống kê |

- Vai trò hệ thống: Thành viên, Quản trị viên. Thành viên chọn một loại Ứng viên hoặc Nhà tuyển dụng trong bản đầu; không tự đăng ký quản trị.
- Một nhà tuyển dụng thuộc một doanh nghiệp; doanh nghiệp có nhiều nhà tuyển dụng và người phụ trách quản lý thành viên. Lượt thuộc doanh nghiệp.
- Đăng ký, đăng nhập, đăng xuất, đổi mật khẩu, sửa cá nhân; quản trị tìm, khóa/mở khóa và quản lý quyền.
- Băm mật khẩu; đổi mật khẩu kiểm tra mật khẩu hiện tại. Khóa tài khoản ngăn thao tác cần xác thực. Đăng xuất xử lý phiên và dữ liệu nhạy cảm. Không xóa tài khoản làm mất lịch sử.
- Kiểm tra vai trò và quyền sở hữu tại máy chủ với từng thao tác/bản ghi; không chỉ ẩn nút. Không truy cập CV hoặc dữ liệu doanh nghiệp khác.
- Doanh nghiệp gồm tên, mã số thuế nếu có, biểu trưng, ảnh, ngành, quy mô, địa chỉ, giới thiệu, trang thông tin, liên hệ và người phụ trách.
- Trạng thái doanh nghiệp: Chờ duyệt, Đã duyệt, Bị từ chối, Tạm khóa. Từ chối có lý do, cho sửa/gửi lại; thay thông tin quan trọng cần duyệt lại theo thiết kế.
- Chỉ doanh nghiệp đã duyệt được mua lượt/gửi tin. Tạm khóa ngừng nghiệp vụ mới, ẩn và dừng nhận hồ sơ ở tin đang tuyển; không xóa lịch sử/lượt. Khôi phục qua quản trị kiểm tra. CV không công khai.

## 3. Ngành nghề và tin tuyển dụng

**Ngành nghề:** tên, mô tả, ảnh, trạng thái; xem, thêm, sửa, tìm, xóa hoặc ngừng sử dụng. Chuẩn hóa tên chống trùng; không xóa ngành có tin. Ngành ngừng dùng không được chọn cho tin mới, lịch sử vẫn hiển thị.

**Tin:** tiêu đề, doanh nghiệp, ngành, ảnh, vị trí, số người cần tuyển, địa điểm, hình thức làm việc, kinh nghiệm, trình độ, lương tối thiểu/tối đa hoặc thỏa thuận, mô tả, yêu cầu, quyền lợi, hạn nhận, người tạo và thời gian. Số người cần tuyển khác số lượt đăng tin.

| Trạng thái tin | Quy tắc |
|---|---|
| Bản nháp | Không cần lượt, sửa trực tiếp |
| Chờ duyệt | Doanh nghiệp đủ điều kiện, giữ một lượt; được rút |
| Đang tuyển | Đã duyệt; chỉ nhận hồ sơ khi còn hạn và doanh nghiệp hoạt động |
| Bị từ chối | Có lý do, sửa và gửi lại |
| Đã đóng / Hết hạn | Dừng nhận hồ sơ |
| Bị ẩn | Quản trị ẩn do vi phạm, có lý do |

- Hạn nhận hợp lệ; lương tối đa không nhỏ hơn tối thiểu.
- Sửa tin đang tuyển tạo bản sửa chờ duyệt; nội dung đã duyệt tiếp tục hiển thị đến khi bản sửa được chấp thuận. Không trừ thêm lượt.
- Tuyển lại tin đóng/hết hạn tạo tin mới, có thể sao chép và dùng lượt mới.
- Tin có hồ sơ lưu trữ thay vì xóa lịch sử. Danh sách có tìm, lọc, phân trang.

## 4. Dịch vụ, giỏ mua và đơn

**Danh mục dịch vụ:** quản trị xem, thêm, sửa, tìm, xóa/ngừng dùng, quản lý ảnh; không xóa danh mục có gói.

**Gói đăng tin:** tên, mô tả, ảnh, danh mục, số lượt/gói, giá, Đang bán/Ngừng bán. Giá dương, lượt nguyên dương. Gói có đơn không được xóa; được ngừng bán. Thay gói không sửa đơn cũ. Bản đầu chỉ lượt thường; lượt chưa dùng không hết hạn. Cấp **ba lượt miễn phí đúng một lần** khi doanh nghiệp được duyệt lần đầu, có lịch sử chống cấp lặp.

| Gói mẫu, giá có thể cấu hình | Lượt/gói | Giá |
|---|---:|---:|
| Cơ bản | 1 | 20.000đ |
| Tiết kiệm | 5 | 90.000đ |

Khu vực dịch vụ cho nhà tuyển dụng có danh mục, gói mới nhất, theo danh mục, tìm, phân trang, chi tiết và thêm giỏ. Thêm có ảnh; sửa/xóa xử lý ảnh cũ không còn tham chiếu.

**Giỏ:** thuộc tài khoản nhà tuyển dụng; thêm, xem, tăng/giảm/nhập số lượng, xóa, tổng tiền/lượt và tạo đơn. Cùng gói gộp dòng; mỗi dòng **1–99 gói**; biểu tượng hiển thị tổng số gói. Ví dụ ba gói cơ bản và hai tiết kiệm = **5 gói, 13 lượt, 240.000đ**.
- Máy chủ tính và kiểm tra lại giá, trạng thái bán, quyền mua, doanh nghiệp nhận lượt; giá đổi phải xem/xác nhận lại.
- Lưu giỏ máy chủ, có bản lưu điện thoại; tạo đơn cần mạng. Chỉ xóa mục đã mua sau tạo đơn thành công; chống tạo đơn lặp ngoài ý muốn.

**Đơn:** mã, doanh nghiệp, người mua, thời điểm, chi tiết gói/số lượng/đơn giá/lượt tại lúc mua, tổng tiền/lượt, trạng thái, thời điểm/người xác nhận.
- Chờ thanh toán → Đã thanh toán hoặc Đã hủy. Chỉ hủy khi chưa thanh toán; không sửa/xóa đơn đã thanh toán.
- Bản đầu: người mua tạo/xem đơn → quản trị xác nhận trong **chế độ trình diễn có nhãn rõ** → cộng lượt. Người mua tự báo đã trả không phải bằng chứng thanh toán.
- Xác nhận và cộng lượt trong cùng giao dịch; mỗi đơn cộng đúng một lần. Giá/gói thay đổi không ảnh hưởng lịch sử.
- Danh sách, chi tiết, tìm mã, lọc ngày/doanh nghiệp/trạng thái; chỉ đơn thanh toán tính doanh thu. Thanh toán trực tuyến/hoàn tiền làm sau.

## 5. Sổ lượt

| Sự kiện | Lượt |
|---|---|
| Tạo nháp | Không đổi |
| Gửi duyệt lần đầu hoặc gửi lại sau từ chối | Còn lại → đang giữ một lượt |
| Duyệt xuất bản | Đang giữ → đã sử dụng |
| Từ chối hoặc rút trước duyệt | Trả lượt giữ về còn lại |
| Đóng, hết hạn, ẩn sau xuất bản | Không hoàn |
| Duyệt bản sửa tin đã xuất bản | Không trừ mới |

Chống âm khi đồng thời, chống cộng/giữ/trừ/trả lặp. Mọi phát sinh ghi doanh nghiệp, số lượt, nguyên nhân, đơn/tin, người và thời gian; đối chiếu được số dư với lịch sử. Không sửa số dư mà không ghi lịch sử.

## 6. Tìm việc, CV và ứng tuyển

**Tìm việc:** ngành, mới nhất, từ khóa, lọc ngành/địa điểm/lương/hình thức/kinh nghiệm, sắp xếp, phân trang máy chủ, chi tiết, doanh nghiệp, việc liên quan, lưu/bỏ lưu không trùng. Giữ bộ lọc khi quay lại; không hiển thị tin hết hạn như còn nhận.

**Hồ sơ:** họ tên, ảnh, liên hệ, giới thiệu, học vấn, kinh nghiệm, kỹ năng, vị trí mong muốn. Nhiều CV **PDF tối đa 10 MB/tập tin**, chọn một khi nộp; kiểm tra loại/kích thước tại máy chủ. CV riêng tư, kiểm tra quyền tải, không phát địa chỉ công khai cố định. Chỉ chủ hồ sơ, người tuyển có quyền và quản trị có nhiệm vụ phù hợp được xem; không xóa tập tin còn được hồ sơ đã nộp tham chiếu.

**Luồng:** mở tin hợp lệ → chọn CV/thư giới thiệu tùy chọn → xem/xác nhận → lưu bản đã nộp → doanh nghiệp xét → thông báo.

| Trạng thái hiện tại | Được chuyển |
|---|---|
| Đã gửi | Đang xem xét, Mời phỏng vấn, Từ chối, Đã rút |
| Đang xem xét | Mời phỏng vấn, Từ chối, Đã rút |
| Mời phỏng vấn | Đã tuyển, Từ chối, Đã rút |
| Đã tuyển / Từ chối / Đã rút | Kết thúc trong bản đầu |

Chỉ ứng viên rút, chỉ nhà tuyển có quyền xử lý các kết quả tuyển. Một ứng viên một hồ sơ/tin, ràng buộc cơ sở dữ liệu; không nộp lại sau rút/từ chối trong bản đầu. Lưu bản hồ sơ/CV lúc nộp, sửa cá nhân không sửa bản cũ. Lưu lịch sử trạng thái. Thư mời có giờ, hình thức, địa điểm/đường dẫn, ghi chú. Chỉ báo kết quả sau lưu thành công.

## 7. Thông báo, thống kê và SQLite

- Thông báo trong ứng dụng: duyệt doanh nghiệp/tin, từ chối/ẩn, xác nhận đơn, đổi trạng thái hồ sơ, phỏng vấn. Đã/chưa đọc, đúng người, mở nội dung theo quyền; không lộ CV/nội dung riêng tư công khai.
- Thống kê ứng viên: đã gửi/đang xét/được mời/đã tuyển. Doanh nghiệp: tin, hồ sơ mới, kết quả, lượt, đơn. Quản trị: người dùng, doanh nghiệp, tin, hồ sơ, đơn, doanh thu đã thanh toán. Lọc thời gian, theo quyền, khớp danh sách chi tiết.
- SQL Server là nguồn chính. SQLite lưu danh mục, tin đã xem, việc đã lưu, bản nháp hồ sơ/tin, bản lưu giỏ, thời điểm cập nhật; tách theo tài khoản.
- Mất mạng được xem dữ liệu cũ và sửa nháp, báo rõ chưa mới. Gửi hồ sơ/tạo đơn/duyệt/đổi trạng thái cần mạng; không báo thành công trước xác nhận.
- Kết nối lại kiểm tra giá/quyền/trạng thái; không âm thầm gửi thao tác quan trọng. Không lưu mật khẩu/khóa dạng văn bản thường.

## 8. Kiến trúc, giao diện và bảo mật

- Ứng dụng tách chức năng, giao diện/nghiệp vụ/dữ liệu; giao diện không trực tiếp truy vấn hoặc gọi mạng. Quản lý trạng thái/điều hướng thống nhất.
- Máy chủ tách tiếp nhận/nghiệp vụ/dữ liệu; /api/v1, phương thức và mã HTTP đúng, lỗi có cấu trúc, kiểm tra quyền/dữ liệu, phân trang.
- Khóa chính thống nhất, ưu tiên UUID nghiệp vụ; khóa ngoại, duy nhất, chỉ mục, kiểu tiền chính xác; giao dịch cho lượt/đơn.
- Cấu trúc dữ liệu có phiên bản chuyển đổi, một nguồn quản lý; không tự chạy phá hủy.
- Chung màu/chữ/khoảng cách/nút/ô/thẻ/hộp thoại; có tải/rỗng/lỗi/thử lại/mất mạng; nhãn và lỗi từng ô, giữ dữ liệu khi lỗi, ngăn gửi lặp, phù hợp điện thoại.
- Xác nhận xóa/rút/đóng/khóa. Không hiển thị chi tiết kỹ thuật máy chủ cho người dùng thường.
- Tập tin kiểm tra loại/kích thước/quyền; thay thành công mới xử lý cũ; không xóa còn tham chiếu, xử lý tập tin mồ côi khi lưu thất bại.
- Không đưa mật khẩu/khóa/mã truy cập/chuỗi kết nối thật/CV thật lên GitHub hay nhật ký. Dữ liệu mẫu có nhãn, tách thử nghiệm/sử dụng thật; tài khoản thử đúng vai trò, không cần quyền quản trị toàn máy chủ.

## 9. Đối chiếu môn học và mở rộng

| Nhóm tiêu chí | Đáp ứng |
|---|---|
| Xác thực, thành viên, vai trò | Tài khoản, khóa/mở, phân quyền |
| Danh mục, ảnh, kiểm tra trước xóa | Danh mục dịch vụ, không xóa khi có gói |
| Sản phẩm, ảnh thêm/sửa/xóa, phân trang | Gói lượt; không xóa khi có đơn |
| Mới nhất/theo danh mục/tìm/chi tiết | Khu vực dịch vụ nhà tuyển dụng |
| Giỏ, biểu tượng, cập nhật số lượng | Mua số lượng gói thật |
| Đặt, chi tiết, quản lý đơn/trạng thái | Đơn mua lượt, tìm/lọc |
| Đặc thù đề tài | Doanh nghiệp, tin, CV, ứng tuyển |

Không giả lập số lượng giỏ bằng số lần ứng tuyển. Giải trình nghiệp vụ tương đương/trang chủ theo vai trò với giảng viên, không khẳng định đã chấp thuận hoặc đủ điểm. Lập nghiệm thu tách bắt buộc/điểm cộng theo đề gốc.

Mở rộng sau: xác thực thư điện tử, quên mật khẩu, đăng nhập bên ngoài, thanh toán trực tuyến, hoàn tiền, tin nổi bật, trò chuyện, gợi ý việc, thông báo đẩy. Không mặc định đã có hoặc thuộc đợt đầu.

## 10. Cấu trúc và thứ tự làm

| Đường dẫn | Nội dung |
|---|---|
| README.md | Chuẩn, cách chạy, tiến độ |
| ung-dung/ | Flutter và kiểm thử |
| may-chu/ | C#, kiểm thử, phiên bản chuyển đổi dữ liệu |
| co-so-du-lieu/ | Sơ đồ, dữ liệu mẫu, tập lệnh hỗ trợ |
| tai-lieu/ | Yêu cầu, thiết kế, nghiệm thu, trình diễn |
| .github/workflows/ | Kiểm tra tự động, tên bắt buộc GitHub |

Thứ tự: **chuẩn/nghiệm thu → khung công nghệ/kiểm tra tự động → tài khoản/quyền → doanh nghiệp/ngành → dịch vụ → giỏ/đơn/lượt → tin/duyệt → tìm việc/hồ sơ/ứng tuyển → phỏng vấn/thông báo/thống kê → kiểm thử/tài liệu/trình diễn**. Mỗi giai đoạn có kết quả chạy và tiêu chí cụ thể.

## 11. Nghiệm thu và hướng dẫn cho các cuộc chat sau

1. Đọc README/tài liệu liên quan và kiểm tra mã, tiến độ, phiên bản chạy thực tế trước khi sửa.
2. Tuân thủ tiếng Việt, công nghệ và nghiệp vụ đã duyệt. Không coi đề xuất cũ là quyết định; thay đổi lớn trình người dùng.
3. Không tự xóa dữ liệu/chạy chuyển đổi phá hủy; không đưa bí mật lên kho.
4. Chức năng hoàn thành phải chạy ứng dụng → máy chủ → dữ liệu, kiểm tra đúng/sai/quyền/mất mạng, có kiểm thử cần thiết; không chỉ giao diện/dữ liệu giả.
5. Kiểm tra đặc biệt: cộng lượt một lần, không âm khi đồng thời, chống ứng tuyển trùng, quyền CV, trạng thái, giá đơn bất biến, hồ sơ đã nộp bất biến, dữ liệu cục bộ tách tài khoản.
6. Chạy định dạng/phân tích/xây dựng/kiểm thử phù hợp; báo chính xác kết quả và giới hạn. Android kiểm tra riêng SQLite/tập tin/bàn phím/quyền; trình duyệt không thay thế Android.
7. Báo đã sửa gì, đã kiểm tra gì, mã lần cập nhật và việc còn thiếu; cập nhật tiến độ/cách chạy. Không bịa kiểm tra.
8. GitHub đối chiếu mã; tập tin đọc/sửa phạm vi cấp; Playwright kiểm tra trình duyệt; Context7 tra tài liệu; Hỗ trợ phân tích lập kế hoạch; SQL Server MCP để sau.
9. Kiểm tra công cụ thực sự có trong từng chat; kết nối cũ không bảo đảm còn chạy. Đọc tập tin không đồng nghĩa chạy lệnh. Hỗ trợ phân tích không thay kiểm thử/ghi nhớ dự án.
10. Ảnh/nhật ký/kết quả phải cùng phiên bản mã. Không ghi thông tin xác thực/đường hầm riêng lên kho.
11. Khi mâu thuẫn hoặc thiếu bằng chứng phải nêu rõ. Nội dung nghiệp vụ sửa phải được duyệt; không coi câu tiếp tục là duyệt thay đổi lớn chưa trình.
12. README GitHub là chuẩn sau ghi thành công; cập nhật phiên bản khi sửa. Không tạo/duy trì README riêng trong thư mục ngoài ý muốn người dùng.
13. Chỉ bổ sung lệnh chạy đã kiểm chứng khi có mã nguồn.

## 12. Tiến độ

| Hạng mục | Trạng thái |
|---|---|
| Bộ chuẩn | Người dùng đã duyệt, trình bày gọn |
| Flutter, máy chủ, cơ sở dữ liệu | Chưa triển khai |
| Kiểm tra tự động, nghiệp vụ | Chưa thực hiện |
| Triển khai trực tuyến | Chưa thực hiện |

Trong phiên thiết lập đã gọi thành công kết nối tập tin, Playwright, Hỗ trợ phân tích; Context7 đã kết nối. Đây là thiết lập công cụ, không phải hoàn thành ứng dụng.
