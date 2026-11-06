\# BÁO CÁO CÁ NHÂN - LAB 1



\## 1. Trả lời Câu hỏi 4 (Phần LLM Few-shot)

\*\*- Kết quả 4.A và 4.B có khớp dự đoán không? Điều gì làm bạn bất ngờ nhất?\*\*

(Bạn điền nhận xét cá nhân của bạn sau khi chạy code phần 4A và 4B vào đây. Ví dụ: F1 score có tăng như dự đoán không, chi phí token thay đổi thế nào...)



\*\*- Vì sao phải đặt temperature=0 và max\_tokens nhỏ khi phân loại?\*\*

Việc đặt `temperature=0` giúp mô hình trả về kết quả mang tính xác định (deterministic), không bị sáng tạo ngẫu nhiên, đảm bảo tính nhất quán khi phân loại. Đặt `max\_tokens` nhỏ giúp tiết kiệm chi phí và tránh việc LLM sinh ra văn bản dài dòng không cần thiết, vì ta chỉ cần nhãn "spam" hoặc "ham" (và một đoạn giải thích ngắn). Nếu `max\_tokens=1`, rủi ro là mô hình có thể bị cắt cụt từ chưa hoàn chỉnh hoặc không thể xuất ra định dạng JSON đầy đủ.



\## 2. Giải trình Thử thách cá nhân (Đề #5)

\*\*Nhiệm vụ:\*\* Viết 4 tin nhắn của riêng bạn (2 spam né từ khoá, 2 ham chứa từ khóa) và so sánh dự đoán giữa BoW vs Embedding+LogReg.



\*\*Các tin nhắn đã tạo:\*\*

\- Spam 1: "Security Alert: Unusual login attempt detected on your bank profile. Verify your identity immediately to secure it."

\- Spam 2: "Delivery failed: We could not deliver your parcel today. Please update your address to avoid return to sender."

\- Ham 1: "Hey Thang, are you free this weekend? Let's go play some pickleball at Diamond court."

\- Ham 2: "I can't believe you managed to win that match yesterday, your serve was amazing!"



\*\*Giải thích kết quả:\*\*

\- \*\*Mô hình BoW:\*\* Có xu hướng dự đoán sai. Do cơ chế chỉ đếm tần suất từ khóa, BoW không nhận diện được 2 tin Spam vì thiếu các mồi nhử quen thuộc, nhưng lại bị "sập bẫy" đánh giá sai 2 tin Ham thành Spam chỉ vì sự xuất hiện của các từ "free" và "win".

\- \*\*Mô hình Embedding:\*\* Dự đoán chính xác. Embedding nén toàn bộ câu vào không gian vector để hiểu ngữ nghĩa. Nó nhận ra văn phong đe dọa/khẩn cấp của Phishing trong 2 tin đầu, đồng thời hiểu được bối cảnh giao tiếp bạn bè (thời gian rảnh, thắng trận thể thao) trong 2 tin sau nên không bị nhầm lẫn.

