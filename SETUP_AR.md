# 🚀 دليل التثبيت والتشغيل - QRS STORE

## المتطلبات الأساسية

قبل البدء، تأكد من تثبيت:

- **Node.js** (الإصدار 18 أو أحدث)
- **npm** أو **pnpm** (مدير الحزم)
- **Git** (لاستنساخ المشروع)

### التحقق من التثبيت

```bash
node --version    # يجب أن يكون 18+
npm --version     # أو pnpm --version
git --version
```

---

## خطوات التثبيت

### 1️⃣ استنساخ المشروع

```bash
git clone https://github.com/your-repo/qrs_store_fullstack.git
cd qrs_store_fullstack
```

### 2️⃣ تثبيت المكتبات

```bash
# باستخدام pnpm (الموصى به)
pnpm install

# أو باستخدام npm
npm install
```

### 3️⃣ إعداد متغيرات البيئة

```bash
# نسخ ملف المثال
cp .env.example .env

# ثم عدّل الملف بمحرر نصي
nano .env
```

**المتغيرات المهمة:**

```env
# قاعدة البيانات
DATABASE_URL=mysql://user:password@localhost:3306/qrs_store

# مفاتيح API
STRIPE_PUBLIC_KEY=pk_test_...
STRIPE_SECRET_KEY=sk_test_...

# البريد الإلكتروني
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# التطبيق
APP_URL=http://localhost:5173
API_URL=http://localhost:3000
```

### 4️⃣ إعداد قاعدة البيانات

```bash
# تشغيل الهجرات
pnpm run migrate

# ملء البيانات الأولية (اختياري)
pnpm run seed
```

### 5️⃣ تشغيل خادم التطوير

```bash
# تشغيل الخادم والعميل معاً
pnpm dev

# أو تشغيل كل منهما بشكل منفصل
pnpm dev:client  # الواجهة الأمامية
pnpm dev:server  # الخادم الخلفي
```

### 6️⃣ فتح المتصفح

```
http://localhost:5173
```

---

## 🔧 الأوامر المتاحة

```bash
# التطوير
pnpm dev              # تشغيل الخادم والعميل
pnpm dev:client       # تشغيل الواجهة الأمامية فقط
pnpm dev:server       # تشغيل الخادم فقط

# البناء والإنتاج
pnpm build            # بناء المشروع
pnpm start            # تشغيل الإنتاج
pnpm build:client     # بناء الواجهة الأمامية
pnpm build:server     # بناء الخادم

# الاختبار
pnpm test             # تشغيل جميع الاختبارات
pnpm test:watch       # الاختبار مع المراقبة
pnpm test:coverage    # تقرير التغطية

# التحقق والتنسيق
pnpm lint             # فحص الأخطاء
pnpm format           # تنسيق الكود
pnpm type-check       # فحص أنواع TypeScript

# قاعدة البيانات
pnpm migrate          # تشغيل الهجرات
pnpm seed             # ملء البيانات الأولية
pnpm db:reset         # إعادة تعيين قاعدة البيانات
```

---

## 🌐 إعدادات الخادم

### المنافذ الافتراضية

- **الواجهة الأمامية**: http://localhost:5173
- **الخادم**: http://localhost:3000
- **قاعدة البيانات**: localhost:3306

### تغيير المنافذ

في ملف `.env`:

```env
VITE_PORT=5173        # منفذ الواجهة الأمامية
SERVER_PORT=3000      # منفذ الخادم
DB_PORT=3306          # منفذ قاعدة البيانات
```

---

## 🗄️ إعداد قاعدة البيانات

### إنشاء قاعدة بيانات جديدة

```bash
# MySQL
mysql -u root -p
CREATE DATABASE qrs_store CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
EXIT;

# PostgreSQL
createdb qrs_store
```

### تشغيل الهجرات

```bash
pnpm run migrate
```

### ملء البيانات التجريبية

```bash
pnpm run seed
```

---

## 🔐 إعداد المصادقة

### Google OAuth

1. اذهب إلى [Google Cloud Console](https://console.cloud.google.com)
2. أنشئ مشروع جديد
3. فعّل Google+ API
4. أنشئ بيانات اعتماد OAuth 2.0
5. أضف رابط إعادة التوجيه: `http://localhost:5173/auth/callback`
6. انسخ Client ID و Client Secret إلى `.env`

```env
GOOGLE_CLIENT_ID=your-client-id.apps.googleusercontent.com
GOOGLE_CLIENT_SECRET=your-client-secret
```

---

## 💳 إعداد Stripe

1. اذهب إلى [Stripe Dashboard](https://dashboard.stripe.com)
2. انسخ المفاتيح من الإعدادات
3. أضفها إلى `.env`

```env
STRIPE_PUBLIC_KEY=pk_test_...
STRIPE_SECRET_KEY=sk_test_...
STRIPE_WEBHOOK_SECRET=whsec_...
```

---

## 📧 إعداد البريد الإلكتروني

### استخدام Gmail

1. فعّل المصادقة ذات العاملين
2. أنشئ كلمة مرور التطبيق
3. أضفها إلى `.env`

```env
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password
SMTP_FROM=noreply@qrsstore.ly
```

---

## 🐛 استكشاف الأخطاء الشائعة

### ❌ خطأ: "Cannot find module"

```bash
# الحل: أعد تثبيت المكتبات
rm -rf node_modules pnpm-lock.yaml
pnpm install
```

### ❌ خطأ: "Port already in use"

```bash
# الحل: استخدم منفذ مختلف
VITE_PORT=5174 pnpm dev
```

### ❌ خطأ: "Database connection failed"

```bash
# الحل: تحقق من متغيرات البيئة
# وتأكد من تشغيل خادم قاعدة البيانات
```

### ❌ خطأ: "TypeScript errors"

```bash
# الحل: تحقق من الأنواع
pnpm type-check

# أو أعد بناء المشروع
pnpm build
```

---

## 📝 ملاحظات مهمة

1. **استخدم pnpm**: أسرع وأكثر كفاءة من npm
2. **متغيرات البيئة**: لا تشارك ملف `.env` على GitHub
3. **قاعدة البيانات**: استخدم MySQL 8.0+ أو PostgreSQL 12+
4. **Node.js**: استخدم الإصدار LTS الحالي أو أحدث

---

## 🚀 النشر على الإنتاج

### البناء

```bash
pnpm build
```

### التشغيل

```bash
pnpm start
```

### استخدام Docker

```bash
# بناء الصورة
docker build -t qrs-store .

# تشغيل الحاوية
docker run -p 3000:3000 qrs-store
```

---

## 📞 الدعم والمساعدة

إذا واجهت مشكلة:

1. تحقق من ملف `.env`
2. اقرأ رسالة الخطأ بعناية
3. ابحث عن الحل في GitHub Issues
4. تواصل مع الفريق

**التيليجرام**: @QRS_STORE
**البريد**: support@qrsstore.ly
**الهاتف**: +218925785561

---

**تم التحديث**: يوليو 2024
