META_DATA_START
title="Hash qilish"
published="tez orada"
META_DATA_END

BLOG_START
Hashing — berilgan kalit yoki satrni ortga qaytarib bo'lmaydigan shaklda xashlangan satrga aylantirish jarayoni. Buni amalga oshiradigan funksiya *xash funksiyasi* deb ataladi.

![Oddiy matnni hashga o'girish](https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/photos/plaintext_to_hash.webp)(500x333)

### Hash qilish nega ahamiyatli?
Parolni hech qachon ma'lumotlar bazasida oddiy matn (plaintext) sifatida saqlamang. Agar xakerlar ma'lumotlar bazamizga kirsa, foydalanuvchilarning parollarini o'g'irlashlari mumkin. Buning o'rniga, **xashlangan parolni** saqlang.

Hashlangan parolni yaratishni huddi borsa kelmas yo'ldek tasavvur qiling. Biz xashlangan parolni yaratishimiz mumkin, lekin uni asl xoliga qaytara olmaymiz. Xo'sh unda qanday qilib berilgan oddiy matnning to'g'riligini tekshiramiz? Bu juda oddiy, biz berilgan oddiy matndan xashlangan parolni yaratamiz va uni saqlangani bilan solishtiramiz.

Maslahat:
> Maxsus belgilarni va 8 ta belgidan ko'proq bo'lgan parolni ishlating. Har bir sayt uchun har xil parol. Shaxsiy ma'lumotlardan foydalanmang. Faqat kuchli va tavsiya etilgan parolni ishlating 😉

### Kuchli parollar & Tuzlash
Masalan, “SHA-256” xesh algoritmini olaylik. `"Salom"` qatorini necha marta hesh qilsangiz ham, u har doim aniq natijani qaytaradi: `185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969`. Agar biz ularni ma'lumotlar bazasida saqlasak, kalit sifatida xeshlangan parol va qiymat sifatida haqiqiy parol bilan, agar bizda xeshlangan parol bo'lsa, haqiqiy parolni osongina olishimiz mumkin. Hakerlar esa buni allaqachon qilishgan, ularda [ko'p ishlatilinadigan parollarning](https://en.wikipedia.org/wiki/Wikipedia:10,000_most_common_passwords) ro'yxati bor. Agar siz ulardan birini yoki boshqa bir oddiy parolni ishlatsangiz, ular sizning zaif parolingizni xeshlangan versiyasini olsalar ham, ular sizning parolingizni xeshlangan versiyasi bo'yicha osongina topishlari mumkin (ular allaqachon ularni to'plagan). Bunday hujum **kamalak jadval hujumi 🌈** deb ataladi. Shuning uchun har doim **kuchli parollardan** foydalaning.

Agar biz parolimizni `tuzlasak`, biz bu hujumdan qutilishimiz mumkin. Agar foydalanuvchi oddiy parol ishlatsa, misol uchun `12345678`, va biz undan xayoliy parol yaratish uchun unga `s@1TValUe` kabi tuz qo'shsak, biz kamalak jadval hujumidan qutilamiz. Biz hashlangan parol bilan tuzni ikkalasini ham ma'lumotlar bazasida saqlaymiz. Parolni tekshirish uchun esa, biz kiritilingan parolga bazadagi tuzni qoshib hashlaymiz va bazadagi hashlangan parol bilan solishtiramiz.

> parol + tuz = xayoliy parol

![Parolni tuzlash](https://raw.githubusercontent.com/akbarjorayev/blogs/main/blogs/hashing/photos/password_salting.webp)(500x500)

Tuzlash bunday amalga oshirilinadi:
```
const crypto = require('crypto');

function hashPassword(password, salt) {
  return crypto.createHmac('sha256', salt).update(password).digest('hex');
}

function verifyPassword(inputPassword, salt, storedHash) {
  return hashPassword(inputPassword, salt) === storedHash;
}

function getSalt() {
  return crypto.randomBytes(16).toString('hex');
}

const simplePassword = '12345678';
const salt = getSalt();
const hashedPassword = hashPassword(simplePassword, salt);

const inputPassword = '12345678';
const isValid = verifyPassword(inputPassword, salt, hashedPassword);

console.log(isValid);
```

### Hash qilish ≠ Shifrlash
Shifrlash - kalit yordamida ma'lumotlarni himoya qilish, uni o'qib bo'lmaydigan matnga aylantirishdir, buni esa faqat shu kalit yordamida asl ko'rinishga keltirish mumkin.

Siz foydalanuvchining ID'sini cookie'da saqlamoqchisiz. Agar siz uni son ko'rinishida (masalan, 1, 2, 3...) saqlasangiz, foydalanuvchi uni o'zgartirib boshqa foydalanuvchi sifatida server'ga so'rovlar yuborishi mumkin. Lekin, siz foydalanuvchi ID'sini shifrlanganini saqlasangiz, uni faqatgina siz asl holiga keltirib o'qiy olasiz. **Bu kalitni hech kimga bermang**.
| Xususiyat            | Hash qilish                        | Shifrlash                               |
|----------------------|------------------------------------|-----------------------------------------|
| Maqsad               | Ma'lumotlar xavfsizligi            | Ma'lumotlarning maxfiyligi              |
| Qaytaruvchanlik      | **Bir tomonga** (qaytarilmas)      | **Ikki tomonga** (qaytariladigan)       |
| Output               | Aniq uzinlik                       | O'zgaruvchan uzunlik (ma'lumot asosida) |
| Kalit ishlatilinishi | Kalit kerak emas                   | Kalit kerak                             |
BLOG_END
