# SOP LRT

[![N|Solid](http://rasioteknologi.com/assets/img/logo/logo-lrt.png)](http://rasioteknologi.com)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](http://rasioteknologi.com)


### Persiapan Tools
  - Text Editor ex: **['visual studio code', 'sublime', 'intelij idea', 'etc']**
  - Browser ex: **['chrome', 'safari', 'firefox', 'etc']**
  - Database manager ex: **['phpmyadmin', 'dbbeaver', 'sqlyog', 'etc']**
  - Version Control Application ex: **['git for windows, mac  or linux']**
  - Postman

### Memulai Project
> Dalam SOP kali ini kita menggunakan framework **Laravel** sebagai contoh
#### 1. Inisialisasi Project 
  - Download dan Install Composer 
  - Install Laravel 
```sh 
  $ composer create-project --prefer-dist laravel/laravel project-name
```
  - Jalankan Project Laravel
```sh 
  $  php artisan serve
```
 - Note : apabila inisialisasi project kita lakukan dengan cara cloning dari git berikut cara menjalakannya
 ```sh 
  $  git clone https://github.com/faisalishak/project-name.git
  $  composer install
  $  cd project-name
  buat file .env dan setting sesuai kebutuhan 
  $  php artisan key:generate
  $  php artisan serve
```

#### 2. Upload Project Menggunakan Version Control (Git)
> apabila repository git telah dibuat lewati point ini, disini kita bisa menggunakan GitHub, Gitlab, Bitbucket DLL.

  - Buat Akun Gitlab atau GitHub dll
  - Login Akun Gitlab atau GitHub dll
  - Buat Repository Private
  - Upload Project, menggunakan terminal arahkan ke root folder project
```sh 
   $ git init 
   $ git add . 
   $ git commit -m "first commit" 
   $ git remote add origin https://github.com/faisalishak/nama-repository.git 
   $ git push -u origin master
```

#### 3. Struktur Project
- Controller dibuat berdasarkan fitur 
- Nama route dibuat berdasarkan fitur
- Nama dan sub folder views dibuat berdasarka fitur
```sh 
ex 1 : 
Controller :
.app/Http/Controller/Admin/BarangController.php
 view :
 .resource/views/admin/barang/index.blade.php
 .resource/views/admin/barang/show.blade.php
 route :
 localhost:8000/admin/barang
 localhost:8000/admin/barang/1
```


#### 3. Naming Format
- Penamaan **variable** menggunakan **chamel style**, ex : **$barang, $totalBarang, $firstName** 
- Penamaan **function/method** menggunakan **chamel style**, ex : **getBarang(), calculate()**
- Penamaan **Response json** menggunakan **underscore style**, ex : **first_name, last_name, address** 
- Penamaan **file views** menggunakan **strip style**, ex : **print-sertifikat.blade.php, profile.blade.php**
- Penamaan **Controller** menggunakan **Capitalize first word**, ex : **BarangController.php, PenjualanBarangController.php, InventoryBarangController.php**
- Penamaan **Midleware** menggunakan **Capitalize first word**, ex : **CorsValidationMiddleware.php**
- Penamaan **route** menggunakan **strip style**, ex : **/admin/barang/print-invoice**
 ```php
 $router->group(['prefix' => 'admin'], function() use ($router){
    $router->group(['prefix' => 'barang'], function() use ($router){
        $router->get('/print-invoice', 'Admin\BarangController@printInvoice');
        $router->get('/', 'Admin\BarangController@index');
        $router->get('/{id}', 'Pos\BarangController@show');
        $router->put('/{id}', 'Pos\BarangController@update');
        $router->delete('/{id}', 'Pos\BarangController@destroy');
    });
});
```

#### 4. Datatable Menggunakan Versi Rest API
> Terkait template source code ini bisa minta ke Saeful Rahman atau Faisal Ishak

#### 5. Constant Variable .ENV
- terkait ini anda dapat menyimpat settingan seperti  **base url, secret string** dan lain"
```
BASE_URL=https://rasioteknologi.com
BASE_URL_API=https://rasioteknologi.com/api/v1/
```
- berikut ini cara untuk mendapatkan value dari variable .env pada file **php**
```php
$company['name'] = $name;
$company['logo'] = env('BASE_URL') . '/images/logo/'. $logo;
return response()->json(company, 200);
```

- berikut ini untuk mendapatkan value dari variable .env pada file **blade**
```html
<script>
//Ajax Function to send a get request
  $.ajax({
    type: "GET",
    url: {{ env('BASE_URL_API') }} + 'barang',
    success: function(response){
        
    }
  });
</script>
```
> Tujuan penggunaan constant variable ENV ini agar lebih mudah ketika devlopment mode atau deployment ke live server.
> Karena tidak usah mengubah banyak url di setiap file cukup mengubah satu file .ENV saja


#### 6. Transaction
- Gunakan transaction di setiap fungsi **tambah, update, delete** data, berikut ini contoh transcation, jangan lupa di-bundle dengan error handling (**try catch**)

```php
public function updateBarang($id, Request $request){
  try{
    DB::beginTransaction();
      
    /**  
     simpan kode update, insert dll disini 
    */
      
    DB::commit();
  }catch(\Exception $e){
    DB::rollback();
        return view('admin.barang.update')->with(['error' => 'Oops, terjadi kesalahan silahkan coba lagi']);
  }
}

public function createBarang($id, Request $request){
  try{
    DB::beginTransaction();
      
    /**  
     simpan kode update, insert dll disini 
    */
      
    DB::commit();
  }catch(\Exception $e){
    DB::rollback();
        return view('admin.barang.create')->with(['error' => 'Oops, terjadi kesalahan silahkan coba lagi']);
  }
} 
```









