# Spring-Boot-Starter (Ringkasan dalam Bahasa Indonesia)

## Intro
Spring Boot memudahkan pengembangan aplikasi dengan menyediakan fitur seperti keamanan, JPA, Spring Data, autentikasi pengguna, dan manajemen role. Tujuannya adalah membantu membuat aplikasi backend yang dapat digunakan sebagai REST API untuk berbagai klien seperti Android, iOS, dan Angular. Firebase juga diintegrasikan untuk autentikasi menggunakan token Google.

## Starter yang Digunakan
Beberapa Spring Boot starter yang digunakan:
- `spring-boot-starter-web`
- `spring-boot-starter-data-jpa`
- `spring-boot-starter-security`
- `spring-boot-starter-actuator`
- `spring-boot-devtools`

Library tambahan:
- `mysql-connector-java`
- `hsqldb`
- `org.modelmapper.modelmapper`

## Web
Contoh resource `TestResource` dibuat untuk menunjukkan:
- Penggunaan `@RestController`
- Injeksi service
- Pemetaan metode ke URL
- Injeksi properti konfigurasi
- Penentuan status HTTP

Exception handler dengan `@ControllerAdvice` digunakan untuk menangani exception dengan respons kustom. ModelMapper digunakan untuk mengonversi objek seperti `TestEntity` ke `TestJson`.

## JPA
JPA digunakan untuk persistensi data dengan `JpaRepository`. Contoh entitas `TestEntity` dibuat dengan ID yang di-generate otomatis. Repositori dibuat dengan mudah:
```java
public interface TestRepository extends CrudRepository<TestEntity, Long> {
    Collection<TestEntity> findAll();
}
```
Repositori ini dapat diinjeksikan ke dalam service.

## Spring Security
Spring Security digunakan untuk mengamankan data. Terdapat tiga role:
- Admin
- User
- Anonymous

API dibagi menjadi tiga bagian:
- `/api/open` untuk anonymous
- `/api/client` untuk user
- `/api/admin` untuk admin

Autentikasi dilakukan terhadap database dengan bantuan `UserService`.

## Spring Actuator
Actuator memungkinkan administrator memantau status aplikasi melalui endpoint seperti `/health`, `/metrics`, dan `/info`. Contoh custom health indicator `PomodoroHealthIndicator` juga disediakan.

## Devtools
Devtools memudahkan pengembangan dengan fitur seperti restart otomatis saat perubahan kode.

## Profiles
Dua profile disediakan:
- `prod` untuk produksi (menggunakan MySQL)
- `dev` untuk pengembangan (menggunakan database embedded)

Profile diaktifkan melalui `application.properties`.

## Swagger 2
Swagger 2 diaktifkan hanya pada profile `dev` untuk dokumentasi API. UI Swagger dapat diakses di `http://localhost:8080/swagger-ui.html`.

## Integrasi Firebase
Firebase diintegrasikan untuk autentikasi klien. Filter `FirebaseFilter` memeriksa header `X-Authorization-Firebase` dan memvalidasi token menggunakan `FirebaseService`. Autentikasi kemudian diproses oleh `FirebaseAuthenticationProvider`.

### Konfigurasi Firebase
Firebase diinisialisasi dengan mengunduh file konfigurasi JSON dari Firebase Console dan menyimpannya di `configPath`.

## TODO
- Menambahkan unit test

Dengan konfigurasi ini, aplikasi Spring Boot siap digunakan sebagai backend untuk berbagai klien dengan dukungan autentikasi Firebase dan keamanan yang terintegrasi.