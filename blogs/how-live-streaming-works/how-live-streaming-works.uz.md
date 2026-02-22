---
title: 'Jonli efir qanday ishlaydi?'
published: 'Fev 22, 2026'
wallpaper: 'https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp'
---

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp">
  <img src="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/blog-thumbnail.webp" alt="Jonli efir qanday ishlaydi muqovasi" width="1024" height="576">
</picture>

## Input

Hammasi kameraning video yozib olishidan boshlanadi. Bu jonli efirning _input_'i hisoblanadi. Lekin video hajmi juda katta bo'ladi, va agar bu 4K video bo'lsa, sizga NASA tezligidagi internet kerak bo'ladi. Shuning uchun bizga **siqish algoritmlari** kerak bo'ladi.

## Siqish (Compression)

Algoritm videoni siqadi, shunda u serverlar orqali tezroq yetkazilinadi. Masalan, tezlashtirilgan quyoshning chiqishi videosini olaylik, unda faqat quyoshning pozitsiyasi o'zgaradi. Siqish tizimga "faqat o'zgargan qismlarni render qil" deydi.

Videolar bitta MP4 fayl qilib yuborilmaydi. Aksincha, ular H.265 (HEVC) yoki H.264 (AVC) formatiga o'tkazilinadi va CDN'larga yetkazish uchun kichik qismlarga (chunk'larga) bo'linadi. Bir chunk videoning bir qismi hisoblanadi, masalan, jonli efirning 2 soniyasi. Shu sababli, internetingiz sekinlashsa yoki to'liq o'chib qolsa, siz jonli efirning 2-3 soniyasini ko'ra olasiz, aynan o'sha soniyalar oldindan yuklab olingan chunk'lardir.

## CDN

CDN'lar (Content Delivery Networks – Kontent Yetkazish Tarmoqlari) dunyo bo'ylab tarqalgan server'lar hisoblanadi, va ular video'ni kesh qiladi va shu yaqin hududdagi foydalanuvchiga yetkazadi. Bu esa asosiy server'ga tushadigan load'ni kamaytiradi va jonli efir kechikishini (latency)'ni kamaytiradi.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/cdn-dark.webp">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/cdn-light.webp">
  <img src="https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/how-live-streaming-works/assets/cdn-light.webp" alt="CDNs (Content Delivery Networks)" width="1472" height="704">
</picture>

## Protokollar

### UDP

UDP (User Datagram Protocol – Foydalanuvchi ma'lumotlari protokoli) internet orqali xabarlar va paketlarni yuborishda ishlatiladi. Aytganimdek, biz media fayllarni qismlarga bo'lib yuboramiz va jonli efir uchun bizga aslida har bir qism kerak emas. Bizning asosiy qilishimiz kerak bo'lgan ish bu, **mediani yetkazib berish**. UDP ba'zi qismlar yo'qolsa ham, ularni yuborishda davom etadi.

```txt
qism1
qism2
qism3
YO'QOLGAN
qism5
...
```

### RTP

RTP (Real-time Transport Protocol) UDP asosida ishlaydi va vaqti va ketma-ketligi kabi metadata'larni qo'shadi. Bu pleyerga paketlarning tartibini tushunishga, audio va videoni sinxronlashtirishga yordam beradi. Ba'zi paketlar yo'qolsa ham, video davom etadi.

## Kechikish

Yuqoridagi ma'lumotlar asosiyda aytishimiz mumkinki, jonli efirlar hech qachon chinakamiga "jonli" bo'lmaydi. Media yozib olinishi, siqilishi, CDNga yuborilishi va foydalanuvchiga yetkazilishi uchun ketadigan vaqt **kechikish** deb ataladi. Asosan jonli efirlar uchun kechikish vaqti taxminan 10 soniya.

Biroq, WebRTC bilan kechikishni 1 soniyadan kamroq qilishimiz mumkin, chunki WebRTC aslida serverlardan foydalanmaydi, u peer-to-peer asosida ishlaydi.
