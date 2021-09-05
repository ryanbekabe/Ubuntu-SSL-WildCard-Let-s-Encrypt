# Ubuntu-SSL-WildCard-Let-s-Encrypt
Memasang SSL WildCard dari Let's Encrypt

Video Ubuntu 18 04 2 LTS Install SSL WildCard Lets Encrypt 05092021: https://youtu.be/_HkNo2V9zFI

Download certbot terlebih dahulu, sudah saya sediakan menjadi certbot.zip, setelah didownload, extract, gunakan command berikut, sesuaikan dengan nama domain Anda:
./certbot certonly --server https://acme-v02.api.letsencrypt.org/directory --manual --preferred-challenges dns -d hanyajasa.com -d *.hanyajasa.com

Saya menggunakan 2 cara penulisan domain yakni hanyajasa.com dan *.hanyajasa.com, hal ini karena jika *.hanyajasa.com saja maka saya harus membuat pengaturan ServerName pada vhost menjadi:
ServerName www.hanyajasa.com
Sedangkan saya menginginkan agar ServerName tetap bisa walau tanpa www, yakni langsung hanyajasa.com

Pastikan Anda memiliki akses ke DNS Management dari penyedia domain yang Anda gunakan.
Karena kita perlu mengatur _acme-challenge dengan tipe TXT sebagai verifikasi dari certbot ke domain yang akan kita gunakan.


Manfaat WildCard SSL pada domain ini adalah ketika kita ingin menambahkan sub-domain baru, maka kita tidak perlu menggenerate SSL baru lagi menggunakan Certbot.
Cukup pakai file fullchain.pem dan privkey.pem yang sudah ada, yang kita buat agar WildCard (*) tadi, maka sub-domain pun memiliki SSL.

Untuk mengecek apakah _acme-challenge berisi teks verifikasi seperti yang ditampilkan oleh Certbot, dapat menggunakan command berikit, sesuai domain Anda: nslookup -q=txt _acme-challenge.hanyajasa.com

Sedangkan pada demonstrasi video di atas, saya menggunakan tool yang sudah saya buat di: https://bekabe.my.id/tool/ping/nslookup.php?cek=hanyajasa.com


Salam,

Riyan Hidayat Samosir

www.hanyajasa.com | bekabeipa@gmail.com
