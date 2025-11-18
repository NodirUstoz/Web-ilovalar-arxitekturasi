# Django 1-amaliy dars

## Kirish: Django nima va nega kerak?

Django — bu Python dasturlash tilida yozilgan bepul va ochiq kodli web framework (ramka). Framework deganda — oldindan tayyor qisman qurilgan uy deb tasavvur qilishingiz mumkin. Sizga faqat o'z xonalaringizni bezash va jihozlash qoladi. Django esa web ilovalar yaratish uchun barcha kerakli asos va qurilma-asboblarni taqdim etadi.

### Real hayot analogiyasi

Tasavvur qiling, siz restoran ochmoqchisiz:

- **Django** — bu tayyor restoran binosi, oshxona jihozlari, menyular tizimi
- **Sizning vazifangiz** — maxsus taomlar retseptlarini yaratish va xizmat ko'rsatish
- **Django'ning vazifasi** — barcha texnik ishlarni (buyurtmalarni qabul qilish, oshxonaga yetkazish, hisobni chiqarish) avtomatik bajarish

### Django bilan qurilgan mashhur saytlar

Django juda kuchli va ishonchli platformadir. Quyidagi taniqli saytlar Django yordamida qurilgan:

- **Instagram** — dastlab to'liq Django asosida ishlab chiqilgan
- **Pinterest** — foydalanuvchilar ma'lumotlarini boshqarish uchun Django ishlatadi
- **Mozilla Support** — Firefox brauzerining qo'llab-quvvatlash sayti
- **Disqus** — ko'plab saytlarda ko'radigan sharhlar tizimi
- **The Washington Post** — amerika gazetasining web platformasi

### Nega aynan Django?

1. **Batteries included** — barcha kerakli narsalar tayyor
2. **Xavfsizlik** — SQL injection, XSS kabi hujumlardan himoya
3. **Tezkor ishlab chiqish** — bir haftada to'liq loyiha yaratish mumkin
4. **Katta jamoa** — dunyoda millionlab dasturchilar Django ishlatadi
5. **Yaxshi hujjatlar** — har bir mavzu batafsil yozilgan

---

## Web ilovalarning umumiy arxitekturasi

Web ilovalar qanday ishlashini tushunish juda muhim. Keling, bosqichma-bosqich ko'rib chiqaylik.

### Client → Server → Database modeli

```
[Foydalanuvchi brauzerda]
         ↓ (HTTP so'rov yuboradi)
[Server - Django ilova]
         ↓ (Ma'lumot so'raydi)
[Database - Ma'lumotlar bazasi]
         ↓ (Ma'lumot qaytaradi)
[Server - Django HTML yasaydi]
         ↓ (HTTP javob qaytaradi)
[Foydalanuvchi HTML sahifani ko'radi]
```

### HTTP sikli

HTTP (HyperText Transfer Protocol) — bu brauzer va server o'rtasida qanday "gaplashishni" belgilaydigan qoidalar to'plami.

**Oddiy misol:**

Siz brauzerda `example.com/products` ni ochasiz:

1. **Request (So'rov):** Brauzer serverga "menga products sahifasini ber" deb so'rov yuboradi
2. **Processing (Ishlov):** Server ma'lumotlar bazasidan mahsulotlarni oladi
3. **Response (Javob):** Server HTML sahifa yasaydi va qaytaradi
4. **Rendering (Ko'rsatish):** Brauzer HTML ni chiroyli sahifaga aylantiradi

### Backend vs Frontend

**Backend** — bu foydalanuvchi ko'rmaydigan, server tomonidagi dastur:
- Ma'lumotlar bazasi bilan ishlash
- Foydalanuvchi tizimga kirganini tekshirish
- Biznes mantiq (masalan: to'lov hisoblash)
- Django — backend framework

**Frontend** — bu foydalanuvchi ko'radigan va o'zaro ta'sir qiladigan qism:
- HTML (sahifa tuzilishi)
- CSS (dizayn, ranglar)
- JavaScript (harakatlar, animatsiyalar)

### Template-Based rendering nima?

Django **Template-Based** tizim ishlatadi. Bu shuni anglatadiki:

1. Server HTML fayllarni oldindan tayyorlaydi
2. Kerakli ma'lumotlarni ma'lumotlar bazasidan olib, HTML ga joylashtiradi
3. Tayyor HTML ni brauzerga yuboradi
4. Brauzer faqat ko'rsatish bilan shug'ullanadi

**Misol:**

```python
# Django serverdagi kod
products = ["Olma", "Nok", "Uzum"]

# HTML template fayliga uzatiladi
# Template bu ro'yxatni HTML jadvalga aylantiradi
# Tayyor HTML brauzerga yuboriladi
```

**Alternative:** SPA (Single Page Application) — React, Vue kabi texnologiyalarda HTML frontendda yaratiladi, Django faqat JSON ma'lumot yuboradi. Lekin bu darsda biz Template-Based usulni o'rganamiz.

---

## Django arxitekturasi (MTV pattern)

Django **MTV** arxitekturasini ishlatadi:
- **M**odel — ma'lumotlar bazasi bilan ishlash
- **T**emplate — HTML sahifalar
- **V**iew — biznes mantiq

### MTV vs MVC farqi

Ko'plab frameworklar MVC (Model-View-Controller) ishlatadi. Django ham xuddi shunday ishlaydi, lekin nomlar farq qiladi:

| MVC atamasi | Django MTV atamasi | Vazifasi |
|-------------|-------------------|----------|
| Model | Model | Ma'lumotlar bazasi |
| View | Template | Foydalanuvchi ko'radigan sahifa |
| Controller | View | Mantiq va boshqaruv |

### Django request-response sikli

```
Foydalanuvchi brauzerni ochadi
         ↓
http://localhost:8000/about/
         ↓
URL dispatcher (urls.py)
         ↓ (qaysi View ni chaqirish kerak?)
View funksiyasi (views.py)
         ↓ (ma'lumot kerakmi?)
Model (models.py) → Database
         ↓ (ma'lumot olindi)
View ma'lumotni Template ga uzatadi
         ↓
Template (HTML fayl) tayyor HTML yasaydi
         ↓
View HTTP Response qaytaradi
         ↓
Brauzer sahifani ko'rsatadi
```

### Har bir qismning vazifasi

**1. Model (models.py)**
```python
# Mahsulot haqida ma'lumotlarni saqlash
class Product:
    nomi = "Olma"
    narxi = 5000
    soni = 100
```

**2. View (views.py)**
```python
# Foydalanuvchi so'rovini qabul qilish
# Ma'lumot bazasidan kerakli mahsulotlarni olish
# Template ga yuborish
```

**3. Template (home.html)**
```html
<!-- View dan kelgan ma'lumotlarni chiroyli ko'rinishda ko'rsatish -->
<h1>Mahsulot: {{ mahsulot_nomi }}</h1>
<p>Narxi: {{ mahsulot_narxi }} so'm</p>
```

**4. URL (urls.py)**
```python
# Qaysi URL qaysi View ga bog'langan
# /products/ → products_view funksiyasi
# /about/ → about_view funksiyasi
```

---

## Django o'rnatish — OS-lar bo'yicha buyruqlar

Django bilan ishlashdan oldin, muhitni to'g'ri sozlash kerak. Har bir operatsion tizim uchun alohida ko'rsatmalar beramiz.

### 1-qadam: Python versiyasini tekshirish

Django ishlashi uchun Python 3.8 yoki undan yuqori versiya kerak.

#### ✔ Windows (PowerShell)

```powershell
python --version
```

**Expected output:**
```
Python 3.11.4
```

**Agar Python o'rnatilmagan bo'lsa:**
- python.org saytidan yuklab oling
- O'rnatishda "Add Python to PATH" ni belgilang

#### ✔ Linux (Ubuntu)

```bash
python3 --version
```

**Expected output:**
```
Python 3.10.12
```

**Agar Python o'rnatilmagan bo'lsa:**
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

#### ✔ macOS (zsh)

```zsh
python3 --version
```

**Expected output:**
```
Python 3.11.5
```

**Agar Python o'rnatilmagan bo'lsa:**
```zsh
# Homebrew orqali
brew install python3
```

---

### 2-qadam: Virtual environment yaratish

Virtual environment — bu loyihangiz uchun alohida Python muhiti. Tasavvur qiling, har bir loyiha uchun alohida xona. Bir xonadagi narsalar boshqa xonaga ta'sir qilmaydi.

**Nega kerak?**
- Har bir loyihada turli Django versiyalari bo'lishi mumkin
- Kerakli kutubxonalar faqat shu loyihada bo'ladi
- Tizimning asosiy Python muhitini buzmaslik

#### ✔ Windows (PowerShell)

**Virtual environment yaratish:**
```powershell
python -m venv venv
```

**Line-by-line tushuntirish:**
- `python` — Python interpreterni chaqirish
- `-m venv` — venv modulini ishga tushirish (virtual environment yaratuvchi)
- `venv` — yaratilayotgan papkaning nomi

**Virtual environment ni faollashtirish:**
```powershell
.\venv\Scripts\Activate.ps1
```

**Expected output:**
```
(venv) PS C:\Users\User\backend>
```

**Izoh:** `(venv)` belgisi chiqishi kerak — bu virtual environment faol ekanligini bildiradi.

**Agar PowerShell xatolik bersa (Execution Policy):**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

Bu xavfsizlik sozlamalarini o'zgartiradi va scriptlarni ishga tushirishga ruxsat beradi.

#### ✔ Linux (Ubuntu)

**Virtual environment yaratish:**
```bash
python3 -m venv venv
```

**Virtual environment ni faollashtirish:**
```bash
source venv/bin/activate
```

**Expected output:**
```
(venv) user@ubuntu:~/backend$
```

**Izoh:** `(venv)` terminal boshida paydo bo'ladi.

#### ✔ macOS (zsh)

**Virtual environment yaratish:**
```zsh
python3 -m venv venv
```

**Virtual environment ni faollashtirish:**
```zsh
source venv/bin/activate
```

**Expected output:**
```
(venv) username@MacBook backend %
```

---

### 3-qadam: Django o'rnatish

Virtual environment faol bo'lganidan keyin Django o'rnatamiz.

#### ✔ Windows

```powershell
pip install django
```

**Expected output:**
```
Collecting django
  Downloading Django-5.0.1-py3-none-any.whl (8.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 8.2/8.2 MB 5.1 MB/s eta 0:00:00
Collecting asgiref<4,>=3.7.0
...
Successfully installed Django-5.0.1 asgiref-3.7.2 sqlparse-0.4.4
```

**Django versiyasini tekshirish:**
```powershell
django-admin --version
```

**Expected output:**
```
5.0.1
```

#### ✔ Linux

```bash
pip3 install django
```

**Django versiyasini tekshirish:**
```bash
django-admin --version
```

#### ✔ macOS

```zsh
pip3 install django
```

**Django versiyasini tekshirish:**
```zsh
django-admin --version
```

---

### Keng tarqalgan xatolar va ularning yechimlari

**1. ModuleNotFoundError: No module named 'django'**

**Sabab:** Virtual environment faol emas yoki Django o'rnatilmagan.

**Yechim:**
```bash
# Avval venv ni faollashtiring
source venv/bin/activate  # Linux/macOS
.\venv\Scripts\Activate.ps1  # Windows

# Keyin Django ni o'rnating
pip install django
```

**2. 'django-admin' is not recognized as an internal or external command**

**Sabab:** Django PATH ga qo'shilmagan.

**Yechim Windows:**
```powershell
python -m django --version
```

**Yechim Linux/macOS:**
```bash
python3 -m django --version
```

**3. Permission denied (macOS/Linux)**

**Sabab:** Fayl ruxsatlari muammosi.

**Yechim:**
```bash
# sudo ishlatmang! Virtual environment ichida ishlashingizga ishonch hosil qiling
which python  # /home/user/backend/venv/bin/python ko'rsatishi kerak
```

---

## Folder yaratish — tartibli arxitektura

Professional dasturchilar loyihalarini tartibli qilishadi. Keling, to'g'ri papka strukturasini yarataylik.

### Loyiha papkasi yaratish

#### ✔ Windows (PowerShell)

```powershell
# Desktop ga o'ting
cd Desktop

# backend papkasini yarating
mkdir backend

# Papkaga kiring
cd backend
```

#### ✔ Linux

```bash
cd ~/Desktop
mkdir backend
cd backend
```

#### ✔ macOS

```zsh
cd ~/Desktop
mkdir backend
cd backend
```

### Virtual environment yaratish (yana bir bor eslatma)

```bash
# Barcha OS uchun
python -m venv venv  # Windows
python3 -m venv venv  # Linux/macOS
```

### Expected folder structure (venv yaratilgandan keyin)

```
backend/
│
├── venv/                 # Virtual environment (bu papkaga kirmaslik kerak)
│   ├── Include/
│   ├── Lib/
│   ├── Scripts/          # Windows
│   └── bin/              # Linux/macOS
│
└── (keyinchalik Django project yaratamiz)
```

**Muhim qoidalar:**

1. **venv papkasiga kirmaslik** — bu avtomatik yaratilgan fayllar
2. **venv ni Git ga qo'shmaslik** — `.gitignore` faylda yoziladi
3. **Har bir yangi loyiha uchun yangi venv yaratish**

---

## Django project yaratish (startproject)

Endi asl Django loyihasini yaratish vaqti keldi. Django project — bu barcha sozlamalar va konfiguratsiyalar joylashgan asosiy papka.

### Project yaratish buyrug'i

#### ✔ Barcha OS uchun bir xil

Virtual environment faol ekanligiga ishonch hosil qiling `(venv)` belgisi ko'rinishi kerak.

```bash
django-admin startproject config .
```

**Line-by-line tushuntirish:**
- `django-admin` — Django ning boshqaruv vositasi
- `startproject` — yangi project yaratish buyrug'i
- `config` — project papkasining nomi (o'zingiz ixtiyoriy nom berishingiz mumkin: mysite, core, project)
- `.` — nuqta — hozirgi papkada yaratish (agar nuqta bo'lmasa, qo'shimcha papka yaratadi)

**Expected output:**

Terminal hech narsa chiqarmaydi, lekin yangi fayllar yaratiladi.

### Yaratilgan fayllarni ko'rish

```bash
# Windows
dir

# Linux/macOS
ls -la
```

**Expected folder structure:**

```
backend/
│
├── venv/
│
├── config/                    # Asosiy sozlamalar papkasi
│   ├── __init__.py           # Python package belgisi (bo'sh fayl)
│   ├── asgi.py               # ASGI server konfiguratsiyasi
│   ├── settings.py           # Barcha sozlamalar (eng muhim!)
│   ├── urls.py               # Asosiy URL marshrutlari
│   └── wsgi.py               # WSGI server konfiguratsiyasi
│
└── manage.py                  # Loyihani boshqarish vositasi
```

### Har bir fayl nima qiladi?

#### 1. manage.py

**Vazifasi:** Django loyihasini boshqarish uchun CLI (Command Line Interface) vositasi.

**Misol buyruqlar:**
```bash
python manage.py runserver     # Serverni ishga tushirish
python manage.py makemigrations  # Migration fayllarini yaratish
python manage.py migrate       # Ma'lumotlar bazasini yangilash
python manage.py createsuperuser  # Admin foydalanuvchi yaratish
```

**Oddiy analogiya:** manage.py — bu mashinangiz uchun boshqaruv pulti. Har bir tugma (buyruq) ma'lum vazifani bajaradi.

**Fayl ichidagi kod (qisqartirilgan):**
```python
#!/usr/bin/env python
import os
import sys

def main():
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'config.settings')
    # Django ni ishga tushirish
    from django.core.management import execute_from_command_line
    execute_from_command_line(sys.argv)

if __name__ == '__main__':
    main()
```

**Line-by-line izoh:**
- `os.environ.setdefault(...)` — Django ga qaysi settings faylni ishlatishni aytadi
- `'config.settings'` — config papkasidagi settings.py faylni anglatadi
- `execute_from_command_line(sys.argv)` — terminal buyruqlarini bajaradi

---

#### 2. config/settings.py

**Vazifasi:** Loyihaning barcha sozlamalari. Bu fayl juda muhim!

**Fayl tuzilishi (asosiy qismlari):**

```python
# settings.py

import os
from pathlib import Path

# Loyihaning asosiy papkasini aniqlash
BASE_DIR = Path(__file__).resolve().parent.parent

# Xavfsizlik kaliti (maxfiy saqlash kerak!)
SECRET_KEY = 'django-insecure-7f3x...'

# Debug rejimi (ishlab chiqishda True, production da False)
DEBUG = True

# Qaysi domenlardan kirishga ruxsat
ALLOWED_HOSTS = []

# O'rnatilgan ilovalar ro'yxati
INSTALLED_APPS = [
    'django.contrib.admin',        # Admin panel
    'django.contrib.auth',         # Foydalanuvchilar tizimi
    'django.contrib.contenttypes', # Content types framework
    'django.contrib.sessions',     # Session boshqaruvi
    'django.contrib.messages',     # Xabarlar tizimi
    'django.contrib.staticfiles',  # Static fayllar (CSS, JS, images)
]

# Middleware (so'rov va javob orasida ishlaydigan qatlamlar)
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

# Asosiy URL konfiguratsiya fayli
ROOT_URLCONF = 'config.urls'

# Template sozlamalari
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],  # Keyinchalik templates papkasini qo'shamiz
        'APP_DIRS': True,  # Har bir app ichidan templates qidirish
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

# WSGI application
WSGI_APPLICATION = 'config.wsgi.application'

# Ma'lumotlar bazasi (default: SQLite)
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Parol quvvatliligi tekshiruvi
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    # ... boshqa validatorlar
]

# Til va vaqt mintaqasi
LANGUAGE_CODE = 'uz-uz'  # O'zbek tilini sozlash mumkin
TIME_ZONE = 'Asia/Tashkent'
USE_I18N = True
USE_TZ = True

# Static fayllar (CSS, JavaScript, Images)
STATIC_URL = 'static/'

# Default primary key field type
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```

**Eng muhim sozlamalar:**

1. **DEBUG = True** — Xatoliklarni batafsil ko'rsatadi (faqat development da)
2. **INSTALLED_APPS** — Loyihadagi barcha ilovalar ro'yxati
3. **DATABASES** — Ma'lumotlar bazasi sozlamalari
4. **TEMPLATES** — HTML fayllar joylashgan papkalar

---

#### 3. config/urls.py

**Vazifasi:** URL manzillarini View funksiyalariga bog'lash.

**Default kod:**

```python
# urls.py

from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

**Line-by-line tushuntirish:**
- `from django.contrib import admin` — Admin panelni import qilish
- `from django.urls import path` — URL yaratish funksiyasini import qilish
- `urlpatterns = [...]` — Barcha URL marshrutlari shu ro'yxatda
- `path('admin/', admin.site.urls)` — `http://localhost:8000/admin/` manzili admin panelga olib boradi

**Oddiy analogiya:** urls.py — bu yo'l xaritasi. Har bir manzil (URL) qayerga olib borishini ko'rsatadi.

---

#### 4. config/wsgi.py va asgi.py

**WSGI (Web Server Gateway Interface):**
- Django ilovani web server bilan bog'laydi
- Klassik HTTP so'rovlar uchun
- Gunicorn, uWSGI kabi serverlar ishlatadi

**ASGI (Asynchronous Server Gateway Interface):**
- Asinxron so'rovlar uchun (WebSockets, HTTP/2)
- Zamonaviy real-time ilovalar uchun
- Daphne, Uvicorn kabi serverlar ishlatadi

**Hozircha bu fayllarni o'zgartirmaslik kerak.**

---

### Keng tarqalgan xatolar

**1. "django-admin: command not found"**

**Yechim:**
```bash
python -m django startproject config .
```

**2. Project yaratildi, lekin noto'g'ri joyda**

**Sabab:** Nuqtani (.) unutgan bo'lsangiz, qo'shimcha papka yaratiladi.

**Yechim:**
```bash
# Noto'g'ri papkani o'chiring
rm -rf config

# To'g'ri qaytadan yarating
django-admin startproject config .
```

**3. "config/" papkasi allaqachon mavjud**

**Yechim:**
```bash
# Eski papkani o'chiring
rm -rf config

# Yangi yarating
django-admin startproject config .
```

---

## App yaratish (startapp main)

Django da **Project** va **App** farqi muhim:

- **Project** — butun website (masalan: internet do'kon)
- **App** — loyiha ichidagi alohida modul (masalan: mahsulotlar, foydalanuvchilar, to'lovlar)

**Oddiy analogiya:**
- Project = Bino
- App = Binoдаgi xonalar (oshxona, yotoq xona, mehmon xona)

### App yaratish buyrug'i

#### ✔ Barcha OS uchun bir xil

```bash
# Windows
python manage.py startapp main

# Linux/macOS
python3 manage.py startapp main
```

**Line-by-line tushuntirish:**
- `python manage.py` — manage.py orqali Django buyruqlarini bajarish
- `startapp` — yangi ilova yaratish buyrug'i
- `main` — ilova nomi (siz blog, shop, users kabi nomlar berishingiz mumkin)

**Expected output:**

Terminal hech narsa chiqarmaydi, lekin yangi papka yaratiladi.

### Expected folder structure

```
backend/
│
├── config/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── main/                      # Yangi yaratilgan app
│   ├── migrations/            # Ma'lumotlar bazasi o'zgarishlari
│   │   └── __init__.py
│   ├── __init__.py           # Python package belgisi
│   ├── admin.py              # Admin panel sozlamalari
│   ├── apps.py               # App konfiguratsiyasi
│   ├── models.py             # Ma'lumotlar bazasi modellari
│   ├── tests.py              # Test kodlari
│   └── views.py              # View funksiyalari (biznes mantiq)
│
├── venv/
└── manage.py
```

### Har bir faylning vazifasi

#### 1. main/views.py

**Vazifasi:** Foydalanuvchi so'rovini qabul qilish va javob qaytarish.

**Default kod:**

```python
from django.shortcuts import render

# Create your views here.
```

**Biz keyinchalik bu faylga funksiyalar qo'shamiz.**

---

#### 2. main/models.py

**Vazifasi:** Ma'lumotlar bazasi jadvallarini Python klasslari sifatida yozish.

**Default kod:**

```python
from django.db import models

# Create your models here.
```

**Misol (keyinchalik yozamiz):**
```python
class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
```

Bu kod ma'lumotlar bazasida "Post" degan jadval yaratadi.

---

#### 3. main/admin.py

**Vazifasi:** Modellarni admin panelda ko'rsatish.

**Default kod:**

```python
from django.contrib import admin

# Register your models here.
```

---

#### 4. main/apps.py

**Vazifasi:** App konfiguratsiyasi.

```python
from django.apps import AppConfig

class MainConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'main'
```

**Line-by-line tushuntirish:**
- `class MainConfig(AppConfig)` — App sozlamalarini o'z ichiga oladi
- `name = 'main'` — App ning nomi (INSTALLED_APPS ga qo'shishda kerak bo'ladi)

---

#### 5. main/migrations/

**Vazifasi:** Ma'lumotlar bazasi o'zgarishlarini kuzatish.

Har safar model o'zgartirilganda, migration fayl yaratiladi. Bu fayl ma'lumotlar bazasini yangilaydi.

---

### App ni INSTALLED_APPS ga qo'shish (MAJBURIY!)

App yaratgach, uni `config/settings.py` da ro'yxatdan o'tkazish kerak. Aks holda Django uni ko'rmaydi!

**config/settings.py faylini oching va INSTALLED_APPS ga qo'shing:**

```python
# config/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    
    # O'zimizning app lari
    'main',  # ← Bu qatorni qo'shing
]
```

**Line-by-line tushuntirish:**
- Django default app lardan keyin vergul qo'yamiz
- `'main',` — bu bizning app imizning nomi
- Vergulni unutmaslik kerak!

**Alternativ yozish usuli (tavsiya etiladi):**

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    
    # Local apps
    'main.apps.MainConfig',  # To'liq yo'l
]
```

Bu usul app konfiguratsiyasini aniqroq ko'rsatadi.

---

### Keng tarqalgan xatolar

**1. App yaratilmadi**

**Sabab:** manage.py faylidan emas, noto'g'ri papkadan buyruq berilgan.

**Yechim:**
```bash
# manage.py bor papkada ekanligingizga ishonch hosil qiling
ls  # manage.py ko'rinishi kerak

# Agar yo'qolgan bo'lsangiz
cd backend
python manage.py startapp main
```

**2. "No module named 'main'"**

**Sabab:** App INSTALLED_APPS ga qo'shilmagan.

**Yechim:**
```python
# config/settings.py
INSTALLED_APPS = [
    ...
    'main',  # ← Buni qo'shishni unutmang
]
```

**3. Bir nechta app yaratish**

Bitta loyihada ko'p app bo'lishi mumkin:

```bash
python manage.py startapp blog
python manage.py startapp shop
python manage.py startapp users
```

Har birini INSTALLED_APPS ga qo'shish kerak:

```python
INSTALLED_APPS = [
    ...
    'blog',
    'shop',
    'users',
]
```

---

## Birinchi view yaratish (home)

View — bu foydalanuvchi so'roviga javob qaytaradigan funksiya. Oddiy qilib aytganda, view "qaysi sahifa ochilsin" degan savolga javob beradi.

### HttpResponse bilan oddiy view yaratish

**main/views.py faylini oching va quyidagi kodni yozing:**

```python
# main/views.py

from django.http import HttpResponse

def home(request):
    return HttpResponse("<h1>Salom, Django!</h1>")
```

### Line-by-line tushuntirish

```python
from django.http import HttpResponse
```
- `from django.http` — Django ning HTTP moduli
- `HttpResponse` — Brauzerga oddiy matn/HTML qaytarish uchun klass
- Import qilmasdan ishlatib bo'lmaydi

```python
def home(request):
```
- `def home` — funksiya nomi (siz ixtiyoriy nom qo'yishingiz mumkin: index, main_page, welcome)
- `(request)` — har bir view funksiyasi **request** parametrini majburiy qabul qiladi
- `request` — bu foydalanuvchining so'rovi haqida ma'lumot (qaysi URL, qanday method: GET/POST, cookie lar va h.k.)

```python
return HttpResponse("<h1>Salom, Django!</h1>")
```
- `HttpResponse(...)` — Javob yaratish
- `"<h1>Salom, Django!</h1>"` — HTML kod, brauzerda katta sarlavha ko'rinadi
- `return` — bu javobni qaytarish (har bir view funksiyasi biror narsa qaytarishi shart)

### Qo'shimcha misollar

**Misol 1: Oddiy matn**

```python
def about(request):
    return HttpResponse("Bu about sahifasi")
```

**Misol 2: Ko'p qatorli HTML**

```python
def contact(request):
    html = """
    <html>
        <head><title>Bog'lanish</title></head>
        <body>
            <h1>Biz bilan bog'laning</h1>
            <p>Email: info@example.com</p>
            <p>Tel: +998 90 123 45 67</p>
        </body>
    </html>
    """
    return HttpResponse(html)
```

**Line-by-line tushuntirish:**
- `html = """..."""` — ko'p qatorli matn uchun uchta qo'shtirnoq
- `return HttpResponse(html)` — tayyorlangan HTML ni qaytarish

**Misol 3: Request obyektidan foydalanish**

```python
def user_info(request):
    browser = request.META.get('HTTP_USER_AGENT', 'Noma'lum')
    html = f"<h1>Siz {browser} brauzeridan kiryapsiz</h1>"
    return HttpResponse(html)
```

**Line-by-line tushuntirish:**
- `request.META` — HTTP headers (brauzer, IP va h.k.)
- `'HTTP_USER_AGENT'` — Brauzer nomi
- `f"..."` — f-string (Python 3.6+), o'zgaruvchilarni matn ichiga joylashtirish

---

### Keng tarqalgan xatolar

**1. "name 'HttpResponse' is not defined"**

**Sabab:** Import qilishni unutgan.

**Yechim:**
```python
from django.http import HttpResponse  # ← Bu qatorni qo'shing
```

**2. "home() takes 0 positional arguments but 1 was given"**

**Sabab:** `request` parametrini yozishni unutgan.

**Noto'g'ri:**
```python
def home():  # ← Noto'g'ri
    return HttpResponse("Salom")
```

**To'g'ri:**
```python
def home(request):  # ← To'g'ri
    return HttpResponse("Salom")
```

**3. View funksiyasi hech narsa qaytarmaydi**

**Sabab:** `return` yo'q.

**Noto'g'ri:**
```python
def home(request):
    HttpResponse("Salom")  # ← return yo'q
```

**To'g'ri:**
```python
def home(request):
    return HttpResponse("Salom")  # ← return bor
```

---

## URL bilan bog'lash

View funksiyasini yaratdik, lekin brauzerda ochish uchun uni URL bilan bog'lash kerak.

### App ichida urls.py yaratish

Django default holda app ichida `urls.py` fayl yaratmaydi. Biz uni qo'lda yaratamiz.

#### ✔ Windows

```powershell
# main papkasida yangi fayl yaratish
New-Item -Path main/urls.py -ItemType File
```

#### ✔ Linux/macOS

```bash
touch main/urls.py
```

### main/urls.py faylini yozish

**main/urls.py ga quyidagi kodni yozing:**

```python
# main/urls.py

from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
```

### Line-by-line tushuntirish

```python
from django.urls import path
```
- `path` — URL marshrut yaratish funksiyasi

```python
from . import views
```
- `.` — hozirgi papka (main papkasi)
- `import views` — main/views.py faylni import qilish
- Bu qator orqali views.py dagi barcha funksiyalarga murojaat qilish mumkin

```python
urlpatterns = [
```
- `urlpatterns` — bu nom majburiy! Django faqat shu nomli ro'yxatni izlaydi
- `[...]` — ro'yxat (list), bir nechta URL marshrutlarini saqlaydi

```python
path('', views.home, name='home'),
```
- `path(...)` — bitta URL marshrut yaratish
- `''` — bo'sh string — bu asosiy sahifa (`http://localhost:8000/`)
- `views.home` — qaysi view funksiyasi ishga tushsin (main/views.py dagi home funksiyasi)
- `name='home'` — bu URL ga nom berish (template larda ishlatish uchun)

**To'liq tushuntirish:**

Foydalanuvchi brauzerda `http://localhost:8000/` ni ochganda:
1. Django `main/urls.py` ga qaradi
2. `path('', ...)` ni topadi
3. `views.home` funksiyasini ishga tushiradi
4. `home` funksiyasi `HttpResponse` qaytaradi
5. Brauzerda "Salom, Django!" ko'rinadi

---

### Project urls.py ga ulash (include)

Endi `main/urls.py` ni asosiy `config/urls.py` ga bog'lash kerak.

**config/urls.py faylini oching va o'zgartiring:**

```python
# config/urls.py

from django.contrib import admin
from django.urls import path, include  # include ni qo'shdik

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),  # ← Bu qatorni qo'shing
]
```

### Line-by-line tushuntirish

```python
from django.urls import path, include
```
- `include` — boshqa urls.py faylni ulash uchun funksiya

```python
path('', include('main.urls')),
```
- `''` — asosiy URL (/) uchun
- `include('main.urls')` — main app idagi urls.py ni ulash
- `'main.urls'` — main papkasidagi urls.py fayl

**Alternativ misollar:**

```python
# Agar barcha main sahifalar /app/ bilan boshlansin
path('app/', include('main.urls')),

# Bu holda:
# http://localhost:8000/app/ → main/urls.py dagi '' path
# http://localhost:8000/app/about/ → main/urls.py dagi 'about/' path
```

---

### URL marshrutlari qanday ishlaydi?

**Misol 1: Asosiy sahifa**

```
Foydalanuvchi: http://localhost:8000/
Django:
  1. config/urls.py → path('', include('main.urls'))
  2. main/urls.py → path('', views.home)
  3. main/views.py → home funksiyasi
  4. HttpResponse("<h1>Salom, Django!</h1>")
```

**Misol 2: Ko'p sahifalar**

**main/views.py:**

```python
from django.http import HttpResponse

def home(request):
    return HttpResponse("<h1>Bosh sahifa</h1>")

def about(request):
    return HttpResponse("<h1>Biz haqimizda</h1>")

def contact(request):
    return HttpResponse("<h1>Bog'lanish</h1>")
```

**main/urls.py:**

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),
    path('contact/', views.contact, name='contact'),
]
```

**Natija:**
- `http://localhost:8000/` → Bosh sahifa
- `http://localhost:8000/about/` → Biz haqimizda
- `http://localhost:8000/contact/` → Bog'lanish

---

### Keng tarqalgan xatolar

**1. "Page not found (404)" — URL topilmadi**

**Sabab 1:** main/urls.py yaratilmagan yoki config/urls.py ga ulanmagan.

**Yechim:**
```python
# config/urls.py
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('main.urls')),  # ← Buni tekshiring
]
```

**Sabab 2:** views.py da funksiya nomi bilan urls.py da yozilgan nom mos kelmaydi.

**Yechim:**
```python
# views.py
def home(request):  # funksiya nomi: home
    ...

# urls.py
path('', views.home, name='home'),  # views.home - to'g'ri
```

**2. "Reverse for 'home' not found"**

**Sabab:** `name='home'` yozilmagan yoki noto'g'ri yozilgan.

**Yechim:**
```python
path('', views.home, name='home'),  # name qo'shilishi shart
```

**3. "ModuleNotFoundError: No module named 'main.urls'"**

**Sabab:** main papkasida urls.py fayl mavjud emas.

**Yechim:**
```bash
# Faylni yaratish
touch main/urls.py  # Linux/macOS
New-Item -Path main/urls.py -ItemType File  # Windows
```

---

## Migrations — Ma'lumotlar bazasini tayyorlash

Django avtomatik ravishda ma'lumotlar bazasini boshqaradi. **Migrations** — bu ma'lumotlar bazasi o'zgarishlarini kuzatish va qo'llash tizimi.

### Migrations nima?

**Oddiy analogiya:**
- Siz binoda yangi xona qurishni rejalashtirdingiz — bu **model** yaratish
- Qurilish chizmasi tayyorlandı — bu **makemigrations** buyrug'i
- Qurilishchilar chizmaga asosan xonani qurdiler — bu **migrate** buyrug'i

### SQLite nima?

Django default holda **SQLite** ma'lumotlar bazasini ishlatadi:
- Oddiy fayl asosida ishlaydigan ma'lumotlar bazasi
- O'rnatish talab qilmaydi
- Kichik loyihalar uchun juda qulay
- Production da PostgreSQL yoki MySQL ishlatiladi

**Fayl joylashuvi:**
```
backend/
├── db.sqlite3  ← Ma'lumotlar bazasi fayli
```

### Default migrations ni qo'llash

Django o'rnatilgan app lari (admin, auth, sessions) uchun migration fayllar allaqachon tayyor. Ularni ma'lumotlar bazasiga qo'llashimiz kerak.

#### ✔ Windows

```powershell
python manage.py migrate
```

#### ✔ Linux/macOS

```bash
python3 manage.py migrate
```

### Expected output

```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying admin.0003_logentry_add_action_flag_choices... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying auth.0010_alter_group_name_max_length... OK
  Applying auth.0011_update_proxy_permissions... OK
  Applying auth.0012_alter_user_first_name_max_length... OK
  Applying sessions.0001_initial... OK
```

**Tushuntirish:**
- Har bir qator bitta migration faylni ma'lumotlar bazasiga qo'llaydi
- `OK` — muvaffaqiyatli bajarildi
- Agar xatolik bo'lsa, aniq xato xabari chiqadi

### Migration nima qildi?

```bash
# db.sqlite3 faylida quyidagi jadvallar yaratildi:

# 1. auth_user — Foydalanuvchilar
# 2. auth_group — Foydalanuvchi guruhlari
# 3. auth_permission — Ruxsatlar
# 4. django_session — Session ma'lumotlari
# 5. django_admin_log — Admin paneldagi harakatlar tarixi
# ... va boshqalar
```

Bu jadvallar admin panel va foydalanuvchilar tizimi uchun kerak.

---

### Keng tarqalgan xatolar

**1. "django.db.utils.OperationalError: unable to open database file"**

**Sabab:** Ma'lumotlar bazasi faylini yaratish uchun ruxsat yo'q.

**Yechim Linux/macOS:**
```bash
# Papka ruxsatlarini tekshirish
ls -la

# Agar kerak bo'lsa
chmod 755 .
```

**Yechim Windows:**
Papka "Read-only" bo'lmasligi kerak.

**2. "No migrations to apply"**

Bu xato emas! Agar barcha migrations allaqachon qo'llanilgan bo'lsa, bu xabar chiqadi.

**3. "django.db.utils.OperationalError: table ... already exists"**

**Sabab:** Migrations konflikti.

**Yechim:**
```bash
# db.sqlite3 ni o'chirish (MA'LUMOTLAR YO'QOLADI!)
rm db.sqlite3

# Migrations papkalarini tozalash (00xx fayllarni o'chirish)
find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
find . -path "*/migrations/*.pyc" -delete

# Qaytadan migrations yaratish
python manage.py makemigrations
python manage.py migrate
```

---

## Serverni ishga tushirish

Django da mahalliy development server bor. Bu server faqat dasturlash jarayonida ishlatiladi.

### Serverni ishga tushirish

#### ✔ Windows

```powershell
python manage.py runserver
```

#### ✔ Linux/macOS

```bash
python3 manage.py runserver
```

### Expected output

```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).
November 18, 2025 - 10:30:45
Django version 5.0.1, using settings 'config.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

**Line-by-line tushuntirish:**
- `Watching for file changes` — Kod o'zgartirilsa, server avtomatik qayta yuklanadi
- `System check identified no issues` — Xatolar yo'q
- `Django version 5.0.1` — Django versiyasi
- `Starting development server at http://127.0.0.1:8000/` — Server manzili
- `Quit the server with CONTROL-C` — To'xtatish uchun Ctrl+C bosish

### Brauzerda ochish

1. Brauzer oching (Chrome, Firefox, Edge)
2. Manzil qatoriga yozing: `http://127.0.0.1:8000/` yoki `http://localhost:8000/`
3. Enter bosing

**Natija:**
"Salom, Django!" yozuvi ko'rinishi kerak (main/views.py dagi home funksiyasidan).

---

### Boshqa portda ishga tushirish

Agar 8000-port band bo'lsa yoki boshqa port ishlatmoqchi bo'lsangiz:

```bash
# 8080 portda ishga tushirish
python manage.py runserver 8080

# Muayyan IP va portda
python manage.py runserver 0.0.0.0:8000
```

**0.0.0.0 nima?**
Bu barcha network interface lardan kirishga ruxsat beradi. Ya'ni tarmoqdagi boshqa kompyuterlar ham sizning serverni ko'ra oladi.

---

### Serverni to'xtatish

#### Barcha OS uchun bir xil

Terminal oynasida `Ctrl + C` tugmalarini bosing.

**Expected output:**
```
^C
Quit the server with CONTROL-C.
```

---

### Keng tarqalgan xatolar

**1. "Error: That port is already in use"**

**Sabab:** 8000-port allaqachon band.

**Yechim 1: Boshqa portdan foydalanish**
```bash
python manage.py runserver 8080
```

**Yechim 2: Band portni topish va to'xtatish (Windows)**
```powershell
# Qaysi dastur 8000 portni ishlatayotganini topish
netstat -ano | findstr :8000

# Chiqgan PID raqamini ko'ring (masalan: 12345)
taskkill /PID 12345 /F
```

**Yechim 3: Band portni topish va to'xtatish (Linux/macOS)**
```bash
# 8000 portni ishlatayotgan process ni topish
lsof -i :8000

# PID raqamini ko'ring va to'xtatish
kill -9 <PID>
```

**2. "ImportError: Couldn't import Django"**

**Sabab:** Virtual environment faol emas.

**Yechim:**
```bash
# Venv ni faollashtiring
source venv/bin/activate  # Linux/macOS
.\venv\Scripts\Activate.ps1  # Windows

# (venv) belgisini tekshiring
```

**3. "DisallowedHost at /"**

**Sabab:** ALLOWED_HOSTS sozlamasi.

**Yechim:**
```python
# config/settings.py
ALLOWED_HOSTS = ['localhost', '127.0.0.1']
```

---

## Admin panel va superuser

Django ning eng kuchli xususiyatlaridan biri — tayyor **Admin Panel**. Bu orqali ma'lumotlar bazasini GUI (grafik interfeys) orqali boshqarish mumkin.

### Superuser yaratish

Superuser — bu barcha ruxsatlarga ega bo'lgan admin foydalanuvchi.

#### ✔ Windows

```powershell
python manage.py createsuperuser
```

#### ✔ Linux/macOS

```bash
python3 manage.py createsuperuser
```

### Expected interaction

```
Username (leave blank to use 'admin'): nodir
Email address: nodir@example.com
Password: 
Password (again): 
Superuser created successfully.
```

**Muhim eslatmalar:**
- Parol terilganda ko'rinmaydi (xavfsizlik uchun)
- Parol kamida 8 belgidan iborat bo'lishi kerak
- Oddiy parol kiritsangiz (`12345678`), ogohlantirish chiqadi, lekin davom etsa bo'ladi

---

### Admin panelga kirish

1. Serverni ishga tushiring:
```bash
python manage.py runserver
```

2. Brauzerda oching:
```
http://127.0.0.1:8000/admin/
```

3. Login sahifasi ochiladi:
   - **Username:** nodir
   - **Password:** (siz yaratgan parol)

4. "Log in" tugmasini bosing

### Admin paneldagi bo'limlar

**1. Authentication and Authorization**
- **Users** — Foydalanuvchilar ro'yxati
- **Groups** — Foydalanuvchi guruhlari

**2. Django Admin Panel xususiyatlari**
- Foydalanuvchilarni qo'shish, o'chirish, tahrirlash
- Parol o'zgartirish
- Ruxsatlarni boshqarish
- Modellarni ko'rish va tahrirlash

---

### Model ni admin panelda ro'yxatdan o'tkazish

Keling, oddiy `Post` modelini yaratib, admin panelda ko'rsataylik.

**1-qadam: Model yaratish (main/models.py)**

```python
# main/models.py

from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.title
```

**Line-by-line tushuntirish:**

```python
from django.db import models
```
- `models` — Django ning ma'lumotlar bazasi modellari moduli

```python
class Post(models.Model):
```
- `Post` — model nomi (ma'lumotlar bazasida jadval nomi `main_post` bo'ladi)
- `(models.Model)` — Django ning bazaviy Model klassidan meros olish

```python
title = models.CharField(max_length=200)
```
- `title` — maydon nomi (ma'lumotlar bazasida ustun nomi)
- `CharField` — matn maydoni (SQL da VARCHAR)
- `max_length=200` — maksimal 200 belgi

```python
content = models.TextField()
```
- `TextField` — katta matn maydoni (SQL da TEXT)
- `max_length` yo'q — cheksiz uzunlikdagi matn

```python
created_at = models.DateTimeField(auto_now_add=True)
```
- `DateTimeField` — sana va vaqt maydoni
- `auto_now_add=True` — obyekt yaratilganda avtomatik hozirgi vaqtni qo'yadi
- Foydalanuvchi bu maydonga qo'lda qiymat kiritmaydi

```python
def __str__(self):
    return self.title
```
- `__str__` — Python ning maxsus metodi
- Admin panelda va shell da obyekt nomi sifatida `title` ko'rsatiladi
- Masalan: "Mening birinchi postim" o'rniga `Post object (1)` emas

---

**2-qadam: Migration yaratish va qo'llash**

```bash
# Migration faylini yaratish
python manage.py makemigrations

# Expected output:
# Migrations for 'main':
#   main/migrations/0001_initial.py
#     - Create model Post
```

```bash
# Migration ni ma'lumotlar bazasiga qo'llash
python manage.py migrate

# Expected output:
# Operations to perform:
#   Apply all migrations: admin, auth, contenttypes, main, sessions
# Running migrations:
#   Applying main.0001_initial... OK
```

**Nima bo'ldi?**
- `main/migrations/0001_initial.py` fayli yaratildi (migration chizmasi)
- `db.sqlite3` faylida `main_post` jadvali yaratildi
- Jadvalda ustunlar: `id`, `title`, `content`, `created_at`

---

**3-qadam: Admin panelda ro'yxatdan o'tkazish (main/admin.py)**

```python
# main/admin.py

from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

**Line-by-line tushuntirish:**

```python
from django.contrib import admin
```
- Django ning admin moduli

```python
from .models import Post
```
- Hozirgi app (main) dan Post modelini import qilish

```python
admin.site.register(Post)
```
- `admin.site` — admin panel obyekti
- `.register(Post)` — Post modelini admin panelda ro'yxatdan o'tkazish
- Endi admin panelda "Posts" bo'limi paydo bo'ladi

---

**4-qadam: Admin panelda sinab ko'rish**

1. Serverni qayta ishga tushiring (agar o'chirilgan bo'lsa):
```bash
python manage.py runserver
```

2. Admin panelni oching: `http://127.0.0.1:8000/admin/`

3. **MAIN** bo'limida **Posts** ni ko'rasiz

4. **Add Post** tugmasini bosing

5. Forma to'ldiring:
   - **Title:** "Django bilan birinchi postim"
   - **Content:** "Bu juda qiziqarli..."
   - **SAVE** tugmasini bosing

6. Yangi post yaratildi! Ro'yxatda ko'rinadi.

---

### Admin panelni sozlash (advanced)

**Yaxshiroq ko'rinish uchun:**

```python
# main/admin.py

from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'created_at']  # Ro'yxatda qaysi ustunlar ko'rinsin
    list_filter = ['created_at']            # Filterlash uchun
    search_fields = ['title', 'content']    # Qidiruv uchun
    date_hierarchy = 'created_at'           # Sana bo'yicha navigatsiya
```

**Line-by-line tushuntirish:**

```python
@admin.register(Post)
```
- Dekorator — `admin.site.register(Post)` ning qisqa usuli

```python
class PostAdmin(admin.ModelAdmin):
```
- `PostAdmin` — admin panel sozlamalari klassi
- `(admin.ModelAdmin)` — Django ning bazaviy admin klassidan meros olish

```python
list_display = ['title', 'created_at']
```
- Admin panelda Post ro'yxatida qaysi maydonlar ko'rinishi
- Default faqat `__str__()` ko'rsatiladi

```python
list_filter = ['created_at']
```
- O'ng tarafda filter paneli paydo bo'ladi
- Sana bo'yicha filterlash mumkin bo'ladi

```python
search_fields = ['title', 'content']
```
- Yuqorida qidiruv maydoni paydo bo'ladi
- Title va content bo'yicha qidirish

```python
date_hierarchy = 'created_at'
```
- Yuqorida sana bo'yicha navigatsiya
- Yil → Oy → Kun darajasida ko'rish

---

### Keng tarqalgan xatolar

**1. "no such table: main_post"**

**Sabab:** Migration qo'llanilmagan.

**Yechim:**
```bash
python manage.py makemigrations
python manage.py migrate
```

**2. Admin panelda model ko'rinmayapti**

**Sabab:** `admin.site.register()` qilinmagan.

**Yechim:**
```python
# main/admin.py
from django.contrib import admin
from .models import Post

admin.site.register(Post)  # ← Buni qo'shing
```

**3. "OperationalError: no such column: main_post.created_at"**

**Sabab:** Model o'zgartirilgan, lekin migration yaratilmagan.

**Yechim:**
```bash
python manage.py makemigrations
python manage.py migrate
```

---

## Templates va Static fayllar

Hozircha biz `HttpResponse` bilan oddiy HTML qaytaryapmiz. Professional loyihalarda **Template** (shablon) fayllari ishlatiladi.

### Template nima?

Template — bu HTML fayl, lekin ichida Django ning maxsus teglari bor. Bu teglar orqali Python o'zgaruvchilarini HTML ga joylashtirish mumkin.

**Oddiy analogiya:**
- Template = Bir xil dizayndagi ma'lumot kartochkasi
- Ma'lumotlar = Har bir kartochkaga yozilgan shaxsiy ma'lumotlar

---

### Templates papkasini yaratish va sozlash

#### 1-qadam: templates papkasini yaratish

```bash
# Project asosida (manage.py yonida)
mkdir templates
```

**Expected folder structure:**

```
backend/
├── config/
├── main/
├── venv/
├── templates/        ← Yangi papka
├── manage.py
└── db.sqlite3
```

---

#### 2-qadam: settings.py da sozlash

**config/settings.py faylini oching:**

```python
# config/settings.py

import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent

# ...

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],  # ← Bu qatorni o'zgartiring
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

**Line-by-line tushuntirish:**

```python
'DIRS': [BASE_DIR / 'templates'],
```
- `DIRS` — Django template fayllarni qayerdan izlashi kerak
- `BASE_DIR` — loyihaning asosiy papkasi (`/home/user/backend/`)
- `/ 'templates'` — templates papkasini qo'shish
- Natija: `/home/user/backend/templates/`

**Alternativ yozish usuli:**

```python
'DIRS': [os.path.join(BASE_DIR, 'templates')],
```

---

### Base template (asosiy shablon) yaratish

Professional loyihalarda **Template Inheritance** (shablon merosi) ishlatiladi. Ya'ni, bir marta dizayn yaratib, barcha sahifalarda ishlatish.

#### templates/base.html

```html
<!-- templates/base.html -->

<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}Mening saytim{% endblock %}</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 1100px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background: #333;
            color: #fff;
            padding: 20px 0;
            text-align: center;
        }
        nav {
            background: #555;
            color: #fff;
            padding: 10px 0;
        }
        nav ul {
            list-style: none;
            text-align: center;
        }
        nav ul li {
            display: inline;
            margin: 0 15px;
        }
        nav ul li a {
            color: #fff;
            text-decoration: none;
        }
        main {
            background: #fff;
            padding: 30px;
            margin-top: 20px;
            border-radius: 5px;
        }
        footer {
            background: #333;
            color: #fff;
            text-align: center;
            padding: 20px 0;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Django Loyiham</h1>
    </header>
    
    <nav>
        <ul>
            <li><a href="/">Bosh sahifa</a></li>
            <li><a href="/about/">Biz haqimizda</a></li>
            <li><a href="/contact/">Bog'lanish</a></li>
        </ul>
    </nav>
    
    <div class="container">
        <main>
            {% block content %}
            <!-- Boshqa sahifalarning kontenti shu yerga tushadi -->
            {% endblock %}
        </main>
    </div>
    
    <footer>
        <p>&copy; 2025 Django Loyiham. Barcha huquqlar himoyalangan.</p>
    </footer>
</body>
</html>
```

**Line-by-line tushuntirish:**

```html
{% block title %}Mening saytim{% endblock %}
```
- `{% block title %}` — bu joy boshqa sahifalarda almashtirilishi mumkin
- `Mening saytim` — default qiymat (agar boshqa sahifa almashtirilmasa)
- `{% endblock %}` — blok tugadi

```html
{% block content %}
<!-- Boshqa sahifalarning kontenti shu yerga tushadi -->
{% endblock %}
```
- Bu eng muhim blok
- Har bir sahifa o'z kontentini shu yerga joylashtiradi

---

### Home sahifa template yaratish

#### templates/home.html

```html
<!-- templates/home.html -->

{% extends 'base.html' %}

{% block title %}Bosh sahifa{% endblock %}

{% block content %}
<h1>Xush kelibsiz!</h1>
<p>Bu Django loyihasining bosh sahifasi.</p>

<div style="margin-top: 30px;">
    <h2>Bizning xizmatlar:</h2>
    <ul>
        <li>Professional web dasturlash</li>
        <li>Ma'lumotlar bazasi dizayni</li>
        <li>API yaratish</li>
    </ul>
</div>
{% endblock %}
```

**Line-by-line tushuntirish:**

```html
{% extends 'base.html' %}
```
- Bu template `base.html` dan meros oladi
- `base.html` dagi barcha kod avtomatik qo'shiladi
- Faqat bloklar ichidagi qismlar almashtiriladi

```html
{% block title %}Bosh sahifa{% endblock %}
```
- `base.html` dagi `{% block title %}` ni almashtiradi
- Brauzer sarlavhasida "Bosh sahifa" ko'rinadi

```html
{% block content %}
<h1>Xush kelibsiz!</h1>
...
{% endblock %}
```
- `base.html` dagi `{% block content %}` ni almashtiradi
- Bu HTML base.html dagi `<main>` tegi ichiga tushadi

---

### View dan template ishlatish

**main/views.py:**

```python
# main/views.py

from django.shortcuts import render

def home(request):
    return render(request, 'home.html')
```

**Line-by-line tushuntirish:**

```python
from django.shortcuts import render
```
- `render` — template faylni render qilish (HTML yasash) funksiyasi
- `HttpResponse` ni almashtiradi

```python
def home(request):
    return render(request, 'home.html')
```
- `render(request, 'home.html')` — `templates/home.html` ni render qilish
- Django avtomatik `base.html` bilan birlashtiradi
- Tayyor HTML brauzerga yuboriladi

---

### Template ga ma'lumot uzatish

**main/views.py:**

```python
# main/views.py

from django.shortcuts import render

def home(request):
    context = {
        'name': 'Nodir',
        'age': 25,
        'skills': ['Python', 'Django', 'PostgreSQL'],
    }
    return render(request, 'home.html', context)
```

**Line-by-line tushuntirish:**

```python
context = {
    'name': 'Nodir',
    'age': 25,
    'skills': ['Python', 'Django', 'PostgreSQL'],
}
```
- `context` — dictionary, template ga uzatiladigan ma'lumotlar
- Kalitlar (key) — template da o'zgaruvchi nomlari
- Qiymatlar (value) — template da ko'rsatiladigan ma'lumotlar

```python
return render(request, 'home.html', context)
```
- 3-parametr `context` — ma'lumotlar dictionary

**templates/home.html:**

```html
{% extends 'base.html' %}

{% block content %}
<h1>Salom, {{ name }}!</h1>
<p>Sizning yoshingiz: {{ age }}</p>

<h2>Sizning ko'nikmalaringiz:</h2>
<ul>
    {% for skill in skills %}
    <li>{{ skill }}</li>
    {% endfor %}
</ul>
{% endblock %}
```

**Django template syntax:**

```html
{{ name }}
```
- Ikki qavsli jingalak — o'zgaruvchini chiqarish
- `context` dictionary dan `name` kalitini oladi

```html
{% for skill in skills %}
<li>{{ skill }}</li>
{% endfor %}
```
- `{% for %}` — Python dagi for sikli
- Har bir `skill` uchun `<li>` tegi yaratadi
- `{% endfor %}` — sikl tugadi

**Django template teglarining boshqalari:**

```html
{% if age > 18 %}
<p>Siz kattasiz</p>
{% else %}
<p>Siz voyaga yetmagansiz</p>
{% endif %}
```

---

### Static fayllar (CSS, JS, Images)

Static fayllar — bu CSS, JavaScript, rasm fayllar. Ular server tomonida o'zgarmaydi.

#### 1-qadam: static papkasini yaratish

```bash
# Project asosida
mkdir static
mkdir static/css
mkdir static/js
mkdir static/images
```

**Expected folder structure:**

```
backend/
├── config/
├── main/
├── templates/
├── static/          ← Yangi papka
│   ├── css/
│   ├── js/
│   └── images/
├── venv/
└── manage.py
```

---

#### 2-qadam: settings.py da sozlash

**config/settings.py:**

```python
# config/settings.py

# Static files (CSS, JavaScript, Images)
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
```

**Line-by-line tushuntirish:**

```python
STATIC_URL = '/static/'
```
- Brauzerda static fayllarga qanday murojaat qilish
- Masalan: `http://localhost:8000/static/css/style.css`

```python
STATICFILES_DIRS = [BASE_DIR / 'static']
```
- Django static fayllarni qayerdan izlashi
- `BASE_DIR / 'static'` — `/home/user/backend/static/`

---

#### 3-qadam: CSS fayl yaratish

**static/css/style.css:**

```css
/* static/css/style.css */

body {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

h1 {
    color: #fff;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
}

.card {
    background: #fff;
    border-radius: 10px;
    padding: 20px;
    margin: 20px 0;
    box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}
```

---

#### 4-qadam: Template da static faylni ulash

**templates/base.html:**

```html
<!-- templates/base.html -->

{% load static %}

<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <title>{% block title %}Mening saytim{% endblock %}</title>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    {% block content %}
    {% endblock %}
    
    <script src="{% static 'js/main.js' %}"></script>
</body>
</html>
```

**Line-by-line tushuntirish:**

```html
{% load static %}
```
- Bu qator **faylning eng yuqorisida** bo'lishi kerak
- `static` tegini ishlatish uchun yuklanadi

```html
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```
- `{% static 'css/style.css' %}` — to'liq yo'lga aylanadi
- Natija: `/static/css/style.css`

```html
<script src="{% static 'js/main.js' %}"></script>
```
- JavaScript faylni ulash

---

### Keng tarqalgan xatolar

**1. "TemplateDoesNotExist at /"**

**Sabab:** Template fayl topilmadi yoki `DIRS` sozlanmagan.

**Yechim:**
```python
# config/settings.py
TEMPLATES = [
    {
        ...
        'DIRS': [BASE_DIR / 'templates'],  # ← Tekshiring
        ...
    },
]
```

**2. Static fayl yuklanmayapti (404)**

**Sabab:** `{% load static %}` yozilmagan yoki `STATICFILES_DIRS` sozlanmagan.

**Yechim:**
```html
<!-- Template faylning eng yuqorisida -->
{% load static %}
```

```python
# config/settings.py
STATICFILES_DIRS = [BASE_DIR / 'static']
```

**3. "Invalid block tag: 'static'"**

**Sabab:** `{% load static %}` yozilmagan.

**Yechim:**
```html
{% load static %}  ← Buni qo'shing

<!DOCTYPE html>
...
```

---

## To'liq amaliy loyiha — Post blog

Keling, hozir o'rgangan barcha narsalarni birlashtirgan holda to'liq blog loyihasini yarataylik.

### Loyiha talablari

1. Bosh sahifa — barcha postlar ro'yxati
2. Post detali — bitta postni to'liq ko'rish
3. About sahifasi
4. Contact sahifasi
5. Admin panelda post yaratish

---

### 1-qadam: Model (allaqachon bor)

**main/models.py:**

```python
# main/models.py

from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200, verbose_name="Sarlavha")
    content = models.TextField(verbose_name="Matn")
    created_at = models.DateTimeField(auto_now_add=True, verbose_name="Yaratilgan vaqt")
    updated_at = models.DateTimeField(auto_now=True, verbose_name="Yangilangan vaqt")
    
    class Meta:
        verbose_name = "Post"
        verbose_name_plural = "Postlar"
        ordering = ['-created_at']  # Eng yangilari birinchi
    
    def __str__(self):
        return self.title
```

**Yangi qo'shilgan:**

```python
verbose_name="Sarlavha"
```
- Admin panelda maydon nomini o'zbekcha ko'rsatish

```python
class Meta:
```
- Model haqida qo'shimcha ma'lumotlar

```python
ordering = ['-created_at']
```
- Postlarni yaratilgan vaqti bo'yicha teskari tartibda (yangilari birinchi)
- `-` belgisi — teskari tartib

```python
verbose_name_plural = "Postlar"
```
- Admin panelda ko'plik shakl

---

### 2-qadam: Views yaratish

**main/views.py:**

```python
# main/views.py

from django.shortcuts import render, get_object_or_404
from .models import Post

def home(request):
    """Bosh sahifa - barcha postlar"""
    posts = Post.objects.all()
    context = {
        'posts': posts,
    }
    return render(request, 'home.html', context)

def post_detail(request, post_id):
    """Bitta postni to'liq ko'rish"""
    post = get_object_or_404(Post, id=post_id)
    context = {
        'post': post,
    }
    return render(request, 'post_detail.html', context)

def about(request):
    """Biz haqimizda sahifasi"""
    return render(request, 'about.html')

def contact(request):
    """Bog'lanish sahifasi"""
    return render(request, 'contact.html')
```

**Line-by-line tushuntirish:**

```python
from .models import Post
```
- Hozirgi app dan Post modelini import qilish

```python
posts = Post.objects.all()
```
- `Post.objects` — Post modelidagi barcha yozuvlarga murojaat
- `.all()` — barchasini olish
- Natija: QuerySet (ma'lumotlar ro'yxati)

```python
get_object_or_404(Post, id=post_id)
```
- Post modelidan `id` bo'yicha bitta yozuvni olish
- Agar topilmasa — 404 sahifa ko'rsatish
- `post_id` — URL dan keladi

---

### 3-qadam: URLs

**main/urls.py:**

```python
# main/urls.py

from django.urls import path
from . import views

app_name = 'main'

urlpatterns = [
    path('', views.home, name='home'),
    path('post/<int:post_id>/', views.post_detail, name='post_detail'),
    path('about/', views.about, name='about'),
    path('contact/', views.contact, name='contact'),
]
```

**Line-by-line tushuntirish:**

```python
app_name = 'main'
```
- Namespace (nom fazosi) — URL nomlarini ajratish
- Template da: `{% url 'main:home' %}`

```python
path('post/<int:post_id>/', views.post_detail, name='post_detail'),
```
- `<int:post_id>` — dinamik qism, faqat raqam qabul qiladi
- Misol: `/post/1/`, `/post/25/`
- `post_id` o'zgaruvchi sifatida view ga uzatiladi

**Boshqa dynamic URL turlari:**
- `<int:pk>` — integer (butun son)
- `<str:slug>` — string (matn)
- `<uuid:id>` — UUID format

---

### 4-qadam: Templates

**templates/home.html:**

```html
<!-- templates/home.html -->

{% extends 'base.html' %}

{% block title %}Bosh sahifa{% endblock %}

{% block content %}
<h1>Blog Postlari</h1>

{% if posts %}
    {% for post in posts %}
    <div class="card">
        <h2>{{ post.title }}</h2>
        <p class="text-muted">{{ post.created_at|date:"d-M-Y, H:i" }}</p>
        <p>{{ post.content|truncatewords:30 }}</p>
        <a href="{% url 'main:post_detail' post.id %}">To'liq o'qish →</a>
    </div>
    {% endfor %}
{% else %}
    <p>Hozircha postlar yo'q. Admin panelda post yarating.</p>
{% endif %}
{% endblock %}
```

**Line-by-line tushuntirish:**

```html
{% if posts %}
```
- Agar postlar bo'lsa

```html
{% for post in posts %}
```
- Har bir post uchun

```html
{{ post.created_at|date:"d-M-Y, H:i" }}
```
- `|date:` — Django filter (filtr)
- Sanani formatlash: `18-Noy-2025, 14:30`

```html
{{ post.content|truncatewords:30 }}
```
- `|truncatewords:30` — faqat birinchi 30 so'zni ko'rsatish
- Qolganini `...` bilan almashtirish

```html
{% url 'main:post_detail' post.id %}
```
- `{% url %}` — URL yaratish
- `'main:post_detail'` — URL nomi (namespace:name)
- `post.id` — parametr
- Natija: `/post/1/`

```html
{% else %}
```
- Agar postlar bo'sh bo'lsa

---

**templates/post_detail.html:**

```html
<!-- templates/post_detail.html -->

{% extends 'base.html' %}

{% block title %}{{ post.title }}{% endblock %}

{% block content %}
<div class="post-detail">
    <h1>{{ post.title }}</h1>
    <p class="text-muted">
        Yaratildi: {{ post.created_at|date:"d-M-Y, H:i" }}
        {% if post.updated_at != post.created_at %}
        | Yangilandi: {{ post.updated_at|date:"d-M-Y, H:i" }}
        {% endif %}
    </p>
    
    <div class="post-content">
        {{ post.content|linebreaks }}
    </div>
    
    <a href="{% url 'main:home' %}">← Orqaga qaytish</a>
</div>
{% endblock %}
```

**Yangi filterlar:**

```html
{{ post.content|linebreaks }}
```
- `|linebreaks` — matn ichidagi yangi qatorlarni `<p>` va `<br>` teglarga aylantirish
- Oddiy matnga HTML formatlash berish

```html
{% if post.updated_at != post.created_at %}
```
- Agar post yangilangan bo'lsa, yangilanish vaqtini ko'rsatish

---

**templates/about.html:**

```html
<!-- templates/about.html -->

{% extends 'base.html' %}

{% block title %}Biz haqimizda{% endblock %}

{% block content %}
<h1>Biz haqimizda</h1>
<p>Biz Django freymvorkini o'rganayotgan dasturchilar jamoasimiz.</p>

<h2>Bizning maqsadimiz</h2>
<ul>
    <li>Professional web ilovalar yaratish</li>
    <li>Yangi texnologiyalarni o'zlashtirish</li>
    <li>Tajriba almashish</li>
</ul>
{% endblock %}
```

---

**templates/contact.html:**

```html
<!-- templates/contact.html -->

{% extends 'base.html' %}

{% block title %}Bog'lanish{% endblock %}

{% block content %}
<h1>Biz bilan bog'laning</h1>

<div class="contact-info">
    <p><strong>Email:</strong> info@example.com</p>
    <p><strong>Telefon:</strong> +998 90 123 45 67</p>
    <p><strong>Manzil:</strong> Toshkent, O'zbekiston</p>
</div>

<h2>Xabar yuboring</h2>
<form method="post">
    <div>
        <label>Ismingiz:</label>
        <input type="text" name="name" required>
    </div>
    <div>
        <label>Email:</label>
        <input type="email" name="email" required>
    </div>
    <div>
        <label>Xabar:</label>
        <textarea name="message" rows="5" required></textarea>
    </div>
    <button type="submit">Yuborish</button>
</form>
{% endblock %}
```

*Eslatma: Form ishlatish uchun CSRF token va POST so'rovni qayta ishlash kerak. Bu keyingi darslarda o'rganiladi.*

---

### 5-qadam: Admin panelda ma'lumot qo'shish

1. Admin panelga kiring: `http://127.0.0.1:8000/admin/`
2. **Postlar** → **POST QO'SHISH**
3. 3 ta post yarating:

**Post 1:**
- **Sarlavha:** "Django bilan tanishuv"
- **Matn:** "Django — Python uchun eng mashhur web freymvork. U tez va xavfsiz ilovalar yaratishga yordam beradi..."

**Post 2:**
- **Sarlavha:** "Python nima uchun mashhur?"
- **Matn:** "Python — oddiy sintaksisga ega dasturlash tili. U web dasturlash, ma'lumotlar tahlili, sun'iy intellekt uchun ishlatiladi..."

**Post 3:**
- **Sarlavha:** "Backend vs Frontend"
- **Matn:** "Backend — server tomoni, ma'lumotlar bazasi bilan ishlash. Frontend — foydalanuvchi ko'radigan qism, dizayn..."

---

### 6-qadam: Natijani ko'rish

1. Serverni ishga tushiring:
```bash
python manage.py runserver
```

2. Brauzerda oching:
- `http://127.0.0.1:8000/` — Bosh sahifa (3 ta post ko'rinadi)
- `http://127.0.0.1:8000/post/1/` — Birinchi postni to'liq ko'rish
- `http://127.0.0.1:8000/about/` — Biz haqimizda
- `http://127.0.0.1:8000/contact/` — Bog'lanish

---

## Keng tarqalgan xatolar va ularning yechimlari

### 1. ModuleNotFoundError: No module named 'django'

**Sabab:** Virtual environment faol emas yoki Django o'rnatilmagan.

**Yechim:**
```bash
# Virtual environment ni faollashtirish
source venv/bin/activate  # Linux/macOS
.\venv\Scripts\Activate.ps1  # Windows

# Django o'rnatish
pip install django
```

**Tekshirish:**
```bash
which python  # /home/user/backend/venv/bin/python ko'rsatishi kerak
django-admin --version
```

---

### 2. TemplateDoesNotExist at /

**Sabab:** Template fayl topilmadi yoki `DIRS` to'g'ri sozlanmagan.

**Yechim:**
```python
# config/settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],  # ← Tekshiring
        'APP_DIRS': True,
        ...
    },
]
```

**Papka strukturasini tekshirish:**
```
backend/
├── templates/
│   ├── base.html
│   ├── home.html
│   └── ...
```

**Fayl nomini tekshirish:**
- `render(request, 'home.html')` — fayl nomi `home.html` bo'lishi kerak
- Katta-kichik harflar farq qiladi: `Home.html` ≠ `home.html`

---

### 3. ImproperlyConfigured

**Sabab:** settings.py da xatolik yoki app INSTALLED_APPS ga qo'shilmagan.

**Yechim:**
```python
# config/settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    
    'main',  # ← Tekshiring
]
```

**Agar SECRET_KEY xatosi bo'lsa:**
```python
# config/settings.py
SECRET_KEY = 'django-insecure-...'  # Bo'sh bo'lmasligi kerak
```

---

### 4. OperationalError: no such table

**Sabab:** Migration qo'llanilmagan.

**Yechim:**
```bash
# Migration fayllarini yaratish
python manage.py makemigrations

# Migration larni qo'llash
python manage.py migrate
```

**Agar muammo davom etsa:**
```bash
# Ma'lumotlar bazasini tozalash (MA'LUMOTLAR YO'QOLADI!)
rm db.sqlite3

# Migrations papkalarini tozalash
find . -path "*/migrations/*.py" -not -name "__init__.py" -delete
find . -path "*/migrations/*.pyc" -delete

# Qaytadan yaratish
python manage.py makemigrations
python manage.py migrate
```

---

### 5. Port band (Error: That port is already in use)

**Sabab:** 8000-port allaqachon ishlatilmoqda.

**Yechim 1: Boshqa port ishlatish**
```bash
python manage.py runserver 8080
```

**Yechim 2: Band procesni to'xtatish (Windows)**
```powershell
# Portni ishlatayotgan processni topish
netstat -ano | findstr :8000

# PID ni ko'ring va to'xtatish
taskkill /PID <PID_RAQAMI> /F
```

**Yechim 3: Band procesni to'xtatish (Linux/macOS)**
```bash
# Portni ishlatayotgan processni topish
lsof -i :8000

# Process ni to'xtatish
kill -9 <PID_RAQAMI>
```

---

### 6. Page not found (404)

**Sabab:** URL noto'g'ri yozilgan yoki urlpatterns da yo'q.

**Yechim:**
```python
# main/urls.py
urlpatterns = [
    path('', views.home, name='home'),
    path('about/', views.about, name='about'),  # ← / bilan tugashi kerak
]
```

**URL ni tekshirish:**
- To'g'ri: `http://localhost:8000/about/`
- Noto'g'ri: `http://localhost:8000/about` (oxirida / yo'q)

**Debug rejimida ko'rish:**
```python
# config/settings.py
DEBUG = True  # Development da True bo'lishi kerak
```

Debug rejimida Django barcha mavjud URL larni ko'rsatadi.

---

### 7. CSRF verification failed

**Sabab:** CSRF token yo'q (form yuborishda).

**Yechim:**
```html
<form method="post">
    {% csrf_token %}  <!-- ← Bu qatorni qo'shing -->
    <input type="text" name="title">
    <button type="submit">Yuborish</button>
</form>
```

**Line-by-line tushuntirish:**
- `{% csrf_token %}` — Django ning xavfsizlik mexanizmi
- Form yuborilganda Django tekshiradi
- Agar token bo'lmasa, 403 Forbidden xatosi chiqadi

---

### 8. Static fayllar yuklanmayapti

**Sabab 1:** `{% load static %}` yozilmagan.

**Yechim:**
```html
{% load static %}  <!-- Faylning eng yuqorida -->

<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
...
```

**Sabab 2:** STATICFILES_DIRS sozlanmagan.

**Yechim:**
```python
# config/settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
```

**Sabab 3:** Fayl nomi yoki yo'li noto'g'ri.

**Yechim:**
```
static/
├── css/
│   └── style.css  ← Aniq bu fayl mavjudligini tekshiring
```

```html
{% static 'css/style.css' %}  ← To'g'ri yo'l
```

---

### 9. Admin panelda model ko'rinmayapti

**Sabab:** Model admin.py da ro'yxatdan o'tkazilmagan.

**Yechim:**
```python
# main/admin.py
from django.contrib import admin
from .models import Post

admin.site.register(Post)  # ← Bu qator majburiy
```

**Alternativ:**
```python
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'created_at']
```

---

### 10. Virtual environment faol emas

**Belgilari:**
- Terminal da `(venv)` ko'rinmaydi
- `pip list` qilganda global Python kutubxonalari ko'rinadi
- Django o'rnatilgan, lekin import qilib bo'lmaydi

**Yechim:**
```bash
# Windows (PowerShell)
.\venv\Scripts\Activate.ps1

# Windows (CMD)
venv\Scripts\activate.bat

# Linux/macOS
source venv/bin/activate
```

**Faollashtirish muvaffaqiyatli bo'lganini tekshirish:**
```bash
# Terminal boshida (venv) belgisi ko'rinishi kerak
(venv) user@computer:~/backend$

# Python yo'lini tekshirish
which python  # Linux/macOS
where python  # Windows

# Natija venv ichidagi python bo'lishi kerak
# To'g'ri: /home/user/backend/venv/bin/python
# Noto'g'ri: /usr/bin/python
```

---

## Amaliy mashqlar

Endi sizning navbatingiz! Quyidagi mashqlarni mustaqil bajarishga harakat qiling.

### Mashq 1: About sahifasini yaratish

**Topshiriq:**
1. `main/views.py` da `about` view funksiyasini yarating
2. Template yarating: `templates/about.html`
3. URL qo'shing: `main/urls.py` da `about/`
4. `base.html` dagi navigatsiyada "Biz haqimizda" havolasini to'g'ri qiling

**Expected natija:**
`http://localhost:8000/about/` manzili "Biz haqimizda" sahifasini ko'rsatadi.

---

### Mashq 2: Contact sahifasi

**Topshiriq:**
1. `contact` view funksiyasini yarating
2. `templates/contact.html` yarating
3. Sahifada quyidagilar bo'lsin:
   - Email: info@example.com
   - Telefon: +998 90 123 45 67
   - Manzil: Toshkent, O'zbekiston
4. URL: `contact/`

**Expected natija:**
`http://localhost:8000/contact/` manzilida bog'lanish ma'lumotlari ko'rinadi.

---

### Mashq 3: Admin panelda 3 ta post qo'shish

**Topshiriq:**
1. Admin panelga kiring
2. 3 ta turli xil post yarating:
   - Birinchisi: Texnologiya haqida
   - Ikkinchisi: Ta'lim haqida
   - Uchinchisi: Sport haqida
3. Har bir post kamida 3 ta paragrafdan iborat bo'lsin

**Expected natija:**
Bosh sahifada 3 ta post ko'rinadi, har birini bosib to'liq o'qish mumkin.

---

### Mashq 4: Post yaratilgan sanasini chiroyli ko'rsatish

**Topshiriq:**
1. `templates/home.html` da post sanasini quyidagi formatda ko'rsating:
   - "18-Noyabr-2025, 14:30"
2. `|date` filtridan foydalaning

**Hint:**
```html
{{ post.created_at|date:"d-F-Y, H:i" }}
```

---

### Mashq 5: Post qidirish funksiyasi (Advanced)

**Topshiriq:**
1. Bosh sahifada qidiruv maydoni qo'shing
2. Foydalanuvchi so'z yozsa, shu so'z bor postlarni ko'rsatsin
3. View da filter ishlatish:
```python
posts = Post.objects.filter(title__icontains=query)
```

**Expected natija:**
Qidiruv maydoni orqali postlarni topish mumkin.

---

## Yakuniy xulosa

### Bu darsda nimani o'rgandik?

1. **Django nima va nega kerak** — Web framework tushunchasi
2. **Web ilovalarning arxitekturasi** — Client-Server-Database modeli
3. **MTV pattern** — Model, Template, View tushunchalari
4. **Django o'rnatish** — 3 xil OS uchun to'liq ko'rsatmalar
5. **Virtual environment** — Loyihalarni ajratish
6. **Project va App yaratish** — startproject va startapp
7. **View funksiyalari** — HttpResponse va render
8. **URL routing** — path, include, dinamik URL
9. **Migrations** — Ma'lumotlar bazasini boshqarish
10. **Admin panel** — Tayyor CRUD interfeys
11. **Templates** — HTML shablon tizimi
12. **Template inheritance** — base.html dan foydalanish
13. **Static fayllar** — CSS, JS, Images
14. **Model yaratish** — Post blog modeli
15. **CRUD operatsiyalari** — Admin panel orqali ma'lumot boshqarish

### Asosiy buyruqlar jadvali

| Vazifa | Windows | Linux/macOS |
|--------|---------|-------------|
| Python versiyasi | `python --version` | `python3 --version` |
| Venv yaratish | `python -m venv venv` | `python3 -m venv venv` |
| Venv faollashtirish | `.\venv\Scripts\Activate.ps1` | `source venv/bin/activate` |
| Django o'rnatish | `pip install django` | `pip3 install django` |
| Project yaratish | `django-admin startproject config .` | `django-admin startproject config .` |
| App yaratish | `python manage.py startapp main` | `python3 manage.py startapp main` |
| Migrations yaratish | `python manage.py makemigrations` | `python3 manage.py makemigrations` |
| Migrations qo'llash | `python manage.py migrate` | `python3 manage.py migrate` |
| Superuser yaratish | `python manage.py createsuperuser` | `python3 manage.py createsuperuser` |
| Server ishga tushirish | `python manage.py runserver` | `python3 manage.py runserver` |

---

### Keyingi dars uchun yo'nalish

**2-amaliy darsda o'rganamiz:**

1. **Forms** — Foydalanuvchidan ma'lumot qabul qilish
2. **ModelForm** — Model asosida avtomatik form yaratish
3. **Validation** — Ma'lumotlarni tekshirish
4. **Messages** — Foydalanuvchiga xabar ko'rsatish
5. **Authentication** — Ro'yxatdan o'tish va kirish tizimi
6. **User permissions** — Ruxsatlar tizimi
7. **Media files** — Foydalanuvchi yuklagan fayllar (rasm, PDF)
8. **Pagination** — Sahifalash (1, 2, 3... sahifalar)
9. **Search** — Qidiruv funksiyasi
10. **Relationships** — ForeignKey, ManyToMany

---

### Manbalar va qo'shimcha o'rganish

**Rasmiy Django hujjatlari:**
- https://docs.djangoproject.com/
- https://docs.djangoproject.com/en/stable/intro/tutorial01/

**O'zbek tilidagi manbalar:**
- Django Uzbekistan Telegram guruhi
- YouTube: Django darsliklari o'zbek tilida

**Amaliyot uchun loyiha g'oyalari:**
1. Shaxsiy blog
2. Todo list (Vazifalar ro'yxati)
3. Kitoblar kutubxonasi
4. Ovqat retseptlari sayti
5. Portfolio websayti

---

### Muhim eslatmalar

1. **Har doim virtual environment faol bo'lishi kerak** — `(venv)` belgisini tekshiring
2. **Kod yozishda tartib** — Models → Migrations → Views → URLs → Templates
3. **Har bir o'zgarishdan keyin** — Serverni qayta ishga tushirish shart emas (Django avtomatik reload qiladi)
4. **DEBUG = True** — Faqat development da, production da False
5. **SECRET_KEY** — Maxfiy saqlash, GitHub ga yuklamaslik
6. **db.sqlite3** — Bu fayl ma'lumotlar bazasi, Git ga qo'shmaslik
7. **venv papkasi** — .gitignore ga qo'shish

---

### Birinchi loyihangizni tugatganingiz bilan tabriklayman! 🎉

Siz endi:
- ✅ Django nima ekanligini bilasiz
- ✅ Web ilovalar qanday ishlashini tushunasiz
- ✅ Django loyiha yaratishingiz mumkin
- ✅ View, URL, Template yaratishingiz mumkin
- ✅ Ma'lumotlar bazasi bilan ishlashingiz mumkin
- ✅ Admin panel bilan tanishsiz

**Keyingi qadam:** Yuqoridagi mashqlarni bajaring va o'z loyihangizni yaratishni boshlang!

**Omad yor bo'lsin! 🚀**

---

### Savol-javoblar (FAQ)

**Savol: Django o'rganish qiyin emasmi?**

Javob: Yo'q! Agar Python bilsangiz, Django oson. Bosqichma-bosqich o'rganish orqali har kim o'zlashtirishi mumkin.

**Savol: Nima uchun Django, emas Flask?**

Javob: Django "batteries included" — barcha kerakli narsalar tayyor. Flask esa minimal, siz hamma narsani o'zingiz qo'shasiz. Boshlang'ich uchun Django oson.

**Savol: Django bilan nima qurish mumkin?**

Javob: Blog, e-commerce, ijtimoiy tarmoq, CRM tizim, API, SaaS loyiha — deyarli har qanday web ilovani.

**Savol: Django frontend bilan ishlaydimi?**

Javob: Ha! Django Templates bilan HTML yasaysiz. Yoki React/Vue bilan REST API tarzida ishlashingiz mumkin.

**Savol: Django ish topishga yordam beradimi?**

Javob: Albatta! Django — O'zbekistonda va dunyoda eng ko'p talab qilinadigan backend texnologiyalardan biri.

---


**Maqolani oxirigacha o'qiganingiz uchun raxmat. Keyingi darsda ko'rishguncha!**
