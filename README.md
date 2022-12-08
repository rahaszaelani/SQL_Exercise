# SQL_Exercise
In this slides i want to share my work on Rakamin Academy's SQL task, in order to showcase some of my SQL skills using PostgreSQL.

About the Data : The Database consist of 4 table, data pelanggan, data alamat, data pemesanan (order) and data merchant From RakaFood business.

Here's the objectives.

1. Salah satu merchant kita, yaitu KFC Depok, ingin membuka cabang baru.  Karena itu mereka meminta insight dari kita untuk melihat daerah mana  yang paling berpotensi di luar kota Depok. Kami membutuhkan data kota  (selain Depok) dan alamat (kolom address) tempat customer berada (ﬁlter  untuk alamat utama saja) beserta total order dari masing-masing alamat  tersebut. Urutkan juga dari total order paling banyak.

2. Dari customer yang pernah melakukan order, kami ingin  memberikan cashback untuk customer yang sudah menggunakan  email ‘@yahoo.com’. Karena itu, kami butuh informasi customer ID,  nomor telepon, metode bayar, dan TPV (Total Payment Value). Pastikan  bahwa mereka bukan penipu. 

3. Tim UX researcher ingin mengetahui alasan dari user yang belum menggunakan digital  payment method dalam pembayaran transaksinya secara kualitatif dan melakukan interview  kepada user secara langsung. Mereka membutuhkan data customer berupa nama, email.  nomor telepon, alamat user, metode_bayar, dan jumlah ordernya (dari table rakamin_orders),  yang dibayarkan secara cash. Pastikan user sudah mengkonﬁrmasi nomor telepon, bukan  penipu, dan masih aktif.

4. Salah satu tantangan bisnis yang sedang dihadapi oleh RakaFood adalah untuk  meningkatkan transaksi menggunakan digital payment (cahsless). Kira-kira dari data  yang kita miliki, data apa yang dapat membantu business problem tersebut? Sediakan  suatu query untuk bisa membantu tim-tim terkait dari RakaFood untuk bisa menjawab  tantangan bisnis tersebut, kemudian jelaskan mengapa menurut Anda data hasil dari  query Anda itu bisa membantu menyelesaikan business problem tersebut, yaitu untuk  meningkatkan digital payment di transaksi RakaFood.

5. Tim customer experience (CX) ingin mengoptimalkan penggunaan dompet digital dan  membuat program membership untuk meningkatkan loyalitas pelanggan. Membership ini  berbasis poin, setiap poin diperoleh dari total belanja minimal 1000 menggunakan dompet  digital. Adapun kategori membership berbasis poin, adalah sebagai berikut:

a.Total poin kurang dari 10 adalah non member

b.Total poin 10 - 100 adalah bronze member

c.Total poin 100 - 300 adalah silver member

d.Total poin lebih dari 300 adalah gold member

Tim CX membutuhkan data jumlah pelanggan di setiap kota berdasarkan kategori  membershipnya. 
