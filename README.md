# EcoFine Payment (نظام إيكو فاين بايمنت)

نظام ERP متخصص لإدارة شركات البيع بالتقسيط مثل **سنتر عبدالله**، مع قابلية التشغيل محليًا (Offline-first) والتوسع إلى بنية سحابية كاملة (Cloud SaaS).

## الرؤية

بناء منصة موحدة لإدارة:
- العملاء والضامنين
- المبيعات (كاش/تقسيط)
- الأقساط والتحصيل
- المصروفات والخزينة
- القضايا القانونية
- التقارير ومؤشرات الأداء

مع قابلية التطوير إلى منتج SaaS متعدد الفروع.

---

## البنية المعمارية المستهدفة

```text
Frontend (React / Django Templates)
        ↓
Backend API (Django + DRF)
        ↓
Supabase PostgreSQL
        ↓
Cloud VPS (24/7)
```

> مبدأ أساسي: **جهاز المستخدم ليس السيرفر**. النظام يجب أن يظل يعمل حتى عند إغلاق أي جهاز محلي.

---

## الوضع الحالي للنظام

- نسخة تشغيل محلية مبنية بـ **React + IndexedDB** (SPA).
- تخزين البيانات داخل المتصفح لتوفير العمل بدون إنترنت.
- تصميم قابل للترقية إلى بنية Client-Server باستخدام Django وPostgreSQL.

---

## الموديولات الرئيسية

- Users
- Customers
- Sales
- Installments
- Payments
- Inventory
- Accounting
- Expenses
- Purchases
- Loyalty
- Legal
- Reports
- Integrations

---

## نموذج بيانات مبدئي

### Customers
- `id`
- `full_name`
- `phone`
- `national_id`
- `address`
- `status` (active / late / legal)

### Sales
- `id`
- `customer_id`
- `total_amount`
- `discount`
- `tax`
- `net_total`
- `paid_amount`
- `remaining_amount`
- `created_at`

### Installments
- `id`
- `sale_id`
- `due_date`
- `amount`
- `paid_amount`
- `status`

### Payments
- `id`
- `customer_id`
- `sale_id`
- `amount`
- `payment_method`
- `reference_number`
- `created_at`

---

## الصلاحيات (RBAC)

الأدوار المستهدفة:
- Super Admin
- Admin
- Accountant
- Sales
- Collector
- Viewer

مع صلاحيات دقيقة لكل Module.

---

## دعم الأوفلاين

- تحويل الواجهة إلى PWA.
- استخدام Service Worker + IndexedDB.
- حفظ العمليات محليًا أثناء انقطاع الإنترنت.
- مزامنة تلقائية عند عودة الاتصال.

---

## الأمان

- HTTPS
- JWT Authentication
- CSRF Protection
- Role-based Permissions
- Rate Limiting
- Logging & Monitoring
- 2FA (مرحلة متقدمة)

---

## النسخ الاحتياطي والتعافي

- Daily backups
- Weekly snapshots
- Monthly export
- Auto restart policy للسيرفر

---

## خطة التنفيذ

### المرحلة 1 (أسبوعين)
- إعداد المشروع (Django + DRF)
- Users + Customers
- نشر أول نسخة على VPS

### المرحلة 2 (3 أسابيع)
- Sales + Installments + Payments
- تقارير أولية

### المرحلة 3 (3 أسابيع)
- Inventory + Accounting + Expenses

### المرحلة 4 (4 أسابيع)
- Loyalty + Legal + Integrations
- WhatsApp notifications

---

## البنية التشغيلية المقترحة

- **Backend:** Python 3.12, Django 5, DRF, Celery
- **Queue/Broker:** Redis
- **Database:** Supabase PostgreSQL
- **Deploy:** Docker + Docker Compose + Nginx + Gunicorn
- **CI/CD:** GitHub Actions

---

## التكلفة التقديرية

- Supabase Free: مجاني (بداية)
- VPS: 5–10 دولار شهريًا
- Domain: حوالي 10 دولار سنويًا

---

## خارطة التوسع

- Multi-branch / Multi-tenant SaaS
- Mobile app
- Online payment gateway
- Public API

---

## ملاحظات

هذه الوثيقة تمثل **إصدارًا تأسيسيًا** لخطة مشروع EcoFine Payment، وقابلة للتحديث مع تقدم التنفيذ الفعلي.

## التشغيل السريع

لتشغيل نسخة الواجهة الحالية محليًا:

```bash
python3 -m http.server 8000
```

ثم افتح:

- `http://localhost:8000/index.html`
