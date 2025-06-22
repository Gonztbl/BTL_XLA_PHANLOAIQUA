# Hệ thống Nhận diện và Phân loại Trái cây theo Mức độ Xanh-Chín
*Báo cáo môn học Xử lý Ảnh số và Thị giác Máy tính - HaUI*

Dự án này xây dựng một hệ thống hoàn chỉnh sử dụng các mô hình Deep Learning để tự động nhận diện loại trái cây (táo, chuối, cam), phân loại tình trạng (tươi/hỏng) và xác định mức độ chín (xanh/chín) từ hình ảnh.

![Screenshot 2025-06-22 103508](https://github.com/user-attachments/assets/b9a9a6d2-77e5-4efd-94d2-304f2ea1faca)

## 📖 Mục lục
- [Tính năng nổi bật](#-tính-năng-nổi-bật)
- [Demo](#-demo)
- [Kiến trúc hệ thống](#-kiến-trúc-hệ-thống)
- [Công nghệ sử dụng](#️-công-nghệ-sử-dụng)
- [Cài đặt](#-cài-đặt)
- [Sử dụng](#-sử-dụng)
- [Kết quả thực nghiệm](#-kết-quả-thực-nghiệm)
- [Thành viên nhóm](#-thành-viên-nhóm)
- [Giấy phép](#-giấy-phép)

---

## ✨ Tính năng nổi bật

-   **Nhận diện đa đối tượng:** Sử dụng **YOLOv8n** để phát hiện và khoanh vùng (bounding box) chính xác nhiều loại trái cây khác nhau trong cùng một bức ảnh.
-   **Phân loại đa cấp:**
    1.  **Tình trạng (Tươi/Hỏng):** Dùng mô hình **CNN (Keras)** để đánh giá trái cây còn tươi hay đã hỏng.
    2.  **Mức độ chín (Xanh/Chín):** Dùng mô hình **MobileNetV2 (PyTorch)** để phân loại độ chín, một yếu tố quan trọng trong nông nghiệp và tiêu dùng.
-   **Phân tích màu sắc chủ đạo:** Trích xuất và hiển thị màu sắc nổi bật nhất của trái cây, giúp người dùng có cái nhìn trực quan về trạng thái của nó.
-   **Giao diện Web trực quan:** Xây dựng bằng **Flask**, cho phép người dùng dễ dàng tải ảnh lên hoặc dán URL để nhận kết quả phân tích tức thì.

## 📸 Demo
![Screenshot 2025-06-22 103508](https://github.com/user-attachments/assets/06ce0a54-0d74-4fcd-a906-7686dcc04bfd)


![Screenshot 2025-06-20 142614](https://github.com/user-attachments/assets/5b1ca941-4958-4d08-b77d-e98e7f423c49)

![Screenshot 2025-06-22 103916](https://github.com/user-attachments/assets/da9c6ef9-d601-498b-a2fa-0e95c8b04d49)

![Screenshot 2025-06-22 103903](https://github.com/user-attachments/assets/a94e5cbd-c53e-47fa-b08d-971fb7986587)

![Screenshot 2025-06-22 103849](https://github.com/user-attachments/assets/01dbbeb8-f0c1-43e2-9153-d5e507f3d508)
![Screenshot 2025-06-22 103835](https://github.com/user-attachments/assets/79318797-9773-4233-be21-f5ceef5a7a2b)
![Screenshot 2025-06-22 104250](https://github.com/user-attachments/assets/e8fe3db7-283d-48e6-9903-01dade1c087d)
![Screenshot 2025-06-22 104457](https://github.com/user-attachments/assets/794560a5-91fc-42a0-939b-307f803fddd5)



## 🏗️ Kiến trúc hệ thống
![Screenshot 2025-06-22 105032](https://github.com/user-attachments/assets/2f70a785-b581-40fb-9913-ab3180f41de3)


Hệ thống hoạt động theo một pipeline xử lý thông minh và hiệu quả:
![sodohoatdong](https://github.com/user-attachments/assets/7131b0ae-b5d5-4b00-9b5d-631f9e23af4d)

1.  **Input:** Người dùng tải ảnh lên qua giao diện Web (Flask).
2.  **Phát hiện đối tượng (Detection):** Mô hình **YOLOv8n** được nạp để xác định vị trí và loại của từng trái cây (táo, chuối, cam).
3.  **Cắt ảnh (Cropping):** Từng vùng ảnh chứa trái cây được cắt ra để xử lý độc lập.
4.  **Tiền xử lý & Phân loại song song:**
    -   Mỗi ảnh crop được đưa vào mô hình **CNN (Keras)** để phân loại **tươi/hỏng**.
    -   Đồng thời, ảnh crop cũng được đưa vào mô hình **MobileNetV2 (PyTorch)** để phân loại **xanh/chín**.
    -   Một module phân tích màu sắc dựa trên không gian màu HSV sẽ tìm ra màu chủ đạo.
5.  **Tổng hợp & Hiển thị:** Tất cả kết quả (bounding box, nhãn loại, nhãn trạng thái, nhãn độ chín, màu chủ đạo) được tổng hợp và trả về giao diện web một cách trực quan.

## 🛠️ Công nghệ sử dụng


| Lĩnh vực | Công nghệ |
| :--- | :--- |
| **Backend & Web App** | ![Flask](https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white) |
| **Deep Learning** | ![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=for-the-badge&logo=PyTorch&logoColor=white) ![TensorFlow](https://img.shields.io/badge/TensorFlow-%23FF6F00.svg?style=for-the-badge&logo=TensorFlow&logoColor=white) ![Keras](https://img.shields.io/badge/Keras-%23D00000.svg?style=for-the-badge&logo=Keras&logoColor=white) |
| **Object Detection** | **Ultralytics YOLOv8** |
| **Xử lý ảnh** | ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white) **Pillow** |
| **Thao tác dữ liệu** | ![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=for-the-badge&logo=numpy&logoColor=white) |
| **Ngôn ngữ** | ![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54) |

## ⚙️ Cài đặt

1.  **Clone repository:**
    ```bash
    git clone https://github.com/ten-cua-ban/ten-du-an.git
    cd ten-du-an
    ```

2.  **Tạo và kích hoạt môi trường ảo (khuyến khích):**
    ```bash
    # Dành cho Windows
    python -m venv venv
    .\venv\Scripts\activate

    # Dành cho macOS/Linux
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Cài đặt các thư viện cần thiết:**
    ```bash
    pip install -r requirements.txt
    ```
    *Lưu ý: File `requirements.txt` nên bao gồm: `flask`, `torch`, `torchvision`, `tensorflow`, `ultralytics`, `opencv-python`, `numpy`, `pillow`, `webcolors`.*

4.  **Tải các model đã huấn luyện:**
    Bạn cần tải các file trọng số (`.pt`, `.keras`) và đặt chúng vào thư mục `weights/`.
    
    <!-- Hướng dẫn người dùng tải model, bạn có thể upload lên Google Drive hoặc GitHub Release -->
    -   Tải các model tại: foldermodel
    -   Tạo một thư mục có tên `weights` trong thư mục gốc của dự án.
    -   Di chuyển các file model đã tải vào thư mục `weights/`.

## 🏃 Sử dụng

1.  **Chạy ứng dụng Flask:**
    ```bash
    python app.py
    ```

2.  **Mở trình duyệt và truy cập:**
    `http://127.0.0.1:5000`

3.  Tải lên một hình ảnh từ máy tính hoặc dán một liên kết URL và nhấn **"Nhận diện"**.

## 📊 Kết quả thực nghiệm

-   **Mô hình nhận diện YOLOv8n:**
    -   **Precision:** ~92%
    -   **Recall:** ~89%
    -   **mAP@0.5:** ~91%
-   **Mô hình phân loại CNN (Tươi/Hỏng):**
    -   **Training Accuracy:** ~97-98%
    -   **Validation Accuracy:** ~95-96%
    -   Mô hình học tốt, ổn định và không có dấu hiệu overfitting.

## 👨‍💻 Thành viên nhóm
Dự án được thực hiện bởi **Nhóm 13**:

| STT | Họ và tên         | MSSV       |
|:---:|:------------------|:-----------|
| 1   | Hoàng Xuân Hiền   | 2022601670 |
| 2   | Phạm Lê Tú An     | 2022602250 |
| 3   | Trịnh Bảo Long    | 2022601773 |
| 4   | Nguyễn Dũng       | 2022602499 |
| 5   | Đỗ Trọng Thích    | 2021604318 |

**Giảng viên hướng dẫn:** TS. Lê Thị Hồng Lan

## 📄 Giấy phép

Dự án này được cấp phép theo Giấy phép MIT. Xem file `LICENSE` để biết thêm chi tiết.
