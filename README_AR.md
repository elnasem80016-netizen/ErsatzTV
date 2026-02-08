# FreeHD - منصة بث مفتوحة المصدر 📺

نسخة معاد صياغتها من ErsatzTV - حل بث IPTV قوي وسهل الاستخدام للاستخدام الشخصي والتعليمي.

## المميزات ✨

- **البث المباشر**: إنشاء قنوات بث IPTV احترافية
- **جدولة متقدمة**: برمجة البث حسب الجداول الزمنية المعقدة
- **الترجمة**: دعم الترجمات المضمنة والخارجية
- **المرونة**: إعدادات قابلة للتخصيص بالكامل
- **الأداء**: معالجة فيديو محسّنة باستخدام FFmpeg
- **مفتوح المصدر**: كود حر متاح للتعديل

## المتطلبات 📋

### Windows/macOS/Linux
- [.NET 10](https://dotnet.microsoft.com/download)
- [FFmpeg 7.0+](https://ffmpeg.org/download.html)

### Docker (الأبسط)
- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/)

## التثبيت السريع 🚀

### باستخدام Docker (الموصى به)

```bash
# النسخة الأساسية
docker-compose -f docker/docker-compose.yml up -d

# مع دعم NVIDIA GPU
docker-compose -f docker/docker-compose.nvidia.yml up -d

# مع دعم Intel VAAPI
docker-compose -f docker/docker-compose.vaapi.yml up -d
```

ثم افتح المتصفح وانتقل إلى:
```
http://localhost:8409
```

### البناء المحلي

```bash
# استعادة النسخ (Dependencies)
dotnet restore

# تشغيل التطبيق
dotnet run --project ErsatzTV/ErsatzTV.csproj
```

## البنية المعمارية 🏗️

```
ErsatzTV/                  # واجهة المستخدم (Blazor Web)
ErsatzTV.Application/      # منطق العمل (Business Logic)
ErsatzTV.Core/             # المكتبات الأساسية
ErsatzTV.Infrastructure/   # قاعدة البيانات والتخزين
ErsatzTV.FFmpeg/           # معالجة الفيديو
ErsatzTV.Scanner/          # مسح مصادر الوسائط
docker/                    # ملفات Docker
```

## التطوير 👨‍💻

### الإعدادات

تُعرّف الإعدادات في:
- `ErsatzTV/appsettings.json` - الإعدادات العامة
- `ErsatzTV/appsettings.Development.json` - إعدادات التطوير
- `docker/docker-compose.yml` - إعدادات Docker

### المتغيرات البيئية

```bash
ASPNETCORE_ENVIRONMENT=Development
TZ=America/Chicago
```

### قاعدة البيانات

البناء الافتراضي يستخدم SQLite. للمزيد من الخيارات، راجع:
- `ErsatzTV.Infrastructure.Sqlite` - SQLite
- `ErsatzTV.Infrastructure.MySql` - MySQL/MariaDB

## النشر على GitHub 📤

### 1. إنشاء Repository الخاص بك

```bash
# تسجيل الدخول (إذا لم تكن مسجلاً)
gh auth login

# إنشاء repository جديد
gh repo create freehd --public --source=. --remote=origin --push
```

### 2. استخدام GitHub Actions (آلي)

ملف الـ workflow موجود في:
```
.github/workflows/docker-build-publish.yml
```

تلقائياً عند:
- كل `push` إلى `main` أو `develop`
- تحديث الصور على GitHub Container Registry

### 3. إنشاء Release

```bash
# إنشاء git tag
git tag -a v1.0.0 -m "الإصدار الأول"
git push origin v1.0.0

# سيقوم GitHub Actions تلقائياً بـ:
# - بناء الصورة
# - نشرها على GHCR
# - إنشاء Release مع الملاحظات
```

### 4. استخدام الصورة

```bash
# السحب من GitHub Container Registry
docker pull ghcr.io/your-username/freehd:latest

# التشغيل
docker run -d \
  -p 8409:8409 \
  -v freehd:/config \
  ghcr.io/your-username/freehd:latest
```

## المساهمة 🤝

هل تريد إضافة ميزة أو إصلاح خلل؟

```bash
# 1. إنشاء فرع
git checkout -b feature/اسم-الميزة

# 2. إجراء التعديلات
# (عدّل الملفات حسب احتياجك)

# 3. الـ commit
git commit -m "إضافة: وصف الميزة"

# 4. الـ push
git push origin feature/اسم-الميزة

# 5. فتح Pull Request عبر GitHub
```

رجاء اتبع:
- [CONTRIBUTING.md](CONTRIBUTING.md)
- معايير الكود الموجودة

## الخلفيات والصور 🎨

يمكنك إضافة صور خلفية في:
```
artwork/
├── backgrounds/
│   ├── default.png
│   ├── dark.png
│   └── streaming.png
├── logos/
│   ├── logo-light.png
│   └── logo-dark.png
└── banners/
    └── channel-banner.png
```

## استكشاف الأخطاء 🔧

### الحاوية لا تبدأ

```bash
# عرض السجلات
docker-compose logs -f freehd

# إعادة تشغيل
docker-compose restart freehd
```

### مشاكل الأداء

1. تحقق من موارد النظام
2. استخدم GPU (NVIDIA/VAAPI) إن أمكن
3. قلل دقة الترميز

### قاعدة البيانات

```bash
# حذف البيانات وإعادة التهيئة
docker-compose down -v
docker-compose up -d
```

## المراجع 📚

- [ErsatzTV الأصلي](https://github.com/ErsatzTV/ErsatzTV)
- [وثائق Docker](https://docs.docker.com/)
- [وثائق GitHub Actions](https://docs.github.com/en/actions)
- [معايير IPTV](https://en.wikipedia.org/wiki/IPTV)

## الترخيص 📄

هذا المشروع مرخص تحت MIT License - انظر [LICENSE](LICENSE)

## الدعم 💬

- **مشاكل تقنية**: أفتح [GitHub Issue](../../issues)
- **النقاشات**: استخدم [GitHub Discussions](../../discussions)
- **الأسئلة العامة**: تفقد [FAQ](docs/FAQ.md)

---

**ملاحظة**: هذا المشروع تعليمي. استخدمه فقط مع المحتوى الذي تملك حقوقه أو لديك إذن باستخدامه.

صُنع بـ ❤️ من قبل المجتمع
