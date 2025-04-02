META_DATA_START
title="WebSocket yoki Socket.IO"
published="Mar 30, 2025"
META_DATA_END

BLOG_START
O'zi bizga ular nega kerak? Ikkala texnologiyalar ham mijoz bilan server ni bog'laydi va ular o'rtasidagi real vaqt muloqotni ta'minlab beradi. Misol uchun, ularni biz chat ilovalarida, guruhlik o'yinlarda, va mijoz va server orasidagi real vaqt muloqot kerak bolgan boshqa ko'plab ilovalarda ishlatishimiz mumkin.

Biz "real vaqt" muloqotiga qisqa vaqtlarda HTTP so'rovini yuborish orqali erishishimiz mumkin, lekin bu usul bizga qimmatga tushadi va katta ilovalar uchun samarasizdi.

## WebSocket
WebSocket — bu TCP ustida ishlovchi ilova darajasidagi protokol bo‘lib, mijoz va server o‘rtasida ikki tomonlama aloqa o‘rnatishga imkon beradi. U mijoz tomonidan yuborilgan **HTTP Upgrade** so‘rovi orqali bog‘lanishni o‘rnatadi va server javob sifatida holat kodini qaytaradi. Agar holat kodi `101` bo‘lsa, bog‘lanish muvaffaqiyatli o‘rnatiladi; aks holda, bog‘lanish muvaffaqiyatsiz tugaydi. Bog‘lanish o‘rnatilgach, WebSocket aloqa uchun TCP/IP ulanishidan foydalanadi.

![WebSocket logo](https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/websocket-vs-socket-io/photos/websocket-logo.webp)

## Socket.IO
Socket.IO — bu JavaScript kutubxonasi bo'lib, real vaqt rejimidagi aloqa o'rnatish uchun WebSocket'dan foydalanadi. Agar WebSocket mavjud bo'lmasa, u uzun so'rov (long polling) usuliga o'tadi. U WebSocket bilan bir xil funksionallikka ega, lekin qo'shimcha o'rnatilgan xususiyatlarni o'z ichiga olganligi sababli ayrim hollarda yanada qulayroq hisoblanadi.

![Socket.IO logo](https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/websocket-vs-socket-io/photos/socket-io-logo.webp)

## Qaysinisi qanaqa?
Har ikkala texnologiyaning asl maqsadi bir xil — ular mijoz va server o'rtasida real vaqt rejimidagi aloqani ta'minlaydi. **Xo'sh, farqi nimada?**

### Ulanish
Har ikkisi ham vaqti-vaqti bilan yurak urishi (heartbeat) signallarini yuboradi. Server mijozga (yoki aksincha) "ping" jo'natadi, agar "pong" javobi olinmasa, ulanish uzilgan deb hisoblanadi. Agar tarmoq muammosi yoki boshqa sabablarga ko'ra mijoz va server o'rtasidagi aloqa uzilib, ping uchun pong kelmasa, Socket.IO avtomatik ravishda qayta ulanib olishga harakat qiladi. WebSocket'da esa qayta ulanish jarayonini qo'lda boshqarish talab etiladi.

### Fallbacks
WebSocket — bu TCP ustida ishlovchi protokol bo'lib, Socket.IO esa fallback mexanizmi deb ataladigan xususiyatga ega. Bu mexanizm Socket.IO'ni WebSocket mavjud bo'lsa, undan foydalanishga va u mavjud bo'lmasa, avtomatik ravishda uzun so'rov (long polling) usuliga o'tishga imkon beradi. Uzun so'rov (long polling) mijoz so'rov yuborganida boshlanadi va javobni olgach, darhol yana bir so'rov yuborib, ulanishni tirik saqlaydi.

### Broadcasting
Bu Socket.IO'da yana bir o'rnatilgan usuldir. Socket.IO'da biz xohlagancha mijozlarga xabar yuborishimiz yoki ularni maxsus xona (room) ga yuborishimiz mumkin. Xona — bu guruh chatiga o'xshaydi. Agar WebSocket'da esa, bunday xususiyatni qo'lda amalga oshirish kerak bo'ladi.

### Voqealarga asoslangan aloqa
WebSocket — bu xabar almashish uchun ikkala tomonlama to'g'ridan-to'g'ri ulanishni ta'minlaydigan xom (raw) ulanishdir. Socket.IO'da esa biz xabarlar, chatga qo'shilish/chiqish va boshqa narsalarni boshqarish uchun maxsus voqealarni (events) yaratishimiz mumkin.

Server (Node.js)
```
const { Server } = require('socket.io');
const io = new Server(3000);

io.on('connection', (socket) => {
    socket.on('custom_event', (data) => socket.emit('response_event', 'Hello from server!'));
});
```

Fordalanuvchi (Brauzer)
```
const socket = io('http://localhost:3000');

socket.emit('custom_event', 'Hello from client!');
socket.on('response_event', (data) => console.log(data));
```

### Ishlash tezligi
WebSocket ilova darajasidagi protokol ulanishi bo'lgani uchun, u Socket.IO'dan pastroq kechikish (latency) ga ega. Socket.IO esa voqeaga asoslangan aloqa kabi o'rnatilgan usullarni o'z ichiga oladi. Socket.IO xabar yuborganda, qo'shimcha metama'lumotlarni (masalan, voqea va ma'lumot o'zi) qo'shadi.

```
{ "event": "custom_event", "data": "Hello" }
```

## Qachon qaysinisi?
1. **Socket.IO**'ni tanlang agar ko'proq o'rnatilgan usullar bilan rivojlantirishni soddalashtirishni xohlasangiz va mijozlar kutishda kichik vaqt sarflashni qabul qilsangiz (masalan, chat ilovalari, hamkorlik vositalari).

2. **WebSocket**'ni tanlang agar rivojlantirishda to'liq erkinlikka ega bo'lishni, hamma narsani boshidan qurishni va yuqori samaradorlik hamda past kechikish (latency) talab qiladigan tizimlar (masalan, savdo platformalari, o'yin serverlari) qurishni istasangiz.
BLOG_END
