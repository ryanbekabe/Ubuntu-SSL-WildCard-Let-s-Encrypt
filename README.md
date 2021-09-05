# Ubuntu-SSL-WildCard-Let-s-Encrypt
Memasang SSL WildCard dari Let's Encrypt

![SSL_WildCard](/Ubuntu-SSL-WildCard-Let-s-Encrypt/raw/main/SSL%20WildCard.png)

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

Sedikit cuplikan log:
```git
2021/09/05 08:18:19.289947 system_key.go:147: cannot determine seccomp compiler version in generateSystemKe                                                             y: error: unsupported argument "version-info"
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Renewing an existing certificate for hanyajasa.com and *.hanyajasa.com

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please deploy a DNS TXT record under the name:

_acme-challenge.hanyajasa.com.

with the following value:

_gUFH6KbKGXDuEsBGWsFYEn1KNH3eVmaSF4F38rJx6U

Before continuing, verify the TXT record has been deployed. Depending on the DNS
provider, this may take some time, from a few seconds to multiple minutes. You can
check if it has finished deploying with aid of online tools, such as the Google
Admin Toolbox: https://toolbox.googleapps.com/apps/dig/#TXT/_acme-challenge.hanyajasa.com.
Look for one or more bolded line(s) below the line ';ANSWER'. It should show the
value(s) you've just added.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Press Enter to Continue

Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/hanyajasa.com/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/hanyajasa.com/privkey.pem
This certificate expires on 2021-12-04.
These files will be updated when the certificate renews.

NEXT STEPS:
- This certificate will not be renewed automatically. Autorenewal of --manual certificates requires the use of an authentication hook script (--manual-auth-hook) but one was not provided. To renew this certificate, repeat this same certbot command before the certificate's expiry date.

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


```


Salam,

Riyan Hidayat Samosir

www.hanyajasa.com | bekabeipa@gmail.com
