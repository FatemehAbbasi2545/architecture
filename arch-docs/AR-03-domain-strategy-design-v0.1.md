---
id: AR-03
version: "0.3"
status: approved
owner: FatemehAbbasi2545
decisions: [DEC-046, DEC-049, DEC-079]
title: شناخت راهبردی دامنه و طراحی مرزهای کسب‌وکار
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


# شناخت راهبردی دامنه و طراحی مرزهای کسب‌وکار 

*Domain Discovery and Strategic Design*

<span dir="rtl">بحث را از **انتخاب فناوری به سمت شناخت دامنه، تعیین مالکیت قواعد کسب‌وکار و کشف مرزهای واقعی سیستم می‌بریم.**</span>

**<span dir="rtl">مهم‌ترین نتیجه این مرحله این است: ما باید ابتدا باید قابلیت‌های کسب‌وکار، فرایندهای واقعی، مالکیت داده‌ها و مرزهای تراکنشی را بشناسیم. سپس معماری نرم‌افزار را از آن‌ها استخراج کنیم.</span>**

<span dir="rtl">**نکته بسیار مهم**:</span> Core Domain <span dir="rtl">را استراتژی محصول تعیین می‌کند، نه صرفاً پیچیدگی فنی یک ماژول.</span>

**<span dir="rtl">دسته‌بندی دامنه‌ها در</span> DDD**

<span dir="rtl">سه دسته را معرفی سه دسته:</span>

<span dir="rtl">-</span> **Core Domain**<span dir="rtl">: قابلیت‌هایی که محصول را متمایز می‌کنند.</span>

<span dir="rtl">-</span> **Supporting Domain**<span dir="rtl">: قابلیت‌های اختصاصی موردنیاز برای پشتیبانی از دامنه اصلی.</span>

<span dir="rtl">-</span> **Generic Domain**<span dir="rtl">: قابلیت‌های عمومی و قابل استفاده مجدد.</span>

<span dir="rtl">این طبقه‌بندی صحیح و کاربردی است؛ اما باید یک سوءبرداشت را اصلاح کنیم.</span>

**Core Domain <span dir="rtl">لزوماً مهم‌ترین ماژول از نظر حجم کد، تعداد کاربران یا حساسیت مالی نیست</span>**<span dir="rtl">.</span> Core Domain <span dir="rtl">آن بخش از مسئله کسب‌وکار است که مزیت رقابتی</span> IEP <span dir="rtl">را ایجاد می‌کند و سرمایه‌گذاری عمیق روی مدل دامنه آن توجیه دارد.</span>

<span dir="rtl">همچنین یک دامنه می‌تواند از نظر عملیاتی بسیار حیاتی باشد، اما در استراتژی تمایز محصول،</span> Supporting <span dir="rtl">یا</span> Generic <span dir="rtl">محسوب شود.</span>

**<span dir="rtl">تطبیق با شناخت فعلی</span> IEP**

<span dir="rtl">با توجه به بازار هدف و اولویت‌های شناخته‌شده، دسته‌بندی اولیه زیر پیشنهاد می شود:</span>

| <span dir="rtl">قابلیت کسب‌وکار</span>                            | <span dir="rtl">دسته‌بندی پیشنهادی</span> | <span dir="rtl">توضیح</span>                                     |
|------------------------------------------------------------------|------------------------------------------|------------------------------------------------------------------|
| <span dir="rtl">مدیریت جامع چرخه عمر پیمان</span>                | Core Candidate                           | <span dir="rtl">نامزد اصلی تمایز محصول</span>                    |
| <span dir="rtl">مدیریت تعهدات و عملکرد پیمان</span>              | Core Candidate                           | <span dir="rtl">وابسته به تحلیل واقعی دامنه</span>               |
| <span dir="rtl">مدیریت تغییرات، الحاقیه‌ها و ادعاهای پیمان</span> | Core Candidate                           | <span dir="rtl">دارای منطق تخصصی صنعت</span>                     |
| <span dir="rtl">کنترل هزینه و پیشرفت پیمان</span>                | Core Candidate                           | <span dir="rtl">نیازمند تعیین مرز با مالی و پروژه</span>         |
| <span dir="rtl">حسابداری عمومی</span>                            | Supporting/Generic Candidate             | <span dir="rtl">حیاتی، اما الزاماً عامل تمایز نیست</span>         |
| <span dir="rtl">مدیریت هویت و احراز هویت</span>                  | Generic                                  | <span dir="rtl">ترجیحاً مبتنی بر استانداردها</span>               |
| <span dir="rtl">مدیریت اسناد</span>                              | Supporting                               | <span dir="rtl">ممکن است در پیمان‌ها منطق تخصصی داشته باشد</span> |
| <span dir="rtl">گردش کار عمومی</span>                            | Supporting/Generic                       | <span dir="rtl">موتور عمومی با فرایندهای اختصاصی</span>          |
| <span dir="rtl">مدیریت ساختار شرکت‌های هلدینگ</span>              | Supporting/Platform                      | <span dir="rtl">قابلیت پایه مشترک میان دامنه‌ها</span>            |

Core Candidate <span dir="rtl">یعنی نامزد دامنه اصلی، نه تصمیم نهایی درباره مرز</span> Bounded Context <span dir="rtl">یا ماژول اجرایی.</span>

<span dir="rtl">  
یک نکته ظریف: مدیریت پیمان ممکن است خودش شامل چندین</span> Subdomain <span dir="rtl">و</span> Bounded Context <span dir="rtl">باشد. بنابراین نباید از همین حالا فرض کنیم تمام قابلیت‌های آن در یک ماژول واحد قرار خواهند گرفت.</span>

<span dir="rtl">**نتیجه**: اصل دسته‌بندی دامنه‌ها پذیرفته می‌شود؛ تعیین نهایی</span> Core Domain<span dir="rtl">ها پس از تکمیل</span> Business Capability Map <span dir="rtl">و تحلیل رقابتی محصول انجام خواهد شد.</span>

> **به‌روزرسانی (DEC-049):** دسته‌بندی نهایی زیردامنه‌ها در DEC-049 ثبت شد و جای جدول بالا را می‌گیرد. زیردامنه‌های هسته شامل مدیریت پیمان دوطرفه، کنترل پروژه و پیشرفت، کنترل بودجه و تعهد، مدیریت هوشمند دارایی و هفت تمایز پلتفرمی AN-01 است. حسابداری عمومی پشتیبان، و هویت و دسترسی عمومی است. ساختار چندشرکتی جزو بستر مشترک است. اولین برش عمودی باید از زیردامنه‌های هسته‌ی ردیف اول انتخاب شود.

**<span dir="rtl">بازبینی فهرست</span> Bounded Context<span dir="rtl">ها</span>**

| Context <span dir="rtl">پیشنهادی</span> | <span dir="rtl">مسئولیت معرفی‌شده</span>                           |
|-----------------------------------------|-------------------------------------------------------------------|
| Tenant Management                       | <span dir="rtl">مشتریان، اشتراک‌ها، تنظیمات و محدودیت‌ها</span>     |
| Organization                            | <span dir="rtl">شرکت‌های حقوقی، شعب و ساختار سازمانی</span>        |
| Identity & Access                       | <span dir="rtl">کاربران، نقش‌ها، مجوزها و سیاست‌های دسترسی</span>   |
| General Ledger                          | <span dir="rtl">حساب‌ها، اسناد مالی، دوره‌های مالی و دفتر کل</span> |
| Workflow                                | <span dir="rtl">فرایندها، وظایف و تأییدیه‌ها</span>                |
| Document Management                     | <span dir="rtl">اسناد، پیوست‌ها و نسخه‌بندی</span>                  |
| Audit & Compliance                      | <span dir="rtl">رویدادهای حسابرسی و شواهد انطباق</span>           |

**<span dir="rtl">این فهرست را باید به‌عنوان</span> Context Catalog <span dir="rtl">اولیه حفظ کنیم، نه نقشه نهایی</span> Bounded Context<span dir="rtl">های</span> IEP<span dir="rtl">.</span>**

**<span dir="rtl">اصلاح اول:</span> Bounded Context <span dir="rtl">با ماژول نرم‌افزاری یکسان نیست</span>**

Bounded Context <span dir="rtl">مرزی است که درون آن مدل دامنه و زبان کسب‌وکار معنای مشخص و سازگاری دارند.</span>

<span dir="rtl">ممکن است یک</span> Bounded Context <span dir="rtl">در یک ماژول پیاده‌سازی شود؛ اما این رابطه همیشه یک‌به‌یک نیست.</span>

<span dir="rtl">برای مثال، یک ماژول مدیریت پیمان ممکن است چند</span> Context <span dir="rtl">مستقل داشته باشد و یک</span> Context <span dir="rtl">نیز در سطح پیاده‌سازی شامل چند مؤلفه باشد.</span>

**<span dir="rtl">اصلاح دوم:</span> Tenant Management <span dir="rtl">با</span> Organization <span dir="rtl">متفاوت است</span>**

**Tenant Management** <span dir="rtl">مسئول هویت و پیکربندی مشتری سازمانی است؛ اما در نصب مستقل</span> On-Premises <span dir="rtl">لزوماً به یک سرویس</span> SaaS Subscription Management <span dir="rtl">نیاز نداریم.</span>

**Organization** <span dir="rtl">مسئول مدل شرکت‌های حقوقی، ساختار هلدینگ، واحدها و روابط سازمانی است.</span>

<span dir="rtl">در نتیجه نباید</span> Tenant <span dir="rtl">را معادل</span> Company <span dir="rtl">یا</span> Holding <span dir="rtl">تعریف کنیم.</span>

**<span dir="rtl">اصلاح سوم:</span> Audit & Compliance <span dir="rtl">نباید یک دامنه مبهم باشد</span>**

<span dir="rtl">فهرست،</span> Audit <span dir="rtl">و</span> Compliance <span dir="rtl">را در یک عنوان قرار داده است</span>.

<span dir="rtl">باید تفکیک کنیم:</span>

<span dir="rtl">-</span> Business Records <span dir="rtl">متعلق به دامنه‌های کسب‌وکار هستند.</span>

<span dir="rtl">-</span> Data Change History <span dir="rtl">مسئول ثبت تاریخچه تغییرات است.</span>

<span dir="rtl">-</span> Security Audit Logs <span dir="rtl">رخدادهای امنیتی را ثبت می‌کنند.</span>

<span dir="rtl">-</span> Operational/Technical Logs <span dir="rtl">برای عیب‌یابی و پایش هستند.</span>

<span dir="rtl">-</span> Compliance <span dir="rtl">شامل الزامات، کنترل‌ها و شواهد انطباق است و الزاماً یک</span> Bounded Context <span dir="rtl">واحد نیست.</span>

<span dir="rtl">این تفکیک به معنی تصمیم قطعی برای ایجاد پنج سرویس یا پنج دیتابیس نیست.</span>

**<span dir="rtl">اصلاح چهارم: دامنه‌های تخصصی صنعت در فهرست غایب‌اند</span>**

<span dir="rtl">در نسخه بعدی</span> Domain Map <span dir="rtl">باید قابلیت‌های مدیریت پیمان، تعهدات قراردادی، الحاقیه‌ها، صورت‌وضعیت‌ها، کنترل پیشرفت، تضامین، مطالبات و تعهدات طرف‌های قرارداد نیز بررسی شوند.</span>

<span dir="rtl">اما هنوز برای تعیین مرز قطعی این</span> Context<span dir="rtl">ها زود است.</span>

**<span dir="rtl">بازبینی تعامل</span> Inventory <span dir="rtl">و</span> Finance**

<span dir="rtl">مثالی داریم: هنگام تأیید رسید کالا،</span> Inventory <span dir="rtl">مالک ثبت تغییر موجودی باشد و</span> Finance <span dir="rtl">از طریق قرارداد رویدادی مشخص، ثبت مالی مربوط را انجام دهد؛ همچنین سازوکار تطبیق و رفع مغایرت طراحی شود.</span>

<span dir="rtl">اصل مالکیت دامنه صحیح است؛ اما نحوه اجرای تراکنش نیازمند دقت بیشتری است.</span>

<span dir="rtl">فرض کنیم رسید کالایی تأیید می‌شود و ارزش موجودی باید در حسابداری ثبت شود.</span>

<span dir="rtl">دو طراحی محتمل داریم:</span>

<img src="AR-03-assets/media/image1.png" style="width:8.425in;height:2.94722in" />

<span dir="rtl">**تصمیم پیشنهادی**: رویدادی‌بودن تعامل بین دو</span> Context<span dir="rtl">، به‌تنهایی به معنی ناهمگام‌بودن یا</span> Eventual Consistency <span dir="rtl">نیست.</span>

<span dir="rtl">انتخاب میان این دو گزینه باید با قواعد واقعی ثبت مالی، زمان قطعی‌شدن عملیات، تحمل تأخیر و الزامات سازگاری داده انجام شود.</span>

**<span dir="rtl">بازبینی معماری</span> AI <span dir="rtl">در</span> SaaS <span dir="rtl">و</span> On-Premises <span dir="rtl"></span>**

**SaaS**<span dir="rtl">: مدل استقرار</span> Cloud SaaS

**On-Premises**<span dir="rtl">: مدل استقرار نصب مستقل برای هر مشتری بر روی زیرساخت خود مشتری</span>

<span dir="rtl">سه الگوی ارائه هوش مصنوعی معرفی شده است:</span>

| <span dir="rtl">الگو</span> | <span dir="rtl">تعریف</span>                                        | <span dir="rtl">ارزیابی جدید</span>                      |
|-----------------------------|---------------------------------------------------------------------|----------------------------------------------------------|
| Cloud AI                    | <span dir="rtl">استفاده از مدل‌های میزبانی‌شده با کنترل داده</span>   | <span dir="rtl">گزینه آینده، مشروط به سیاست مشتری</span> |
| Private AI                  | <span dir="rtl">مدل اختصاصی در محیط خصوصی مشتری</span>              | <span dir="rtl">گزینه مناسب برای برخی سازمان‌ها</span>    |
| Local AI                    | <span dir="rtl">اجرای مدل در زیرساخت داخلی، حتی بدون اینترنت</span> | <span dir="rtl">قابلیت راهبردی مهم برای نصب مستقل</span> |

<span dir="rtl">همچنین پیشنهاد استفاده از</span> Model Gateway / Provider Abstraction <span dir="rtl">برای جلوگیری از وابستگی به یک ارائه‌دهنده و جداسازی</span> Tenant <span dir="rtl">در</span> Retrieval<span dir="rtl">،</span> Vector Index<span dir="rtl">،</span> Cache<span dir="rtl">، حافظه عامل‌ها و ابزارهای اجرایی، مطرح می شود.</span>

**<span dir="rtl">اصلاح معماری پیشنهادی</span>**

<span dir="rtl">به‌جای اینکه سه الگوی</span> Cloud<span dir="rtl">،</span> Private <span dir="rtl">و</span> Local <span dir="rtl">را سه معماری مستقل بدانیم، بهتر است آن‌ها را **گزینه‌های استقرار** و **اجرای مدل** در یک معماری</span> AI <span dir="rtl">قابل پیکربندی تعریف کنیم.</span>

<span dir="rtl">البته این گزینه‌ها کاملاً هم‌معنی نیستند:</span> Private AI <span dir="rtl">ممکن است در ابر خصوصی اجرا شود، درحالی‌که</span> Local AI <span dir="rtl">بر اجرای داخلی تأکید دارد. اجرای بدون اینترنت نیز یک قابلیت جداگانه است که باید آزموده شود.</span>

<span dir="rtl">برای</span> IEP<span dir="rtl">، چهار اصل مهم پیشنهاد می شود:</span>

<span dir="rtl">1. قابلیت‌های ضروری</span> ERP <span dir="rtl">بدون سرویس</span> AI <span dir="rtl">خارجی کار کنند.</span>

<span dir="rtl">2.</span> AI Provider <span dir="rtl">قابل تعویض باشد، بدون تغییر قواعد دامنه.</span>

<span dir="rtl">3. اطلاعات و مجوزهای</span> Tenant <span dir="rtl">و</span> Company <span dir="rtl">در تمام مسیرهای</span> AI <span dir="rtl">اعمال شوند.</span>

<span dir="rtl">4. ارسال داده به ارائه‌دهندگان خارجی تابع سیاست امنیتی و مجوزهای مشتری باشد.</span>

**<span dir="rtl">یک نکته مهم درباره</span> On-Premises <span dir="rtl">(نصب مستقل): </span>**SaaS-Ready <span dir="rtl">بودن نباید باعث شود نصب مستقل برای احراز هویت، اجرای فرایندهای اصلی یا دسترسی به داده‌های عملیاتی به سرویس مرکزی فروشنده وابسته باشد.</span>

<span dir="rtl">بااین‌حال، اینکه کدام قابلیت‌های</span> AI <span dir="rtl">باید در حالت کاملاً آفلاین ارائه شوند، هنوز نیازمند تصمیم محصول و ارزیابی سخت‌افزار است.</span>

<span dir="rtl">**وضعیت**: اصول جداسازی و استقلال از ارائه‌دهنده، مبنای معماری؛ جزئیات استقرار مدل‌ها و سطح پشتیبانی آفلاین، باز.</span>

**<span dir="rtl">  
بازبینی اولین برش عملی معماری</span>**

<span dir="rtl">سناریوی</span> Procure-to-Pay <span dir="rtl">به‌عنوان نخستین برش عملی پیشنهاد شده است.</span>

<span dir="rtl">مراحل آن عبارت‌اند از:</span>

**Procure-to-Pay <span dir="rtl">— سناریوی پیشنهادی </span>**

<span dir="rtl">1. ثبت درخواست خرید</span>

<span dir="rtl">2. گردش تأیید درخواست</span>

<span dir="rtl">3. صدور سفارش خرید</span>

<span dir="rtl">4. ثبت رسید کالا در انبار</span>

<span dir="rtl">5. ثبت و تطبیق صورت‌حساب تأمین‌کننده</span>

<span dir="rtl">6. ایجاد بدهی و سند حسابداری</span>

<span dir="rtl">7. تأیید و ثبت پرداخت</span>

<span dir="rtl">8. تحلیل هوشمند مغایرت‌ها و ریسک‌ها</span>

<span dir="rtl">این سناریو برای آزمون معماری بسیار مناسب است؛ زیرا چندین دامنه و قابلیت زیرساختی را درگیر می‌کند. فایل نیز همین هدف را بیان کرده است.</span>

<span dir="rtl">اما با توجه به شناخت ما از اولویت‌های</span> IEP<span dir="rtl">، یک اصلاح مهم پیشنهاد می‌کنم.</span>

**Procure-to-Pay <span dir="rtl">را به‌عنوان سناریوی مرجع معماری حفظ کنیم، ولی هنوز آن را اولین برش اجرایی محصول ندانیم.</span>**

<span dir="rtl">چرا؟</span>

<span dir="rtl">چون محصول اولیه</span> IEP <span dir="rtl">قرار است بر نیازهای تخصصی صنعت و مدیریت جامع پیمان متمرکز باشد. بنابراین ممکن است یک سناریوی واقعی مدیریت پیمان، هم ارزش کسب‌وکاری بیشتری داشته باشد و هم مرزهای مهم‌تری از معماری را آشکار کند.</span>

<span dir="rtl">برای نمونه، می‌توان در آینده سناریویی از ثبت پیمان تا مدیریت تعهدات، تغییرات، صورت‌وضعیت و تأیید پرداخت را بررسی کرد.</span>

<span dir="rtl">این صرفاً یک **نامزد جایگزین** است؛ هنوز نباید آن را قطعی کنیم.</span>

**<span dir="rtl">معیار انتخاب</span> Vertical Slice**

<span dir="rtl">سناریوی نخست باید بتواند موارد زیر را به‌صورت واقعی آزمایش کند:</span>

<span dir="rtl">- مرزهای دامنه و</span> Aggregate<span dir="rtl">ها</span>

<span dir="rtl">- تراکنش‌ها و سازگاری داده</span>

<span dir="rtl">-</span> Workflow <span dir="rtl">و تأییدهای چندمرحله‌ای</span>

<span dir="rtl">-</span> Tenant <span dir="rtl">و</span> Company Authorization

<span dir="rtl">-</span> Audit <span dir="rtl">و</span> Optimistic Concurrency

<span dir="rtl">- اسناد و پیوست‌ها</span>

<span dir="rtl">- یکپارچه‌سازی بین ماژول‌ها</span>

<span dir="rtl">- یک قابلیت</span> AI <span dir="rtl">با ارزش مشخص</span>

<span dir="rtl">- نصب، ارتقا، پشتیبان‌گیری و بازیابی</span> On-Premises

<span dir="rtl">این معیارها باید مبنای انتخاب باشند، نه صرفاً رایج‌بودن یک فرایند در پلتفرم های سازمانی موجود.</span>

**<span dir="rtl">خروجی‌های مرحله شناخت دامنه</span>**

| <span dir="rtl">خروجی</span>                  | <span dir="rtl">معیار پذیرش پیشنهادی</span>                                                           |
|-----------------------------------------------|-------------------------------------------------------------------------------------------------------|
| Product Vision                                | <span dir="rtl">بازار هدف، ارزش پیشنهادی، تمایز و محدودیت‌های محصول روشن باشد</span>                   |
| Business Capability Map                       | <span dir="rtl">قابلیت‌ها مستقل از ساختار نرم‌افزار شناسایی و اولویت‌بندی شوند</span>                    |
| Domain Map                                    | Subdomain<span dir="rtl">ها و ارتباطات اصلی مشخص باشند</span>                                         |
| Bounded Context Catalog                       | <span dir="rtl">مسئولیت، زبان دامنه و مالکیت قواعد هر</span> Context <span dir="rtl">تعریف شود</span> |
| Context Map                                   | <span dir="rtl">نوع رابطه و قرارداد بین</span> Context<span dir="rtl">ها مشخص باشد</span>             |
| Domain Event Catalog                          | <span dir="rtl">رخدادهای معنادار کسب‌وکار و پیامدهای آن‌ها ثبت شوند</span>                              |
| Deployment Strategy                           | <span dir="rtl">مدل نصب مستقل و الزامات آمادگی</span> SaaS <span dir="rtl">مشخص باشند</span>          |
| Tenant Isolation Strategy                     | <span dir="rtl">جداسازی داده و کنترل دسترسی</span> Tenant/Company <span dir="rtl">مستند باشد</span>   |
| NFR & Security Matrix <span dir="rtl"></span> | <span dir="rtl">الزامات قابل‌اندازه‌گیری و کنترل‌های اثبات‌پذیر تعریف شوند</span>                         |
| ADR Register                                  | <span dir="rtl">تصمیم‌ها، گزینه‌های ردشده و دلایل انتخاب قابل ردیابی باشند</span>                       |

<span dir="rtl">**اصلاح مهم**: نباید مرحله شناخت دامنه را فقط با تولید این اسناد پایان‌یافته بدانیم.</span>

<span dir="rtl">لازم است مدل‌های تهیه‌شده با تحلیلگران کسب‌وکار و خبرگان دامنه اعتبارسنجی شوند. برای دامنه‌های پیچیده مانند پیمان، این اعتبارسنجی می‌تواند از طریق سناریوهای واقعی،</span> Event Storming <span dir="rtl">و بررسی استثناهای فرایندی انجام شود.</span>

**<span dir="rtl">دفتر تصمیم‌های تجمیعی — به‌روزرسانی مرحله دوم</span>**

<span dir="rtl">شناسه‌های مرحله اول را حفظ می‌کنیم. موارد زیر تغییر وضعیت یا توضیح تکمیلی پیدا کرده‌اند:</span>

| <span dir="rtl">شناسه</span> | <span dir="rtl">موضوع</span>                                                | <span dir="rtl">نتیجه مرحله دوم</span>                                                                                 |
|------------------------------|-----------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| IEP-003                      | DDD <span dir="rtl">و مرزبندی دامنه</span>                                  | <span dir="rtl">تأکید بر تفکیک</span> Subdomain<span dir="rtl">،</span> Bounded Context <span dir="rtl">و ماژول</span> |
| IEP-005                      | Event-Driven Integration                                                    | <span dir="rtl">تأیید استفاده انتخابی؛ عدم الزام ارتباط ناهمگام</span>                                                 |
| IEP-009                      | On-Premises First, SaaS-Ready                                               | <span dir="rtl">تقویت ضرورت استقلال نصب</span>                                                                         |
| IEP-011                      | Tenant <span dir="rtl">و</span> Company                                     | <span dir="rtl">تأیید تفکیک مدل مشتری و شرکت حقوقی</span>                                                              |
| IEP-012                      | Company-aware Authorization                                                 | <span dir="rtl">گسترش صریح به</span> Retrieval <span dir="rtl">و ابزارهای</span> AI                                    |
| IEP-013                      | <span dir="rtl">تفکیک</span> Business Records <span dir="rtl">و</span> Logs | <span dir="rtl">اصلاح</span> Context <span dir="rtl">مبهم</span> Audit & Compliance                                    |
| IEP-016                      | AI-Native                                                                   | <span dir="rtl">تقویت</span> Provider Abstraction <span dir="rtl">و کنترل مسیر اجرای</span> AI                         |
| IEP-023                      | Legal Hold                                                                  | <span dir="rtl">همچنان نیازمند تطبیق با اسناد بعدی</span>                                                              |
| IEP-024                      | Workflow                                                                    | <span dir="rtl">نیازمند تعیین مرز موتور عمومی و قواعد دامنه</span>                                                     |

**<span dir="rtl">تصمیم‌ها و موضوعات جدید</span>**

| <span dir="rtl">شناسه</span> | <span dir="rtl">موضوع</span>                                                                              | <span dir="rtl">وضعیت</span>                               |
|------------------------------|-----------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| IEP-026                      | Core Domain <span dir="rtl">بر اساس استراتژی محصول تعیین شود</span>                                       | <span dir="rtl">اصل پذیرفتنی برای معماری دامنه</span>      |
| IEP-027                      | <span dir="rtl">مدیریت جامع پیمان به‌عنوان نامزد</span> Core Domain                                        | <span dir="rtl">پیشنهادی بر اساس اولویت فعلی</span>        |
| IEP-028                      | <span dir="rtl">فهرست</span> Bounded Context<span dir="rtl">ها</span>                                     | <span dir="rtl">پیش‌نویس، نیازمند بازطراحی</span>           |
| IEP-029                      | <span dir="rtl">تعامل</span> Inventory <span dir="rtl">و</span> Finance                                   | <span dir="rtl">مالکیت دامنه روشن؛ الگوی تراکنش باز</span> |
| IEP-030                      | AI Provider Abstraction                                                                                   | <span dir="rtl">اصل معماری پیشنهادی</span>                 |
| IEP-031                      | <span dir="rtl">جداسازی</span> Tenant/Company <span dir="rtl">در تمام مسیرهای</span> AI                   | <span dir="rtl">الزام امنیتی پیشنهادی</span>               |
| IEP-032                      | Procure-to-Pay <span dir="rtl">به‌عنوان</span> Vertical Slice <span dir="rtl"></span>                      | <span dir="rtl">پیشنهاد اولیه؛ اولویت اجرایی باز</span>    |
| IEP-033                      | <span dir="rtl">انتخاب</span> Vertical Slice <span dir="rtl">بر اساس ارزش دامنه و پوشش ریسک معماری</span> | <span dir="rtl">معیار پیشنهادی</span>                      |
| IEP-034                      | Business Capability Map <span dir="rtl">پیش از تثبیت</span> Context Map                                   | <span dir="rtl">اولویت روش‌شناختی پیشنهادی</span>           |
| IEP-035                      | <span dir="rtl">اعتبارسنجی مدل دامنه با خبرگان کسب‌وکار</span>                                             | <span dir="rtl">معیار کیفیت پیشنهادی</span>                |

<span dir="rtl">واژه «پذیرفتنی» در این جدول به معنی تأیید فنی در بازبینی است؛ هر موردی که توافق صریح تیم درباره آن احراز نشده، هنوز مصوب نهایی نیست</span>.

**<span dir="rtl">موارد اصلاح‌شده، منسوخ یا نیازمند تصمیم</span>**

<span dir="rtl">**حفظ و تقویت می‌شود:** دسته‌بندی راهبردی دامنه‌ها، مرزبندی</span> DDD<span dir="rtl">، مالکیت قواعد کسب‌وکار، استقلال از ارائه‌دهنده</span> AI <span dir="rtl">و ضرورت</span> Business Capability Map<span dir="rtl">.</span>

<span dir="rtl">**نیازمند بازنویسی است:** فهرست</span> Bounded Context<span dir="rtl">ها، مفهوم</span> Tenant Management<span dir="rtl">، معماری</span> Audit & Compliance<span dir="rtl">، مثال تعامل</span> Inventory/Finance <span dir="rtl">و گزینه‌های استقرار</span> AI<span dir="rtl">.</span>

<span dir="rtl">**باز می‌ماند:** انتخاب اولین</span> Vertical Slice<span dir="rtl">، مرز دقیق</span> Context<span dir="rtl">های مدیریت پیمان، فناوری</span> Workflow <span dir="rtl">و الزامات اجرایی</span> AI <span dir="rtl">آفلاین.</span>

<span dir="rtl">فعلا، تصمیمی را که بتوانیم با اطمینان «رسماً منسوخ‌شده» بنامیم پیدا نکردیم. آنچه وجود دارد عمدتاً پیشنهادهای اولیه‌ای است که با اطلاعات جدید باید اصلاح شوند.</span>

**<span dir="rtl">متن بازنویسی‌شده برای سند معماری</span> IEP**

IEP — Domain Discovery & Strategic Design Foundation

**<span dir="rtl">شناخت راهبردی دامنه</span>**

<span dir="rtl">معماری</span> IEP <span dir="rtl">باید بر پایه شناخت قابلیت‌های کسب‌وکار، اهداف راهبردی محصول و فرایندهای واقعی سازمان‌های هدف شکل گیرد. دسته‌بندی</span> Core<span dir="rtl">،</span> Supporting <span dir="rtl">و</span> Generic <span dir="rtl">بر اساس نقش هر</span> Subdomain <span dir="rtl">در ارزش و تمایز محصول انجام می‌شود، نه صرفاً پیچیدگی فنی آن.</span>

**<span dir="rtl">مرزبندی دامنه</span>**

Bounded Context<span dir="rtl">ها از تحلیل مدل‌های کسب‌وکار، زبان مشترک، قواعد، چرخه عمر داده و وابستگی‌های فرایندی استخراج می‌شوند. ساختار ماژول‌های نرم‌افزار باید از این مرزبندی پشتیبانی کند، بدون آنکه الزاماً با آن رابطه یک‌به‌یک داشته باشد.</span>

**<span dir="rtl">مالکیت داده و تراکنش</span>**

<span dir="rtl">هر</span> Context <span dir="rtl">مالک قواعد و داده‌های تحت مسئولیت خود است. ارتباطات بین</span> Context<span dir="rtl">ها از طریق قراردادهای روشن انجام می‌شود. انتخاب تعامل همگام یا ناهمگام تابع الزامات سازگاری، زمان‌بندی، قابلیت بازیابی و قواعد واقعی کسب‌وکار است.</span>

**<span dir="rtl">ساختار سازمانی</span>**

Tenant <span dir="rtl">مرز منطقی مشتری سازمانی است و</span> Company <span dir="rtl">شخصیت حقوقی درون آن را نمایندگی می‌کند. کنترل دسترسی باید در سطح</span> Tenant <span dir="rtl">و</span> Company <span dir="rtl">در تمام مسیرهای عملیاتی، اسنادی، تحلیلی و هوشمند اعمال شود.</span>

**<span dir="rtl">هوش مصنوعی</span>**

<span dir="rtl">معماری</span> AI <span dir="rtl">باید از منطق دامنه مستقل و نسبت به ارائه‌دهنده مدل قابل انعطاف باشد. مدل‌های</span> Cloud<span dir="rtl">،</span> Private <span dir="rtl">و</span> Local <span dir="rtl">گزینه‌های استقرار هستند و انتخاب آن‌ها تابع نیاز امنیتی، زیرساختی و عملیاتی مشتری خواهد بود.</span>

**<span dir="rtl">اعتبارسنجی معماری</span>**

<span dir="rtl">پیش از توسعه گسترده، یک</span> Vertical Slice <span dir="rtl">واقعی انتخاب و پیاده‌سازی می‌شود تا مرزهای دامنه، تراکنش‌ها،</span> Workflow<span dir="rtl">، امنیت،</span> Audit<span dir="rtl">، هوش مصنوعی و استقرار مستقل در شرایط قابل آزمون ارزیابی شوند.</span>

**<span dir="rtl">معیار تکمیل شناخت دامنه</span>**

<span dir="rtl">مرحله شناخت دامنه زمانی آماده ورود به طراحی تفصیلی است که قابلیت‌های اصلی، مرزهای پیشنهادی</span> Context<span dir="rtl">ها، قراردادهای کلیدی، ریسک‌های معماری و تصمیم‌های باز شناسایی شده و با خبرگان دامنه اعتبارسنجی شده باشند.</span>

**<span dir="rtl">جمع‌بندی مرحله دوم</span>**

<span dir="rtl">مرحله دوم یک نتیجه راهبردی مهم برای ما دارد</span>**: <span dir="rtl">شناخت دامنه باید هدایت‌کننده معماری باشد، نه اینکه معماری از قبل انتخاب‌شده، ساختار دامنه را به کسب‌وکار تحمیل کند</span>.**

<span dir="rtl">در این مرحله همچنین روشن شد که فهرست</span> Context<span dir="rtl">های یک</span> ERP <span dir="rtl">عمومی، برای محصول تخصصی</span> IEP <span dir="rtl">کافی نیست و سناریوی</span> Procure-to-Pay <span dir="rtl">نیز نباید بدون مقایسه با سناریوهای مدیریت پیمان، به‌عنوان نخستین پیاده‌سازی قطعی انتخاب شود</span>.
