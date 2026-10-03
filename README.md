# Day 14 — Robotaxi: Tracking & Camera–LiDAR Fusion

Bài cá nhân **4 giờ**: hoàn thiện một track 3D dài trên CVAT, tự QC theo thời gian, rồi đối chiếu cuboid với ảnh camera trước để ghi discrepancy có căn cứ.

| Tài liệu | Đọc khi nào |
| --- | --- |
| [Bài lab](docs/lab.md) | Đầu buổi và trong suốt bài: các bước, checkpoint, cách kết thúc |
| [Hướng dẫn bằng hình](docs/huong-dan-hinh.md) | Lần đầu mở job 3D: chỗ bấm để tạo track, fit cuboid, đọc keyframe/outside/occluded, Save → completed |
| [Overlay camera trên CVAT local](docs/cvat-overlay.md) | Khi muốn xem cuboid chiếu lên ảnh `image_1` ngay trong job 3D |
| [Phiếu cá nhân](docs/personal-notes.txt) | Ghi frame fit, L/W/H, keyframe, phát hiện temporal và discrepancy |

## Bắt đầu

1. Bấm **Use this template** để tạo repo của bạn, rồi clone về máy (Windows: PowerShell hoặc GitHub Desktop đều được).
2. Bật lại CVAT local đã cài ở Day 2 (`docker compose start` trong thư mục CVAT; Windows: mở Docker Desktop, start nhóm container CVAT). Không cần cài CVAT mới.
3. Nhận gói dữ liệu `day14-coach-data-pack.zip` từ Lab Coach, giải nén **ở thư mục gốc repo** để có thư mục `private/`:

   ```bash
   unzip ~/Downloads/day14-coach-data-pack.zip
   ```

   Windows PowerShell: `Expand-Archive $HOME\Downloads\day14-coach-data-pack.zip -DestinationPath .` (hoặc chuột phải file zip → Extract All, chọn thư mục repo).
4. Mở job Day 14 Lab Coach giao và object mục tiêu. Đọc [bài lab](docs/lab.md) từ đầu.
5. Bật overlay nếu muốn xem cuboid trên ảnh camera trước. Chạy từ thư mục gốc repo:

   | Máy | Lệnh |
   | --- | --- |
   | macOS / Linux | `python3 scripts/cvat-overlay/overlay.py up` |
   | Windows (PowerShell, CMD) | `python scripts\cvat-overlay\overlay.py up` (máy chỉ có `py` thì gõ `py` thay `python`) |

   Rồi tải lại tab CVAT bằng Ctrl+Shift+R (macOS: Cmd+Shift+R). Không cần WSL hay bash. Gặp lỗi, xem [cvat-overlay.md](docs/cvat-overlay.md).

## Nộp bài

Annotation nộp bằng **Save → completed** trên CVAT. Coach thu bản trước/sau và review riêng; không nộp ZIP lên VLearn.

## Dữ liệu

Dữ liệu Robotaxi VinFast chỉ dùng cho buổi lab, giữ bảo mật và không chia sẻ ra ngoài. Repo này không chứa PCD, ảnh gốc hay annotation (ảnh trong `images/huong-dan/` là ảnh giao diện, phần ảnh camera đã làm mờ); Lab Coach cấp dữ liệu theo kênh riêng. Không commit, đăng ảnh chụp màn hình hay đưa dữ liệu lên repo, VLearn, mạng xã hội hoặc dịch vụ AI bên ngoài.

Dữ liệu buổi lab (calibration `calib-diagnostic.json` và thư mục `frame-maps/`) **không nằm trong repo**: Lab Coach phát riêng trong buổi học. Chép chúng vào thư mục `private/` ở gốc repo (đã gitignore), không commit, không chia sẻ ra ngoài lớp. Không sửa hai thứ này để ảnh khớp hơn.
