# ĐỒ ÁN CUỐI KÌ: PHÂN LOẠI VÀ XỬ LÝ TRÁI CÂY TRONG MÔI TRƯỜNG TỰ NHIÊN  
## Mô tả đồ án:  
Đồ án này sử dụng Yolov11 để phát hiện và đếm trái cây trong môi trường tự nhiên từ hình ảnh được tải lên. Ứng dụng được xây dựng với HTML và CSS đơn giản, kết hợp với Flask để tạo ra một trang web với giao diện dễ nhìn, dễ thao tác.  

## Các tính năng chính:  
- Phát hiện ra trái cây: Dùng Yolov11 để phân loại ra 13 loại trái cây đã được huấn luyện.
- Đếm số lượng có được của từng loại quả.
- Cho biết dinh dưỡng và công dụng của từng trái.
- Có các chức năng khác như:
  + Nếu trong một ảnh có nhiều trái, thì có thể gọi ra một trái để hiển thị lên màn hình.
  + Dùng xác định biên để xác định có bao nhiêu trái trong ảnh và vị trí của mỗi trái.
 
## Cách huấn luyện
### Bước 1: Xác định chủ đề cần làm và lập ra kế hoạch:  
- Chủ đề: Phân loại và xử lý trái cây.  
- Mục tiêu cần làm:  
  + Tìm những loại quả thường gặp trong tự nhiên.  
  + Tìm các ảnh của các loại quả đó (càng nhiều ảnh càng tốt).  
  + Gán nhãn ảnh (có thể dùng Roboflow hoặc Kaggle).  
  + Huấn luyện mô hình với phiên bản Yolov11 (có thể huấn luyện trên Google Colab hay VSCode).
  + Sử dụng mô hình học tốt nhất best.pt sau khi huấn luyện xong.
 
### Bước 2: Tìm ảnh của các loại quả  
- Có thể tìm trực tiếp trên Internet, chụp ngoài tự nhiên hoặc dataset có sẵn của Kaggle.

### Bước 3: Gán nhãn ảnh bằng Roboflow  
- Ví dụ minh họa:
<img width="656" height="653" alt="image" src="https://github.com/user-attachments/assets/3e67b9da-817b-4509-a08c-ae6672fc26f3" />

<img width="1160" height="652" alt="image" src="https://github.com/user-attachments/assets/a2f08fc2-b646-422a-b31e-3110df4ac1a7" />  

### Bước 4:  Huấn luyện mô hình với Google Colab (VSCode tương tự nhưng có thể lâu hơn)  
- Trước tiên, cần kết nối Colab với GPU T4 có sẵn trên Colab giúp quá trình huấn luyện nhanh chóng hơn.
- Dùng câu lệnh sau để kiểm tra
```bash
!nvidia-smi
```

- Kết quả hiện ra:
<img width="788" height="341" alt="image" src="https://github.com/user-attachments/assets/e4cbd453-3bf9-4d32-bd08-4eda95d19876" />  

Như vậy có thể tiến hành huấn luyện.  

- Tiếp theo cần kiểm tra xem phiên bản Ultralytics và Python có phù hợp với nhau hay không:
```bash
%pip install "ultralytics<=8.3.40" supervision roboflow
# prevent ultralytics from tracking your activity
!yolo settings sync=False
import ultralytics
ultralytics.checks()
```

- Lấy dataset từ Roboflow về Colab thông qua API
```bash
!pip install roboflow

from roboflow import Roboflow
rf = Roboflow(api_key="ILbu6FprpxIeaOUXbk4Q")
project = rf.workspace("fruit-detector-blc0f").project("fruits-detection-exam")
version = project.version(13)
dataset = version.download("yolov11")
```

- Bắt đầu huấn luyện mô hình:
```bash
!pip install -q ultralytics
from ultralytics import YOLO

model = YOLO('yolo11s.pt')
model.train(
    data='/content/Fruits-Detection-Exam-13/data.yaml',
    epochs=150,
    imgsz=640,
    batch=16
)
```

- Có thể thay đổi epochs thành 100 hay 200 tùy ý, nhưng không nên ít hơn 100 vì mô hình học không tối ưu.
- imgsz có thể để mặc định là 640x640.
- batch size có thể thay đổi thành 4, 8 hoặc 16 tùy vào cấu hình máy và số lượng dataset, nếu dataset ít thì chỉ cần dùng 4 hoặc 8.  

### Bước 5: Lấy mô hình học tốt nhất xong thời gian huấn luyện  
- Tiến hành lưu mô hình về máy hoặc folder mình muốn
```bash
from google.colab import files
files.download('runs/detect/train/weights/best.pt')
```

## Cấu trúc thư mục  
<img width="545" height="263" alt="image" src="https://github.com/user-attachments/assets/9db75b7b-109c-4ffb-b08d-5ad519675160" />  

## Hướng dẫn chạy thử dự án  
### Bước 1: Lấy dự án về máy cá nhân và lưu trong folder bất kỳ  
```bash
git clone https://github.com/trdphatphattran/Digital-Image-Processing.git
```

### Bước 2: Dùng VSCode chạy thử dự án  
- Mở VSCode, vào thư mục chứ code vừa lưu về.
- Tìm đến file app.py và run.

### Bước 3: Test các chức năng  
- Trong giao diện, chọn 1 hoặc nhiều hình ảnh trái cây gắn vào và ấn vào "Xử lý ảnh", ví dụ:
<img width="1262" height="778" alt="image" src="https://github.com/user-attachments/assets/8a479bfd-32e4-496e-ae2c-143228aec6a3" />

- Xem kết quả được tìm thấy và số lượng của chúng, ví dụ:
<img width="840" height="773" alt="image" src="https://github.com/user-attachments/assets/7ee3f0c9-9f1d-4e95-9bcc-8ca36be7df74" />

<img width="425" height="402" alt="image" src="https://github.com/user-attachments/assets/525a97df-9c95-4515-980f-171a13080820" />  

- Thử các chức năng khác, trong "Chế độ xử lý" chọn "Đối tượng cụ thể", sau đó nhập tên trái đó vào; bên "Chức năng xử lý" có thể chọn "Phát hiện biên" gồm 2 chế độ khác nhau giúp phát hiện vị trí rõ ràng của từng quả trong ảnh lớn đó; ngoài ra có thể ấn vào "Công dụng" hoặc "Dinh dưỡng", ví dụ:
<img width="1345" height="656" alt="image" src="https://github.com/user-attachments/assets/e50ddfb5-0581-471f-b978-4cf9b9f14443" />

## Dataset tham khảo  
- [Roboflow](https://app.roboflow.com/fruit-detector-blc0f/fruits-detection-exam/browse?queryText=&pageSize=50&startingIndex=0&browseQuery=true)  
- [Kaggle](https://www.kaggle.com/datasets/shreyapmaher/fruits-dataset-images)  

## Các tài liệu có thể tham khảo  
- [Yolov11](https://docs.ultralytics.com/vi/models/yolo11/)  
- [OpenCV](https://opencv.org/)
- [Roboflow](https://roboflow.com/)
- [Kaggle](https://www.kaggle.com/)
















  
    





