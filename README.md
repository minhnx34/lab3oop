# Bài thực hành số 3

## Kiến thức được thực hành

Các khái niệm cơ bản của lập trình hướng đối tượng (OOP), SOLID, các mẫu thiết kế cấu trúc và các mẫu thiết kế khởi tạo.

## Mục tiêu

Thực hành triển khai các mẫu thiết kế khởi tạo kết hợp với các mẫu thiết kế cấu trúc và những kiến thức đã học trước đó.

## Nhiệm vụ

Triển khai mô hình đối tượng của một trình mô phỏng chiến đấu giữa các sinh vật giả tưởng, vận dụng những kiến thức lý thuyết được thực hành.

Viết các bài kiểm thử đơn vị và kiểm thử chức năng cho giải pháp đã triển khai.

## Mô tả

Bạn sẽ triển khai phần lõi logic của một trò chơi, chịu trách nhiệm về cơ chế cấu hình sinh vật và chiến đấu giữa chúng.

Chiến đấu là cuộc đối đầu giữa hai người chơi, chính xác hơn là giữa các sinh vật trên bàn chơi của họ. Sinh vật có chỉ số tấn công và sức khỏe. Trong trận chiến, các sinh vật của hai người chơi lần lượt tấn công một sinh vật ngẫu nhiên của đối phương. Chỉ những sinh vật có chỉ số sức khỏe dương mới có thể tấn công hoặc bị tấn công. Chỉ những sinh vật có chỉ số tấn công dương mới có thể tấn công.

Sinh vật có thể có các bộ điều chỉnh, ảnh hưởng đến cách chúng thực hiện tấn công hoặc nhận sát thương. Ngoài ra, các sinh vật cụ thể còn có những khả năng khác nhau, cũng có thể ảnh hưởng đến quá trình tấn công và nhận sát thương.

Khi một sinh vật tấn công sinh vật của đối phương, nó không nhận sát thương từ đối phương.

Các chỉ số tấn công và sức khỏe sau đây có thể được biểu diễn bằng ký hiệu (x/y), trong đó x là chỉ số tấn công và y là chỉ số sức khỏe. Sinh vật có chỉ số (1/2) có chỉ số tấn công bằng 1 và chỉ số sức khỏe bằng 2.

## Yêu cầu chức năng

### Sinh vật

- Có chỉ số tấn công (số nguyên).
- Có chỉ số sức khỏe (số nguyên).
- Có thể tấn công sinh vật khác.
- Có thể nhận sát thương.
- Cho phép thay đổi chỉ số tấn công và sức khỏe.

Có nhiều loại sinh vật cụ thể với các khả năng khác nhau, ảnh hưởng đến cách chúng thực hiện các thao tác tấn công và nhận sát thương.

Cần xem xét sinh vật ở một số ngữ cảnh khác nhau:

### Sinh vật trong trận chiến

Trong trận chiến, sinh vật có thể thay đổi các chỉ số của mình (tấn công và sức khỏe), điều này ảnh hưởng đến kết quả trận chiến. Những thay đổi này chỉ được duy trì trong trận chiến: sau khi trận chiến kết thúc, các chỉ số của sinh vật trên bàn chơi của người chơi phải giữ nguyên.

### Sinh vật trên bàn chơi của người chơi

Sinh vật trên bàn chơi của người chơi cũng có thể thay đổi các chỉ số của mình. Những thay đổi này chỉ áp dụng cho các sinh vật trên bàn chơi của người chơi cụ thể đó: chúng không được ảnh hưởng đến các sinh vật trên bàn chơi của những người chơi khác, cũng như các sinh vật trong danh mục sinh vật.

### Sinh vật trong danh mục sinh vật

Các sinh vật "trong danh mục" có thể được thêm vào bàn chơi của người chơi. Sau đó, những thay đổi về chỉ số của sinh vật trên bàn chơi không được ảnh hưởng đến sinh vật "trong danh mục".

### Danh mục sinh vật

Danh mục sinh vật được biểu diễn bằng một tập hợp các đối tượng cho phép tạo ra sinh vật đã được cấu hình sẵn. Việc triển khai danh mục sinh vật phải cho phép cấu hình các chỉ số và các bộ điều chỉnh của chúng.

### Bộ điều chỉnh

Bộ điều chỉnh bổ sung những hành vi nhất định cho sinh vật. Chúng có thể ảnh hưởng đến cách thực hiện các thao tác tấn công và nhận sát thương.

Có thể áp dụng nhiều bộ điều chỉnh lên một sinh vật, bao gồm nhiều bộ điều chỉnh cùng loại. Các hiệu ứng của chúng phải được kết hợp với nhau.

### Lá chắn ma thuật

Lá chắn ma thuật cho phép sinh vật tránh hoàn toàn sát thương một lần duy nhất. Sau lần đầu tiên nhận đòn gây sát thương, lá chắn ma thuật sẽ mất hiệu lực. Sinh vật có lá chắn ma thuật sẽ nhận đầy đủ sát thương từ những lần tiếp theo.

### Tinh thông tấn công

Tinh thông tấn công cho phép sinh vật tấn công hai lần nếu sau lần tấn công đầu tiên, sinh vật vẫn còn chỉ số sức khỏe dương.

Nếu sinh vật chết sau lần tấn công đầu tiên, bộ điều chỉnh này không có tác dụng.

### Hút máu

Hút máu cho phép sinh vật hồi phục sức khỏe thông qua các đòn tấn công. Khi sinh vật có Hút máu tấn công sinh vật khác, chỉ số sức khỏe của nó tăng thêm 1.

### Phép thuật

Phép thuật cho phép áp dụng vĩnh viễn những cải thiện nhất định lên sinh vật trên bàn chơi của người chơi.

- Thuốc sức mạnh: tăng chỉ số tấn công của sinh vật thêm 5 đơn vị.
- Thuốc sức bền: tăng chỉ số sức khỏe của sinh vật thêm 5 đơn vị.
- Bùa hộ mệnh bảo vệ: áp dụng Lá chắn ma thuật cho sinh vật.
- Độc dược Kalenov: áp dụng Hút máu cho sinh vật.

Việc sử dụng phép thuật đồng nghĩa với việc thay đổi trạng thái của đối tượng sinh vật.

### Bàn chơi của người chơi

- Bàn chơi của người chơi chứa các sinh vật.
- Có thể thêm tối đa 7 sinh vật vào bàn chơi của một người chơi.
- Các thao tác diễn ra với sinh vật trên bàn chơi không được ảnh hưởng đến sinh vật trong danh mục, tương tự như mối quan hệ giữa sinh vật trong trận chiến và sinh vật trên bàn chơi.
- Bàn chơi phải triển khai thao tác lấy các sinh vật có thể tấn công và các sinh vật có thể bị tấn công.

### Trận chiến

Thực thể trận chiến triển khai chức năng tiến hành trận chiến giữa hai bàn chơi của hai người chơi. Trận chiến lần lượt chọn sinh vật tấn công và sinh vật bị tấn công, luân phiên giữa hai người chơi trong việc chọn các sinh vật này (người chơi thay phiên nhau tấn công).

Trận chiến có thể có hai kết quả: một trong hai người chơi chiến thắng hoặc hòa.

Nếu người chơi có sinh vật có thể tấn công, nhưng đối phương không có sinh vật nào có thể bị tấn công, người chơi đó được tính là thắng. Nếu người chơi không có sinh vật nào có thể tấn công, người chơi đó bỏ lượt và lượt được chuyển sang đối phương. Nếu người chơi không có sinh vật nào có thể tấn công, đồng thời đối phương không có sinh vật nào có thể bị tấn công, trận chiến được tính là hòa.

## Các sinh vật cụ thể

### Nhà phân tích chiến đấu

Nhà phân tích chiến đấu sử dụng kỹ năng của mình để xác định chiến lược và điểm yếu của đối phương. Trước khi tấn công sinh vật của đối phương, nó tăng chỉ số tấn công của mình thêm 3 cho đến hết trận chiến. Chỉ số ban đầu là (2/4).

### Chiến binh hung ác

Các đòn tấn công từ sinh vật khác chỉ khiến chiến binh này mạnh hơn. Khi nhận sát thương không gây chết, nó tăng gấp đôi chỉ số tấn công của mình cho đến hết trận chiến. Chỉ số ban đầu là (1/7).

### Rương Mimic

Khả năng khác thường của Mimic cho phép nó sao chép đối thủ. Khi tấn công sinh vật khác, chỉ số tấn công và sức khỏe của Mimic trở thành giá trị lớn nhất giữa các chỉ số tương ứng của nó và của đối thủ. Chỉ số ban đầu là (1/1).

Nếu Mimic có chỉ số (1/10) tấn công một sinh vật có chỉ số (5/2), thì trước khi thực hiện đòn tấn công, chỉ số của Mimic trở thành (5/10).

### Nỗi kinh hoàng bất tử

Thứ đã chết thì không thể bị giết... ít nhất là một lần. Một lần trong mỗi trận chiến, khi Nỗi kinh hoàng bất tử nhận sát thương gây chết, nó sẽ tái sinh, giữ nguyên chỉ số tấn công nhưng có chỉ số sức khỏe bằng 1. Chỉ số ban đầu là (3/4).

### Bậc thầy bùa hộ mệnh

Kỹ năng chiến đấu điêu luyện cùng khả năng sử dụng các tạo vật ma thuật khiến Bậc thầy bùa hộ mệnh trở thành một đối thủ đáng gờm. Sinh vật này được trang bị sẵn các bộ điều chỉnh "Lá chắn ma thuật" và "Tinh thông tấn công". Chỉ số ban đầu là (5/2).

## Yêu cầu phi chức năng

- Việc triển khai phải tuân theo các khái niệm cơ bản của lập trình hướng đối tượng.
- Phải sử dụng các mẫu thiết kế khởi tạo và cấu trúc trong quá trình triển khai.
- Việc triển khai phải hỗ trợ thêm các bộ điều chỉnh mới mà không vi phạm nguyên tắc OCP.
- Việc triển khai phải hỗ trợ thêm các phép thuật mới mà không vi phạm nguyên tắc OCP.
- Việc cấu hình và tạo sinh vật phải được đóng gói trong các kiểu riêng biệt.
- Việc cấu hình và tạo các loại sinh vật khác nhau phải có một trừu tượng chung.
- Phải có khả năng áp dụng bất kỳ bộ điều chỉnh nào lên bất kỳ sinh vật nào vào bất kỳ thời điểm nào.
- Các sinh vật cụ thể không được biết về các bộ điều chỉnh.
- Các lớp triển khai sinh vật được thiết kế để có bộ điều chỉnh cũng không được biết về sự tồn tại của các bộ điều chỉnh.
- Việc cấu hình những sinh vật được thiết kế để có bộ điều chỉnh phải đóng gói quá trình áp dụng các bộ điều chỉnh đó.
- Việc cấu hình sinh vật phải cho phép tiếp tục tùy chỉnh cấu hình sau đó.
- Các bộ điều chỉnh không được có một trừu tượng riêng.
- Phải triển khai một trừu tượng có chức năng áp dụng bộ điều chỉnh lên thực thể.

## Kiểm thử

Giải pháp được triển khai phải được bao phủ bởi các bài kiểm thử đơn vị và kiểm thử chức năng.

Các kịch bản kiểm thử cần được tự xây dựng; mức độ đầy đủ của việc kiểm thử được xác định dựa trên sự hiện diện của các bài kiểm thử chức năng của từng mô-đun riêng lẻ, cũng như các bài kiểm thử cho những kịch bản sử dụng chính của mô hình đối tượng.
