# Web ilovalar arxitekturasi

## 1. Kirish

### Web ilovalar qanday ishlaydi?

Zamonaviy internet dunyosida biz har kuni yuzlab web ilovalar bilan o'zaro aloqada bo'lamiz: ijtimoiy tarmoqlar, onlayn do'konlar, bank tizimlari, ta'lim platformalari va boshqalar. Ammo ortda nima sodir bo'lishini tushunish, dasturchi sifatida rivojlanishingiz uchun muhim asos hisoblanadi.

Web ilova — bu internetda ishlaydigon va foydalanuvchilarga ma'lum xizmatlarni taqdim etuvchi dasturiy ta'minot. U oddiy statik sahifalardan tortib, murakkab biznes tizimlariga qadar turlicha bo'lishi mumkin. Har bir web ilova asosan ikkita asosiy qismdan iborat: **frontend** (foydalanuvchi ko'radigan qism) va **backend** (server tomonida ishlaydigan mantiq va ma'lumotlar bazasi).

### Client–Server modeli

Web ilovalarning ishlash printsipi **Client-Server** arxitekturasiga asoslanadi. Bu arxitektura juda oddiy, lekin kuchli kontseptsiya:

**Client (Mijoz)** — bu foydalanuvchi qurilmasi va brauzer. Siz Chrome, Firefox yoki Safari ochganingizda, bu client hisoblanadi. Client so'rov (request) yuboradi va javob (response) kutadi.

**Server (Server)** — bu kuchli kompyuter yoki kompyuterlar guruhi bo'lib, u mijoz so'rovlarini qabul qiladi, qayta ishlaydi va javob qaytaradi. Server backend dasturlari, ma'lumotlar bazasi va biznes mantiqi joylashgan joy.

Keling, oddiy misol bilan tushuntiramiz. Tasavvur qiling, siz Instagram'ga kiryapsiz:

1. **Browser → Server**: Siz brauzerga "instagram.com" yozyapsiz. Brauzeringiz HTTP so'rov yuboradi.
2. **Server → Database**: Server sizning so'rovingizni qabul qilib, "Bu foydalanuvchi kim? Qanday ma'lumotlarni ko'rsatish kerak?" deb ma'lumotlar bazasiga murojaat qiladi.
3. **Database → Server**: Ma'lumotlar bazasi sizning profilingiz, rasmlaringiz, do'stlaringiz haqidagi ma'lumotlarni serverga qaytaradi.
4. **Server → Browser**: Server bu ma'lumotlarni HTML, CSS, JavaScript formatida tizimlab, brauzeringizga yuboradi.
5. **Browser**: Brauzer bu ma'lumotlarni chiroyli ko'rinishda sizga ko'rsatadi.

Bu jarayon millisekundlar ichida sodir bo'ladi va har safar siz sahifani yangilaganingizda yoki yangi post ochganingizda takrorlanadi.

### Request-Response sikli chuqurroq

Request-Response sikli web ilovalarning yurak urishi hisoblanadi. Bu sikl quyidagi qadamlardan iborat:

**1. HTTP Request yaratilishi**: Foydalanuvchi harakatga kelganda (masalan, havola bosish, forma yuborish), brauzer HTTP so'rov yaratadi. Bu so'rovda URL manzil, HTTP metodi (GET, POST, PUT, DELETE), sarlavhalar (headers) va ba'zan ma'lumotlar (body) bo'ladi.

**2. So'rovning serverga yetib borishi**: So'rov internet orqali serverga jo'natiladi. Bu jarayonda DNS (Domain Name System) domain nomini IP manzilga aylantiradi, so'ngra TCP/IP protokollari orqali so'rov serverga yetkaziladi.

**3. Server tomonida qayta ishlash**: Server so'rovni qabul qilib, uni tahlil qiladi. Keyin biznes mantiq ishlaydi: ma'lumotlar tekshiriladi, autentifikatsiya va avtorizatsiya amalga oshiriladi, kerakli ma'lumotlar bazasidan olinadi yoki saqlanadi.

**4. Javob generatsiyasi**: Server kerakli ma'lumotlarni to'plab, ularni formatlab (HTML, JSON, XML), HTTP javob yaratadi. Javobda status kodi (200 OK, 404 Not Found, 500 Server Error), sarlavhalar va tanasi bo'ladi.

**5. Brauzerda ko'rsatish**: Brauzer javobni qabul qilib, uni qayta ishlaydi va foydalanuvchiga ko'rsatadi. Agar HTML bo'lsa, render qilinadi; agar JSON bo'lsa, JavaScript orqali sahifaga dinamik qo'shiladi.

Bu sikl har bir foydalanuvchi o'zaro ta'siri uchun takrorlanadi va zamonaviy web ilovalar sekundiga minglab bunday sikllarni qayta ishlashi mumkin.

## 2. Web Ilovalar Arxitekturasi Asoslari

### Monolit arxitektura

Monolit arxitektura — bu barcha dastur komponentlari bitta yaxlit tizimda birlashtirilgan yondashuv. Bu klassik va eng qadimgi web ilovalar arxitekturasi bo'lib, hali ham ko'plab loyihalarda qo'llaniladi.

**Monolit arxitekturaning xususiyatlari:**

Monolit dasturda barcha funksiyalar — autentifikatsiya, biznes mantiq, ma'lumotlar bazasi bilan ishlash, fayllar bilan ishlash — bitta codebase ichida joylashgan. Dastur bitta server jarayoni (process) sifatida ishga tushadi va barcha qismlar bir-biri bilan to'g'ridan-to'g'ri funksiya chaqiruvlar orqali muloqot qiladi.

Misol uchun, kichik onlayn do'kon yaratyapsiz deylik. Monolit arxitekturada:
- Foydalanuvchi ro'yxatdan o'tish
- Mahsulot kataloги
- Savatcha tizimi
- To'lov jarayoni
- Admin panel

Barchasi bitta Django loyihasida, bitta ma'lumotlar bazasida bo'ladi.

**Afzalliklari:**
- Oddiy rivojlantirish: Barcha kod bir joyda, tushunish va boshqarish oson
- Tezkor prototiplash: Yangi funksiya qo'shish uchun yangi fayl yaratib, kodingizni yozasiz
- Sodda deploy: Bitta arxiv fayl yoki konteyner yetarli
- Kamroq murakkablik: Tarmoq muloqoti, distributed tizim muammolari yo'q
- Tezroq ishlash: Ichki funksiya chaqiruvlar tarmoq so'rovlariga qaraganda ancha tez

**Kamchiliklari:**
- Miqyoslash qiyinligi: Butun dasturni ko'paytirish kerak, faqat bir qismini emas
- Texnologiya bog'liqligi: Butun dastur bitta til va frameworkda yozilgan
- Deploy xavfi yuqori: Bir qism o'zgarishi butun dasturni qayta deploy qilishni talab qiladi
- Kodning o'sishi: Vaqt o'tishi bilan kod bazasi juda katta va murakkab bo'lib qolishi mumkin
- Jamoa ishlashi qiyin: Ko'p dasturchilar bir xil kod bazasida ishlashsa, konfliktlar ko'payadi

### Microservices arxitektura

Microservices — bu monolit dasturning qarama-qarshi yondashuviy bo'lib, dastur ko'plab kichik, mustaqil xizmatlar (services)ga bo'linadi. Har bir xizmat o'z vazifasini bajaradi va API orqali boshqalar bilan muloqot qiladi.

**Microservices arxitekturaning xususiyatlari:**

Dastur bir nechta alohida servislarga ajratiladi. Har bir servis:
- O'z ma'lumotlar bazasiga ega bo'lishi mumkin
- Alohida deploy qilinadi
- Mustaqil ravishda miqyoslanadi
- O'z texnologiyasini tanlashi mumkin

Masalan, yuqoridagi onlayn do'konni microservices sifatida qurganingizda:
- **Auth Service**: Foydalanuvchi autentifikatsiyasi (Python + Django)
- **Product Service**: Mahsulotlar katalogi (Node.js + Express)
- **Cart Service**: Savatcha tizimi (Go)
- **Payment Service**: To'lovlar (Java + Spring)
- **Notification Service**: Email/SMS yuborish (Python + Celery)

Har biri alohida server, alohida kod bazasi, alohida deploy.

**Afzalliklari:**
- Mustaqil miqyoslash: Faqat kerakli xizmatni ko'paytirish mumkin
- Texnologiya erkinligi: Har bir xizmat uchun eng mos texnologiyani tanlash
- Tez deploy: Faqat o'zgargan xizmatni qayta deploy qilasiz
- Xatolar izolyatsiyasi: Bir xizmat ishdan chiqsa, boshqalari ishlayveradi
- Jamoa mustaqilligi: Har bir jamoa o'z xizmatini mustaqil rivojlantiradi

**Kamchiliklari:**
- Yuqori murakkablik: Ko'plab xizmatlarni boshqarish, monitoring qilish qiyin
- Tarmoq latency: Xizmatlar o'rtasidagi muloqot sekinroq
- Ma'lumotlar izchilligi: Distributed transactions murakkab
- Katta infrastruktura: Ko'proq serverlar, konteynerlar, orkestatsiya kerak
- Debugging qiyinligi: Xatolarni kuzatish ko'plab tizimlarni tahlil qilishni talab qiladi

### MVC / MTV kabi patternlar

Design patterns — bu dasturlashda umumiy muammolarning isbotlangan yechimlari. Web dasturlashda eng mashhur patternlardan biri MVC (Model-View-Controller) va uning o'zgarishi MTV (Model-Template-View).

**MVC (Model-View-Controller):**

Bu pattern dasturni uchta asosiy qismga ajratadi:
- **Model**: Ma'lumotlar tuzilmasi va biznes mantiq
- **View**: Foydalanuvchi interfeysini ko'rsatish
- **Controller**: Foydalanuvchi so'rovlarini boshqarish va Model bilan View o'rtasida vositachilik

Real hayot misoli: Restoran.
- Model — oshxona (ovqat tayyorlash, retseptlar)
- View — dasturxon va idishlar (ovqatni taqdimot)
- Controller — ofitsiant (buyurtma qabul qilish, oshxonaga yetkazish, ovqatni olib kelish)

**MTV (Model-Template-View):**

Django o'z versiyasini MTV deb ataydi, ammo konsepsiya o'xshash:
- **Model**: Xuddi MVC'dagi kabi — ma'lumotlar
- **Template**: View'ning o'rnini bosadi — HTML shablonlar
- **View**: Controller'ning o'rnini bosadi — biznes mantiq

Bu nomlanish farqi faqat terminologiya masalasi. Django yaratuvchilari "View" so'zini mantiq uchun, "Template" so'zini esa ko'rinish uchun ishlatishni mantiqiyroq deb topdilar.

### Server-side rendering (SSR) va Client-side rendering (CSR)

Zamonaviy web dasturlashda sahifalarni qanday generatsiya qilish masalasi muhim.

**Server-side Rendering (SSR):**

SSR'da HTML sahifalar to'g'ridan-to'g'ri serverda generatsiya qilinadi va tayyor HTML brauzerga yuboriladi.

Jarayon:
1. Foydalanuvchi URL ochadi
2. Server ma'lumotlarni bazadan oladi
3. Server HTML ni to'liq yasaydi
4. Tayyor HTML brauzerga yuboriladi
5. Brauzer shunchaki ko'rsatadi

**Afzalliklari:**
- Tezroq dastlabki yuklanish (First Contentful Paint)
- SEO uchun yaxshi (qidiruv tizimlari osongina indeksatsiya qiladi)
- Oddiy brauzerlar uchun mos
- Server kuchli bo'lsa, tezkor ishlash

**Kamchiliklari:**
- Har safar serverga so'rov kerak
- Interaktivlik past
- Server yuklamasi yuqori

Misol: Yangiliklar sayti, blog, e-commerce sahifalar asosan SSR ishlatadi.

**Client-side Rendering (CSR):**

CSR'da server faqat minimal HTML va JavaScript yuboradi. JavaScript brauzerda ishga tushib, sahifani dinamik yaratadi.

Jarayon:
1. Foydalanuvchi URL ochadi
2. Server minimal HTML + JavaScript yuboradi
3. Brauzer JavaScript'ni yuklab, ishga tushiradi
4. JavaScript API'ga so'rov yuborib, ma'lumot oladi
5. JavaScript HTML'ni dinamik yaratadi

**Afzalliklari:**
- Yuqori interaktivlik (SPA — Single Page Application)
- Server yuklamasi past
- Desktop ilova tajribasi
- Tezkor navigatsiya (sahifa yangilanmaydi)

**Kamchiliklari:**
- Dastlabki yuklanish sekinroq
- SEO qiyin (zamonaviy yechimlar bor)
- JavaScript majburiy
- Kuchli brauzer kerak

Misol: Gmail, Facebook, Twitter — bular asosan CSR ishlatadi.

### Backend va Frontend nima?

**Backend** — bu server tomonidagi dasturlash bo'lib, foydalanuvchi ko'rmaydigan, ammo dasturning asosiy mantiqini tashkil etuvchi qism.

Backend mas'uliyatlari:
- Autentifikatsiya va avtorizatsiya
- Biznes mantiq (narxlarni hisoblash, statistika)
- Ma'lumotlar bazasi bilan ishlash
- API yaratish
- Xavfsizlik ta'minlash
- Fayl yuklash va saqlash
- Email/SMS yuborish
- To'lov tizimlariga integratsiya

Backend texnologiyalar: Python (Django, Flask), JavaScript (Node.js), Java (Spring), PHP (Laravel), Ruby (Rails), Go, C# (.NET).

**Frontend** — bu client tomonidagi dasturlash, ya'ni foydalanuvchi ko'rgan va o'zaro ta'sir qilgan narsa.

Frontend mas'uliyatlari:
- Foydalanuvchi interfeysi (UI)
- Foydalanuvchi tajribasi (UX)
- Animatsiyalar va interaktivlik
- Formalar yaratish va validatsiya
- Responsive dizayn (mobil moslashtirish)
- Backend bilan API orqali muloqot

Frontend texnologiyalar: HTML, CSS, JavaScript, React, Vue.js, Angular, Svelte.

Real misol bilan:
Onlayn bankingga kiryapsiz.
- **Frontend**: Login formasi, chiroyli dizayn, balansni ko'rsatish, animatsiyalar
- **Backend**: Parolni tekshirish, balansni hisoblab chiqish, tranzaksiyalarni saqlash, xavfsizlik

Zamonaviy dasturlashda Full-stack developer — bu ham backend, ham frontend bilan ishlay oladigan dasturchi.

## 3. Django Arxitekturasi Nima?

### Django qanday ishlaydi?

Django — bu Python dasturlash tilida yozilgan yuqori darajali web framework bo'lib, tezkor va xavfsiz web ilovalar yaratishni ta'minlaydi. Django "Batteries included" falsafasiga amal qiladi, ya'ni ko'plab funksiyalar dastlab o'rnatilgan holda keladi.

Django arxitekturasi qatlamli (layered) tuzilishga ega. Har bir qatlam o'z vazifasini bajaradi va boshqa qatlamlar bilan aniq interfeys orqali muloqot qiladi.

**Django'ning asosiy qatlamlari:**

1. **HTTP qatlami**: So'rovlar va javoblar
2. **URL Dispatcher**: URL'larni qayta ishlash
3. **View qatlami**: Biznes mantiq
4. **Model qatlami**: Ma'lumotlar bazasi
5. **Template qatlami**: HTML generatsiya
6. **Middleware qatlami**: So'rov va javoblarni qayta ishlash

### Request/Response sikli Django'da

Django'da har bir foydalanuvchi so'rovi quyidagi bosqichlardan o'tadi:

**1-bosqich: HTTP so'rov kelishi**
Foydalanuvchi brauzerda `http://example.com/blog/post/5/` degan URL ni ochadi. Brauzer HTTP GET so'rovini serverga yuboradi.

**2-bosqich: WSGI/ASGI interfeysi**
Web server (Nginx, Apache) so'rovni qabul qilib, uni WSGI (Web Server Gateway Interface) yoki ASGI orqali Django ilovasiga yo'naltiradi. WSGI — bu Python web ilovalar uchun standart interfeys.

**3-bosqich: Middleware orqali o'tish (so'rov)**
So'rov Django middleware'lar zanjiridan o'tadi. Har bir middleware so'rovni tahlil qilishi, o'zgartirishi yoki to'xtatishi mumkin. Masalan:
- SecurityMiddleware: Xavfsizlik tekshiruvlari
- SessionMiddleware: Session ma'lumotlarini yuklash
- AuthenticationMiddleware: Foydalanuvchini aniqlash
- CSRFMiddleware: CSRF hujumlardan himoya

**4-bosqich: URL Dispatcher**
Django `urls.py` fayllaridagi patternlarni tekshiradi va so'ralgan URL ga mos keladigan view funksiyasini topadi. Masalan, `/blog/post/5/` URL uchun `views.post_detail` funksiyasi chaqiriladi va `id=5` parametr uzatiladi.

**5-bosqich: View funksiyasi ishlaydi**
View funksiyasi biznes mantiqni amalga oshiradi:
- Kerakli parametrlarni oladi
- Ma'lumotlar bazasiga so'rov yuboradi (ORM orqali)
- Ma'lumotlarni qayta ishlaydi
- Template'ga kontekst ma'lumotlarini uzatadi yoki API uchun JSON qaytaradi

**6-bosqich: Model qatlami (agar kerak bo'lsa)**
Agar view ma'lumotlar bazasidan ma'lumot olishi kerak bo'lsa, Django ORM ishlatiladi. ORM Python kodini SQL ga aylantiradi va ma'lumotlar bazasiga so'rov yuboradi.

**7-bosqich: Template rendering**
Agar HTML javob kerak bo'lsa, Django template engine ishga tushadi. Template fayl ochiladi, kontekst ma'lumotlari bilan to'ldiriladi va tayyor HTML generatsiya qilinadi.

**8-bosqich: Middleware orqali o'tish (javob)**
Generatsiya qilingan javob yana middleware'lar orqali o'tadi (teskari tartibda). Middleware'lar javobni o'zgartirishi mumkin, masalan, qo'shimcha header'lar qo'shish.

**9-bosqich: HTTP javob yuborilishi**
Tayyor HTTP javob WSGI orqali web serverga, keyin esa brauzerga yuboriladi.

Bu jarayon millisekundlar ichida amalga oshadi va Django'ning optimallashtirilgan arxitekturasi tufayli juda samarali ishlaydi.

### Django Middleware

Middleware — bu Django'ning request/response jarayoniga global ta'sir etuvchi komponentlar. Ularni "so'rov va javob o'rtasidagi filtrlar" deb tasavvur qilish mumkin.

**Middleware qanday ishlaydi:**

Middleware klasslar `settings.py` dagi `MIDDLEWARE` ro'yxatida tartib bilan joylashgan. Har bir so'rov bu zanjirning yuqoridan pastga o'tadi, javob esa pastdan yuqoriga.

```
Request → MW1 → MW2 → MW3 → View → MW3 → MW2 → MW1 → Response
```

**Middleware metodlari:**
- `process_request(request)`: So'rov view'ga yetmasdan oldin
- `process_view(request, view_func, view_args, view_kwargs)`: View chaqirilishidan oldin
- `process_template_response(request, response)`: Template render qilingandan keyin
- `process_response(request, response)`: Har bir javob uchun
- `process_exception(request, exception)`: View exception keltirganda

**Real hayot misoli:**

Tasavvur qiling, sizning saytingizda barcha so'rovlar uchun foydalanuvchi tilini aniqlash kerak. Middleware yaratib, har bir so'rovda brauzer tilini tekshirasiz va mos tilni o'rnatasiz. Bu middleware barcha view'lar uchun avtomatik ishlaydi.

### URL Dispatcher (Routing)

Django'da URL dispatcher — bu URL'larni view funksiyalariga bog'lovchi tizim. Bu Django'ning eng muhim qismlaridan biri.

**URL patterns:**

Django URL patternlarini regex (regular expression) yoki oddiy string'lar bilan yaratish imkonini beradi.

Misol:
- `/blog/` → blog ro'yxati
- `/blog/5/` → 5-raqamli blog post
- `/blog/python-tutorial/` → "python-tutorial" slug'li post

**URL dispatcher afzalliklari:**
- RESTful URL'lar yaratish oson
- URL parametrlarini avtomatik ajratib olish
- URL nomlarini qo'llash (reverse URL)
- Namespace'lar orqali modular tashkil etish

Real misol: E-commerce saytda mahsulot sahifasi `/products/laptop-dell-xps/` ko'rinishida bo'lishi mumkin. Django bu URL'ni tahlil qilib, slug parametrini view'ga uzatadi.

### Template Engine

Django Template Engine — bu HTML sahifalarni dinamik generatsiya qiluvchi kuchli vosita. U xavfsiz, tez va o'qish oson.

**Template tizimining afzalliklari:**
- Python kodi va HTML ni ajratish
- Template inheritance (meros olish)
- Auto-escaping (XSS hujumlardan himoya)
- Custom filters va tags
- Reusable components

Misol: Barcha sahifalarda bir xil header va footer bo'ladi. Base template yaratib, boshqa template'lar undan meros oladi. Shunda header o'zgarsa, faqat bir joyda o'zgartirasiz.

### ORM (Object-Relational Mapping)

Django ORM — bu ma'lumotlar bazasi bilan Python obyektlari kabi ishlashga imkon beruvchi abstraktsiya qatlami. SQL yozishingiz shart emas.

**ORM afzalliklari:**
- SQL yozmasdan ma'lumotlar bazasi bilan ishlash
- Ma'lumotlar bazasi mustaqilligi (PostgreSQL, MySQL, SQLite)
- Migration tizimi
- QuerySet optimizatsiyasi
- Xavfsiz (SQL injection'dan himoya)

Misol: Foydalanuvchilarni olish uchun SQL o'rniga:
```python
users = User.objects.filter(is_active=True).order_by('-date_joined')[:10]
```

Bu sodda, o'qilishi oson va xavfsiz.

### Admin Panel Arxitekturasi

Django Admin — bu Django'ning eng kuchli va unikal xususiyatlaridan biri. Bu avtomatik generatsiya qilinadigan admin interfeys.

**Admin panel qanday ishlaydi:**

Django sizning modellaringizni o'qib, ularga mos admin interfeys yaratadi. Siz faqat model yaratib, admin.py'da ro'yxatdan o'tkazasiz — hammasi tayyor.

**Admin panel imkoniyatlari:**
- CRUD operatsiyalari (Create, Read, Update, Delete)
- Qidiruv va filtrlar
- Ommaviy amallar (bulk actions)
- Inline editing
- Permissions va user groups
- Customizable interface

Real misol: Yangiliklar sayti uchun Django loyihasi yaratyapsiz. Article modelini yaratasiz va admin'ga qo'shasiz — tahrirchilar darhol maqolalarni qo'shish, tahrirlash, o'chirish imkoniyatiga ega bo'lishadi. Hech qanday admin panel yaratmadingiz!

## 4. MTV Arxitekturasi (Django Modeli)

### MTV va MVC farqi

MTV (Model-Template-View) va MVC (Model-View-Controller) arxitekturalari konsepsiyalar jihatidan juda o'xshash, lekin terminologiyada farq qiladi. Django MTV'ni tanlash sababi — nomlanish aniqroq va mantiqiyroq.

**MVC Arxitektura:**
- **Model**: Ma'lumotlar va biznes mantiq
- **View**: Foydalanuvchi interfeysini ko'rsatish
- **Controller**: So'rovlarni boshqarish, Model va View ni bog'lash

**Django MTV Arxitektura:**
- **Model**: Ma'lumotlar tuzilmasi (xuddi MVC'dagi kabi)
- **Template**: Foydalanuvchi interfeysini ko'rsatish (MVC'dagi View)
- **View**: Biznes mantiq va so'rovlarni boshqarish (MVC'dagi Controller)

**Nima uchun farq?**

Django yaratuvchilar "View" so'zini mantiq uchun ishlatishni mantiqiyroq deb topdilar, chunki view — bu foydalanuvchi "ko'radigan" ma'lumotlarni tayyorlovchi funksiya. "Template" esa faqat ko'rinish uchun.

Aslida, faqat nomlanish farqi. Ikkala arxitektura ham bir xil maqsadga xizmat qiladi: **Separation of Concerns** — dasturning turli qismlarini ajratish va har biriga aniq mas'uliyat berish.

Real misol: Kitob do'koni dasturi.
- **Model**: Kitoblar, mualliflar, kategoriyalar — ma'lumotlar bazasida
- **View**: Kitoblarni qidirish, savatga qo'shish, buyurtma yaratish — mantiq
- **Template**: Kitoblar ro'yxati sahifasi, kitob detallari, savatcha — HTML

### Model → Ma'lumotlar Tuzilmasi

Model — bu Django ilovasining poydevori. Model ma'lumotlar tuzilmasini belgilaydi va ma'lumotlar bazasi jadvallari bilan to'g'ridan-to'g'ri bog'langan.

**Model nima qiladi:**

1. **Ma'lumotlar strukturasini belgilash**: Har bir model Python klassi sifatida yoziladi. Klass attributlari ma'lumotlar bazasi ustunlarini bildiradi.

2. **Ma'lumotlar validatsiyasi**: Model fieldlarda validatsiya qoidalari belgilanadi (masalan, email formati, maksimal uzunlik).

3. **Ma'lumotlar bazasi bilan muloqot**: Model orqali ma'lumotlarni saqlash, o'qish, yangilash, o'chirish mumkin.

4. **Munosabatlarni belgilash**: Modellar orasidagi bog'lanishlar (one-to-one, one-to-many, many-to-many).

**Real misol:**

Blog uchun model. Har bir blog post'da sarlavha, matn, muallif, sana bo'ladi:

Ma'lumotlar bazasida bu avtomatik jadval yaratadi. Django migrations tizimi orqali jadvalni yaratish, o'zgartirish oson.

**Model'ning kuchi:**

Model faqat ma'lumotlar strukturasi emas, balki biznes mantiqi ham. Metodlar qo'shib, murakkab amallarni bajarishingiz mumkin. Masalan, "Bu postni o'qishga qancha vaqt ketadi?" ni hisoblash metodi.

### Template → UI (Foydalanuvchi Interfeysi)

Template — bu Django'da HTML sahifalarni yaratish uchun ishlatiladi gan shablonlar. Template faqat ko'rinish uchun javobgar va hech qanday biznes mantiq emas.

**Template'ning asosiy tamoyillari:**

1. **Separation**: Template faqat ma'lumotlarni ko'rsatadi, hisoblash va qarorlar view'da qabul qilinadi.

2. **Reusability**: Bir template ko'plab joylarda ishlatilishi mumkin.

3. **Inheritance**: Base template yaratib, boshqalar undan meros oladi.

4. **Context variables**: View'dan template'ga ma'lumotlar uzatiladi.

**Template tili:**

Django o'z template tilini ishlatadi. Bu til oddiy va xavfsiz:
- `{{ variable }}` — o'zgaruvchini chiqarish
- `{% tag %}` — mantiq (if, for, block)
- `{{ value|filter }}` — filtrlar (date formatlash, lowecase qilish)

**Real hayot misoli:**

Blog ro'yxati sahifasi. Template view'dan postlar ro'yxatini oladi va chiroyli HTML sifatida ko'rsatadi. Agar post bo'lmasa, "Hech narsa topilmadi" xabarini ko'rsatadi.

Template faqat ma'lumotlarni ko'rsatadi:
- Post sarlavhalari
- Qisqa matn
- Sanalar
- Mualliflar

Hamma hisoblashlar va mantiq view'da amalga oshirilgan.

### View → Biznes Mantiq

View — bu Django'ning miyasi. View so'rovlarni qabul qiladi, kerakli amallarni bajaradi va javob qaytaradi.

**View nima qiladi:**

1. **So'rovni qabul qilish**: HTTP request ob'yekti orqali barcha ma'lumotlarga kirish (GET parametrlar, POST ma'lumotlari, cookielar, headerlar).

2. **Autentifikatsiya va avtorizatsiya**: Foydalanuvchi tizimga kirganmi? Ruxsati bormi?

3. **Ma'lumotlarni olish**: Model orqali ma'lumotlar bazasidan kerakli ma'lumotlarni olish.

4. **Biznes mantiq**: Hisoblashlar, validatsiya, biznes qoidalarini qo'llash.

5. **Ma'lumotlarni tayyorlash**: Template uchun kontekst yaratish yoki API uchun JSON.

6. **Javob qaytarish**: HTTP response ob'yekti — HTML, JSON, redirect, xato.

**View turlari:**

Django ikki xil view yozish imkonini beradi:

1. **Function-based views (FBV)**: Oddiy Python funksiyalar
2. **Class-based views (CBV)**: Python klasslari (kuchliroq, qayta foydalanish oson)

**Real misol:**

Mahsulot detallari sahifasi uchun view:
- URL'dan mahsulot ID sini oladi
- Ma'lumotlar bazasidan o'sha mahsulotni qidiradi
- Agar topilmasa, 404 xatosi
- Agar topilsa, o'xshash mahsulotlarni ham topadi
- Barcha ma'lumotlarni template'ga yuboradi
- Template HTML yaratadi va foydalanuvchiga ko'rsatiladi

**View'ning mas'uliyati:**

View "nima ko'rsatish" va "qanday ko'rsatish" o'rtasidagi ko'prik. U biznes qarorlarini qabul qiladi, lekin dizayn va layoutni template'ga qoldiradi.

### URL → Dispatcher Sifatida Roli

Django'da URL dispatcher — bu so'rovlarni to'g'ri view'ga yo'naltiruvchi marshrutlovchi. Bu Django'ning eng chiroyli va kuchli qismlaridan biri.

**URL Dispatcher'ning asosiy rollari:**

1. **Routing**: Har bir URL'ni mos view'ga bog'lash.

2. **Parametr ajratish**: URL'dan parametrlarni avtomatik ajratib, view'ga uzatish.

3. **URL nomlari**: Har bir URL'ga nom berish va kodni reverse URL orqali yozish.

4. **Namespace**: Turli app'larning URL'larini ajratish.

5. **Moslashuvchanlik**: Regex yoki oddiy patternlar orqali murakkab URL strukturalarini qo'llab-quvvatlash.

**URL patternlarning ahamiyati:**

Yaxshi URL'lar — bu foydalanuvchi uchun tushunarli va SEO uchun foydali. Django bu jihatdan juda qulay.

Yaxshi URL misollari:
- `/blog/2025/01/django-tutorial/` — aniq, SEO friendly
- `/products/electronics/laptops/` — ierarxik
- `/users/john/profile/` — o'qilishi oson

Yomon URL misollari:
- `/page?id=12345` — tushunarsiz
- `/p/x/y/z/` — ma'nosiz

**Real misol:**

Blog ilovasi uchun URL strukturasi:
- `/` — bosh sahifa
- `/blog/` — barcha postlar
- `/blog/category/python/` — Python bo'yicha postlar
- `/blog/2025/01/15/my-post/` — aniq post (sana + slug)
- `/blog/author/john/` — John'ning postlari

Har bir URL o'z view'ga bog'langan va Django avtomatik parametrlarni ajratadi.

### Yakuniy MTV Diagrammasi (Matn ko'rinishida)

MTV arxitekturasining to'liq oqimi quyidagicha:

```
1. User → HTTP Request → http://example.com/blog/5/

2. WSGI/ASGI → Django ga uzatadi

3. Middleware chain → So'rovni qayta ishlash (xavfsizlik, session, auth)

4. URL Dispatcher (urls.py):
   - Pattern: /blog/<int:id>/
   - View: blog_detail
   - Parameter: id=5

5. View funksiyasi (views.py):
   - blog_detail(request, id=5)
   - Biznes mantiq ishlatadi
   - Model ga murojaat qiladi

6. Model (models.py):
   - Post.objects.get(id=5)
   - Ma'lumotlar bazasiga SQL so'rov
   - Ma'lumot qaytaradi

7. View davom etadi:
   - Ma'lumotni qayta ishlaydi
   - Kontekst yaratadi: {'post': post}
   - Template'ga uzatadi

8. Template (blog_detail.html):
   - Kontekst ma'lumotlarini oladi
   - HTML generatsiya qiladi
   - {% block %} larni to'ldiradi

9. View → HTTP Response (HTML)

10. Middleware chain → Javobni qayta ishlash (teskari tartibda)

11. WSGI → Web Server → User Browser

12. Browser → HTML'ni render qiladi → Foydalanuvchi ko'radi
```

Bu sikl har bir so'rov uchun takrorlanadi. Django'ning optimallashtirilgan arxitekturasi tufayli bu jarayon juda tez amalga oshadi.

## 5. Django Project va App Tuzilishi

### Django Project Nima?

Django project — bu butun web ilovasining konteyner i. U barcha sozlamalar, konfiguratsiyalar va app'larni o'zida mujassamlashtiradi. Project — bu dasturning "uyı".

**Project tarkibi:**

Project yaratilganda Django avtomatik ravishda bir nechta fayllar va kataloglar yaratadi. Har biri muhim rol o'ynaydi:

- **Asosiy katalog**: Project nomi bilan
- **manage.py**: Django boshqaruv skripti
- **settings.py**: Barcha sozlamalar
- **urls.py**: Asosiy URL routerı
- **wsgi.py**: WSGI serveri uchun entry point
- **asgi.py**: ASGI serveri uchun entry point (async)

**Project mas'uliyatlari:**

1. **Global sozlamalar**: Ma'lumotlar bazasi, tillar, vaqt zonasi, static fayllar manzili
2. **Xavfsizlik**: SECRET_KEY, ALLOWED_HOSTS, xavfsizlik middleware'lar
3. **URL marshrutlash**: Root URL konfiguratsiyasi
4. **App'larni ro'yxatdan o'tkazish**: INSTALLED_APPS ro'yxati
5. **Middleware tartibı**: Request/response processing
6. **Template va static fayllar yo'llari**: Qayerdan qidirish kerak

**Real hayot misoli:**

Onlayn ta'lim platformasi yaratyapsiz. Project nomi `education_platform`. Bu project ichida:
- Autentifikatsiya tizimi
- Kurslar katalogi
- Video darslar
- To'lov tizimi
- Forum

Barchasi bitta project ostida, ammo har biri alohida app sifatida.

### Django App Nima?

Django app — bu muayyan vazifani bajaruvchi mustaqil modul. App — bu project ichidagi "mini-dastur".

**App xususiyatlari:**

1. **Mustaqillik**: App boshqa app'lardan mustaqil ishlashi kerak
2. **Qayta foydalanish**: Bir app bir nechta project'larda ishlatilishi mumkin
3. **Single responsibility**: Har bir app bitta aniq vazifani bajaradi
4. **Modul arlik**: App'ni olib tashlash yoki qo'shish oson

**App tarkibi:**

Har bir app o'z strukturasiga ega:
- **models.py**: App ma'lumotlar modellari
- **views.py**: App biznes mantiqi
- **urls.py**: App URL marshrutlari (ixtiyoriy, lekin tavsiya etiladi)
- **admin.py**: Admin panel sozlamalari
- **apps.py**: App konfiguratsiyası
- **tests.py**: Test kodlari
- **migrations/**: Ma'lumotlar bazasi o'zgarishlari
- **templates/**: App-specific shablonlar
- **static/**: App-specific static fayllar

### Nima Uchun Bir Project Ichida Bir Nechta App Bo'ladi?

Bu Django'ning eng kuchli konseptsiyalaridan biri — **modular arxitektura**. Katta loyihalarni kichik, boshqariladigan qismlarga ajratish.

**Modul arlik afzalliklari:**

**1. Separation of Concerns:**
Har bir app o'z vazifasiga javobgar. Autentifikatsiya app faqat foydalanuvchi bilan ishlaydi, blog app faqat maqolalar bilan.

**2. Ommaviy rivojlantirish:**
Katta jamoada har bir dasturchi o'z app'ida ishlashi mumkin. Konfliktlar kamayadi.

**3. Qayta foydalanish:**
Bir marta yaxshi autentifikatsiya app yozib, uni barcha loyihalarda ishlatish mumkin.

**4. Test qilish oson:**
Har bir app alohida test qilinadi. Bug topish va tuzatish osonroq.

**5. Kodni tushunish oson:**
Yangi dasturchi loyihaga qo'shilganda, faqat kerakli app'ni o'rganadi, butun loyihani emas.

**6. Kengaytirish qulayligi:**
Yangi funksiya kerakmi? Yangi app yarating va project'ga qo'shing.

**Real hayot misoli:**

E-commerce platformasi uchun app'lar:

1. **accounts**: Foydalanuvchi ro'yxatdan o'tish, login, profil
2. **products**: Mahsulotlar katalogi, kategoriyalar
3. **cart**: Savatcha tizimi
4. **orders**: Buyurtmalar boshqaruvi
5. **payments**: To'lov integratsiyalari
6. **reviews**: Mahsulot sharhlari
7. **notifications**: Email/SMS bildirishnomalar
8. **analytics**: Statistika va hisobotlar

Har biri mustaqil, lekin birgalikda to'liq tizim.

### App'larni Modular Bo'lishi: Professional Tushuntirish

Modular arxitektura — bu zamonaviy dasturiy ta'minot arxitekturasining asosidir. Django bu konseptsiyani juda yaxshi qo'llab-quvvatlaydi.

**Modularlikning asosiy tamoyillari:**

**1. High Cohesion (Yuqori bog'liqlik ichkarida):**
App ichidagi barcha komponentlar bir-biriga yaqin bo'lishi kerak. Masalan, blog app'ida Post model, PostView, post shablonlari birgalikda.

**2. Low Coupling (Past bog'liqlik tashqarida):**
App'lar o'zaro kam bog'liq bo'lishi kerak. Bitta app o'zgarishi boshqalarga ta'sir qilmasligi kerak.

**3. Single Responsibility Principle:**
Har bir app bitta mas'uliyatga ega. Agar app ikki xil vazifani bajarayotgan bo'lsa, uni ikkiga bo'lish kerak.

**4. Dependency Management:**
App'lar o'rtasidagi bog'lanishlarni diqqat bilan boshqarish. Circular dependency'dan qochish.

**5. Interface Segregation:**
App'lar o'rtasidagi muloqot aniq API orqali bo'lishi kerak.

**Yaxshi modular loyihaning belgilari:**

- Har bir app 1000 qatordan oshmaydigan views.py ga ega
- Models.py aniq va tushunarli
- App'ni olib tashlash 15 daqiqadan ko'p vaqt olmaydi
- Bir app'ning testi boshqa app'lar bilan bog'liq emas
- App'ni boshqa project'ga ko'chirish mumkin

**Yomon modular loyihaning belgilari:**

- Bitta app "god object" bo'lib, hamma narsani qiladi
- App'lar o'rtasida ko'p import'lar
- Bir app o'zgarishi boshqa 5 app'ni buzadi
- Test qilish uchun butun loyihani ishga tushirish kerak

### Django Yaratgan Strukturadagi Fayllar

Django loyiha yaratilganda avtomatik ravishda bir qancha fayllar generatsiya qilinadi. Har birining o'z vazifasi va ahamiyati bor.

**manage.py:**

Bu Django'ning asosiy boshqaruv skripti. Bu orqali barcha Django buyruqlari bajariladi.

Vazifalar:
- Development server ishga tushirish: `python manage.py runserver`
- Ma'lumotlar bazasi migratsiyalari: `python manage.py migrate`
- Superuser yaratish: `python manage.py createsuperuser`
- Static fayllarni yig'ish: `python manage.py collectstatic`
- Test ishlatish: `python manage.py test`
- Custom buyruqlar bajarish

Qachon chaqiriladi: Dasturchi terminal orqali chaqiradi, production'da avtomatik scriptlar orqali.

Qaysi jarayonda: Development va deployment jarayonlarida.

**settings.py:**

Bu Django loyihasining asosiy sozlamalar fayli. Butun loyihaning konfiguratsiyasi shu yerda.

Vazifalar:
- Ma'lumotlar bazasi sozlamalari (DATABASE)
- Installed app'lar ro'yxati (INSTALLED_APPS)
- Middleware tartibı (MIDDLEWARE)
- Template sozlamalari (TEMPLATES)
- Static va media fayllar yo'llari (STATIC_URL, MEDIA_URL)
- Xavfsizlik sozlamalari (SECRET_KEY, ALLOWED_HOSTS, DEBUG)
- Internationalization (LANGUAGE_CODE, TIME_ZONE)
- Email sozlamalari
- Cache sozlamalari

Qachon chaqiriladi: Django ishga tushganda birinchi bo'lib o'qiladi.

Qaysi jarayonda: Barcha jarayonlarda — development, testing, production. Odatda environment bo'yicha turli settings fayllar ishlatiladi.

**urls.py:**

Bu root URL konfiguratsiya fayli. Barcha URL marshrutlari shu yerdan boshlanadi.

Vazifalar:
- Root URL patternlarni belgilash
- Admin panel URL'ini ulash
- App URL'larini include qilish
- Static va media fayllar URL'larini sozlash (development'da)

Qachon chaqiriladi: Har bir HTTP so'rov kelganda URL dispatcher tomonidan.

Qaysi jarayonda: Request handling jarayonida, middleware'dan keyin.

**wsgi.py:**

Web Server Gateway Interface entry point. Bu production serverlar uchun.

Vazifalar:
- Django ilovasini WSGI-compatible formatda taqdim etish
- WSGI server (Gunicorn, uWSGI) bilan bog'lanish
- Django sozlamalarini yuklash

Qachon chaqiriladi: Web server (Nginx + Gunicorn) Django'ni ishga tushirganda.

Qaysi jarayonda: Production deployment. Development'da `runserver` WSGI'ni ichkarida ishlatadi.

**asgi.py:**

Asynchronous Server Gateway Interface entry point. Async funksiyalar uchun.

Vazifalar:
- Django ilovasini ASGI-compatible formatda taqdim etish
- WebSocket'lar, async view'lar uchun
- Real-time funksiyalar (chat, notifications)

Qachon chaqiriladi: ASGI server (Daphne, Uvicorn) Django'ni ishga tushirganda.

Qaysi jarayonda: Async funksiyalar talab qilingan production'da.

**App fayllari:**

**models.py:**
- Vazifasi: Ma'lumotlar bazasi modellari
- Qachon: ORM so'rovlar bajarilganda
- Jarayonda: Ma'lumotlar bazasi operatsiyalari

**views.py:**
- Vazifasi: Biznes mantiq va so'rov qayta ishlash
- Qachon: URL dispatcher view'ni chaqirganda
- Jarayonda: Request handling

**admin.py:**
- Vazifasi: Admin panel sozlamalari
- Qachon: Admin panelga kirilganda
- Jarayonda: Admin interfeys generatsiyasi

**migrations/:**
- Vazifasi: Ma'lumotlar bazasi o'zgarishlari tarixi
- Qachon: `makemigrations` va `migrate` buyruqlari
- Jarayonda: Schema o'zgarishlari

**templates/:**
- Vazifasi: HTML shablonlar
- Qachon: View template render qilganda
- Jarayonda: Response generatsiyasi

**static/:**
- Vazifasi: CSS, JS, rasımlar
- Qachon: Sahifa yuklanayotganda
- Jarayonda: Frontend rendering

## 6. Django Project Yaratish (startproject)

### django-admin startproject Buyruq

Django loyiha yaratish juda oddiy:

```bash
django-admin startproject myproject
```

Bu buyruq `myproject` nomli katalog yaratadi va ichiga kerakli fayllarni joylashtiradi.

### Yaratilgan Katalog Strukturasi

Buyruq bajarilgandan keyin quyidagi struktura hosil bo'ladi:

```
myproject/
    manage.py
    myproject/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```

**Tashqi myproject/:**
Bu loyihaning ildiz katalogi. Bu katalog nomini istalgan joyda o'zgartirishingiz mumkin, Django uchun ahamiyati yo'q. Odatda bu joyda:
- `manage.py`
- `requirements.txt` (dependency'lar)
- `README.md` (loyiha haqida)
- `.gitignore` (git uchun)
- Virtual environment (venv/)

**Ichki myproject/:**
Bu asliy Python package. Bu katalog nomi muhim, chunki u import qilishda ishlatiladi. Masalan, `myproject.settings` yoki `myproject.urls`.

**__init__.py:**
Bu fayl bo'sh, lekin muhim. U Python'ga bu katalog package ekanligini bildiradi. Django 3.2+ versiyalarida bu fayl avtomatik yaratilmaydi, lekin siz qo'shishingiz mumkin.

**settings.py to'liq tahlili:**

Bu faylda loyihaning barcha sozlamalari. Qatorma-qator tahlil qilaylik:

1. **SECRET_KEY**: Bu Django xavfsizlik uchun ishlatadigan maxfiy kalit. U CSRF tokenlar, session'lar, parol resetlash tokenlarini yaratishda ishlatiladi. Production'da bu keyni hech qachon oshkor qilmaslik kerak. Environment variable'da saqlash tavsiya etiladi.

2. **DEBUG**: Development rejimida True, production'da False. True bo'lganda Django batafsil xato sahifalarini ko'rsatadi. Production'da bu xavfsiz emas, chunki dastur strukturasini ko'rsatadi.

3. **ALLOWED_HOSTS**: Production'da Django qaysi domainlarga xizmat ko'rsatishini belgilaydi. Bo'sh ro'yxat hamma joydan so'rovga ruxsat bermaydi. Masalan: `['example.com', 'www.example.com']`.

4. **INSTALLED_APPS**: Django va sizning app'laringiz ro'yxati. Har bir app bu yerda ro'yxatdan o'tishi kerak. Django'ning default app'lari:
   - `django.contrib.admin`: Admin panel
   - `django.contrib.auth`: Autentifikatsiya
   - `django.contrib.contenttypes`: Content type framework
   - `django.contrib.sessions`: Session framework
   - `django.contrib.messages`: Messaging framework
   - `django.contrib.staticfiles`: Static fayllar

5. **MIDDLEWARE**: So'rov va javob o'rtasidagi processing layer'lar. Tartib muhim, yuqoridan pastga so'rov, pastdan yuqoriga javob o'tadi.

6. **ROOT_URLCONF**: Asosiy URL konfiguratsiya fayli. Odatda `myproject.urls`.

7. **TEMPLATES**: Template engine sozlamalari. Backend, kataloglar, context processorlar.

8. **DATABASES**: Ma'lumotlar bazasi sozlamalari. Default SQLite, production'da PostgreSQL tavsiya etiladi.

9. **AUTH_PASSWORD_VALIDATORS**: Parol qoidalari. Minimal uzunlik, umumiy parollar, raqamli parollar check qilish.

10. **LANGUAGE_CODE va TIME_ZONE**: Til va vaqt zonasi. Masalan: `'uz'` va `'Asia/Tashkent'`.

11. **STATIC_URL va MEDIA_URL**: Static (CSS, JS) va media (foydalanuvchi yuklagan) fayllar URL'lari.

**urls.py tahlili:**

Root URL konfiguratsiya. Oddiy strukturada:
- Admin panel yo'nalishi: `path('admin/', admin.site.urls)`
- App URL'larini ulash: `path('blog/', include('blog.urls'))`

URL pattern'lar `path()` yoki `re_path()` orqali yaratiladi. `path()` oddiyroq, `re_path()` regex ishlatadi.

**wsgi.py va asgi.py:**

Bu fayllar production deployment uchun. Ular Django ilovasini web server bilan bog'laydi. Odatda bu fayllarni o'zgartirish shart emas.

### manage.py Qanday Ishlaydi

`manage.py` — bu Django'ning command-line utility'si. U Django buyruqlarini bajarish uchun wrapper.

Ichida nimalar bor:
- Django settings modulini o'rnatadi
- Django management buyruqlarini chaqiradi
- Environment sozlamalarini boshqaradi

Eng ko'p ishlatiladigan buyruqlar:
- `runserver`: Development server
- `makemigrations`: Model o'zgarishlaridan migration yaratish
- `migrate`: Migration'larni ma'lumotlar bazasiga qo'llash
- `createsuperuser`: Admin foydalanuvchi yaratish
- `collectstatic`: Static fayllarni yig'ish
- `test`: Testlarni ishga tushirish
- `shell`: Django shell (interactive Python)

## 7. Django App Yaratish (startapp)

### python manage.py startapp Buyrugi

App yaratish ham oddiy:

```bash
python manage.py startapp blog
```

Bu `blog` nomli app yaratadi va kerakli fayllarni generatsiya qiladi.

### App Nima Uchun Alohida Bo'lishi Kerak?

**Modularlik sabablari:**

1. **Aniqlik**: Har bir app bitta vazifani bajaradi. Blog app faqat blog funksiyalariga javobgar.

2. **Mustaqillik**: App boshqa project'larda ishlatilishi mumkin. Yaxshi yozilgan auth app har qanday loyihada ishlaydi.

3. **Boshqarish qulayligi**: Kichik kod bazasi — kam bug, oson test, tezroq development.

4. **Jamoa ishi**: Har bir dasturchi o'z app'ida ishlaydi, git konfliktlari kamayadi.

5. **Qayta foydalanish**: Django community ko'plab tayyor app'larni taqdim etadi (django-allauth, django-rest-framework). Ularni shunchaki install qilib ishlatishingiz mumkin.

### Real Hayotdan Misol

**E-commerce platformasi:**

Tasavvur qiling, katta onlayn do'kon yaratyapsiz. Uni bitta katta app sifatida yozish o'rniga, quyidagi app'larga bo'lasiz:

**accounts** (Foydalanuvchilar):
- Ro'yxatdan o'tish
- Login/Logout
- Profil
- Parol tiklash

**products** (Mahsulotlar):
- Mahsulot modeli
- Kategoriyalar
- Qidiruv
- Filtrlar

**cart** (Savatcha):
- Savatga qo'shish/olib tashlash
- Miqdorni o'zgartirish
- Umumiy narx hisoblash

**orders** (Buyurtmalar):
- Buyurtma yaratish
- Buyurtma tarixi
- Status tracking

**payments** (To'lovlar):
- To'lov integratsiyalari
- To'lov tarixı
- Invoices

**reviews** (Sharhlar):
- Mahsulot baholash
- Izoh qoldirish
- Rating tizimi

**dashboard** (Boshqaruv paneli):
- Statistika
- Hisobotlar
- Analytics

Har bir app o'z vazifasini bajaradi va alohida rivojlantirish, test qilish, miqyoslash mumkin.

### App'ni settings.py → INSTALLED_APPS ga Qo'shish

App yaratib bo'lgach, uni Django'ga "tanıtish" kerak. Buning uchun `settings.py` dagi `INSTALLED_APPS` ro'yxatiga qo'shiladi:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    # ... boshqa Django app'lar
    
    # Sizning app'laringiz
    'blog',  # yoki 'blog.apps.BlogConfig'
]
```

**Nima uchun bu kerak?**

1. **Django avtomatik topish**: INSTALLED_APPS'dagi app'larning migration'lari, static fayllari, template'lari avtomatik topiladi.

2. **Migration tizimi**: Django faqat installed app'larning migration'larini bajaradi.

3. **Admin avtomatik import**: Admin'dagi model registratsiyalari avtomatik yuklanadi.

4. **Template loader**: Django installed app'larning templates kataloglarini qidiradi.

5. **URL routing**: Root urls.py'dan app URL'larini include qilish mumkin.

App'ni qo'shmasangiz, Django uni "ko'rmaydi" va model'lar, view'lar ishlamaydi.

### App Ichidagi Fayllar Roli

**models.py:**

Bu yerda app'ning barcha ma'lumotlar modellari yoziladi.

Vazifasi:
- Ma'lumotlar strukturasini belgilash
- Ma'lumotlar bazasi jadvallari yaratish
- Model metodlari va property'lar
- Model relationships (ForeignKey, ManyToMany)

Qachon ishlaydi:
- ORM so'rovlar bajarilganda
- Migration yaratish va qo'llash vaqtida
- Admin panelda

Real misol — Blog uchun:
```python
# models.py
class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.title
```

**views.py:**

App'ning barcha view funksiyalari yoki klasslari.

Vazifasi:
- So'rovlarni qabul qilish
- Biznes mantiq amalga oshirish
- Ma'lumotlar bazasidan ma'lumot olish
- Template'ga ma'lumot uzatish yoki JSON qaytarish

Qachon ishlaydi:
- URL dispatcher view'ni chaqirganda
- Har bir HTTP so'rov uchun

Real misol — Blog post ro'yxati:
```python
# views.py
def post_list(request):
    posts = Post.objects.all().order_by('-created_at')
    return render(request, 'blog/post_list.html', {'posts': posts})
```

**urls.py (app-level):**

App'ning URL marshrutlari. Bu fayl default yaratilmaydi, siz qo'lda yaratasiz.

Vazifasi:
- App ichidagi URL patternlarni belgilash
- URL nomlarini berish (reverse URL uchun)
- View'larni URL'ga bog'lash

Qachon ishlaydi:
- Root urls.py'dan include qilinganda
- Har bir so'rov URL routing'dan o'tganda

Real misol:
```python
# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'
urlpatterns = [
    path('', views.post_list, name='list'),
    path('<int:pk>/', views.post_detail, name='detail'),
]
```

**admin.py:**

Admin panelda modellarni qanday ko'rsatish.

Vazifasi:
- Modellarni admin'da ro'yxatdan o'tkazish
- Admin interfeys'ni customization qilish
- List display, search, filters sozlash

Qachon ishlaydi:
- Admin panelga kirilganda
- Django ishga tushganda (admin auto-discovery)

Real misol:
```python
# admin.py
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'created_at']
    search_fields = ['title', 'content']
    list_filter = ['created_at', 'author']
```

**tests.py:**

App'ning test kodlari.

Vazifasi:
- Model'larni test qilish
- View'larni test qilish
- Business logic'ni test qilish
- Integration test'lar

Qachon ishlaydi:
- `python manage.py test` buyrug'i bajarilganda
- CI/CD pipeline'da

Real misol:
```python
# tests.py
from django.test import TestCase
from .models import Post

class PostModelTest(TestCase):
    def test_post_creation(self):
        post = Post.objects.create(title="Test", content="Content")
        self.assertEqual(post.title, "Test")
```

**forms.py (ixtiyoriy, lekin ko'p ishlatiladi):**

Django form klasslari.

Vazifasi:
- HTML forma yaratish
- Ma'lumotlarni validatsiya qilish
- Ma'lumotlarni tozalash (clean data)
- Model bilan bog'lash (ModelForm)

Qachon ishlaydi:
- View'da forma render qilinganda
- POST so'rov kelganda validatsiya uchun

Real misol:
```python
# forms.py
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

**migrations/:**

Ma'lumotlar bazasi o'zgarishlari tarixi.

Vazifasi:
- Model o'zgarishlarini kuzatish
- SQL script'lar generatsiya qilish
- O'zgarishlarni qayta qo'llash (rollback) imkoniyati

Qachon ishlaydi:
- `makemigrations` buyrug'i bajarilganda yaratiladi
- `migrate` buyrug'i bajarilganda qo'llaniladi

**templates/:**

App-specific HTML shablonlar.

Vazifasi:
- HTML sahifalar yaratish
- View'dan kelgan ma'lumotlarni ko'rsatish
- Template inheritance

Qachon ishlaydi:
- View `render()` funksiyasini chaqirganda

**static/:**

App-specific static fayllar (CSS, JS, images).

Vazifasi:
- Styling (CSS)
- Client-side logic (JavaScript)
- Rasmlar va boshqa media

Qachon ishlaydi:
- Sahifa brauzerda yuklanayotganda

## 8. Django'da URL Routing Mexanizmi

### URL Dispatcher Qanday Ishlaydi

URL dispatcher — Django'ning yo'l topuvchisi. Har bir kiruvchi so'rovni tahlil qilib, to'g'ri view'ga yo'naltiradi.

**Ishlash jarayoni:**

1. **So'rov keladi**: `http://example.com/blog/2025/django-tutorial/`
2. **Middleware'dan o'tadi**: Xavfsizlik, session, auth
3. **URL dispatcher ishga tushadi**:
   - ROOT_URLCONF dan boshlaydi (settings.py'da ko'rsatilgan)
   - URL pattern'larni yuqoridan pastga tekshiradi
   - Birinchi mos kelgan pattern'ni topadi
   - Agar include() bo'lsa, app-level urls.py ga o'tadi
   - Parametrlarni ajratib oladi
   - Mos view'ni chaqiradi

**Pattern matching:**

Django ikki xil pattern matching qo'llab-quvvatlaydi:

1. **path()**: Oddiy va o'qilishi oson
2. **re_path()**: Regex bilan murakkab pattern'lar

### Root urls.py

Project yaratilganda avtomatik yaratiladi. Bu barcha URL'larning boshlang'ich nuqtasi.

**Asosiy struktura:**

```python
# myproject/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),
    path('shop/', include('shop.urls')),
    path('', include('home.urls')),
]
```

Bu yerda:
- `/admin/` — admin panel
- `/blog/` — blog app'ning barcha URL'lari
- `/shop/` — do'kon app'ning URL'lari
- `/` — bosh sahifa

### App-level urls.py

Har bir app o'z URL'larini boshqaradi. Bu faylni qo'lda yaratish kerak.

**Misol — Blog app:**

```python
# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'

urlpatterns = [
    path('', views.post_list, name='list'),
    path('<int:pk>/', views.post_detail, name='detail'),
    path('category/<slug:slug>/', views.category_posts, name='category'),
    path('create/', views.post_create, name='create'),
]
```

Bu URL'lar `/blog/` prefix bilan ishlatiladi:
- `/blog/` → post_list
- `/blog/5/` → post_detail (pk=5)
- `/blog/category/python/` → category_posts (slug='python')
- `/blog/create/` → post_create

### include() Funksiyasi

`include()` — app URL'larini asosiy urls.py'ga ulash uchun ishlatiladi.

**Afzalliklari:**

1. **Modularlik**: Har bir app o'z URL'larini boshqaradi
2. **Namespace**: URL nomlarini ajratish
3. **Prefix**: Avtomatik URL prefix qo'shish
4. **Maintainability**: Kodni boshqarish oson

**Real misol:**

E-commerce loyihasi uchun:

```python
# main/urls.py
urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('home.urls')),  # Bosh sahifa
    path('products/', include('products.urls')),  # Mahsulotlar
    path('cart/', include('cart.urls')),  # Savatcha
    path('orders/', include('orders.urls')),  # Buyurtmalar
    path('accounts/', include('accounts.urls')),  # Foydalanuvchi
]
```

Har bir app o'z URL'larida prefix'ni bilmaydi, faqat o'z ichki URL'larini boshqaradi.

### URL Parametrlari va Path Converters

Django avtomatik URL parametrlarni ajratib, view'ga uzatadi.

**Path converters:**

- `<int:pk>` — butun son
- `<str:username>` — string
- `<slug:slug>` — slug (harf, raqam, tire, underscore)
- `<uuid:id>` — UUID
- `<path:path>` — har qanday yo'l (slash bilan)

Real misol:
```python
path('user/<str:username>/', views.user_profile)
# /user/john/ → username='john'

path('post/<int:year>/<int:month>/<slug:slug>/', views.post_detail)
# /post/2025/01/django-tutorial/ → year=2025, month=1, slug='django-tutorial'
```

### Reverse URL (URL Nomlari)

Django URL'larni qattiq kod sifatida yozmaslik uchun nom berish imkonini beradi.

**Afzalligi:**

URL o'zgarsa, kod har joyda o'zgartirish shart emas.

**Ishlatilishi:**

Template'da:
```html
<a href="{% url 'blog:detail' pk=post.id %}">O'qish</a>
```

View'da:
```python
from django.urls import reverse
from django.shortcuts import redirect

return redirect('blog:list')
# yoki
url = reverse('blog:detail', kwargs={'pk': 5})
```

Bu URL'lar o'zgarganda avtomatik yangilanadi.

## 9. Django'da Templates Arxitekturasi

### Template Engine

Django o'z template engine'iga ega. U HTML generatsiyasini oson va xavfsiz qiladi.

**Template engine xususiyatlari:**

1. **Variables**: `{{ variable }}` — Python obyektlarini chiqarish
2. **Tags**: `{% tag %}` — mantiq (if, for, block)
3. **Filters**: `{{ value|filter }}` — ma'lumotlarni formatlash
4. **Comments**: `{# comment #}` — izohlar
5. **Auto-escaping**: XSS hujumlardan avtomatik himoya

**Qanday ishlaydi:**

View template render qilganda:
1. Template fayli topiladi (TEMPLATES sozlamalariga asosan)
2. Template parse qilinadi (compile)
3. Context ma'lumotlari template'ga uzatiladi
4. Template render qilinadi (HTML generatsiya)
5. HTML view'ga qaytadi

### Base Template

Base template — bu barcha sahifalar uchun asosiy shablon. U umumiy strukturani o'z ichiga oladi.

**Afzalliklari:**

1. **DRY (Don't Repeat Yourself)**: Kod takrorlanmaydi
2. **Consistency**: Barcha sahifalar bir xil strukturaga ega
3. **Oson yangilash**: Bir joyda o'zgartirish — hamma joyda o'zgaradi

**Real misol:**

```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}Mening Saytim{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <header>
        <nav>
            <!-- Navigation menu -->
        </nav>
    </header>
    
    <main>
        {% block content %}
        {% endblock %}
    </main>
    
    <footer>
        <!-- Footer content -->
    </footer>
</body>
</html>
```

### Template Inheritance

Template inheritance — meros olish mexanizmi. Child template base'dan meros olib, faqat kerakli qismlarni o'zgartiradi.

**Ishlash printsipi:**

1. Base template'da `{% block %}` belgilanadi
2. Child template `{% extends %}` orqali meros oladi
3. Child faqat kerakli block'larni override qiladi

**Real misol:**

```html
<!-- blog/post_list.html -->
{% extends 'base.html' %}

{% block title %}Blog - {{ block.super }}{% endblock %}

{% block content %}
    <h1>Blog Postlari</h1>
    {% for post in posts %}
        <article>
            <h2>{{ post.title }}</h2>
            <p>{{ post.content|truncatewords:50 }}</p>
        </article>
    {% endfor %}
{% endblock %}
```

### Context O'zgaruvchilar

Context — bu template'ga uzatiladigan ma'lumotlar lug'ati.

**View'da context yaratish:**

```python
def post_detail(request, pk):
    post = Post.objects.get(pk=pk)
    context = {
        'post': post,
        'related_posts': Post.objects.filter(category=post.category)[:5],
        'current_user': request.user,
    }
    return render(request, 'blog/detail.html', context)
```

**Template'da ishlatish:**

```html
<h1>{{ post.title }}</h1>
<p>Muallif: {{ post.author.username }}</p>
<p>Sana: {{ post.created_at|date:"d F Y" }}</p>

<h3>O'xshash maqolalar:</h3>
{% for related in related_posts %}
    <a href="{{ related.get_absolute_url }}">{{ related.title }}</a>
{% endfor %}
```

Context processorlar — bu barcha template'larga avtomatik qo'shiladigan o'zgaruvchilar. Masalan, `request.user` barcha joyda mavjud.

### Static Fayllarni Ulash

Static fayllar — CSS, JavaScript, rasmlar.

**Sozlash:**

settings.py'da:
```python
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
```

**Template'da ishlatish:**

```html
{% load static %}

<link rel="stylesheet" href="{% static 'css/style.css' %}">
<script src="{% static 'js/main.js' %}"></script>
<img src="{% static 'images/logo.png' %}" alt="Logo">
```

`{% load static %}` — static tag'ni yuklaydi. Keyin `{% static %}` orqali fayllarni ulaysiz. Django avtomatik to'g'ri yo'lni topadi.

## 10. Django'da Modellar va ORM Arxitekturasi

### Django Modeli va Ma'lumotlar Bazasi

Django ORM (Object-Relational Mapping) — bu SQL va Python obyektlari o'rtasidagi ko'prik.

**Model — jadval aloqasi:**

Har bir Django model klassi ma'lumotlar bazasida bitta jadvalga mos keladi:
- Model klass nomi → jadval nomi (lowercase, plural)
- Model field'lari → jadval ustunlari
- Model instance'i → jadvalda bitta qator (row)

Real misol:

```python
class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    published_date = models.DateField()
    price = models.DecimalField(max_digits=6, decimal_places=2)
```

Bu model ma'lumotlar bazasida `app_book` jadvali yaratadi:
- `id` (auto-generated primary key)
- `title` (VARCHAR(200))
- `author_id` (INTEGER, foreign key)
- `published_date` (DATE)
- `price` (DECIMAL(6,2))

### Migrations Nima?

Migration — bu model o'zgarishlarini ma'lumotlar bazasiga qo'llash usuli. Bu Django'ning eng kuchli xususiyatlaridan biri.

**Migration jarayoni:**

1. **Model o'zgartirish**: models.py'da o'zgartirish kiritasiz
2. **Migration yaratish**: `python manage.py makemigrations`
3. **Migration ko'rish**: Django Python faylida migration yaratadi
4. **Migration qo'llash**: `python manage.py migrate`
5. **Ma'lumotlar bazasi o'zgaradi**: SQL script'lar bajariladi

**Migration afzalliklari:**

- Version control: Barcha o'zgarishlar tarixı
- Team work: Jamoa a'zolari bir xil schemani ishlatadi
- Rollback: Oldingi versiyaga qaytish mumkin
- Database agnostic: Har qanday ma'lumotlar bazasi uchun

**Real misol:**

Dastlab Book modelida `pages` field yo'q. Keyin qo'shmoqchisiz:

1. models.py'da field qo'shasiz:
```python
pages = models.IntegerField(default=0)
```

2. `makemigrations` buyrug'i:
```bash
python manage.py makemigrations
```

Django avtomatik migration fayli yaratadi (masalan, `0002_book_pages.py`).

3. `migrate` buyrug'i:
```bash
python manage.py migrate
```

Django SQL script bajaradi va `pages` ustuni jadvalga qo'shiladi. Mavjud ma'lumotlar saqlanadi, yangi field default qiymat oladi.

### ORM va SQL Generatsiya

Django ORM Python kodini SQL ga aylantiradi. Bu avtomatik va samarali.

**Misol — ORM vs SQL:**

ORM:
```python
books = Book.objects.filter(price__lt=50).order_by('-published_date')[:10]
```

Django generatsiya qilgan SQL:
```sql
SELECT * FROM app_book 
WHERE price < 50 
ORDER BY published_date DESC 
LIMIT 10;
```

Siz SQL yozmadingiz, lekin Django optimal SQL yaratdi.

**ORM afzalliklari:**

1. **Python sintaksis**: SQL bilmasangiz ham ishlaysiz
2. **Database agnostic**: PostgreSQL, MySQL, SQLite — farqi yo'q
3. **SQL injection himoya**: Parametrli so'rovlar
4. **Optimization**: Lazy loading, select_related, prefetch_related
5. **Chaining**: Bir necha filtrlarni birlashtirishingiz mumkin

**Real misol — murakkab so'rov:**

```python
books = Book.objects.filter(
    author__country='USA',
    published_date__year__gte=2020,
    price__lt=100
).select_related('author').prefetch_related('reviews')[:20]
```

Bu so'rov:
- Amerikal mualliflar kitoblarini topadi
- 2020-yıldan keyin nashr etilganlarni
- Narxi $100 dan kam
- Author ma'lumotlarini bitta so'rovda oladi (JOIN)
- Reviews'ni alohida efficient so'rovda oladi
- Faqat 20 ta natija

Django buni optimal SQL'ga aylantiradi va performance'ni ta'minlaydi.

### QuerySet Arxitekturasi

QuerySet — bu ma'lumotlar bazasidan olingan obyektlar to'plami. Ammo u "lazy" — ya'ni darhol bajarilmaydi.

**QuerySet xususiyatlari:**

1. **Lazy evaluation**: Faqat kerak bo'lganda bajariladi
2. **Chainable**: Bir necha operatsiyalarni birlashtirishingiz mumkin
3. **Cacheable**: Natija keshlanadi, takroriy so'rov yo'q
4. **Sliceable**: Python list kabi slice qilishingiz mumkin

**Lazy evaluation misoli:**

```python
books = Book.objects.filter(price__lt=50)  # Hali SQL so'rov yo'q
books = books.filter(author__name='John')  # Hali yo'q
books = books.order_by('-published_date')  # Hali yo'q

# Faqat iteratsiya qilganda SQL bajariladi
for book in books:  # Hozir SQL bajarildi
    print(book.title)
```

Barcha filtrlar bitta SQL so'rovga birlashadi. Samarali!

**QuerySet metodlari:**

- `filter()`: Filtrlar qo'shish
- `exclude()`: Exclude qilish
- `order_by()`: Tartiblash
- `values()`: Faqat fieldlarni olish
- `annotate()`: Aggregation
- `select_related()`: ForeignKey JOIN
- `prefetch_related()`: ManyToMany efficient loading
- `count()`: Sanash
- `exists()`: Mavjudligini tekshirish
- `first()`, `last()`: Birinchi/oxirgi obyekt

**Real misol — Blog statistika:**

```python
from django.db.models import Count, Avg

posts = Post.objects.filter(
    status='published'
).annotate(
    comment_count=Count('comments'),
    avg_rating=Avg('reviews__rating')
).order_by('-comment_count')
```

Bu so'rov har bir post uchun commentlar sonı va o'rtacha ratingni hisoblaydi. Va bularning barchasi bitta SQL so'rovda!

## 11. Django'da Admin Panel Arxitekturasi

### Admin Panel Qanday Ishlaydi

Django Admin — bu CMS (Content Management System) kabi interfeys bo'lib, avtomatik generatsiya qilinadi.

**Admin arxitekturasi:**

1. **Model introspection**: Django modellaringizni o'qiydi va ularning strukturasini tushunadi
2. **CRUD interface**: Har bir model uchun Create, Read, Update, Delete interface'larini yaratadi
3. **Customizable**: Juda ko'p customization imkoniyatlari
4. **Permission-based**: User permissions asosida interface o'zgaradi

**Admin'ning kuchi:**

Django bilan 30 daqiqada to'liq funksional CMS yaratishingiz mumkin. Hech qanday admin panel kod yozmasdan!

### Admin Model Registratsiya Jarayoni

Admin'da model ko'rsatish uchun uni ro'yxatdan o'tkazish kerak.

**Oddiy registratsiya:**

```python
# admin.py
from django.contrib import admin
from .models import Book

admin.site.register(Book)
```

Shuncha! Admin panelda Book modeli paydo bo'ldi va siz CRUD operatsiyalar qila olasiz.

**Advanced registratsiya:**

```python
@admin.register(Book)
class BookAdmin(admin.ModelAdmin):
    list_display = ['title', 'author', 'published_date', 'price']
    list_filter = ['published_date', 'author']
    search_fields = ['title', 'author__name']
    ordering = ['-published_date']
    date_hierarchy = 'published_date'
```

Endi admin panelda:
- Ro'yxatda 4 ta ustun ko'rinadi
- Filtrlar sidebar'da
- Qidiruv maydoni tepada
- Sana bo'yicha drilldown

### Admin Customization (Qisqacha)

Admin juda ko'p customization imkoniyatlarini taqdim etadi:

**List display customization:**
- Custom metodlar qo'shish
- Related field'larni ko'rsatish
- Boolean field'larni ikonka sifatida
- Color coding

**Filters va search:**
- Custom filter'lar yaratish
- Autocomplete search
- Advanced search

**Inline editing:**
- Related modellarni bir sahifada tahrirlash
- Tabular yoki stacked layout

**Actions:**
- Ommaviy amallar (bulk actions)
- Custom admin action'lar yaratish
- Export/import funksiyalari

**Permissions:**
- Model-level permissions
- Object-level permissions
- Custom permission'lar

**Appearance:**
- Custom CSS/JS
- Template override
- Third-party packages (django-admin-tools, django-grappelli)

Admin panelning bu kuchi Django'ni juda mashhur CMS platformasi qiladi. Ko'plab loyihalar faqat Django admin'ni ishlatib, alohida admin panel yaratmaydi.

## 12. Yakuniy Xulosa

### Django Arxitekturasi Nimani Osonlashtiradi?

Django arxitekturasi web dasturlashning murakkabliklarini yashiradi va dasturchilar uchun qulay muhit yaratadi:

**1. Tezkor prototiplash:**
Django bilan fikringizni bir necha soatda ishlaydigan prototypega aylantirishingiz mumkin. Migrations, admin, ORM — barchasi tayyor.

**2. Xavfsizlik:**
Django ko'plab xavfsizlik xususiyatlarini default qo'shadi: SQL injection, XSS, CSRF, clickjacking himoyasi. Siz qo'shimcha harakat qilmasdan xavfsiz kod yozasiz.

**3. Scalability:**
Django arxitekturasi katta loyihalar uchun mo'ljallangan. Instagram, Pinterest, Spotify Django'da yozilgan.

**4. DRY (Don't Repeat Yourself):**
Django sizni kod takrorlamaslikka undaydi. Template inheritance, model methods, mixins — barchasi kodingizni tozaroq qiladi.

**5. Batteries included:**
Ko'plab funksiyalar dastlab mavjud: auth, admin, forms, messages, sessions. Siz faqat biznes mantiqga e'tibor berasiz.

**6. Community va packages:**
Django juda katta community'ga ega. Har qanday muammo uchun tayyor package yoki tutorial topishingiz mumkin.

### Nima Uchun Startuplar Django Tanlaydi?

**1. Tezlik:**
Startup'lar tez MVP (Minimum Viable Product) yaratishlari kerak. Django bunga eng yaxshi vosita.

**2. Kichik jamoa:**
Django bilan kichik jamoa katta natijaga erishishi mumkin. Bir dasturchi full-stack yozishi mumkin.

**3. Narx samaradorligi:**
Python va Django bepul. Hosting arzon. Development tez. Bu startup budget'i uchun ideal.

**4. Miqyoslash:**
Startup o'sishi bilan Django ham o'sadi. Mikroservisga o'tish oson.

**5. Developer happiness:**
Django "beginner-friendly" va "developer happiness" ta'kidlaydi. Bu kod yozishni zavqli qiladi.

**Real misollar:**

- **Instagram**: Eng katta Django loyiha. Millionlab foydalanuvchi, millionlab foto/video.
- **Pinterest**: Katta trafik, murakkab recommendation tizimi.
- **Spotify**: Music streaming platform.
- **Dropbox**: File storage va sharing.
- **Mozilla**: Firefox support saytlari.

Bularning barchasi Django bilan ishlaydi va katta scale'da muvaffaqiyatli.

### Keyingi Darsda Nimalar Qilinadi?

Endi siz Django arxitekturasi nazariyasini yaxshi bilib oldingiz. Keyingi darslar amaliy bo'ladi:

**Dars 2: Django'da Model yaratish va Ma'lumotlar Bazasi bilan Ishlash**
- Model field turlari
- Relationships (ForeignKey, ManyToMany, OneToOne)
- Migration'lar bilan ishlash
- QuerySet API to'liq qo'llanma
- Database optimization

**Dars 3: Django Views va URL Routing**
- Function-based vs Class-based views
- Generic views
- URL parameters va routing patterns
- Request va Response obyektlari
- Middleware yaratish

**Dars 4: Django Templates va Forms**
- Template inheritance va tags
- Custom template tags va filters
- Django Forms va ModelForms
- Form validation
- File upload handling

**Dars 5: Django Admin Customization**
- Admin interface'ni to'liq sozlash
- Inline editing
- Custom admin actions
- Permissions va groups

**Dars 6: Django REST Framework (API yaratish)**
- RESTful API asoslari
- Serializers
- ViewSets va Routers
- Authentication va Permissions
- API documentation

**Dars 7: Django Authentication va Authorization**
- User model bilan ishlash
- Custom user model yaratish
- Login/Logout/Register funksiyalari
- Password reset
- Social authentication

**Dars 8: Django Testing**
- Unit tests
- Integration tests
- Test fixtures
- Coverage
- CI/CD integration

**Dars 9: Django Deployment**
- Production settings
- Static files management
- Database migration production'da
- Gunicorn + Nginx
- Docker va containerization
- Cloud deployment (AWS, DigitalOcean, Heroku)

**Dars 10: Django Best Practices va Optimization**
- Code organization
- Security best practices
- Performance optimization
- Caching strategies
- Monitoring va logging

### Muhim Xulosa

Django — bu shunchaki framework emas, balki to'liq "filozofiya". U sizga tizimli fikrlashni, strukturalashtirilgan kod yozishni o'rgatadi. Django bilan ishlash Python community'ning eng yaxshi practice'larini o'rganish demakdir.

Agar siz Django arxitekturasini yaxshi tushungan bo'lsangiz, boshqa framework'lar (Flask, FastAPI, Express.js, Spring) ni ham tez o'rganasiz, chunki ko'pchilik MVC/MTV patterniga amal qiladi.

Django o'rganish — bu investitsiya. Bir marta yaxshi o'rgansangiz, yillar davomida foydasi bo'ladi. Web dasturlash olamida Django hali ham eng mashhur va eng samarali framework'lardan biri hisoblanadi.