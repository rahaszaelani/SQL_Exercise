# SQL_Exercise
In this slides i want to share my work on Rakamin Academy's SQL task, in order to showcase some of my SQL skills using PostgreSQL.

About the Data : The Database consist of 4 table, data pelanggan, data alamat, data pemesanan (order) and data merchant From RakaFood business.

Here's the objectives.

1. Salah satu merchant kita, yaitu KFC Depok, ingin membuka cabang baru.  Karena itu mereka meminta insight dari kita untuk melihat daerah mana  yang paling berpotensi di luar kota Depok. Kami membutuhkan data kota  (selain Depok) dan alamat (kolom address) tempat customer berada (ﬁlter  untuk alamat utama saja) beserta total order dari masing-masing alamat  tersebut. Urutkan juga dari total order paling banyak.

2. Dari customer yang pernah melakukan order, kami ingin  memberikan cashback untuk customer yang sudah menggunakan  email ‘@yahoo.com’. Karena itu, kami butuh informasi customer ID,  nomor telepon, metode bayar, dan TPV (Total Payment Value). Pastikan  bahwa mereka bukan penipu. 

3.Tim UX researcher ingin mengetahui alasan dari user yang belum menggunakan digital  payment method dalam pembayaran transaksinya secara kualitatif dan melakukan interview  kepada user secara langsung. Mereka membutuhkan data customer berupa nama, email.  nomor telepon, alamat user, metode_bayar, dan jumlah ordernya (dari table rakamin_orders),  yang dibayarkan secara cash. Pastikan user sudah mengkonﬁrmasi nomor telepon, bukan  penipu, dan masih aktif.

4. Salah satu tantangan bisnis yang sedang dihadapi oleh RakaFood adalah untuk  meningkatkan transaksi menggunakan digital payment (cahsless). Kira-kira dari data  yang kita miliki, data apa yang dapat membantu business problem tersebut? Sediakan  suatu query untuk bisa membantu tim-tim terkait dari RakaFood untuk bisa menjawab  tantangan bisnis tersebut, kemudian jelaskan mengapa menurut Anda data hasil dari  query Anda itu bisa membantu menyelesaikan business problem tersebut, yaitu untuk  meningkatkan digital payment di transaksi RakaFood.

5.Tim customer experience (CX) ingin mengoptimalkan penggunaan dompet digital dan  membuat program membership untuk meningkatkan loyalitas pelanggan. Membership ini  berbasis poin, setiap poin diperoleh dari total belanja minimal 1000 menggunakan dompet  digital. Adapun kategori membership berbasis poin, adalah sebagai berikut:
a.Total poin kurang dari 10 adalah non member
b.Total poin 10 - 100 adalah bronze member
c.Total poin 100 - 300 adalah silver member
d.Total poin lebih dari 300 adalah gold member
Tim CX membutuhkan data jumlah pelanggan di setiap kota berdasarkan kategori  membershipnya. 


SQL Query :

-- Answer no 1

select alamat, kota, count (id_order) as jumlah_order
from rakamin_customer as rc
left join rakamin_customer_address as rca on rca.id_pelanggan=rc.id_pelanggan
left join rakamin_order as ro on ro.id_pelanggan=rc.id_pelanggan
where  (rca.kota != 'Depok') and (ro.id_merchant = 5) 
group by 1,2
order by 3 DESC ;

-- Answer no 2

select rc.id_pelanggan, telepon,metode_bayar,(kuantitas * harga) as total_payment_value
from rakamin_customer as rc
right join rakamin_order as ro on ro.id_pelanggan=rc.id_pelanggan
where (email like '%yahoo.com') and (penipu = 0) 
group by 1,2,3,4
order by 4 desc
;
-- Answer no 3

select rc.nama, rc.email, rc.telepon, rca.alamat, ro.metode_bayar, count (ro.kuantitas) as total_order
from rakamin_customer as rc
join rakamin_customer_address as rca on rc.id_pelanggan=rca.id_pelanggan
left join rakamin_order as ro on ro.id_pelanggan=rc.id_pelanggan
	where (rc.penipu = 0) and (rc.konfirmasi_telepon <> 0) and (rc.pengguna_aktif = 1 ) and (ro.metode_bayar = 'cash')
group by 1,2,3,4,5

-- Answer no 4

select rc.nama, rc.email, rca.alamat,count (ro.kuantitas) as jumlah_pesanan, ro.metode_bayar
from rakamin_customer as rc
join rakamin_customer_address as rca on rc.id_pelanggan=rca.id_pelanggan
left join rakamin_order as ro on ro.id_pelanggan=rc.id_pelanggan
	where (rc.penipu = 0) and (rc.konfirmasi_telepon <> 0 ) and (rc.pengguna_aktif = 1 )  and (ro.metode_bayar = 'cash')
group by 1,2,3,5
order by 4 DESC;

note : Dengan mengetahui siapa saja customer yang masih melakukan pembayaran dengan cash kita dpat memberikan promosi agar mereka mau mencoba beralih ke digital payment.

-- Answer no 5

select  rca.kota, 
        count (distinct rca.id_pelanggan) as jumlah_pelanggan, 
        customer_loyalty
from 
(
(select id_pelanggan,harga*kuantitas as total_belanja,harga*kuantitas/1000 as poin,
case when harga*kuantitas/1000 < 10 then 'non'
     when harga*kuantitas/1000 between 10 and 100 then 'bronze_member'
	 when harga*kuantitas/1000 between 100 and 300 then 'silver_member'
	 when harga*kuantitas/1000 > 300 then 'gold_member'
	 end as customer_loyalty
	 from rakamin_order 
	 where metode_bayar <> 'cash') as ro
	 left join rakamin_customer_address as rca on rca.id_pelanggan=ro.id_pelanggan
	 ) 
	 group by 1,3;
	 
