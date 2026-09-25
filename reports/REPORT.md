# Báo cáo vòng lặp Active Learning

Tên: Le Tuan Anh
Công cụ gán nhãn: CVAT

## 1. Dữ liệu và cách chia tập
Camera đứng một chỗ, một chiếc xe nằm trong hình vài giây. Ảnh học và ảnh kiểm tra phải cách nhau theo thời gian. Nếu trộn ngẫu nhiên, cùng một xe có thể vừa được AI học vừa được dùng để chấm. Điểm sẽ đẹp hơn sự thật (bị rò rỉ dữ liệu). Do đó phải chia theo thời gian và để khoảng trống ở giữa.

## 2. Kết quả lần chạy đầu
Điểm khớp khung vòng 0 là 0.771. Xe nhỏ chỉ được tìm thấy khoảng 0.182, xe vừa 0.547, xe lớn 0.561. Nghĩa là xe ở xa bị bỏ sót nhiều hơn xe ở gần. Nhãn dùng để chấm cũng do máy vẽ, chưa có người xem từng khung, nên có thể nhãn chấm sai chứ không phải AI sai.

## 3. Cách chọn ảnh
Mỗi ảnh có một điểm. Một nửa điểm là AI không chắc. Ba phần mười là AI vẽ nhiều khung còn lưỡng lự. Hai phần mười là ảnh có khác thời gian với ảnh khác. Hai ảnh trong cùng lô phải cách nhau ít nhất 2 giây, vì camera đứng yên, ảnh sát nhau gần như giống hệt. Các ảnh đứng đầu như frame_0182.jpg có mức độ lưỡng lự cao nên được chọn. Điểm cao không có nghĩa sửa ảnh đó sẽ làm AI giỏi hơn.

## 4. Kết quả sau khi học thêm
Ở vòng 1, tôi đã sửa và thêm 154 khung. Tuy nhiên AP50 giảm so với vòng 0 (-0.314). Điều này là bình thường vì nhãn chấm (test) chưa được người duyệt, và 12 ảnh có thể chưa đủ để bao phủ hết sự thay đổi, hoặc mô hình bị quá khớp (overfit) vào lô 12 ảnh tối này, dẫn đến dự đoán sai trên tập test.

## 5. Có nên làm tiếp vòng 2?
Tôi đề xuất dừng lại. Điểm giảm mạnh cho thấy việc fine-tune trực tiếp trên 12 ảnh có thể gây catastrophic forgetting hoặc overfit. Ngoài ra, việc nhãn của tập test chưa được người kiểm tra lại khiến cho điểm số không phản ánh đúng 100% sự tiến bộ thật sự của AI trên thực tế. Cần xem xét nhãn tập test trước khi học tiếp.
