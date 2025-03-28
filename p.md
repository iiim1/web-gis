1. **Konsep Dasar OOP**:
   - OOP berfokus pada objek yang merupakan kombinasi data (atribut) dan fungsi (metode)
   - Empat pilar OOP: Enkapsulasi, Inheritance, Polimorfisme, Abstraksi
   - Perbedaan pemrograman prosedural vs OOP

2. **Class dan Object**:
   - Class adalah blueprint, objek adalah instance dari class
   - Atribut menyimpan data, metode menentukan perilaku
   - Contoh: Class `Mobil` dengan atribut `merek`, `model` dan metode `percepat()`, `rem()`

3. **Access Modifiers**:
   - `public`: dapat diakses dari mana saja
   - `private`: hanya dalam class yang sama
   - `protected`: dalam package yang sama dan subclass
   - Default (no modifier): dalam package yang sama

4. **Inheritance**:
   - Subclass mewarisi atribut dan metode dari superclass
   - Keyword `extends`
   - Method overriding menggunakan `@Override`
   - Keyword `super` untuk mengakses superclass

5. **Polimorfisme**:
   - Kemampuan objek merespons metode yang sama dengan cara berbeda
   - Compile-time (overloading) vs runtime (overriding) polymorphism

6. **Abstraksi**:
   - Menyembunyikan detail implementasi
   - Menggunakan abstract class dan interface

7. **Konstruktor**:
   - Metode khusus untuk inisialisasi objek
   - Default constructor, parameterized constructor, copy constructor
   - Constructor overloading dan chaining

8. **Garbage Collection**:
   - Proses otomatis penghapusan objek tidak terpakai
   - Metode `finalize()` (tidak direkomendasikan)
   - Resource management modern dengan `try-with-resources`

### Jawaban Latihan Soal:

1. **Apa itu inheritance dan manfaatnya?**
   - Inheritance adalah mekanisme dimana subclass mewarisi atribut dan metode dari superclass
   - Manfaat: code reuse, ekstensi mudah, struktur hierarkis, pemeliharaan lebih mudah

2. **Perbedaan method overriding dan overloading**
   - Overriding:
     - Dilakukan di subclass
     - Nama, parameter, dan return type sama dengan superclass
     - Runtime polymorphism
   - Overloading:
     - Dilakukan dalam class yang sama
     - Nama sama, parameter berbeda
     - Compile-time polymorphism

3. **Mengapa Java tidak mendukung multiple inheritance untuk class?**
   - Untuk menghindari "diamond problem" (ambiguity saat subclass mewarisi method dengan nama sama dari multiple superclass)
   - Sebagai gantinya, Java menyediakan interface untuk multiple inheritance

4. **Hierarki kelas untuk sistem perpustakaan**
   ```java
   class Item {
       private String id;
       private String judul;
   }
   
   class Buku extends Item {
       private String pengarang;
   }
   
   class Majalah extends Item {
       private int edisi;
   }
   
   class DVD extends Item {
       private int durasi;
   }
   ```

5. **Apa yang terjadi jika subclass punya method dengan nama sama tapi parameter berbeda?**
   - Ini disebut method overloading (bukan overriding)
   - Subclass akan memiliki kedua method (dari superclass dan method baru)
   - Tidak ada hubungan khusus antara kedua method tersebut

6. **Kegunaan keyword `super`**
   - Memanggil constructor superclass: `super(parameters)`
   - Mengakses method superclass yang di-override: `super.methodName()`
   - Mengakses atribut superclass: `super.attributeName`

7. **Output kode inheritance**
   ```
   B
   C
   ```
   - Karena terjadi runtime polymorphism (method overriding)

8. **Implementasi class `Circle`**
   ```java
   public class Circle {
       private double radius;
       
       public Circle() {
           this(1.0);
       }
       
       public Circle(double radius) {
           this.radius = radius;
       }
       
       public Circle(Circle other) {
           this(other.radius);
       }
       
       public double getArea() {
           return Math.PI * radius * radius;
       }
       
       public double getCircumference() {
           return 2 * Math.PI * radius;
       }
   }
   ```

9. **Masalah pada kode constructor**
   - Problem: constructor `Parent` memanggil method `initialize()` yang bisa di-override
   - Risiko: jika subclass meng-override `initialize()` tanpa memanggil `super.initialize()`, atribut `value` di superclass tidak akan diinisialisasi
   - Solusi: hindari memanggil method yang bisa di-override dari constructor

10. **Resource management untuk koneksi database/file**
    - Implementasikan interface `AutoCloseable` atau `Closeable`
    - Gunakan `try-with-resources` untuk pembersihan otomatis
    - Contoh:
    ```java
    public class DatabaseConnection implements AutoCloseable {
        // implementasi koneksi
        
        @Override
        public void close() throws Exception {
            // tutup koneksi
        }
    }
    
    // Penggunaan
    try (DatabaseConnection conn = new DatabaseConnection()) {
        // gunakan koneksi
    }
    ```

### **Latihan Soal Access Modifier & Non-Access Modifier**

#### **1. Jelaskan perbedaan antara enkapsulasi dan information hiding!**
- **Enkapsulasi**:  
  Membungkus data (atribut) dan metode yang mengoperasikannya dalam satu unit (class).  
  Contoh: Class `RekeningBank` dengan atribut `saldo` dan metode `setor()`, `tarik()`.

- **Information Hiding**:  
  Menyembunyikan detail implementasi internal, hanya mengekspos antarmuka yang diperlukan.  
  Contoh: Atribut `saldo` dibuat `private`, sehingga hanya bisa diakses via `getSaldo()`.

#### **2. Perbedaan `protected` dan `default` access level**
| **`protected`** | **`default` (no modifier)** |
|----------------|----------------|
| Dapat diakses oleh subclass meskipun beda package | Hanya diakses dalam package yang sama |
| Cocok untuk atribut/metode yang perlu diwariskan | Cocok untuk komponen internal package |

**Contoh Penggunaan:**
```java
// Superclass di package 'kendaraan'
public class Kendaraan {
    protected int kecepatan;  // Bisa diakses subclass di package lain
    String merk;             // Hanya bisa diakses dalam package 'kendaraan'
}
```

#### **3. Situasi menggunakan `private` untuk method**
- Untuk helper methods yang hanya digunakan internal class.  
  Contoh:
  ```java
  private boolean isValid(String input) {
      return input != null && !input.trim().isEmpty();
  }
  ```
- Untuk mencegah subclass meng-override method penting.

#### **4. Perbedaan `static final` vs `final`**
| **`static final`** | **`final`** |
|-------------------|------------|
| Konstanta global (nilai sama untuk semua instance) | Konstanta per-instance (nilai bisa beda tiap objek) |
| Contoh: `Math.PI` | Contoh: `final String nomorSeri` di class `Produk` |

**Implementasi:**
```java
class Mobil {
    static final int RODA = 4;  // Nilai sama untuk semua mobil
    final String noPlat;        // Beda tiap mobil, tapi tidak bisa diubah setelah inisialisasi
}
```

#### **5. Masalah access modifier pada kode `Mahasiswa` dan `SistemAkademik`**
```java
// Masalah:
Mahasiswa mhs = new Mahasiswa();       // Error: Class Mahasiswa tidak public (tidak bisa diakses dari package lain)
mhs.setNim("12345");                   // Error: Method setNim() tidak terlihat (karena Mahasiswa tidak bisa diinstansiasi)
mhs.nama = "Budi";                     // Error: Atribut nama memiliki default access (tidak terlihat di package berbeda)
mhs.usia = 20;                         // Error: Atribut usia protected (hanya bisa diakses subclass atau package yang sama)
mhs.jurusan = "Informatika";           // Valid: Atribut jurusan public
```

#### **6. Mengapa utility methods sering dibuat `static`?**
- **Alasan**:  
  - Tidak tergantung state objek (contoh: `Math.sqrt()`).  
  - Tidak perlu instansiasi class.  
- **Contoh method yang tidak sebaiknya `static`**:  
  Method yang memerlukan akses ke atribut instance, seperti `getNama()` di class `Mahasiswa`.

#### **7. Implementasi class `BankAccount` dengan 4 access level**
```java
public class BankAccount {
    public String nomorRekening;  // Public: Bisa diakses siapa saja
    protected double saldo;       // Protected: Bisa diakses subclass
    String pemilik;               // Default: Hanya dalam package
    private String pin;           // Private: Hanya dalam class ini

    // Constructor
    public BankAccount(String nomor, String pemilik, String pin) {
        this.nomorRekening = nomor;
        this.pemilik = pemilik;
        this.pin = pin;
        this.saldo = 0;
    }

    // Public method untuk akses terkontrol ke saldo
    public double getSaldo() {
        return saldo;
    }

    // Private method untuk validasi
    private boolean validatePin(String inputPin) {
        return this.pin.equals(inputPin);
    }
}
```

#### **8. Penggunaan `synchronized` dan dampaknya**
- **Kapan digunakan**:  
  Saat multiple thread mengakses resource bersama (contoh: variabel counter).  
- **Dampak kinerja**:  
  Memperlambat eksekusi karena thread harus menunggu akses ke resource yang dikunci.

---

### **Latihan Soal Constructor & Garbage Collection**

#### **1. Perbedaan default constructor vs parameterized constructor**
- **Default constructor**:  
  - Tidak punya parameter.  
  - Dibuat otomatis oleh Java jika tidak ada constructor lain.  
  - Contoh: `public Mahasiswa() { }`  

- **Parameterized constructor**:  
  - Menerima parameter untuk inisialisasi objek.  
  - Contoh: `public Mahasiswa(String nama, String nim) { ... }`  

**Penggunaan**:  
- Default constructor: Ketika objek bisa dibuat dengan nilai default.  
- Parameterized constructor: Ketika objek harus diinisialisasi dengan nilai spesifik.

#### **2. Jika tidak ada default constructor**
- Java tidak akan membuat default constructor secara otomatis jika ada constructor lain.  
- Contoh:
  ```java
  class Buku {
      Buku(String judul) { ... }  // Hanya ada constructor berparameter
  }
  
  Buku buku = new Buku();  // Error: Tidak ada default constructor
  ```

#### **3. Constructor chaining**
- **Konsep**:  
  Satu constructor memanggil constructor lain dalam class yang sama (`this()`) atau superclass (`super()`).  
- **Contoh**:
  ```java
  class Pegawai {
      Pegawai() {
          this("John Doe");  // Memanggil constructor lain
      }
      Pegawai(String nama) {
          this(nama, 25);
      }
  }
  ```

#### **4. Perbedaan `this()` dan `super()`**
| **`this()`** | **`super()`** |
|-------------|-------------|
| Memanggil constructor lain dalam class yang sama | Memanggil constructor superclass |
| Harus jadi statement pertama dalam constructor | Harus jadi statement pertama dalam constructor |

#### **5. Java tidak punya destruktor seperti C++**
- **Alasan**:  
  Java menggunakan **Garbage Collector** untuk menghapus objek secara otomatis.  
- **Cara kerja**:  
  Objek dihapus ketika tidak ada referensi yang menunjuk ke objek tersebut.

#### **6. Limitasi `finalize()`**
1. Tidak dijamin kapan akan dieksekusi.  
2. Bisa memperlambat garbage collection.  
3. Tidak bisa mengandalkannya untuk pembersihan resource kritis (seperti file/database).  
4. **Alternatif**: Gunakan `try-with-resources` atau implementasi `AutoCloseable`.

#### **7. Cara kerja `try-with-resources`**
- **Mekanisme**:  
  Resource yang mengimplementasi `AutoCloseable` akan otomatis ditutup setelah blok `try`.  
- **Keuntungan vs `try-catch-finally`**:  
  Lebih ringkas dan mencegah lupa menutup resource di blok `finally`.

#### **9. Masalah pada kode constructor yang memanggil method overrideable**
```java
class Parent {
    Parent() {
        initialize();  // Berbahaya jika di-override
    }
    void initialize() { ... }
}

class Child extends Parent {
    @Override
    void initialize() {
        // Subclass mungkin belum sepenuhnya diinisialisasi
    }
}
```
**Masalah**:  
Jika `Child` meng-override `initialize()`, constructor `Parent` akan memanggil versi `Child` sebelum `Child` sepenuhnya terbentuk.

#### **10. Resource management untuk koneksi database/file**
```java
public class DatabaseConnection implements AutoCloseable {
    private Connection conn;

    public DatabaseConnection(String url) throws SQLException {
        this.conn = DriverManager.getConnection(url);
    }

    @Override
    public void close() throws SQLException {
        if (conn != null) {
            conn.close();
        }
    }
}

// Penggunaan:
try (DatabaseConnection db = new DatabaseConnection("jdbc:mysql://localhost:3306/mydb")) {
    // Gunakan koneksi
}  // Koneksi otomatis ditutup di sini
```

---

### **Tambahan Best Practices**
1. **Gunakan builder pattern** untuk constructor dengan banyak parameter.  
2. **Hindari "telescoping constructor"** (constructor dengan banyak overload).  
3. **Selalu tutup resource** dengan `try-with-resources`.  
4. **Jangan gunakan `finalize()`** untuk pembersihan resource penting.

Berikut rangkuman poin-poin penting dan jawaban latihan soal berdasarkan materi yang diberikan:

### Rangkuman Poin Penting:

1. **Konstruktor**:
   - Metode khusus untuk inisialisasi objek
   - Nama sama dengan class, tidak memiliki return type
   - Jenis: default, parameterized, copy constructor
   - Constructor overloading dan constructor chaining (`this()`)

2. **Destruktor**:
   - Java menggunakan Garbage Collection (tidak ada destruktor eksplisit)
   - Metode `finalize()` (deprecated sejak Java 9)
   - Alternatif modern: `AutoCloseable` dan try-with-resources

3. **Getter dan Setter**:
   - Prinsip enkapsulasi (data hiding)
   - Konvensi JavaBeans (`getX()`, `setX()`, `isX()` untuk boolean)
   - Validasi data dalam setter
   - Defensive copying untuk tipe mutable

4. **Kata Kunci `this`**:
   - Referensi ke instance saat ini
   - Mengatasi variable shadowing
   - Constructor chaining (`this()`)
   - Method chaining (return `this`)

5. **Kata Kunci `super`**:
   - Referensi ke superclass
   - Mengakses anggota superclass yang di-shadow/override
   - Memanggil konstruktor superclass (`super()`)

### Jawaban Latihan Soal:

**1. Perbedaan default dan parameterized constructor:**
- Default constructor: tanpa parameter, dibuat otomatis jika tidak ada konstruktor lain
- Parameterized constructor: memiliki parameter untuk inisialisasi spesifik
- Default digunakan ketika ingin inisialisasi dengan nilai default, parameterized untuk inisialisasi spesifik

**2. Jika tidak ada default constructor:**
- Jika hanya ada parameterized constructor, default constructor tidak otomatis dibuat
- Harus dibuat manual jika masih diperlukan

**3. Constructor chaining:**
- Teknik memanggil konstruktor lain dalam class yang sama
- Implementasi: menggunakan `this(parameters)`
```java
public class Contoh {
    public Contoh() {
        this(0); // Memanggil constructor lain
    }
    public Contoh(int x) {
        // inisialisasi
    }
}
```

**4. Perbedaan `this()` dan `super()`:**
- `this()`: memanggil konstruktor lain dalam class yang sama
- `super()`: memanggil konstruktor superclass
- Keduanya harus statement pertama dalam konstruktor

**5. Java tidak memiliki destruktor seperti C++:**
- Java menggunakan Garbage Collection otomatis
- Tidak perlu manajemen memori manual
- Lebih aman dari memory leaks (tapi tidak deterministik)

**6. Limitasi `finalize()`:**
- Tidak dijamin dipanggil
- Performa buruk
- Tidak bisa diprediksi waktu eksekusinya
- Alternatif: implement `AutoCloseable` dan try-with-resources

**7. Try-with-resources:**
- Mekanisme: secara otomatis memanggil `close()` setelah blok try
- Keuntungan:
  - Lebih ringkas
  - Jaminan resources dibersihkan
  - Lebih mudah dibaca
```java
try (Resource res = new Resource()) {
    // gunakan resource
} // res.close() otomatis dipanggil
```

**8. Implementasi class `Circle`:**
```java
public class Circle {
    private double radius;
    
    // Default constructor
    public Circle() {
        this(1.0);
    }
    
    // Parameterized constructor
    public Circle(double radius) {
        this.radius = radius;
    }
    
    // Copy constructor
    public Circle(Circle other) {
        this(other.radius);
    }
    
    public double getArea() {
        return Math.PI * radius * radius;
    }
    
    public double getCircumference() {
        return 2 * Math.PI * radius;
    }
}
```

**9. Masalah pada kode Parent-Child:**
- Masalah: konstruktor Parent memanggil method yang di-override
- Saat Child diinstansiasi, `initialize()` Child dipanggil sebelum konstruktor Child selesai
- Solusi: jangan panggil method yang bisa di-override dari konstruktor

**10. Resource management untuk koneksi database:**
- Implement `AutoCloseable`
- Gunakan try-with-resources
- Contoh:
```java
public class DatabaseConnection implements AutoCloseable {
    // implementasi koneksi
    
    @Override
    public void close() throws Exception {
        // bersihkan resource
    }
}

// Penggunaan
try (DatabaseConnection conn = new DatabaseConnection()) {
    // gunakan koneksi
} // otomatis close()
```

**Tambahan untuk materi getter/setter:**

**1. Enkapsulasi dengan getter/setter:**
- Penyembunyian implementasi internal
- Kontrol akses ke data
- Validasi data melalui setter
- Fleksibilitas mengubah implementasi

**2. `getX()` vs `isX()`:**
- `getX()`: konvensi umum untuk getter
- `isX()`: khusus untuk tipe boolean
- Gunakan `isX()` untuk boolean untuk konsistensi

**3. Defensive copying:**
- Penting untuk mencegah modifikasi tidak sah pada objek mutable
- Contoh masalah tanpa defensive copy:
```java
private Date birthDate;

public Date getBirthDate() {
    return birthDate; // Client bisa modifikasi Date
}

// Solusi:
public Date getBirthDate() {
    return new Date(birthDate.getTime());
}
```

**4. Implementasi `RekeningBank`:**
```java
public class RekeningBank {
    private String nomorRekening;
    private double saldo;
    
    public void deposit(double amount) {
        if (amount <= 0) throw new IllegalArgumentException();
        saldo += amount;
    }
    
    public void withdraw(double amount) {
        if (amount <= 0) throw new IllegalArgumentException();
        if (amount > saldo) throw new IllegalStateException();
        saldo -= amount;
    }
}
```

**5. Immutable objects:**
- Keuntungan: thread-safe, aman di-share, tidak perlu defensive copy
- Kerugian: perlu buat objek baru untuk setiap perubahan
- Contoh: String, wrapper classes (Integer, Double)

**6. Masalah pada class Student:**
- Tidak ada defensive copying untuk array grades dan Date
- Bisa dimodifikasi dari luar
- Solusi:
```java
public int[] getGrades() {
    return Arrays.copyOf(grades, grades.length);
}

public Date getBirthDate() {
    return birthDate != null ? new Date(birthDate.getTime()) : null;
}
```

**7. Lazy initialization:**
- Menunda inisialisasi sampai benar-benar dibutuhkan
- Contoh:
```java
private List<Data> data;
public List<Data> getData() {
    if (data == null) {
        data = loadData(); // mahal
    }
    return data;
}
```

**8. Read-only dan write-only:**
- Read-only: hanya getter (contoh: ID, tanggal dibuat)
- Write-only: hanya setter (contoh: password)
```java
// Read-only
public String getId() {
    return id;
}

// Write-only
public void setPassword(String pass) {
    this.password = hash(pass);
}
```

**9. Validasi email dalam setter:**
```java
public void setEmail(String email) {
    if (email == null || !email.matches(".+@.+\\..+")) {
        throw new IllegalArgumentException("Email tidak valid");
    }
    this.email = email;
}
```

**10. Perbandingan pendekatan:**
- JavaBeans:
  - Keuntungan: standar, didukung banyak framework
  - Kerugian: verbose
- Fluent Interface:
  - Keuntungan: lebih ringkas, bisa chaining
  - Kerugian: tidak standar
- Builder Pattern:
  - Keuntungan: baik untuk objek kompleks
  - Kerugian: lebih banyak kode

**1. Polimorfisme:**
- Kemampuan objek untuk menampilkan banyak bentuk
- Dua jenis:
  - Compile-time (static binding): Method overloading
  - Runtime (dynamic binding): Method overriding
- Memungkinkan fleksibilitas dan ekstensibilitas kode
- Contoh: `Animal a = new Dog(); a.makeSound()`

**2. Interface:**
- Kontrak yang hanya berisi deklarasi method (Java 8+ punya default/static methods)
- Semua method secara default public abstract
- Fields selalu public static final
- Kelas bisa implement banyak interface
- Digunakan untuk:
  - Multiple inheritance
  - Loose coupling
  - Mendefinisikan kemampuan tanpa implementasi

**3. Abstract Class:**
- Kelas yang tidak bisa diinstantiasi
- Bisa berisi abstract dan concrete methods
- Bisa memiliki konstruktor
- Single inheritance
- Digunakan untuk:
  - Template method pattern
  - Berbagi kode antar subclass
  - Mengelola state bersama

**4. Perbedaan Penting:**
- Interface: what (kontrak), Abstract Class: how (implementasi parsial)
- Interface untuk kemampuan, Abstract Class untuk hubungan is-a
- Java 8+ interface bisa punya implementasi (default methods)

### Jawaban Latihan Soal:

**Polimorfisme:**
1. Polimorfisme adalah kemampuan objek untuk menampilkan banyak bentuk. Contoh: seorang guru yang juga orang tua, tombol power yang fungsinya berbeda tergangkat perangkat.

2. Compile-time polymorphism terjadi saat kompilasi (method overloading), runtime polymorphism terjadi saat eksekusi (method overriding). Overloading: nama method sama, parameter beda. Overriding: subclass mengimplementasikan ulang method parent.

3. Contoh valid overloading:
```java
void print(int x) {}
void print(String s) {}
```
Tidak valid:
```java
int calculate() {}
double calculate() {} // Return type tidak cukup
```

4. Aturan overriding:
- Nama dan parameter sama
- Return type covariant
- Tidak lebih restriktif access modifier
- Tidak throw broader checked exception
Contoh:
```java
class Parent { void show() {} }
class Child extends Parent { @Override void show() {} }
```

5. Upcasting: konversi subclass ke superclass (otomatis). Downcasting: superclass ke subclass (perlu cast). Downcasting diperlukan saat ingin mengakses method khusus subclass.

6. `instanceof` memeriksa tipe objek sebelum downcasting:
```java
if (animal instanceof Dog) {
    Dog d = (Dog) animal;
}
```

8. Manfaat polimorfisme:
- Fleksibilitas (tambah subclass tanpa ubah kode)
- Reusability (gunakan ulang kode)
- Loose coupling (kurangi ketergantungan)
Contoh: sistem pembayaran dengan berbagai metode.

**Interface:**
1. Abstract class bisa punya implementasi dan state, interface tidak (sebelum Java 8). Abstract class untuk template, interface untuk kontrak.

2. Multiple interface implementation contoh: Smartphone bisa Chargeable dan Callable.

3. Default methods di Java 8 memungkinkan menambah method ke interface tanpa merusak kelas implementasi. Keuntungan: evolusi API lebih mudah.

4. Contoh polimorfisme dengan interface:
```java
List<String> list = new ArrayList<>();
list = new LinkedList<>(); // Polimorfisme
```

5. Functional interface punya 1 abstract method, digunakan untuk lambda:
```java
@FunctionalInterface
interface Runner { void run(); }
Runner r = () -> System.out.println("Running");
```

7. Diamond problem diatasi dengan harus mengoverride method yang ambigu:
```java
interface A { default void show() {} }
interface B { default void show() {} }
class C implements A, B {
    @Override public void show() { A.super.show(); }
}
```

9. Object class adalah root class semua kelas di Java. Interface bukan kelas, tapi kontrak yang bisa diimplementasikan kelas.

**Abstract Class:**
1. Abstract class punya implementasi parsial, interface tidak. Pilih abstract class ketika butuh berbagi kode atau state.

2. Abstract method:
- Tidak punya body
- Harus diimplementasikan subclass
- Deklarasi: `abstract void method();`

3. Tidak bisa, karena abstract class tidak lengkap (ada method tanpa implementasi).

4. Konstruktor abstract class untuk inisialisasi state yang dibutuhkan subclass, dipanggil saat instantiasi subclass.

5. Template Method Pattern mendefinisikan skeleton algoritma di superclass, biarkan subclass implementasi langkah spesifik. Contoh:
```java
abstract class Game {
    abstract void initialize();
    abstract void start();
    // Template method
    final void play() {
        initialize();
        start();
    }
}
```

7. Subclass harus implement semua abstract methods kecuali subclass itu sendiri abstract.

8. Hirarki abstract class contoh:
```java
abstract class Animal {}
abstract class Mammal extends Animal {}
class Dog extends Mammal {}
```
Berguna untuk hierarki kompleks dengan shared code.

9. Ya, abstract class bisa implement interface:
```java
interface Drawable {}
abstract class Shape implements Drawable {}

Berikut rangkuman poin-poin penting dari materi Anonymous Class dan Lambda Expression beserta jawaban untuk latihan soal (kecuali yang meminta kode):

### Rangkuman Anonymous Class:
1. **Definisi**: Class tanpa nama yang didefinisikan & diinstansiasi sekaligus
2. **Karakteristik**:
   - Tidak punya nama
   - Single-use (tidak reusable)
   - Dapat extend class/implement interface
   - Tidak bisa punya constructor eksplisit
3. **Penggunaan**:
   - Event handling
   - Callback functions
   - Strategy pattern
   - Thread implementation
4. **Keterbatasan**:
   - Tidak bisa akses non-final variable lokal
   - Tidak support static members
   - Scope `this` mengacu ke anonymous class itu sendiri

### Rangkuman Lambda Expression:
1. **Definisi**: Ekspresi fungsi anonymous yang ringkas
2. **Syarat**: Hanya untuk functional interface (1 abstract method)
3. **Sintaks**:
   - `(params) -> expression`
   - `(params) -> { statements; }`
4. **Keunggulan**:
   - Kode lebih ringkas
   - Mendukung pemrograman fungsional
   - Integrasi dengan Stream API
5. **Method Reference**:
   - `Class::staticMethod`
   - `object::instanceMethod`
   - `Class::instanceMethod`
   - `Class::new` (constructor)

### Perbedaan Anonymous Class vs Lambda:
1. **Sintaks**: Lambda lebih ringkas
2. **Scope `this`**: Lambda mengacu ke enclosing class
3. **Target**: Lambda hanya untuk functional interface
4. **State**: Lambda tidak bisa punya state/fields

### Jawaban Latihan Soal:

1. **Anonymous Class**:
   - Class tanpa nama yang dibuat & diinstansiasi sekaligus
   - Karakteristik: single-use, extend/implement, no constructor, akses final var lokal

2. **Perbedaan**:
   - Anonymous: multi-method, punya state, `this` sendiri
   - Class biasa: reusable, punya nama, constructor
   - Contoh: Anonymous untuk event handler sekali pakai, class biasa untuk logika kompleks/reusable

3. **Implementasi Interface**:
   ```java
   new Interface() {
       @Override
       public void method() {
           // implementasi
       }
   };
   ```

4. **Constructor Anonymous Class**:
   - Tidak bisa punya constructor eksplisit
   - Inisialisasi pakai instance initializer block `{ ... }`

5. **Keterbatasan**:
   - Tidak bisa reusable (karena tanpa nama)
   - Tidak bisa punya static members
   - Tidak bisa extend & implement sekaligus
   - Alasan: didesain untuk implementasi sederhana sekali pakai

6. **Lambda vs Anonymous**:
   - Lambda: hanya functional interface, lebih ringkas, `this` ke enclosing
   - Anonymous: bisa multi-method, punya state
   - Gunakan lambda untuk functional interface sederhana, anonymous untuk kompleks

7. **Comparator<Student>**:
   ```java
   new Comparator<Student>() {
       @Override
       public int compare(Student s1, Student s2) {
           return Double.compare(s1.getGrade(), s2.getGrade());
       }
   };
   ```

8. **Effectively Final**:
   - Variabel lokal yang tidak diubah setelah inisialisasi
   - Bisa diakses lambda meski tidak dideklarasi final

9. **Anonymous Thread**:
   ```java
   new Thread() {
       @Override
       public void run() {
           for (int i=1; i<=10; i++) {
               System.out.println(i);
               Thread.sleep(1000);
           }
       }
   }.start();
   ```

10. **Event System**:
    - `EventListener` interface dengan `onEvent()`
    - `EventManager` punya list listener
    - Anonymous class untuk implementasi handler spesifik

### Jawaban Latihan Lambda:

1. **Definisi Lambda**:
   - Fungsi anonymous ringkas
   - Karakteristik: tidak punya nama, target functional interface, bisa disimpan variabel

2. **Functional Interface**:
   - Interface dengan 1 abstract method
   - Contoh: 
     - `Predicate<T>`: `boolean test(T t)`
     - `Function<T,R>`: `R apply(T t)`
     - `Consumer<T>`: `void accept(T t)`

3. **Variasi Sintaks**:
   - `() -> expr`
   - `param -> expr`
   - `(param) -> expr`
   - `(T param) -> expr`
   - `(p1,p2) -> { statements; return expr; }`

4. **Perbedaan Lambda vs Anonymous**:
   - Lambda: hanya functional interface, lebih ringkas, no state
   - Anonymous: bisa multi-method, punya state
   - Pilih lambda untuk fungsi sederhana, anonymous untuk kompleks

5. **Method Reference**:
   - `Integer::parseInt` (static)
   - `str::length` (instance tertentu)
   - `String::length` (instance arbitrary)
   - `ArrayList::new` (constructor)

6. **Calculator Interface**:
   - `@FunctionalInterface interface Calculator { double calculate(a,b); }`
   - Implementasi: `(a,b) -> a+b`, `(a,b) -> a-b`, dll

7. **Akses Variabel Lokal**:
   - Hanya bisa akses variabel final/effectively final
   - Batasan: tidak bisa diubah nilainya

8. **Stream API Operations**:
   - Filter genap: `list.stream().filter(n -> n%2==0)`
   - Uppercase: `list.stream().map(String::toUpperCase)`
   - Maksimum: `list.stream().max(Integer::compare)`
   - Rata-rata: `list.stream().mapToDouble(d->d).average()`

9. **Effectively Final**:
   - Variabel yang tidak diubah setelah inisialisasi
   - Lambda bisa akses meski tidak dideklarasi final

10. **Student Processing**:
    - Filter grade: `.filter(s -> s.getGrade() > min)`
    - Group by age: `.collect(Collectors.groupingBy(Student::getAge))`
    - Rata-rata: `.mapToDouble(Student::getGrade).average()`
    - Tertinggi: `.max(Comparator.comparing(Student::getGrade))`

Berikut rangkuman poin-poin penting dari materi OOP Java dan Unit Testing beserta jawaban latihan soalnya:

### Rangkuman Poin Penting:

**1. Konsep OOP:**
- Encapsulation: Penyembunyian data (private fields, public methods)
- Inheritance: Pewarisan sifat class (extends)
- Polymorphism: Kemampuan objek berperilaku berbeda (method overriding)
- Abstraction: Abstract class dan interface

**2. Komponen OOP Java:**
- Class dan Object
- Constructor dan Method
- Package dan Import
- Modifier (public, private, protected)
- Keyword this, super, static, final

**3. Koleksi dan Exception:**
- List, Set, Map
- try-catch-finally
- Custom exception

**4. Unit Testing dengan JUnit:**
- Annotations: @Test, @BeforeEach, @AfterEach
- Assertions: assertEquals, assertTrue, assertThrows
- Test lifecycle
- FIRST principles (Fast, Independent, Repeatable, Self-validating, Thorough)

**5. Mocking dengan Mockito:**
- @Mock, @InjectMocks
- when().thenReturn()
- verify()

**6. TDD (Test-Driven Development):**
- Red-Green-Refactor cycle
- Tulis test sebelum implementasi

### Jawaban Latihan Soal:

**1. Inheritance & Polymorphism dalam Inventory System:**
- Inheritance: Class `Transaction` sebagai parent, `InboundTransaction` dan `OutboundTransaction` sebagai child
- Polymorphism: Method `getTransactionType()` yang dioverride di subclass

**2. Perbedaan DAO vs Service Layer:**
- DAO: Bertanggung jawab untuk operasi CRUD ke data storage
- Service: Mengandung business logic, mengkoordinasikan beberapa DAO
- Dipisahkan untuk separation of concerns dan memudahkan penggantian implementasi

**3. Encapsulation dalam Class Product:**
- Fields dibuat private
- Akses melalui getter/setter
- Method bisnis seperti increaseStock() yang memvalidasi input
- Manfaat: Kontrol akses data, validasi terpusat, fleksibilitas perubahan implementasi

**4. Exception Handling di decreaseStock():**
- Menggunakan try-catch untuk menangkap IllegalArgumentException dan IllegalStateException
- Keuntungan: Memberikan feedback spesifik ke caller, mencegah program crash, memisahkan error handling dari business logic

**6. Modifikasi untuk Batch Processing:**
- Buat class `ProductImporter` dengan method `importFromCSV()`
- Gunakan library seperti OpenCSV untuk parsing
- Validasi data sebelum disimpan
- Gunakan transaction pattern untuk rollback jika ada error

**7. Nested Transactions:**
- Buat class `TransactionBatch` yang mengandung multiple `Transaction`
- Gunakan pattern Unit of Work
- Implementasi rollback manual jika ada yang gagal
- Contoh:
  ```java
  public boolean processBatch(List<Transaction> transactions) {
      for (Transaction t : transactions) {
          if (!t.process()) {
              rollbackAll(); // Kembalikan semua perubahan
              return false;
          }
      }
      return true;
  }
  ```

**8. Logging:**
- Gunakan SLF4J dengan Logback:
  ```java
  import org.slf4j.Logger;
  import org.slf4j.LoggerFactory;

  public class InventoryService {
      private static final Logger logger = LoggerFactory.getLogger(InventoryService.class);
      
      public void updateProduct(Product p) {
          logger.debug("Updating product: {}", p.getId());
          try {
              // logic
          } catch (Exception e) {
              logger.error("Failed to update product", e);
          }
      }
  }
  ```

**9. Concurrent Access:**
- Tantangan: Race condition, deadlock
- Solusi:
  - Gunakan synchronized method/blocks
  - Gunakan ConcurrentHashMap untuk data storage
  - Implementasi optimistic/pessimistic locking
  - Gunakan transaction isolation

**10. Reporting dengan Strategy Pattern:**
- Buat interface `ReportGenerator`
- Implementasi berbagai format:
  ```java
  public interface ReportGenerator {
      void generate(List<ReportData> data);
  }

  public class CSVReportGenerator implements ReportGenerator { ... }
  public class JSONReportGenerator implements ReportGenerator { ... }
  public class ConsoleReportGenerator implements ReportGenerator { ... }
  ```

**Latihan Unit Testing:**

**2. Test Class BankAccount:**
```java
public class BankAccountTest {
    private BankAccount account;

    @BeforeEach
    void setUp() {
        account = new BankAccount("123", "John", 1000);
    }

    @Test
    void deposit_positiveAmount_increasesBalance() {
        account.deposit(500);
        assertEquals(1500, account.getBalance());
    }

    @Test
    void withdraw_sufficientFunds_decreasesBalance() {
        account.withdraw(300);
        assertEquals(700, account.getBalance());
    }

    @Test
    void withdraw_insufficientFunds_throwsException() {
        assertThrows(InsufficientFundsException.class, () -> 
            account.withdraw(1500));
    }

    @Test
    void transfer_validAmount_updatesBothAccounts() {
        BankAccount dest = new BankAccount("456", "Jane", 500);
        account.transfer(dest, 300);
        assertEquals(700, account.getBalance());
        assertEquals(800, dest.getBalance());
    }
}
```

**5. Test ShoppingCart dengan Mockito:**
```java
@ExtendWith(MockitoExtension.class)
class ShoppingCartTest {
    @Mock ProductRepository productRepo;
    @InjectMocks ShoppingCart cart;

    @Test
    void addItem_validProduct_addsToCart() {
        Product p = new Product("1", "Laptop", 1000);
        when(productRepo.findById("1")).thenReturn(Optional.of(p));
        
        cart.addItem("1", 2);
        
        assertEquals(1, cart.getItems().size());
        verify(productRepo).findById("1");
    }

    @Test
    void calculateTotal_multipleItems_returnsCorrectSum() {
        Product p1 = new Product("1", "Mouse", 50);
        Product p2 = new Product("2", "Keyboard", 100);
        
        cart.addItem(p1, 2);
        cart.addItem(p2, 1);
        
        assertEquals(200, cart.calculateTotal());
    }
}
```

**6. Testing Exception:**
```java
@Test
void divide_byZero_throwsException() {
    Calculator calc = new Calculator();
    Exception e = assertThrows(ArithmeticException.class, () -> 
        calc.divide(10, 0));
    assertEquals("Cannot divide by zero", e.getMessage());
}
```

**8. Test Inheritance:**
```java
public class VehicleTest {
    @Test
    void vehicleStart_startsEngine() {
        Vehicle v = new Car();
        assertEquals("Car engine started", v.start());
    }
}

public class CarTest {
    @Test
    void carHonk_returnsBeep() {
        Car c = new Car();
        assertEquals("Beep beep!", c.honk());
    }
}
```

**10. Test Auth Subsystem:**
```java
@ExtendWith(MockitoExtension.class)
public class AuthServiceTest {
    @Mock UserRepository userRepo;
    @Mock PasswordEncoder encoder;
    @InjectMocks AuthService authService;

    @Test
    void login_validCredentials_returnsUser() {
        User user = new User("test", "encodedPass");
        when(userRepo.findByUsername("test")).thenReturn(user);
        when(encoder.matches("pass", "encodedPass")).thenReturn(true);
        
        Optional<User> result = authService.login("test", "pass");
        
        assertTrue(result.isPresent());
        verify(userRepo).findByUsername("test");
    }
}
