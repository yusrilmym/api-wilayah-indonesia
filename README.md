API Data Wilayah Indonesia
==========================

Repository ini berisi source code untuk generate (REST) API statis berisi data wilayah Indonesia
serta perintah untuk mendeploynya ke _static hosting_ [Github Page](https://pages.github.com/).

Demo: [https://yusrilmym.github.io/api-wilayah-indonesia](https://yusrilmym.github.io/api-wilayah-indonesia/)

#### Apa yang dimaksud API statis? 

API statis adalah API yang _endpoint_-nya terdiri dari file statis.

#### Keuntungan API statis?

* Dapat dihosting pada _static file hosting_ seperti Github Page, Netlify, dsb.
* Proses lebih cepat karena tidak membutuhkan server-side scripting.

#### Bagaimana cara kerjanya?

* Daftar provinsi, kab/kota, kecamatan, kelurahan/desa disimpan pada folder `data` berupa file `csv` (agar mudah diedit).
* Kemudian script `generate.php` dijalankan. Script ini akan membaca file `csv` didalam folder `data`, kemudian men-generate ribuan endpoint (file) kedalam folder `static/api`.
* API siap 'dihidangkan'.

#### Saya mau hosting di Github saya sendiri, bagaimana caranya?

* Klik fork di pojok kanan atas.
* Pada halaman forking, **HAPUS CENTANG** "Copy the master branch only".
* Klik "Create Fork".
* Setelah selesai di Fork, klik Settings (bukan setting account, tapi setting repository).
* Klik menu "Pages" untuk masuk ke menu pengaturan GitHub Pages.
* Pada menu pengaturan GitHub Pages:
  * Pilih Source: Deploy from a Branch
  * Branch: `gh-pages`
  * Direktori: `/root`
  * Klik Save
* Tunggu beberapa menit (5-10 menitan), kembali ke halaman home repository (https://github.com/usernamekamu/api-wilayah-indonesia).
* Kalau halaman sudah terdeploy, di bagian kanan halaman, akan muncul informasi "Environments". Kalau belum tunggu lagi beberapa menit, lalu refresh.
* Kalau sudah muncul informasi Environmentsnya, klik bagian "🚀 github-pages".
* Di halaman Deployments, klik "View Deployment" untuk melihat halaman yang berhasil terdeploy.

## ENDPOINTS

#### 1. Mengambil Daftar Provinsi

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/provinces.json
```

Contoh Response:

```
[
    {
        "id": "32",
        "name": "JAWA BARAT"
    },
    {
        "id": "33",
        "name": "JAWA TENGAH"
    },
  ...
]
```

#### 2. Mengambil Daftar Kab/Kota pada Provinsi Tertentu

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/regencies/{provinceId}.json
```

Contoh untuk mengambil daftar kab/kota di provinsi Jawa Barat (ID = 32):

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/regencies/32.json
```

Contoh Response:

```
[
    {
        "id": "3212",
        "province_id": "32",
        "name": "KABUPATEN INDRAMAYU"
    },
    {
        "id": "3213",
        "province_id": "32",
        "name": "KABUPATEN SUBANG"
    },
  ...
]
```

#### 3. Mengambil Daftar Kecamatan pada Kab/Kota Tertentu

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/districts/{regencyId}.json
```

Contoh untuk mengambil daftar kecamatan di Kabupaten Indramayu (ID = 3212):

```
https://yusrilmym.github.io/api-wilayah-indonesia/api/districts/3212.json
```

Contoh Response:

```
[
    {
        "id": "3212220",
        "regency_id": "3212",
        "name": "SUKRA"
    },
    {
        "id": "3212221",
        "regency_id": "3212",
        "name": "PATROL"
    }
  ...
]
```

#### 4. Mengambil Daftar Kelurahan pada Kecamatan Tertentu

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/villages/{districtId}.json
```

Contoh untuk mengambil daftar kelurahan di Patrol (ID = 3212221):

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/villages/3212221.json
```

Contoh Response:

```
[
    {
        "id": "3212221007",
        "district_id": "3212221",
        "name": "PATROL BARU"
    },
    {
        "id": "3212221008",
        "district_id": "3212221",
        "name": "MEKARSARI"
    }
  ...
]
```

#### 5. Mengambil Data Provinsi berdasarkan ID Provinsi

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/province/{provinceId}.json
```

Contoh untuk mengambil data provinsi Aceh (ID = 11):

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/province/11.json
```

Contoh Response:

```
{
  "id": "11",
  "name": "ACEH"
}
```

#### 6. Mengambil Data Kab/Kota berdasarkan ID Kab/Kota

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/regency/{regencyId}.json
```

Contoh untuk mengambil data kabupaten Aceh Selatan (ID = 1103):

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/regency/1103.json
```

Contoh Response:

```
{
  "id": "1103",
  "province_id": "11",
  "name": "KABUPATEN ACEH SELATAN"
}
```

#### 7. Mengambil Data Kecamatan berdasarkan ID Kecamatan

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/district/{districtId}.json
```

Contoh untuk mengambil data kecamatan Trumon Timur (ID = 1103011):

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/district/1103011.json
```

Contoh Response:

```
{
  "id": "1103011",
  "regency_id": "1103",
  "name": "TRUMON TIMUR"
}
```

#### 8. Mengambil Data Kelurahan berdasarkan ID Kelurahan

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/village/{villageId}.json
```

Contoh untuk mengambil data kelurahan Jambo Dalem (ID = 1103011010):

```
GET https://yusrilmym.github.io/api-wilayah-indonesia/api/village/1103011010.json
```

Contoh Response:

```
{
  "id": "1103011010",
  "district_id": "1103011",
  "name": "JAMBO DALEM"
}
```

## LIMITASI

Karena API ini dihosting di Github Page, Github Page sendiri memberikan batasan bandwith 100GB/bulan. Rata-rata endpoint disini memiliki ukuran 1KB/endpoint, jadi kurang lebih request yang dapat digunakan adalah 100.000.000 request per bulan, atau sekitar 3.000.000 request/hari.

Karena limitasi ini, disarankan untuk hosting API ini di github kamu sendiri.

Untuk lebih detail tentang limitasi Github Page, bisa dilihat [disini](https://help.github.com/en/articles/about-github-pages#usage-limits).
