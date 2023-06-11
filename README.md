# Tugas 5 Pemrograman Jaringan

Abidjanna Zulfa Hamdika / 5025201197 / Progjar A

Github : <https://github.com/hufahamdika/ProgjarA_Tugas5_2023>

1. **Spesifikasi**
- Komputer

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.001.png)

- Environment

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.002.png)

Environment dijalankan menggunakan wsl dan docker desktop di IPv4 Address 172.16.16.101
**


1. **Implementasikan arsitektur load balancer dengan**

   a. Metode Asynchronus
   
Metode Asynchronus perlu dilakukan beberapa perubahan agar tidak terjadi error saat pembacaan backend port. Perubahan terletak pada penggalan kode berikut

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.003.png)![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.004.png)

Setelah melakukan perubahan tersebut, perlu disesuaikan juga port yang digunakan pada file lb\_async.py dan runserver\_async.py

- lb\_async.py

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.005.png)
- runserver\_async.py

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.006.png)

   b. Metode Server Pool

Berbeda dengan metode Asynchronus, Metode server pool tidak memerlukan perubahan berarti. Akan tetapi tetap perlu dilakukan penyesuain port pada file lb\_process.py dan runserver\_process.py

- lb\_process.

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.008.png)
- runserver\_process.py

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.007.png)

2.  **Buatlah perbandingan kinerja web server**

Perbanding dilakukan dengan menggunakan perintah wrk. Oleh karena itu, wrk perlu di install terlebih dahulu di environment. Instalasi dapat menggunakan perintah **sudo apt-get install wrk**. Perbandingan kemudian dapat dilakukan dengan melakukan testing dengan perintah **wrk -c 1000 -t {concurrency} [http://{IP]() dan Port tempat mesin dijalankan}.** Concurrency menggunakan concurrency 10, 50, 100, 150, dan 200

- Metode Asynchronus

Dalam metode Asynchronus, testing dilakukan dengan cara menjalankan server dengan perintah **python3 async\_server.py**. Perintah wrk kemudian dijalankan pada terminal lain. Berikut adalah hasil dari testing** 


![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.009.png)



- Metode Asynchronus dengan Load Balancer

Testing dilakukan dengan menjalankan perintah **phyton3 lb\_async.py** dan **runserver\_async.sh** di dua terminal yang berbeda. Berikut adalah hasil dari testing

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.010.png)

- Metode Server 

Pada metode ini, testing dilakukan dengan cara menjalankan server dengan perintah **python3 server\_process\_pool\_http.py**. Lalu perintah wrk dijalankan untuk testing pada terminal lain. Berikut adalah hasil dari testin

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.011.png)g


- Metode Server Pool dengan Load 

Testing dilakukan dengan menjalankan perintah **phyton3 lb\_process.py** dan **runserver\_process.sh** di dua terminal yang berbeda. Berikut adalah hasil dari testing

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.012.png)

- Tabel perbandingan dari seluruh metode

<table><tr><th><b>Client</b></th><th><b>Concurrency</b></th><th><b>Failed Requests (Socket Errors)</b></th><th><b>Waiting (Latency)</b></th><th><b>Requests/Sec</b></th></tr>
<tr><td rowspan="5">Asynchronus</td><td>10</td><td>7</td><td>15.91 ms</td><td>557.30</td></tr>
<tr><td>50</td><td>12</td><td>16.61 ms</td><td>559.03</td></tr>
<tr><td>100</td><td>4</td><td>16.65 ms</td><td>591.13</td></tr>
<tr><td>150</td><td>6</td><td>18.22 ms</td><td>582.75</td></tr>
<tr><td>200</td><td>7</td><td>18.46 ms</td><td>581.12</td></tr>
<tr><td rowspan="5">Asynchronus dengan Load Balancing</td><td>10</td><td>104</td><td>91.25 ms</td><td>828.32</td></tr>
<tr><td>50</td><td>89</td><td>83.78 ms</td><td>877.77</td></tr>
<tr><td>100</td><td>112</td><td>93.36 ms</td><td>855.46</td></tr>
<tr><td>150</td><td>86</td><td>91.50 ms</td><td>884.36</td></tr>
<tr><td>200</td><td>127</td><td>119.76 ms</td><td>746.07</td></tr>
<tr><td rowspan="5">Server Pool</td><td>10</td><td>14</td><td>39.60 ms</td><td>299.32</td></tr>
<tr><td>50</td><td>33</td><td>83.85 ms</td><td>187.47</td></tr>
<tr><td>100</td><td>23</td><td>98.91 ms</td><td>142.77</td></tr>
<tr><td>150</td><td>24</td><td>111.22 ms</td><td>123.79</td></tr>
<tr><td>200</td><td>18</td><td>139.92 ms</td><td>111.82</td></tr>
<tr><td rowspan="5">Server Pool dengan Load Balancing</td><td>10</td><td>382</td><td>477.04 ms</td><td>91..02</td></tr>
<tr><td>50</td><td>325</td><td>414.28 ms</td><td>79.11</td></tr>
<tr><td>100</td><td>228</td><td>299.88 ms</td><td>58.29</td></tr>
<tr><td>150</td><td>210</td><td>737.63 ms</td><td>41.88</td></tr>
<tr><td>200</td><td>191</td><td>225.25 ms</td><td>51.19</td></tr>
</table>

- Kesimpulan

Berdasarkan hasil pengamatan, dapat diketahui apabila Load Balancing berdampak secara keseluruhan pada failed requests dan waiting time. Metode yang menggunakan Load Balancing secara keseluruhan memiliki failed request dan waiting time yang secara signifikan lebih banyak daripada metode yang tidak menggunakan Load Balancing. Akan tetapi, efek yang diberikan oleh Load Balancing pada requests/sec berbeda pada metode Asynchronus dan Server Pool. Pada metode Asynchronus, penggunaan Load Balancing membuat jumlah request/sec yang terjadi meningkat dengan cukup signifikan. Sebaliknya, pada metode Server Pool, penggunaan Load Balancing membuat jumlah request/sec menurun dari sebelumnya. 

`	`Secara keseluruhan, dapat disimpulkan apabila penggunaan metode Asynchronus menghasilkan hasil yang lebih baik dimana jumlah failed requests dan waiting time lebih kecil dibandingkan dengan metode Server Pool dan jumlah requests/sec yang dihasilkan lebih besar. Penggunaan Load Balancing juga turut dapat membantu performa metode Asynchronus dimana hasil request/sec yang dihasilkan juga turut bertambah dengan *trade off* jumlah failed requests dan waiting yang turut meningkat juga.
**


1. **Buatlah gambar dari arsitektur percobaan**

- Tanpa Load Balancing

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.013.jpeg)

Tanpa Load Balancing, Client akan langsung mengarah ke Server untuk melakukan requests

- Dengan Load Balancing

![](/Readme%20Images/Aspose.Words.ad9d7a77-b1a0-4b29-b6af-dbc1b92c0197.014.jpeg)

Load Balancer bertugas dan berfungsi untuk mendistribusikan secara merata request ke beberapa server. Ini secara teori membuat kinerja server tidak seberat sebelumnya sehingga dapat mendaptkan hasil yang lebih maksimal. 
