# Multi-Agent-Search
This project is my solutions of Berkeley Pacman solution

## Problem Search

### Q1:  Reflex Agent:

    Bài này yêu cầu người dùng lâpj trình 1 tác tử phản ứng với những thay đổi của mỗi trường khi 
    chính chúng hay vật khác làm thay đổi nó. Hàm sẽ trả về 1 số điểm đại diện cho giá trị của 
    việc đi nước đi tiếp theo.
    Chính vì thế vào mỗi bước đi hợp lệ tiếp theo em dùng hàm getScore() để lấy điểm. Mục tiêu
    là pacman ăn hết thức ăn và tránh ma vì thế số điểm ở bước đi gần thức ăn tăng lên bằng 
    khoảng cách đến thực ăn, ngược lại với ma, ta cần tránh xa chúng. Cho nên số điểm sẽ giảm
    bằng cách lấy số điểm hiện tại trừ đi khoảng cách đến con ma gần nhất. Khoảng cách ở đây 
    có thể dùng manhattan hoặc euclid. Cách tính này đảm bảo pacman đi đến nơi hợp lý bằng cách
    ước lượng số điểm tương quan giữa food và ghost.         

### Q2: Minimax
    Như đã biết về thuậ toán minimax, ta có nhiều người chơi, họ sẽ đều chọn những nước đi tối ưu
    trong từng lượt của mình. Ở node max là nước đi tối ưu mà người chiến thắng chọn và node min 
    là giá trị nhỏ nhất. Nước đi của 2 bên là xen kẽ nên em dùng 1 hàm để quy để gọi 2 node min, 
    max 1 cách liên tiếp. Tác tử 0 là pacman và >= 1 là ma. Nếu là pacman ta lấy các nước đi 
    hợp lệ của nó bằng hàm getLegalActions() sau đó lấy các giá trị max trên các đường có thể đi
    đó kèm theo hướng đi bằng các gọi đệ quy dự đoán những con ghost sẽ làm gi. Lúc tác tử là ghost
    ta lấy giá trị min trên node của từng con ma, bằng cách gọi tiếp đệ quy xem pacman sẽ lựa 
    chọn tối ưu ra sao. Nếu ma tăng độ sau của cây quyết định xuống 1. Cứ như vậy ta sẽ có các 
    hành động tường ứng với các giá trị min max để pacman thắng.  
    
### Q3: Alpha-Beta Pruning
    Bài 3 là cải tiến của bài 2. Ta vẫn dùng cây quyết định để dự đoán các nước đi tối ưu giữa cacs
    đối thủ. Tuy nhiên cần thêm 2 giá trị là A ( âm vô cungf) và B (dương vô cungf) ở mỗi node. Trong
    đó khi duyệt A là max của Node có thể đạt được, B là min giá trị Node đạt được. Nếu ở Node nào đó
    B < A thì cắt phần chưa duyệt đi vì giá trị đó chắc chắn không được sử dụng.

### Q4: Expectimax
    Thuậ toán minimax hoạt dộng tốt nếu cả 2 bên đều đưa ra nước đi tối ưu trong từng hoành cảnh, 
    bài này yêu cầu giải quyết khi nước đi của ma là không tối ưu. Vì thế em không dự đoán ma sẽ 
    đi theo giá trị min trong Node của nó nữa mà sẽ lấy trung bình các giá trị nó có thể đi rồi cho 
    pacman đưa ra nước đi tối ưu với các lựa chọn đó. 

### Q5: Evaluation Function
    Giống bài 1 tuy nhiên em sử dụng thêm 1 giá trị đó là scaredTimer là thời gian pacman không sợ ma.
    Lúc này khi lập trình không cần để ý đến vị trí của những con ma nữa vì pacman không sợ ma. Cho nên
    em để điểm giữ nguyên. Nếu hết thời gian  l
