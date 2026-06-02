# Hướng dẫn cài đặt Hệ Điều Hành Arch Linux
## Chuẩn bị trước khi cài đặt hệ điều hành Arch Linux
1. Về USB
-  Bạn cần chuẩn bị một USB có dung lượng từ 2 GB trở lên để có thể chứa tệp ISO nặng khoảng 1,5 GB và đảm bảo USB của bạn không chứa tài liệu quan trọng trong quá trình nạp tệp ISO vào USB.
-  Bạn cần sử dụng các phần mềm như *Rufus*, *BalenaEtcher*, *Ventoy*, hoặc dùng công cụ dòng lệnh... dd của Linux hoặc MacOS nhưng tôi không khuyến khích dùng dd.
-  Còn việc sử dụng như thế nào bạn có thể lên các diễn đàn trên mạng để tìm hiểu vì tôi không có bài viết hướng dẫn điều đó!
2. Về tính trọn vẹn và xác thực của tệp ISO, cách cài tệp ISO và kiểm tra System Firmware của máy tính
- Để cài tệp ISO của Arch Linux hãy vào đường liên kết https://archlinux.org/download/ để cài đặt.
- Tôi khuyên bạn nên kiểm tra mã SHA256 của tệp trước khi tải từ các nguồn khác kể cả archlinux.org mặc dù trang chính chủ archlinux.org là an toàn. Điều này nhằm đảm bảo tránh các mối độc hại từ các trang mạng hoặc lỗi đường truyền mạng dẫn đến quá trình cài đặt bị lỗi tệp.
- Đối với Windows vào PowerShell gõ lệnh:
```
Get-FileHash <Đường dẫn đến tệp ISO của bạn> -Algorithm SHA256
/*
Ví dụ: <Đường dẫn đến tệp ISO của bạn> thay thành C:\Users\John\Downloads\archlinux-xxxx.iso 
*/
```
-  Đối với Linux/MacOS vào Bash gõ lệnh:
```
sha256sum <Đường dẫn đến tệp ISO của bạn>
/*
Ví dụ: <Đường dẫn đến tệp ISO của bạn> thay thành /home/John/Downloads/archlinux-xxxx.iso
*/
```
-  Để kiểm tra System Firmware của máy tính của bạn thuộc chuẩn UEFI hay chuẩn BIOS/Legacy đối với Windows và Linux/MacOS, hãy làm theo dưới đây.
- Đối với Windows vào cmd.exe với *quyền quản trị viên* kiểm tra bằng Batch và gõ lệnh như sau:
```
bcdedit | find "path"
```
Nếu kết quả màn hình trả về dòng có đuôi .efi thì máy thuộc chuẩn UEFI.
Nếu kết quả màn hình trả về dòng có đuôi .exe thì máy thuộc chuẩn BIOS/Legacy.
- Đối với Linux vào Bash gõ lệnh sau:
```
[ -d /sys/firmware/efi ] && echo "UEFI" || echo "Legacy/BIOS"
```
Nó sẽ trả về chữ UEFI lên màn hình nếu là chuẩn UEFI hoặc trả về Legacy/BIOS nếu là chuẩn BIOS/Legacy.
- Đối với MacOS vào gõ lệnh sau:
```
ioreg -l -p IODeviceTree | grep "firmware-abi"
```
Nó sẽ trả về **"firmware-abi" = <"EFI64">** nếu là dạng EFI 64-bit tương ứng chuẩn UEFI.
3. Phím tắt và cách vào Boot Menu
- Điều quan trọng là bạn phải biết các phím tắt để vào Boot Menu, tôi sẽ nói một vài phím tắt tùy thuộc vào từng hãng máy tính **(Lưu ý là tôi không thể liệt kê hết các dòng máy, cho nên bạn hãy lên Google để tìm kiếm phím tắt phù hợp với dòng máy của bạn!)**
-  Dell: Nhấn F12
-  HP: Nhấn F9 hoặc ESC
-  ASUS: Nhấn F8 hoặc ESC
-  Acer: Nhấn F12
-  Các dòng khác bạn lên Google tìm kiếm.
-  Khi biết phím tắt. Hãy tắt máy tính của bạn (Shut Down), sau đó mở lên và nhấn liên tục phím tắt cho đến khi vào Boot Menu.
4. Chọn khởi động từ USB
- Khi vào Boot Menu hãy dùng phím mũi tên lên/xuống để tìm dòng có tên USB và tên chuẩn UEFI hoặc BIOS/Legacy của máy bạn. Nếu chọn đúng thì màn hình sẽ chuyển sang menu của Arch Linux khi đó hãy chọn dòng ***Arch Linux install medium (x86_64, UEFI)*** và nhấn *ENTER*
- Sau đó đợi khoảng thời gian và trong lúc này màn hình sẽ hiện chữ để nạp dữ liệu USB lên RAM. Đợi khi nào có dòng ***root@archiso ~ # _*** thì bạn đã vào môi trường Arch Linux của USB.
***Sang tiêu đề kế tiếp để đọc hướng dẫn thiết lập hệ điều hành Arch Linux trong giao diện cài đặt***
> Lưu ý phải đảm bảo bạn đã vào môi trường Arch Linux của USB từ các bước làm trên!!!

## Thiết lập cách cài đặt hệ điều hành Arch Linux trong giao diện cài đặt