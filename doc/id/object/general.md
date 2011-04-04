## Penggunaan Object dan Propertinya

Dalam JavaScript segala seuatu berlaku sebagai object, kecuali 
[`null`](#core.undefined) dan [`undefined`](#core.undefined).

    false.toString() // 'false'
    [1, 2, 3].toString(); // '1,2,3'
    
    function Foo(){}
    Foo.bar = 1;
    Foo.bar; // 1

Adalah sebuah kesalahpahaman bahwa number literal tidak dapat digunakan
sebagai object. Hal ini dikarenakan adanya kecacatan dalam parser
JavaScript yang akan selalu menterjemahkan *dot notation* dalam sebuah
angka sebagai sebuah floating point literal.

    2.toString(); // menghasilkan SyntaxError

Sebenarnya terdapat beberapa cara yang dapat dilakukan untuk membuat
number literal berlaku seperti object.

    2..toString(); // titik kedua yang akan dianggap sebagai notasi
object
    2 .toString(); // perhatikan spasi sebelum titik
    (2).toString(); // 2 akan dievaluasi terlebih dahulu

### Object sebagai sebuah tipe data

Object dalam JavaScript dapat pula digunakan sebagai [*Hashmap*][1],
yang terdiri dari nama properti yang dipetakan kepada nilai.

Sebuah object sederhana dapat dibuat dengan menggunakan notasi `{}`.
Object yang dibuat dengan cara ini akan menjadi turunan dari
`Object.prototype` dan tidak memiliki [properti](#object.hasownproperty) yang telah terdefinisi.

    var foo = {}; // sebuah object kosong

    // sebuah object dengan properti 'test' yang bernilai 12
    var bar = {test: 12}; 

### Mengakses properti

Properti pada Object dapat diakses melalui 2 cara, yaitu menggunakan
notasi titik (dot notation), atau menggunakan notasi kurung siku (square
bracket notation).
    
    var foo = {name: 'Kitten'}
    foo.name; // kitten
    foo['name']; // kitten
    
    var get = 'name';
    foo[get]; // kitten
    
    foo.1234; // SyntaxError
    foo['1234']; // works

Kedua notasi tersebut bekerja secara identik, with the only difference being that
the square bracket notation allows for dynamic setting of properties, as well as
the use of property names that would otherwise lead to a syntax error.

### Menghapus Properti

Properti dari sebuah object hanya dapat dihapus dengan menggunakan
operasi `delete`; mengisi properti dengan nilai `undefined` atau `null`
hanya akan menghapus *value*-nya saja, tidak dengan *key* propertinya.

    var obj = {
        bar: 1,
        foo: 2,
        baz: 3
    };
    obj.bar = undefined;
    obj.foo = null;
    delete obj.baz;

    for(var i in obj) {
        if (obj.hasOwnProperty(i)) {
            console.log(i, '' + obj[i]);
        }
    }

Contoh diatas akan menghasilkan output `bar undefined` dan `foo
null` - hanya `baz` yang dihapus dan hilang dari output.

### Notation of keys

    var test = {
        'case': 'I am a keyword so I must be notated as a string',
        delete: 'I am a keyword too so me' // raises SyntaxError
    };

Properti dari object dapat dinotasikan sebagai susunan karakter biasa
atau dapat pula sebagai string. Dikarenakan kecacatan lainnya dalam
desain parser JavaScript, contoh di atas akan menghasilkan `SyntaxError`
(terjadi pada ECMAScript sebelum versi 5).

Galat ini muncul dikarenakan `delete` adalah sebuah *keyword*; oleh
karena itu, keyword tersebut harus dinotasikan sebagai sebuah notasi
*string literal* hal ini dilakukan untuk memastikan bahwa JavaScript
engine versi terdahulu dapat menginterpretasikannya dengan benar.

[1]: http://en.wikipedia.org/wiki/Hashmap

