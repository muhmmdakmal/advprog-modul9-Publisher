## AdvProg - Tutorial Module 09

<h2>

Nama    : Muhammad Akmal Abdul Halim

Kelas   : B

NPM     : 2306245125
</h2>

**a. How much data your publisher program will send to the message broker in one
run?**

Dalam sekali eksekusi, program publisher Anda akan mengirimkan 5 pesan ke message broker. Setiap pesan berisi sebuah objek UserCreatedEventMessage yang terdiri dari dua field yaitu user_id dan user_name. Pesan-pesan ini dikirim ke topic/queue "user_created" menggunakan library CrosstownBus yang memanfaatkan protokol AMQP. Dapat dilihat dari kode main.rs bahwa program melakukan lima kali pemanggilan fungsi publish_event() dengan data pengguna yang berbeda-beda (Amir, Budi, Cica, Dira, dan Emir), yang semuanya menggunakan NPM 2306245125 sebagai bagian dari nama pengguna.

**b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber
program, what does it mean?**

URL "amqp://guest:guest@localhost:5672" yang sama pada program publisher dan subscriber menunjukkan bahwa kedua program terhubung ke instance message broker yang sama. Komponen URL ini terdiri dari protokol AMQP, kredensial autentikasi "guest:guest" (yang merupakan default), alamat server "localhost" yang berarti broker berjalan di mesin lokal, dan port 5672 yang merupakan port standar untuk AMQP. Penggunaan URL yang identik ini sangat penting karena memastikan bahwa pesan yang dikirim oleh publisher akan diterima oleh subscriber yang mendengarkan pada broker yang sama. Ini merupakan prinsip dasar dalam pola komunikasi publish-subscribe, di mana publisher dan subscriber tidak berkomunikasi langsung melainkan melalui perantara message broker yang sama.

## Message Broker: RabbitMQ
![alt text](<img/Screenshot 2025-05-06 000430.png>)

## Sending and Processing Event
![alt text](img/pub1.jpg)

Saat menjalankan perintah cargo run pada aplikasi subscriber, aplikasi tersebut akan berada dalam keadaan menunggu untuk menerima data. Kemudian, ketika aplikasi publisher dijalankan, lima data yang sudah disiapkan akan dikirimkan melalui RabbitMQ. Seluruh data tersebut akan diterima sekaligus oleh aplikasi subscriber dan tampil di terminal dalam satu kali proses.

## Monitoring chart based on publisher
![alt text](img/pub2.jpg)

Lonjakan (spike) pada grafik terjadi setelah saya menjalankan perintah cargo run pada publisher sebanyak 3 kali. Setiap kali publisher dijalankan, ia mengirimkan 5 pesan ke message broker RabbitMQ. Dengan demikian, total pesan yang dikirim mencapai 15. Akibatnya, laju pesan (message rate) meningkat drastis dalam waktu singkat, yang terlihat sebagai spike pada grafik “Message rates” di dashboard RabbitMQ.