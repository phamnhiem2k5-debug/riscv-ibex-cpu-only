# RISC-V SoC Architecture Comparison

Bộ mã nguồn ba mô hình phục vụ nghiên cứu, mô phỏng và so sánh kiến trúc RISC-V SoC.

## Cấu trúc

| Thư mục | Nội dung |
| --- | --- |
| `models/IBEX_CPU_ONLY_FROM_CPU_PURE_2026-11-05/` | Hệ thống Ibex CPU-only, RTL, kiểm chứng CPU12/ISA23 và script đóng IP |
| `models/CPU_NEURAL_AXI_ONLY/` | Hệ thống Ibex với bộ tăng tốc Neural INT2 bên ngoài và cầu giao tiếp AXI |
| `models/RISC+ACCELERATOR/` | Mô hình tham khảo RISC-V với phần mở rộng/tăng tốc; giữ tài liệu nguồn riêng |
| `extras/` | Các file bàn giao và cấu hình board đi kèm gói gốc |
| `docs/` | Hướng dẫn, danh sách file và SHA-256 đối chiếu |

Giữ tên và cấu trúc nội bộ từng mô hình để hạn chế ảnh hưởng tới các script và project Vivado hiện có. RTL, testbench, firmware và các file được giữ lại không thay đổi nội dung. Dữ liệu tạm, kết quả nhị phân, thư mục work của CPU-only, backup lịch sử và lịch sử Git cũ đã được loại khỏi bản đóng gói. Danh sách đầy đủ nằm trong `docs/EXCLUDED_FILES.csv`.

## Môi trường và cách chạy

Luồng Ibex trong gói sử dụng Vivado 2022.2.x. Xem README riêng của từng mô hình trước khi chạy. Trong Vivado Tcl Console, thay `/path/to/repo` bằng đường dẫn thực tế trên máy bạn (Windows có thể dùng `D:/...`).

CPU-only: script tạo project, chạy kiểm chứng và đóng IP theo README riêng:

```tcl
catch {close_sim}
source {/path/to/repo/models/IBEX_CPU_ONLY_FROM_CPU_PURE_2026-11-05/RUN_FROM_TESTED_RTL.tcl}
```

CPU + Neural: điểm vào demo 12 testcase có sẵn trong gói:

```tcl
catch {close_sim}
source {/path/to/repo/models/CPU_NEURAL_AXI_ONLY/soc_4ip_build/DEMO_SOC4IP_NEURAL12.tcl}
```

Các project `.xpr` và script cũ có thể còn tham chiếu tuyệt đối tới ổ đĩa hoặc môi trường ban đầu. Việc sắp xếp folder không tự chuyển đổi toàn bộ các đường dẫn đó. Xem `docs/REPRODUCIBILITY.md` trước khi chạy trên máy khác.

## Kiểm chứng và kết quả

Gói này đã được kiểm tra tính toàn vẹn file bằng SHA-256 và kiểm tra ZIP. Chưa chạy lại mô phỏng, tổng hợp hay triển khai Vivado trong lần đóng gói này. Các CSV, báo cáo và bằng chứng còn lại là dữ liệu từ archive đầu vào; không đại diện cho một lần chạy mới. Các tuyên bố hiệu năng trong tài liệu từng mô hình cần được đối chiếu riêng trước khi dùng để so sánh.

## Nguồn và quyền tác giả

Được tổ chức từ `SoC_design_3model.zip` do người dùng cung cấp. Giữ nguyên các thông báo bản quyền và LICENSE có sẵn. README của `RISC+ACCELERATOR` dẫn tới `AryaP-1243/fpga-riscv-nn-extensions`; xem đó là nguồn tham khảo và giữ ghi nhận tác giả. Không gán giấy phép mới chung cho toàn bộ repository.

## Upload GitHub

1. Giải nén gói này.
2. Tạo repository tên `riscv-soc-architecture-comparison`.
3. Upload **nội dung bên trong** folder gốc, để `README.md`, `.gitignore`, `models/`, `docs/` và `extras/` nằm ngay tại gốc repository.
4. Nếu trình duyệt giới hạn số lượng file, dùng Git hoặc GitHub Desktop để đưa cả folder lên.
