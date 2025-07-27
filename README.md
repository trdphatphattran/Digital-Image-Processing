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




  
    





