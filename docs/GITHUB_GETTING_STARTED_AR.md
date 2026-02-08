# দ দليل البدء على GitHub 🚀

مرحباً! هذا دليلك الأول للنشر على GitHub بطريقة احترافية.

## الخطوة الأولى: إعداد حسابك 🔐

### 1. إنشاء حساب GitHub

1. اذهب إلى [github.com](https://github.com)
2. اضغط "Sign up"
3. اكمل البيانات:
   - **البريد الإلكتروني**: بريدك الحقيقي
   - **كلمة المرور**: قوية وآمنة
   - **اسم المستخدم**: freehd-dev (أو أي اسم تحبه)
4. تأكيد البريد الإلكتروني

### 2. تثبيت Git محلياً

```bash
# Windows
# نزّل من: https://git-scm.com/download/win

# Mac
brew install git

# Linux
sudo apt-get install git
```

### 3. إعداد بيانات Git

```bash
git config --global user.name "اسمك"
git config --global user.email "بريدك@example.com"

# تحقق من الإعدادات
git config --global --list
```

## الخطوة الثانية: إنشاء Repository 📦

### الطريقة 1: عبر الويب (أسهل)

1. سجل دخول إلى GitHub
2. اضغط "+" في الزاوية العلوية اليمنى
3. اختر "New repository"
4. املأ:
   - **Repository name**: `freehd`
   - **Description**: `منصة بث مفتوحة المصدر`
   - **Public**: ✓ (مجاني وعام)
   - **Add README**: ❌ (لدينا واحد بالفعل)
   - **Add .gitignore**: Python
5. اضغط "Create repository"

### الطريقة 2: عبر سطر الأوامر

```bash
# تحميل GitHub CLI
# Windows: https://cli.github.com/
# Mac: brew install gh
# Linux: curl -fsSLo- https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo tee /etc/apt/trusted.gpg.d/githubcli-archive-keyring.gpg > /dev/null

# تسجيل الدخول
gh auth login

# إنشاء repository
gh repo create freehd --public --source=. --remote=origin --push
```

## الخطوة الثالثة: رفع الكود الأول 📤

### 1. تهيئة Git محلياً

```bash
cd /workspaces/ErsatzTV

# إذا لم يكن بالفعل repository
git init

# إضافة all المحتويات
git add .

# الـ commit الأول
git commit -m "feat: الإصدار الأولي من FreeHD

- تغيير الاسم إلى freehd
- إضافة GitHub Actions workflows
- إضافة وثائق تعليمية عربية
- إضافة منشئ الخلفيات"

# إضافة الـ remote
git remote add origin https://github.com/your-username/freehd.git

# رفع الكود
git branch -M main
git push -u origin main
```

## الخطوة الرابعة: إعدادات GitHub 🔧

### 1. حماية فرع main

```
Settings > Branches > Branch protection rules
├─ Add rule
├─ Branch name pattern: main
├─ ✓ Require status checks to pass
├─ ✓ Require branches to be up to date
└─ Save changes
```

### 2. إعدادات الإجراءات (Actions)

```
Settings > Actions > General
├─ Workflow permissions: Read and write
├─ Allow scripts in PR: ✓
└─ Save
```

### 3. Secret للنشر (إذا كنت تريد CI/CD مستقبلاً)

```
Settings > Secrets and variables > Actions
├─ New repository secret
├─ Name: DOCKER_USERNAME
├─ Value: اسم المستخدم Docker
└─ Add secret
```

## الخطوة الخامسة: الاستخدام اليومي 💻

### إضافة تحسينات جديدة

```bash
# تحديث من GitHub أولاً
git pull origin main

# إنشاء فرع جديد
git checkout -b feature/my-feature

# عمل التعديلات
# ... (عدّل الملفات)

# عرض التغييرات
git status
git diff

# إضافة التغييرات
git add .
git commit -m "feat: إضافة ميزة جديدة"

# رفع الفرع
git push origin feature/my-feature
```

### إنشاء Pull Request

1. اذهب لـ GitHub
2. ستجد إعلان "Compare & pull request"
3. أضف:
   - **Title**: وصف الميزة
   - **Description**: تفاصيل التغييرات
4. اضغط "Create pull request"
5. بعد الموافقة, merge الفرع

### إغلاق Pull Request

```bash
# محليًا
git pull origin main
git branch -d feature/my-feature

# أو حذفه من GitHub
# Settings > Branches > Delete branch
```

## إنشاء Release (إصدار رسمي) 🎉

### الطريقة 1: عبر GitHub

1. اذهب إلى "Releases"
2. اضغط "Create a new release"
3. امأل:
   - **Tag version**: `v1.0.0` (الإصدار الأول)
   - **Release title**: `الإصدار 1.0.0 - الأولي`
   - **Describe**: اكتب أهم التغييرات
   - **Pre-release**: ❌ (إذا كانت نسخة نهائية)
4. اضغط "Publish release"

### الطريقة 2: عبر سطر الأوامر

```bash
# إنشاء tag محلياً
git tag -a v1.0.0 -m "الإصدار 1.0.0"

# رفع الـ tag
git push origin v1.0.0

# ستقوم GitHub Actions تلقائيًا بـ:
# 1. بناء الصورة
# 2. نشرها على GHCR
# 3. إنشاء Release
```

## مراقبة GitHub Actions ⚙️

### عرض الـ Workflows

```
Actions > ... (الـ workflow الذي تريده)
├─ اختر آخر run
├─ شاهد السجل
└─ استمتع بالنتائج
```

## أفضل الممارسات 💡

### رسائل Commit الجيدة

```bash
# ✅ جيد
git commit -m "feat: إضافة دعم الترجمات"

# ❌ سيء
git commit -m "update"
```

### حجم الـ Commits

```bash
# ❌ كبير جداً
git add .   # الملفات جميعها

# ✅ منطقي
git add ErsatzTV/
git add .github/workflows/
```

### Pull Requests الصغيرة

```bash
# ❌ PR بـ 100 ملف
# ✅ PR ب 5-10 ملفات فقط
```

## الأسئلة الشائعة ❓

### كيف أغير اسم الـ repository؟

```
Settings > General > Repository name
├─ غيّر الاسم
└─ Save
```

### كيف أحذف الـ repository؟

```
Settings > Danger Zone > Delete this repository
├─ اكتب الاسم
└─ Delete
```

### نسيت كلمة المرور؟

```
https://github.com/password_reset
```

### كيف أضيف متعاون؟

```
Settings > Collaborators > Add people
├─ ابحث عن الشخص
└─ Share
```

## موارد تعليمية 📚

- [GitHub Docs](https://docs.github.com) - الوثائق الرسمية
- [Git Handbook](https://guides.github.com/introduction/git-handbook/) - شرح Git
- [Hello World](https://guides.github.com/activities/hello-world/) - tutorial بسيط
- [Markdown Guide](https://www.markdownguide.org/) - تنسيق النصوص

## نصائح ذهبية 🌟

1. **ادخل كثيراً**: كل عمل يومي commit
2. **اكتب رسائل واضحة**: غيرك سيشكرك
3. **استخدم branches**: للميزات الجديدة
4. **مراجع الـ code**: قبل merge
5. **احتفل بالإصدارات**: أنت قمت بعمل رائع! 🎉

---

الآن أنت جاهز لبدء رحلتك مع GitHub!

**نصيحة أخيرة**: 
```bash
# احفظ هذا الأمر المفيد
git log --oneline --graph --all
```

هذا سيريك شجرة مشاريعك بشكل رائع جداً! 🌲

Happy Coding! 🚀
