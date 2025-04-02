META_DATA_START
title="Create React App o'ldi"
published="Fev 25, 2025"
META_DATA_END

BLOG_START
Ha, [Create React App (CRA)](https://react.dev/blog/2025/02/14/sunsetting-create-react-app) rasman vafot etdi.  

React, Facebook (hozirgi Meta) tomonidan ishlab chiqilgan bo‘lib, dinamik foydalanuvchi interfeyslarini yaratish uchun eng mashhur kutubxonalardan biri bo‘lib qolmoqda. Yillar davomida CRA React loyihalarini tez ishga tushirish uchun asosiy vosita bo‘lib kelgan va haftasiga 200 mingdan ortiq yuklab olingan.  

## Nega CRA'dan voz kechishimiz kerak?  
CRA'ning ishlash samaradorligi — ayniqsa loyihalarni sekin qurish va eskirgan asboblari — uni zamonaviy dasturlashda qo'llab bo'lmaydigan qildi, ayniqsa katta loyihalarda. Yaxshiroq muqobillar paydo bo'lishi bilan uning kamchiliklari aniqroq bo'ldi:  

- **O'zgarishlar sekin** – Loyihadagi o'zgarishlarni ko'rish uchun ko'p vaqt talab etiladi.  
- **Local server sekin** – Local server ishga tushishi `npm start` juda sekin.  
- **Samarasiz qurishlar** – Loyihani production ga qo'yish uchun `npm build` ko'p resurs talab qiladi va deployment narxini oshiradi.  
- **Samarasizlik** – Katta bundle’lar va eskirgan optimallashtirishlar foydalanuvchi ishlatishini sekinlashtiradi.  

![Qaysi yo'ldan borish kerak?](https://raw.githubusercontent.com/akbarjorayev/blogs/refs/heads/main/blogs/create-react-app-is-dead/photos/which_way_to_go.webp)

Agar o'rnini bosuvchi texnologiya izlayotgan bo'lsangiz, mana, ikkita eng yaxshi tanlov:  

### 1. [Vite](https://vite.dev/)  
Vite — bu yuqori samarali frontend qurilish vositasi bo'lib, CRA'ga nisbatan sezilarli darajada tez. U darhol Hot Module Replacement (HMR), zamonaviy ES modulini qo'llab-quvvatlaydi va deyarli 0ms da ishga tushadi. Biroq, u faqat frontend uchun mo'ljallangan, server komponentlarni rander qila olmaydi va API bilan ham ishlay olmaydi. 

### 2. [Next.js](https://nextjs.org/)  
Next.js to'liq stack React ilovalari uchun eng yaxshi tanlovdir. U server komponentlarni render qilish (SSR), statik sayt generatsiyasi (SSG), API yo'llari va middleware larni taqdim etadi va buni siz full-stack va katta loyihalarda bemalol ishlata olasiz.

React ekotizimi rivojlanishi bilan, Vite va Next.js kabi zamonaviy vositalar CRA'ga qaraganda ancha yaxshi tezlikni taminlab bermoqda. Agar siz hali ham CRA'dan foydalanayotgan bo'lsangiz, endi u bilan xayrlashish payti keldi.
BLOG_END
