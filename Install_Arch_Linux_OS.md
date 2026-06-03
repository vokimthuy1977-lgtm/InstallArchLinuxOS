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
1. Các thiết lập cơ bản
- Đầu tiên hãy đảm bảo màn hình của bạn có cái nhìn thuận tiện cho đôi mắt. Tôi luôn kính trọng điều này cho đôi mắt của bạn thông qua lệnh:
```
setfont ter-132b
```
Lệnh này tăng kích thước màn hình to hơn so với ban đầu, bạn có thể tùy chỉnh số bao nhiêu tùy thích cho phù hợp.
- Sau khi phù hợp mắt, ta sẽ kiểm tra kết nối Internet. Qua danh sách 2 nhé.
2. Kết nối Internet và thời gian ở USB
- Đầu tiên bạn hãy gõ lệnh:
```
timedatectl set-ntp true
```
Lệnh này có tác dụng đồng bộ thời gian giữa bộ cài USB và trên trang mạng.
- Để kiểm tra kết nối Internet không dây, bạn hãy gõ lệnh:
```
ping google.com
```
Nó sẽ gửi các gói tin nhỏ lên máy chủ Google nhằm kiểm tra mạng. Nếu kết quả trả về các dòng ví dụ ***64 bytes from hkg12s33-in-f14.1e100.net (142.250.204.46): icmp_seq=1 ttl=115 time=25.4 ms*** thì chứng tỏ máy bạn đang có Internet, nên bạn có thể bỏ qua danh sách 2 để sang danh sách 3 để đọc tiếp, nhưng tôi khuyên bạn nên đọc hết danh sách 2.
> Trước khi đọc tiếp hay sang danh sách 3, bạn bấm tổ hợp phím ***Ctrl + C*** để ngắt kết nối máy chủ Google.

- Nếu bạn chỉ thấy dòng *ping: google.com: Name or service not known* hoặc *Temporary failure in name resolution* thì chứng tỏ bạn đang mất kết nối Internet. Trước hết hãy gõ lệnh sau và *ENTER*:
```
iwctl
```
Lệnh này sẽ vào trình quản lý và kết nối Wifi trên bộ cài USB của bạn, dấu hiệu là bạn sẽ thấy dòng *[iwd]# _* xuất hiện trước màn hình.
- Sau khi vào trình quản lý và kết nối Wifi, hãy gõ lệnh sau để hiển thị tên thẻ mạng Wifi vật lý của máy tính bạn:
```
device list
```
Lệnh này sẽ hiển thị tên thẻ mạng Wifi của bạn và hãy dùng tên thẻ mạng đó cho các lệnh sau đây.
- Sau khi có tên thẻ mạng Wifi, bạn hãy gõ lệnh sau để dò các Wifi xung quanh:
```
station <Tên thẻ mạng của bạn> scan
```
> Lưu ý là nó sẽ không hiển thị lên màn hình điều gì cả!

- Sau khi gõ lệnh trên, hãy gõ tiếp lệnh phía dưới để hiển thị các tên Wifi đã quét:
```
station <Tên thẻ mạng của bạn> get-networks
```
Lệnh này sẽ hiển thị danh sách các Wifi đã quét. Hãy tìm kiếm Wifi của bạn và kết nối chúng qua lệnh dưới đây:
```
station <Tên thẻ mạng của bạn> connect <Tên Wifi của bạn>
```
> Lưu ý quan trọng, khi gõ lệnh kết nối vào Wifi, nó sẽ yêu cầu bạn nhập mật khẩu cho Wifi đó. Xin lưu ý là trong quá trình nhập mật khẩu sẽ không hiển thị lên màn hình do cơ chế bảo mật. Nên bạn cứ yên tâm gõ mật khẩu như bình thường và nhấn *ENTER*, nếu gõ sai thì nó sẽ yêu cầu gõ lại!

- Khi kết nối Wifi không dây hoàn tất. Hãy gõ lệnh sau để thoát khỏi trình quản lý và kết nối Wifi:
```
quit
```
Lúc này bạn sẽ quay lại dấu nhắc lệnh ban đầu.
> 💡 Mẹo: Có thể gõ lại lệnh **ping google.com** để kiểm tra kết nối Internet!

3. Phân vùng và định dạng ổ cứng, gắn vào cây thư mục của USB để tương tác với các phân vùng
- Để kiểm tra các phân vùng đã có chưa, hãy gõ lệnh:
```
lsblk
```
Lệnh này hiển thị cả ổ cứng và các phân vùng trong ổ cứng đó, cũng như đã gắn hoặc chưa.
- Nếu chưa có các phân vùng như sda1, sda2, sda3 thì hãy làm như sau. Gõ lệnh:
```
cfdisk
```
Lệnh này sẽ vào bảng giao diện đồ họa dạng văn bản của trình quản lý ổ đĩa.
Sau đó chọn gpt nếu máy chuẩn UEFI hoặc dos nếu máy chuẩn BIOS/Legacy.
Xóa hết toàn bộ phân vùng cũ ***(Lưu ý đảm bảo các phân vùng cũ của bạn không có dữ liệu quan trọng. Tránh việc định dạng phân vùng Boot của hệ điều hành khác vì sẽ khiến lỗi hệ thống)*** và tạo ra 3 phân vùng cho mỗi vai trò sau đây.
- Đối với sda1 đó là phân vùng Boot. Kích thước chỉ nên từ 700 MB đến 1 GB
- Đối với sda2 đó là phân vùng Swap. Kích thước chỉ nên khoảng 4 GB
- Đối với sda3 đó là phân vùng Root. Kích thước là phần còn lại sau khi cấp dung lượng cho hai phân vùng phía trên.
> Sự thật nổ não và thú vị: thực sự là sda không có số phía trước nó chính là toàn bộ cả ổ cứng của bạn. Còn sda có số phía trước ví dụ sda1, sda2, sda3 nó chỉ là các phân vùng trong chính cái ổ cứng sda đó mà thôi!!!

***Sau khi phân vùng ổ cứng, tiếp theo bạn phải định dạng các phân vùng đó theo các chuẩn như FAT32, EXT4 cũng như tạo Swap cho phân vùng Swap***
- Thực hiện lệnh sau để định dạng và đánh dấu phân vùng Boot:
```
mkfs.vfat -F 32 /dev/sda1
```
Lệnh này định dạng phân vùng /dev/sda1 theo loại FAT32 và đánh dấu đây là phân vùng Boot.
- Thực hiện lệnh sau để định dạng và đánh dấu phân vùng Swap:
```
mkswap /dev/sda2
```
Lệnh này định dạng phân vùng /dev/sda2 và đánh dấu đây là phân vùng Swap.
- Thực hiện lệnh sau để định dạng và đánh dấu phân vùng Root:
```
mkfs.ext4 /dev/sda3
```
Lệnh này định dạng phân vùng /dev/sda3 theo loại EXT4 và đánh dấu đây là phân vùng Root.
- Sau khi việc định dạng phân vùng hoàn tất với các phân vùng sda1, sda2, sda3 phù hợp, ta sẽ vào cách để gắn phân vùng vào cây thư mục của USB.
- Đối với phân vùng Root (sda3) ta sẽ gắn bằng lệnh như sau:
```
mount /dev/sda3 /mnt
```
Lệnh này có tác dụng gắn phân vùng Root vào thư mục /mnt. Tức là khi bạn dùng lệnh *cd /mnt* bạn sẽ thấy các thư mục và tệp dữ liệu nằm trong phân vùng Root (sda3), ví dụ /mnt/usr, /mnt/bin, /mnt/home, /mnt/etc,...
- Đối với phân vùng Boot (sda1) ta sẽ gắn bằng các lệnh như sau:
```
mkdir -p /mnt/boot
```
Lệnh này có tác dụng tạo thư mục boot trong mục /mnt. Sau đó mới thực hiện lệnh phía dưới:
```
mount /dev/sda1 /mnt/boot
```
Lệnh này có tác dụng gắn phân vùng Boot vào thư mục /mnt/boot. Tức là khi bạn *cd /mnt/boot* bạn sẽ thấy toàn bộ các thư mục và tệp dữ liệu trong phân vùng Boot (sda1).
> Lưu ý: Bản thân mọi thư mục và tệp nằm trong mục /mnt/boot thì *CHÚNG ĐỀU NẰM TRONG PHÂN VÙNG BOOT (sda1)*. Còn *BẢN THÂN* chính cái thư mục /mnt/boot nó chỉ là thư mục trung gian ánh xạ vào phân vùng Boot, cho nên bản thân cái thư mục /mnt/boot nó thuộc phân vùng Root (sda3), *NHƯNG* mọi thư mục con và tệp con trong chính thư mục /mnt/boot thì nó đều thuộc *PHÂN VÙNG BOOT* chứ không phải phân vùng Root.

- Tiếp theo ta sẽ kích hoạt phân vùng Swap (sda2) bằng lệnh:
```
swapon /dev/sda2
```
> Bạn có thể tắt bằng việc dùng lệnh **swapoff /dev/sda2** nếu không thích dùng RAM Ảo.

4. Cài đặt gói cần thiết và bước chân vào hệ điều hành Arch Linux thực thụ
- Điều đầu tiêu sau khi gắn các phân vùng vào cây thư mục là bạn cần tải các gói cần thiết và là lõi của Arch Linux như sau:
```
pacstrap -K /mnt base linux linux-firmware base-devel vim grub efibootmgr
```
Lệnh này tải các gói cần thiết vào phân vùng Root của bạn (Cần Internet, nếu không có Internet hãy quay lại danh sách 2 để xử lí).
- Sau khi có các gói cần thiết, bạn hãy gõ lệnh sau để tạo một tệp thông tin để bộ khởi động gắn các phân vùng vào đúng vị trí thư mục cây:
```
genfstab -U /mnt >> /mnt/etc/fstab
```
Sau đó gõ lệnh sau để vào hệ điều hành Arch Linux thực thụ:
```
arch-chroot /mnt
```