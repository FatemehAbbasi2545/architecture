---
id: AR-02
version: "0.2"
status: approved
owner: FatemehAbbasi2545
decisions: [DEC-046, DEC-079]
title: چشم‌انداز محصول و مبانی معماری
---

> **این سند به «سری قدیمی» معماری تعلق دارد.**
> پیش از استقرار نظام حاکمیت تصمیم نوشته شده و مرجع جاری نیست. محتوایش ممکن است با تصمیم‌های
> تازه ناسازگار باشد. مرجع فعلی معماری: `AR-05` (انواع سند)، `AR-06` (نظام حاکمیت تصمیم) و
> پرونده‌های پذیرفته‌شده در `arch-decision-records/`.

> **نگاشت واژه‌ها با اسناد تحلیل و دفتر تصمیم‌ها:**
> - **Tenant** در این سند همان **سازمان بهره‌بردار** است: هویت منطقی و کسب‌وکاری مشتری، یک شرکت یا یک هلدینگ، جدا از نصب، پایگاه داده و مجوز (DEC-046 و واژه‌نامه‌ی AN-99).
> - **Company** همان **شرکت** است، یعنی شخصیت حقوقی درون سازمان بهره‌بردار، و **Holding** همان **هلدینگ** است.
> - **نصب** فقط استقرار زیرساختی است، نه هویت مشتری (DEC-046).
> - چندسازمانی، یعنی چند مشتری مستقل روی یک نصب و یک پایگاه داده، در دامنه نیست؛ چندشرکتی هست. فعلاً هر نصب یک سازمان بهره‌بردار دارد و آمادگی برای میزبانی در آینده فقط یک ویژگی طراحی است (DEC-079).
> - شناسه‌های IEP-0xx در این سند پیش از دفتر تصمیم‌ها نوشته شده‌اند. موضوع IEP-010 و IEP-011 امروز در DEC-046 و DEC-079 آمده است.


# چشم‌انداز محصول و مبانی معماری

*Product Vision & Architecture Foundations*

**<span dir="rtl">بخش اول:</span>**

<span dir="rtl">هسته تراکنشی</span> IEP <span dir="rtl">بر اساس</span> Modular Monolith <span dir="rtl">با مرزبندی دامنه‌ای و معماری ماژولار طراحی می‌شود. استفاده از</span> Microservices <span dir="rtl">فقط زمانی مجاز است که نیاز عملیاتی، مقیاس‌پذیری یا استقلال چرخه عمر آن توجیه شده باشد.</span>

<span dir="rtl">بااین‌حال، سه اصلاح ضروری داریم:</span>

<span dir="rtl">1. ماژول الزاماً معادل</span> Bounded Context <span dir="rtl">نیست. مرزهای واقعی باید از تحلیل دامنه استخراج شوند.</span>

<span dir="rtl">2. هر ماژول باید مالک قواعد کسب‌وکار و داده‌های خود باشد؛ ولی استقلال منطقی الزاماً به معنی دیتابیس فیزیکی مستقل نیست.</span>

<span dir="rtl">3. ارتباط بین ماژول‌ها نباید همگی ناهمگام (</span>async<span dir="rtl">) باشد. عملیات نیازمند سازگاری تراکنشی می‌توانند از ارتباط همگام (</span>sync<span dir="rtl">) کنترل‌شده استفاده کنند.</span>

<span dir="rtl">**وضعیت:** معماری کلان مورد توافق؛ جزئیات مرزهای ماژولی هنوز نیازمند تحلیل دامنه.</span>

**<span dir="rtl">بخش دوم:</span>**

**<span dir="rtl">فناوری‌های</span> Backend <span dir="rtl">و</span> Frontend**

| <span dir="rtl">فناوری</span> | <span dir="rtl">ارزیابی بازبینی</span>                                 |
|-------------------------------|------------------------------------------------------------------------|
| C# / ASP.NET Core             | <span dir="rtl">انتخاب مبنای هسته کسب‌وکار</span>                       |
| Angular + TypeScript          | <span dir="rtl">انتخاب مبنای رابط وب</span>                            |
| Clean Architecture + DDD      | <span dir="rtl">رویکرد معماری؛ نیازمند تعریف دقیق قواعد وابستگی</span> |
| PostgreSQL                    | <span dir="rtl">انتخاب مبنای پایگاه داده تراکنشی</span>                |

<span dir="rtl">**وضعیت**: فناوری‌های اصلی مشخص</span>

**<span dir="rtl">بخش سوم:</span>**

**<span dir="rtl">معماری</span> Tenant<span dir="rtl">،</span> Company <span dir="rtl">و استقرار</span>**

<span dir="rtl">ما تصمیم گرفتیم دو مدل استقرار داشته باشیم.</span>

- SaaS <span dir="rtl">ابری (</span>Cloud SaaS<span dir="rtl">) با مدل</span> Database-per-Tenant

- <span dir="rtl">نصب مستقل بر روی زیرساخت خود مشتری (</span>On-Premises<span dir="rtl">)</span>

<span dir="rtl">ولی در ابتدا فقط از مدل نصب مستقل (</span>On-Premises<span dir="rtl">) استفاده کنیم. قابلیت و امکان</span> SaaS <span dir="rtl">ابری (</span>Cloud SaaS<span dir="rtl">) رو داشته باشیم یعنی معماری ما</span> SaaS-Ready <span dir="rtl">باشد اما تا اطلاع ثانوی فقط از مدل استقرار نصب مستقل (</span>On-Premises<span dir="rtl">) استفاده کنیم.</span>

<span dir="rtl">مدل استقرار</span> SaaS <span dir="rtl">ابری با الگوی</span> Database-per-Tenant <span dir="rtl"></span>

<span dir="rtl">مدل استقرار</span> On-Premises <span dir="rtl">(نصب مستقل برای هر مشتری بر روی زیرساخت خود مشتری)</span>

<span dir="rtl">-</span> Tenant <span dir="rtl">نماینده مشتری سازمانی و مرز منطقی استقلال داده‌های اوست.</span>

<span dir="rtl">-</span> Company <span dir="rtl">نماینده شرکت حقوقی درون</span> Tenant <span dir="rtl">است.</span>

<span dir="rtl">- یک</span> Tenant <span dir="rtl">می‌تواند شامل صدها</span> Company <span dir="rtl">باشد.</span>

<span dir="rtl">- هر</span> Tenant <span dir="rtl">دارای دیتابیس اصلی کسب‌وکار مستقل است.</span>

<span dir="rtl">- استقرار فعلی</span> IEP <span dir="rtl">فقط</span> On-Premises <span dir="rtl">خواهد بود.</span>

<span dir="rtl">- معماری باید امکان</span> SaaS <span dir="rtl">را در آینده حفظ کند.</span>

<span dir="rtl">نکته فنی دیگر: وجود دیتابیس مستقل، کنترل دسترسی در سطح</span> Company <span dir="rtl">را حذف نمی‌کند. این کنترل باید در تمام مسیرهای خواندن، نوشتن، گزارش‌گیری، فایل‌ها و</span> AI <span dir="rtl">اعمال شود.</span>

<span dir="rtl">**وضعیت**: مبنای معماری توافق‌شده، با جزئیات اجرایی قابل تکمیل.</span>

**<span dir="rtl">بخش چهارم:</span>**

**<span dir="rtl">معماری داده و</span> PostgreSQL**

PostgreSQL <span dir="rtl">-- دیتابیس تراکنشی</span>

<span dir="rtl">بارهای تحلیلی و گزارش‌گیری سنگین نباید به‌گونه‌ای اجرا شوند که</span> SLO<span dir="rtl">های عملیات تراکنشی را مختل کنند. جداسازی بارهای کاری می‌تواند از طریق</span> Read Replica<span dir="rtl">، پایگاه داده تحلیلی مستقل، مدل‌های داده مخصوص گزارش یا سایر الگوهای مناسب انجام شود.</span>

<span dir="rtl">انتخاب</span> ClickHouse <span dir="rtl">از روز اول الزامی نیست.</span>

<span dir="rtl">همچنین</span> CDC <span dir="rtl">تنها روش انتقال داده به لایه تحلیلی نیست. انتخاب آن باید بر اساس نیاز به تازگی داده، هزینه عملیاتی، سازگاری و قابلیت بازیابی انجام شود.</span>

<span dir="rtl">در مورد داده‌های برداری نیز پیشنهاد می شود: بار سنگین</span> AI Retrieval <span dir="rtl">از</span> PostgreSQL <span dir="rtl">عملیاتی جدا شود و</span> Qdrant <span dir="rtl">می تواند گزینه جایگزین باشد.</span>

<span dir="rtl">این یک اصل معماری مناسب است، اما انتخاب قطعی</span> pgvector <span dir="rtl">یا</span> Qdrant <span dir="rtl">هنوز لازم نیست.</span>

**<span dir="rtl">بخش پنجم:</span>**

**<span dir="rtl">معماری یکپارچه‌سازی و</span> Messaging**

<span dir="rtl">این فناوری ها را می توانیم در نظر بگیریم:</span> RabbitMQ<span dir="rtl">،</span> Kafka<span dir="rtl">،</span> REST<span dir="rtl">،</span> gRPC <span dir="rtl">و</span> API Gateway

<span dir="rtl">اینجا باید دو موضوع را از هم جدا کنیم:</span>

<span dir="rtl">تصمیم معماری: یکپارچه‌سازی قابل اتکا، قراردادهای پایدار، تحویل قابل پیگیری پیام‌ها و کنترل خطا.</span>

<span dir="rtl">انتخاب فناوری:</span> RabbitMQ<span dir="rtl">،</span> Kafka<span dir="rtl">،</span> gRPC<span dir="rtl">،</span> Kong<span dir="rtl">،</span> APISIX<span dir="rtl">،</span> Envoy <span dir="rtl">و سایر محصولات.</span>

<span dir="rtl">اولی می‌تواند جزو الزامات معماری باشد؛ دومی نیازمند سناریوی عملیاتی و ارزیابی است.</span>

<span dir="rtl">در</span> IEP <span dir="rtl">نباید</span> Message Broker <span dir="rtl">را برای تمام ارتباطات داخلی اجباری کنیم.</span>

<span dir="rtl">همچنین</span> Transactional Outbox <span dir="rtl">به‌تنهایی تحویل دقیقاً یک‌بار را تضمین نمی‌کند. مصرف‌کننده باید در برابر پیام تکراری مقاوم باشد و سازوکار</span> Retry<span dir="rtl">، خطای دائمی و بازیابی نیز تعریف شود.</span>

<span dir="rtl">**وضعیت**: اصول یکپارچه‌سازی مورد توافق؛ فناوری‌های مشخص باز.</span>

**<span dir="rtl">بخش ششم:</span>**

**<span dir="rtl">امنیت،</span> Audit <span dir="rtl">و انطباق با الزامات افتا</span>**

<span dir="rtl">کنترل‌های مهم:</span> MFA<span dir="rtl">،</span> SSO<span dir="rtl">،</span> RBAC/ABAC<span dir="rtl">، رمزنگاری،</span> Tenant Isolation<span dir="rtl">،</span> API Security<span dir="rtl">،</span> Audit<span dir="rtl">، مدیریت</span> Secrets<span dir="rtl">، امنیت زنجیره تأمین و تفکیک وظایف.</span>

<span dir="rtl">زنجیره ردیابی را پیشنهادی:</span>

Requirement → Architecture Control → Implementation → Security Test → Evidence

<span dir="rtl">این بخش بسیار ارزشمند است.</span>

<span dir="rtl">اما لازم است آن را با تصمیم‌های جدیدمان درباره</span> Audit <span dir="rtl">(داده های عملیاتی و</span> log <span dir="rtl">رخدادها و تغییرات(ردپا)) تکمیل کنیم.</span>

<span dir="rtl">در معماری فعلی باید چهار دسته را مستقل تعریف کنیم:</span>

| <span dir="rtl">دسته</span> | <span dir="rtl">ماهیت</span>                         |
|-----------------------------|------------------------------------------------------|
| Business Records            | <span dir="rtl">داده‌ها و اسناد رسمی کسب‌وکار</span>   |
| Data Change History         | <span dir="rtl">سابقه تغییرات داده‌های کسب‌وکار</span> |
| Security Audit Logs         | <span dir="rtl">رخدادهای امنیتی و دسترسی</span>      |
| Operational/Technical Logs  | <span dir="rtl">رخدادهای فنی و عملیاتی سیستم</span>  |

<span dir="rtl">بر اساس گفتگوهای بعدی، مدیر امنیت مشتری باید بتواند سیاست‌های نگهداری و حذف لاگ‌های مشمول</span> Retention <span dir="rtl">را در چارچوب مجوزهای تعریف‌شده مدیریت کند. حذف کنترل‌شده لاگ‌های منقضی‌شده نباید به معنی حذف اسناد رسمی کسب‌وکار باشد.</span>

<span dir="rtl">همچنین داده‌های حساس مانند رمز عبور،</span> Token <span dir="rtl">و</span> Secret <span dir="rtl">نباید به‌عنوان مقدار قدیم و جدید در</span> Audit <span dir="rtl">ذخیره شوند.</span>

**<span dir="rtl">بخش هفتم:</span>**

**<span dir="rtl">هوش مصنوعی و</span> AI-Native**

<span dir="rtl">یک اصل مهم: مدل زبانی نباید مستقیماً عملیات نوشتن روی دیتابیس عملیاتی یا اجرای کنترل‌نشده تراکنش مالی انجام دهد.</span>

<span dir="rtl">این اصل باید در معماری</span> IEP <span dir="rtl">حفظ شود.</span>

<span dir="rtl">مسیر پیشنهادی:</span>

User → AI Gateway → Identity & Policy → Authorized Tools → Business Services → Audit

Audit <span dir="rtl">در اینجا یعنی ثبت در دیتابیس</span>

<span dir="rtl">از نظر مفهومی مناسب است، اما به اصلاح نیاز دارد.</span>

<span dir="rtl">مجوز اجرای عملیات باید در سرویس‌های کسب‌وکار نیز به‌صورت قطعی کنترل شود؛ نباید صرفاً به</span> AI Gateway <span dir="rtl">یا یک</span> Policy Check <span dir="rtl">اولیه اعتماد کنیم.</span>

<span dir="rtl">برای</span> IEP<span dir="rtl">، اصل زیر پیشنهاد می شود:</span>

**<span dir="rtl">هوش مصنوعی می‌تواند تحلیل، پیش‌بینی، پیشنهاد و در محدوده مجاز، اجرای فرایند انجام دهد؛ اما نمی‌تواند قواعد قطعی دامنه، کنترل دسترسی، الزامات تأیید انسانی یا تضمین‌های تراکنشی را دور بزند.</span>**

<span dir="rtl">از طرف دیگر، ایده</span> Semantic Business Model <span dir="rtl">بسیار مهم است. تعریف دقیق مفاهیم کسب‌وکار برای گزارش‌ها، تحلیل‌ها و</span> AI <span dir="rtl">می‌تواند از انتخاب یک مدل زبانی خاص ارزشمندتر باشد.</span>

<span dir="rtl">**وضعیت**:</span> AI-Native <span dir="rtl">به‌عنوان جهت‌گیری محصول؛ معماری اجرایی، موارد استفاده، سطح خودمختاری و فناوری‌ها نیازمند طراحی تکمیلی.</span>

**<span dir="rtl">بخش هشتم:</span>**

**Performance<span dir="rtl">،</span> Availability <span dir="rtl">و</span> Disaster Recovery**

<span dir="rtl">ما می توانیم برای شاخص های</span> Availability<span dir="rtl">،</span> API Latency<span dir="rtl">،</span> RPO <span dir="rtl">و</span> RTO <span dir="rtl">مقدار عددی پیشنهادی، تعیین کنیم.</span>

<span dir="rtl">برای معماری</span> On-Premises<span dir="rtl">(نصب مستقل بر روی زیرساخت خود مشتری)، یک ملاحظه مهم داریم:</span>

<span dir="rtl">ما نمی‌توانیم بدون تعیین توپولوژی نصب، ظرفیت سخت‌افزاری، شبکه،</span> Backup<span dir="rtl">،</span> HA <span dir="rtl">و مسئولیت‌های عملیاتی مشتری، این اعداد را برای تمام نصب‌ها تضمین کنیم.</span>

<span dir="rtl">بنابراین پیشنهاد می‌شود در</span> IEP <span dir="rtl">میان سه مفهوم تمایز بگذاریم:</span>

<span dir="rtl">-</span> **Product Capability**<span dir="rtl">: محصول از نظر فنی چه قابلیت‌های تاب‌آوری و بازیابی دارد؟</span>

<span dir="rtl">-</span> **Reference Deployment**<span dir="rtl">: با چه توپولوژی و حداقل منابعی می‌توان به اهداف مشخص رسید؟</span>

<span dir="rtl">-</span> **Contractual SLA**<span dir="rtl">: چه سطح خدمتی با چه مسئولیت‌هایی به مشتری تعهد داده می‌شود؟</span>

<span dir="rtl">همچنین</span> Retry <span dir="rtl">در عملیات مالی باید با</span> Idempotency <span dir="rtl">و قواعد تراکنشی همراه باشد.</span>

**<span dir="rtl">بخش نهم:</span>**

**<span dir="rtl">تضمین کیفیت و</span> Quality Engineering**

<span dir="rtl">آزمون‌ها را می تواندر حوزه‌های عملکرد، قابلیت اتکا، امنیت، صحت داده، معماری، کیفیت</span> AI<span dir="rtl">، نگهداری‌پذیری و بازیابی دسته‌بندی کرد.</span>

<span dir="rtl">این بخش را باید حفظ و تقویت کنیم.</span>

<span dir="rtl">اما یک نکته مهم:</span>

Quality Engineering <span dir="rtl">یک فعالیت انتهایی تیم</span> QA <span dir="rtl">نیست؛ مجموعه‌ای از الزامات، معیارهای پذیرش، آزمون‌های خودکار و شواهد قابل ردیابی در تمام چرخه توسعه است.</span>

<span dir="rtl">برای مثال، اگر اصل معماری ما</span> Company Isolation <span dir="rtl">باشد، باید آزمون‌های خودکار ثابت کنند که کاربر مجاز شرکت</span> A <span dir="rtl">نمی‌تواند داده شرکت</span> B <span dir="rtl">را بدون مجوز بخواند یا تغییر دهد.</span>

<span dir="rtl">همین منطق درباره</span> Audit<span dir="rtl">،</span> Optimistic Concurrency<span dir="rtl">،</span> Idempotency<span dir="rtl">، بازیابی اطلاعات و امنیت ابزارهای</span> AI <span dir="rtl">نیز برقرار است.</span>

**<span dir="rtl">بخش دهم</span>**

**<span dir="rtl">نقشه راه و مستندات معماری</span>**

<span dir="rtl">هفت مرحله پیشنهادی: شناخت محصول، طراحی دامنه، امنیت، داده، زیرساخت،</span> PoC <span dir="rtl">و تثبیت معماری</span>

<span dir="rtl">همچنین تهیه</span> Domain Map<span dir="rtl">،</span> C4<span dir="rtl">،</span> Security Architecture<span dir="rtl">،</span> Data Architecture<span dir="rtl">،</span> NFR Specification<span dir="rtl">،</span> Threat Model<span dir="rtl">،</span> ADR <span dir="rtl">و سایر مستندات، ضروری است.</span>

<span dir="rtl">این چارچوب همچنان مفید است.</span>

<span dir="rtl">اما باید پیش از تثبیت معماری، تحلیل دامنه صنعت هدف و مدیریت جامع پیمان را در اولویت قرار دهیم. همچنین معماری هلدینگ‌های چندشرکتی، فرم‌ساز و تفکیک پرتال داخلی و خارجی باید در طراحی لحاظ شوند.</span>

**<span dir="rtl">نقشه راه اولیه باید در مراحل بعدی بازنویسی شود.</span>**

**<span dir="rtl">دفتر تصمیم‌های تجمیعی</span>**

<span dir="rtl">این نخستین نسخه دفتر تصمیم‌هاست. شناسه‌ها موقت اما پایدار هستند و در مراحل بعدی وضعیت آن‌ها را به‌روزرسانی خواهیم کرد</span>.

| <span dir="rtl">شناسه</span> | <span dir="rtl">موضوع</span>                                                                            | <span dir="rtl">وضعیت فعلی</span>                                 |
|------------------------------|---------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| IEP-001                      | <span dir="rtl">امنیت، کیفیت، عملکرد و قابلیت اتکا به‌عنوان اهداف بنیادی</span>                          | <span dir="rtl">اصل راهبردی</span>                                |
| IEP-002                      | <span dir="rtl">هسته تراکنشی</span> Modular Monolith                                                    | <span dir="rtl">توافق‌شده</span>                                   |
| IEP-003                      | DDD <span dir="rtl">و مرزبندی دامنه‌ای</span>                                                            | <span dir="rtl">توافق‌شده در سطح رویکرد</span>                     |
| IEP-004                      | Microservices <span dir="rtl">فقط با توجیه عملیاتی</span>                                               | <span dir="rtl">توافق‌شده</span>                                   |
| IEP-005                      | Event-Driven Integration <span dir="rtl">به‌صورت انتخابی</span>                                          | <span dir="rtl">توافق‌شده</span>                                   |
| IEP-006                      | ASP.NET Core <span dir="rtl">و</span> C<span dir="rtl">\#</span>                                        | <span dir="rtl">انتخاب مبنا</span>                                |
| IEP-007                      | Angular <span dir="rtl">و</span> TypeScript                                                             | <span dir="rtl">انتخاب مبنا</span>                                |
| IEP-008                      | PostgreSQL <span dir="rtl">برای</span> OLTP                                                             | <span dir="rtl">انتخاب مبنا</span>                                |
| IEP-009                      | On-Premises First, SaaS-Ready                                                                           | <span dir="rtl">توافق‌شده</span>                                   |
| IEP-010                      | Database-per-Tenant                                                                                     | <span dir="rtl">توافق‌شده</span>                                   |
| IEP-011                      | <span dir="rtl">تفکیک</span> Tenant <span dir="rtl">و</span> Company                                    | <span dir="rtl">توافق‌شده</span>                                   |
| IEP-012                      | Company-aware Authorization                                                                             | <span dir="rtl">اصل الزامی معماری</span>                          |
| IEP-013                      | <span dir="rtl">تفکیک</span> Business Records <span dir="rtl">و انواع</span> Log                        | <span dir="rtl">توافق‌شده در سطح مفهومی</span>                     |
| IEP-014                      | <span dir="rtl">سیاست نگهداری و حذف کنترل‌شده لاگ‌ها</span>                                               | <span dir="rtl">توافق‌شده در سطح سیاست؛ جزئیات باز</span>          |
| IEP-015                      | Optimistic Concurrency <span dir="rtl">در مرز</span> Aggregate                                          | <span dir="rtl">مبنای توافق‌های بعدی؛ نیازمند جزئیات اجرایی</span> |
| EP-016                       | AI-Native <span dir="rtl">و اجرای عملیات از مسیر سرویس‌های مجاز دامنه</span>                             | <span dir="rtl">اصل معماری</span>                                 |
| IEP-017                      | Semantic Business Model                                                                                 | <span dir="rtl">پیشنهاد راهبردی</span>                            |
| IEP-018                      | ClickHouse<span dir="rtl">،</span> Elasticsearch <span dir="rtl">و موتور</span> Vector                  | <span dir="rtl">باز</span>                                        |
| IEP-019                      | RabbitMQ<span dir="rtl">،</span> Kafka <span dir="rtl">و</span> API Gateway <span dir="rtl">مشخص</span> | <span dir="rtl">باز</span>                                        |
| IEP-020                      | Flutter<span dir="rtl">،</span> Go <span dir="rtl">و</span> Micro-Frontend                              | <span dir="rtl">باز</span>                                        |
| IEP-021                      | <span dir="rtl">اهداف عددی</span> SLO / RPO / RTO <span dir="rtl"></span>                               | <span dir="rtl">پیشنهادی</span>                                   |
| EP-022                       | Quality Engineering <span dir="rtl">و آزمون‌پذیری الزامات</span>                                         | <span dir="rtl">اصل مهندسی</span>                                 |
| IEP-023                      | Legal Hold <span dir="rtl">برای شواهد</span> Audit                                                      | <span dir="rtl">نیازمند تطبیق با اسناد بعدی</span>                |
| IEP-024                      | <span dir="rtl">انتخاب موتور</span> Workflow / BPMN                                                     | <span dir="rtl">باز</span>                                        |
| IEP-025                      | <span dir="rtl">مدل استقرار و عملیات سرویس‌های</span> AI <span dir="rtl">در محیط</span> On-Premises      | <span dir="rtl">باز</span>                                        |

**<span dir="rtl">اصول غیرقابل مذاکره — نسخه پیشنهادی برای</span> IEP**

<span dir="rtl">در این مرحله بهتر است بین اهداف بنیادی اعلام‌شده و اصول اجرایی استخراج‌شده از آن اهداف تفاوت بگذاریم.</span>

<span dir="rtl">اصول اجرایی پیشنهادی:</span>

**<span dir="rtl">اصول بنیادی معماری</span> IEP**

<span dir="rtl">1. هیچ عملیات کسب‌وکار نباید کنترل دسترسی معتبر</span> Tenant <span dir="rtl">و</span> Company <span dir="rtl">را دور بزند.</span>

<span dir="rtl">2. یکپارچگی داده‌های تراکنشی و قواعد دامنه نباید قربانی معماری توزیع‌شده یا قابلیت‌های</span> AI <span dir="rtl">شود.</span>

<span dir="rtl">3. داده‌های محرمانه نباید از مسیر</span> Audit<span dir="rtl">،</span> Logging<span dir="rtl">،</span> Telemetry <span dir="rtl">یا</span> AI <span dir="rtl">افشا شوند.</span>

<span dir="rtl">4. عملیات حساس باید قابلیت ردیابی، کنترل مجوز و آزمون‌پذیری داشته باشند.</span>

<span dir="rtl">5. قابلیت‌های ضروری محصول در نصب مستقل نباید به اتصال اجباری به زیرساخت مرکزی فروشنده وابسته باشند.</span>

<span dir="rtl">6. معماری باید امکان بازیابی قابل آزمون، مدیریت خطا و ارتقای کنترل‌شده را فراهم کند.</span>

<span dir="rtl">7. فناوری جدید فقط با نیاز مشخص و توجیه فنی یا تجاری وارد محصول شود.</span>

<span dir="rtl">8. الزامات امنیتی و کیفیت باید به کنترل اجرایی و شواهد آزمون قابل ردیابی تبدیل شوند.</span>

**<span dir="rtl">پرسش‌های باز استخراج‌شده از مرحله اول</span>**

| <span dir="rtl">حوزه</span> | <span dir="rtl">پرسش باقی‌مانده</span>                                                                                       |
|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| Domain                      | <span dir="rtl">مرز دقیق</span> Bounded Context<span dir="rtl">های اصلی</span> IEP <span dir="rtl">چیست؟</span>             |
| Workflow                    | <span dir="rtl">کدام فرایندها نیازمند</span> BPMN <span dir="rtl">و کدام نیازمند ارکستراسیون فنی هستند؟</span>              |
| AI                          | <span dir="rtl">اولین قابلیت‌های هوشمند محصول کدام‌اند و چه سطحی از خودمختاری مجاز است؟</span>                                |
| Data                        | <span dir="rtl">چه بار کاری، انتخاب پایگاه تحلیلی مستقل را توجیه می‌کند؟</span>                                              |
| Security                    | <span dir="rtl">ماتریس الزامات افتا و شواهد انطباق چگونه تعریف می‌شود؟</span>                                                |
| Audit                       | <span dir="rtl">قواعد دقیق</span> Retention<span dir="rtl">، حذف، استثناها و</span> Legal Hold <span dir="rtl">چیست؟</span> |
| Infrastructure              | <span dir="rtl">حداقل و مرجع توپولوژی نصب مستقل چه خواهد بود؟</span>                                                        |
| Reliability                 | SLO<span dir="rtl">ها برای چه سناریوها و کلاس‌هایی از استقرار تعیین می‌شوند؟</span>                                           |
| Architecture                | <span dir="rtl">معیار رسمی استخراج یک ماژول از</span> Monolith <span dir="rtl">چیست؟</span>                                 |

**<span dir="rtl">متن بازنویسی‌شده معماری مبنا — حاصل مرحله اول</span>**

<span dir="rtl">این متن، خروجی یکپارچه و اصلاح‌شده مرحله اول است و می‌تواند مبنای نسخه‌های بعدی سند معماری قرار گیرد.</span>

**IEP — Architecture Foundation**

**<span dir="rtl">چشم‌انداز</span>**

IEP <span dir="rtl">یک پلتفرم هوشمند سازمانی با معماری ماژولار، امنیت سازمانی، قابلیت اتکای بالا و توسعه‌پذیری بلندمدت است که برای مدیریت فرایندهای پیچیده کسب‌وکار و ساختارهای چندشرکتی طراحی می‌شود.</span>

**<span dir="rtl">معماری نرم‌افزار</span>**

<span dir="rtl">هسته تراکنشی بر اساس</span> Domain-Driven Design<span dir="rtl">، مرزبندی روشن ماژول‌ها و</span> Modular Monolith <span dir="rtl">توسعه می‌یابد. ارتباطات داخلی بر اساس نیاز به سازگاری تراکنشی یا استقلال پردازشی انتخاب می‌شوند.</span> Microservices <span dir="rtl">و ارتباطات ناهمگام صرفاً در موارد دارای توجیه مشخص استفاده خواهند شد.</span>

**<span dir="rtl">معماری استقرار</span>**

<span dir="rtl">محصول در فاز عملیاتی نخست به‌صورت مستقل در زیرساخت مشتری مستقر می‌شود. طراحی از ابتدا امکان ارائه</span> SaaS <span dir="rtl">را حفظ می‌کند، بدون آنکه پیچیدگی کامل عملیات</span> SaaS <span dir="rtl">به استقرار اولیه تحمیل شود.</span>

**<span dir="rtl">معماری داده</span>**

PostgreSQL <span dir="rtl">پایگاه داده اصلی تراکنشی است. هر</span> Tenant <span dir="rtl">دیتابیس کسب‌وکار مستقل دارد و می‌تواند شامل چندین</span> Company <span dir="rtl">باشد. کنترل دسترسی شرکت‌ها در تمام مسیرهای داده الزامی است. بارهای تحلیلی و هوش مصنوعی باید به‌گونه‌ای مدیریت شوند که عملکرد و یکپارچگی تراکنش‌های عملیاتی مختل نشود.</span>

**<span dir="rtl">معماری امنیت</span>**

<span dir="rtl">**ا**منیت از ابتدای طراحی در تمام لایه‌ها اعمال می‌شود. کنترل دسترسی، جداسازی داده، حفاظت از اطلاعات حساس، ثبت رخدادهای قابل ردیابی، تفکیک وظایف و مدیریت امن عملیات، بخش ذاتی معماری هستند. الزامات قابل اعمال امنیتی باید به کنترل‌ها و آزمون‌های اثبات‌پذیر نگاشت شوند.</span>

**<span dir="rtl">معماری هوش مصنوعی</span>**

AI <span dir="rtl">یکی از قابلیت‌های بنیادی محصول است، اما اختیار اجرای عملیات آن باید از مسیر قراردادهای معتبر دامنه، کنترل‌های امنیتی و سیاست‌های تأیید عبور کند. انتخاب مدل‌ها، پروتکل‌ها و زیرساخت</span> AI <span dir="rtl">باید مستقل از منطق اصلی کسب‌وکار و قابل تغییر باشد.</span>

**<span dir="rtl">مهندسی کیفیت</span>**

<span dir="rtl">عملکرد، قابلیت اتکا، امنیت، نگهداری‌پذیری، یکپارچگی داده و بازیابی باید از طریق معیارهای قابل‌اندازه‌گیری و آزمون‌های تکرارپذیر اثبات شوند. هیچ ادعای کیفی صرفاً بر اساس انتخاب فناوری پذیرفته نخواهد شد.</span>

<span dir="rtl">مرحله اول سه دستاورد اصلی برای ما دارد: چشم‌انداز محصول را مشخص می‌کند، مبنای معماری ماژولار را ارائه می‌دهد و کیفیت و امنیت را از ابتدا وارد طراحی می‌کند.</span>

<span dir="rtl">در مقابل، سه ضعف اصلی آن نیز روشن شد: انتخاب‌های فناوری بیش از حد زودهنگام، نبود تفکیک کافی میان تصمیم قطعی و پیشنهاد، و فقدان جزئیات دامنه و مدل عملیاتی محصول.</span>

<span dir="rtl">نتیجه این مرحله را به‌عنوان</span> Baseline <span dir="rtl">موقت شماره ۱ ثبت می‌کنیم. در مراحل بعدی، هر تصمیم را با شواهد جدید اصلاح یا تثبیت خواهیم کرد.</span>
