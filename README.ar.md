<a id="top"></a>

<p align="center">
<picture>
  <source media="(prefers-color-scheme: dark)" srcset="docs/assets/banner-dark.svg?v=2">
  <source media="(prefers-color-scheme: light)" srcset="docs/assets/banner-light.svg?v=2">
  <img src="docs/assets/banner-dark.svg?v=2" width="100%"
       alt="MaxManager — ضبط أداء يسأل قبل أن يفعل">
</picture>
</p>

<p align="center">
  <a href="https://github.com/nader295/Max-Manger/releases/latest"><img alt="التنزيل" src="https://img.shields.io/badge/download-latest_release-2ea44f?style=for-the-badge"></a>
  <img alt="أندرويد" src="https://img.shields.io/badge/Android-10%2B-3DDC84?style=for-the-badge&logo=android&logoColor=white">
  <img alt="جذر" src="https://img.shields.io/badge/root-required-607D8F?style=for-the-badge">
  <img alt="لغات" src="https://img.shields.io/badge/languages-84%2B-607D8F?style=for-the-badge">
  <img alt="رخصة" src="https://img.shields.io/badge/licence-proprietary-B36A42?style=for-the-badge">
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <b>العربية</b>
</p>

<p align="center">
  <a href="#التثبيت"><b>ثبّت الوحدة</b></a> ·
  <a href="#كيف-تبدو"><b>انظر الشاشات</b></a> ·
  <a href="docs/README.md"><b>اقرأ الوثائق</b></a>
</p>

<p align="center"><b>هذا المستودع هو الوجه العام لـMaxManager</b> — الوثائق واللقطات والتنزيلات.
والتطبيق وطبقته الأصلية <b>مصدر مغلق</b>: لا شيء هنا يُبنى، وسطور الأوامر المنقولة في هذه
الصفحات تُشغَّل داخل ذلك المستودع.</p>

| | |
| --- | --- |
| **المنصّة** | أندرويد 10 أو أحدث (API 29) · `arm64-v8a` و`armeabi-v7a` |
| **الجذر** | Magisk · KernelSU · KernelSU Next — أو Shizuku لجزء منه |
| **الشاشات** | ٥٣ شاشة في تسعة مجالات ضبط، ومعها رفّ أدوات |
| **اللغات** | ٨٤ لغة زائد الإنجليزيّة، والاتجاه من اليمين مفروض ببوابة |
| **الرخصة** | مملوكة — ولا تُستعمل إلا بإذن كتابيّ من صاحب الحقّ |

---

<a id="المحتويات"></a>

<details>
<summary><b>المحتويات</b> — أقسام الصفحة السبعة عشر بترتيب القراءة</summary>

| | القسم | السؤال الواحد الذي يجيب عنه |
| --- | --- | --- |
| ١ | [في عشر ثوانٍ](#في-عشر-ثوانٍ) | ما هذا، ولمن؟ |
| ٢ | [كيف يبدو](#كيف-تبدو) | الشاشات، ووثيقة التصميم وراءها |
| ٣ | [لماذا بُني هكذا](#لماذا-هكذا) | الطبقات الثلاث ومسار الكتابة الواحد |
| ٤ | [Max Atlas](#max-atlas) | لماذا يعمل أيّ شيء على هاتفك أنت |
| ٥ | [Max AI](#max-ai) | ما الذي يتغيّر، وكيف يُقاس |
| ٦ | [ما تتحكم فيه](#ما-تتحكم-فيه) | المجالات التسعة، والتحكّم لكلّ تطبيق، والملفّات |
| ٧ | [المراقبة والقياس والتشخيص](#المراقبة) | القراءات الحيّة، والطبقات، والسجلات، والتشخيص |
| ٨ | [اللغات](#اللغات) | ٨٤ لغة، والاتجاه من اليمين مفروض ببوابة |
| ٩ | [المتطلبات](#المتطلبات) | هل يعمل على هاتفي؟ |
| ١٠ | [التثبيت](#التثبيت) | كيف أُشغّله |
| ١١ | [لمطوّري الروم](#لمطوّري-الروم) | عدّة الدمج في AOSP |
| ١٢ | [ما لن يفعله](#ما-لن-يفعله) | القواعد التي لا تُطفأ |
| ١٣ | [الوثائق](#الوثائق) | كل صفحة تحت `docs/` |
| ١٤ | [الأسئلة الشائعة](#الأسئلة) | الأسئلة التي تتكرّر |
| ١٥ | [الدعم](#الدعم) | إلى أين يذهب البلاغ |
| ١٦ | [الرخصة](#الرخصة) | مملوكة، ومكتوبة صراحةً |
| ١٧ | [Credits](#credits) | مَن كتب ما لم يكتبه هذا المشروع |

</details>

---

<a id="في-عشر-ثوانٍ"></a>

## <img src="docs/assets/ic-timer.svg?v=2" width="22" height="22" align="absmiddle" alt="في عشر ثوانٍ"> في عشر ثوانٍ

**MaxManager لوحة تحكّم في الأداء والطاقة لأندرويد المتجذّر — لا تعرض لك إلا الضوابط الموجودة فعلًا
على جهازك.**

التجذير يمنحك مئات واجهات النواة وخريطة واحدة لا توجد. ومعظم تطبيقات الضبط تجيب على ذلك بجدار
مفاتيح: نصفها لا يفعل شيئًا على عتادك، ولا واحد منها يخبرك بما غيّره، وحين ينكسر شيء تكتشف ذلك لاحقًا.
MaxManager مبنيّ بالاتجاه المعاكس.

- **الضابط الذي لا تكشفه نواتك ليس على الشاشة.** لا معطَّلًا بل **غائبًا**.
- **كل تغيير يُثبَّت لا يُفترض.** تُقرأ القيمة بعد كتابتها، والتغيير الذي لم يستقرّ يُبلَّغ عنه كفشل
  مع محاولة رجوع.
- **حين لا يعلم يقول `status_unknown`.** لا صفراً معقولًا قط.
- **لا شيء يعمل خلف ظهرك.** المحرّكات مطفأة حتى تشغّلها، وكل كتابة تمرّ بمسار واحد مُدقَّق.

وأبوابٌ بابان حسب من أنت:

| **أريد استعماله** | **أبني رومات** |
| --- | --- |
| [كيف يبدو](#كيف-تبدو) · [ما تتحكم فيه](#ما-تتحكم-فيه) · [التثبيت](#التثبيت) | [لمطوّري الروم](#لمطوّري-الروم) — عدّة الدمج، عند الطلب |
| ٥٣ شاشة في تسعة مجالات ضبط، وأدوات مساعدة | ملفّات Soong وخدمة init ونطاق sepolicy وقائمة صلاحيات مُمتَزَجة |
| [المتطلبات](#المتطلبات): أندرويد 10+ وجذر (أو Shizuku لجزء منها) | الإذن أولًا: برمجيات مملوكة، والدمج بإذن كتابي |

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="كيف-تبدو"></a>
<a id="اللقطات"></a>

## <img src="docs/assets/ic-phone.svg?v=2" width="22" height="22" align="absmiddle" alt="الشاشات"> كيف يبدو

<!-- screenshots:start -->
<details open>
<summary><b>الرئيسية و Max AI</b> · ٦ إطارات</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/01-start.png"><img src="docs/screenshots/01-start.png" width="140" alt="MaxManager — البداية"></a><br><sub><b>البداية</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/02-now-home.png"><img src="docs/screenshots/02-now-home.png" width="140" alt="MaxManager — الرئيسية"></a><br><sub><b>الرئيسية</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/03-max-ai.png"><img src="docs/screenshots/03-max-ai.png" width="140" alt="MaxManager — Max AI"></a><br><sub><b>Max AI</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/04-max-ai-plan.png"><img src="docs/screenshots/04-max-ai-plan.png" width="140" alt="MaxManager — خطة Max AI"></a><br><sub><b>خطة Max AI</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/05-max-ai-live.png"><img src="docs/screenshots/05-max-ai-live.png" width="140" alt="MaxManager — التحكّم الحيّ"></a><br><sub><b>التحكّم الحيّ</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/06-max-ai-loops.png"><img src="docs/screenshots/06-max-ai-loops.png" width="140" alt="MaxManager — حصيلة الحلقات"></a><br><sub><b>حصيلة الحلقات</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details open>
<summary><b>التحكّم لكل تطبيق</b> · ٦ إطارات</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/26-apps-list.png"><img src="docs/screenshots/26-apps-list.png" width="140" alt="MaxManager — التطبيقات"></a><br><sub><b>التطبيقات</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/27-app-settings.png"><img src="docs/screenshots/27-app-settings.png" width="140" alt="MaxManager — لكل تطبيق"></a><br><sub><b>لكل تطبيق</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/28-app-settings-display.png"><img src="docs/screenshots/28-app-settings-display.png" width="140" alt="MaxManager — لكل تطبيق · العرض"></a><br><sub><b>لكل تطبيق · العرض</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/29-app-settings-gaming.png"><img src="docs/screenshots/29-app-settings-gaming.png" width="140" alt="MaxManager — لكل تطبيق · الألعاب"></a><br><sub><b>لكل تطبيق · الألعاب</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/30-app-settings-power.png"><img src="docs/screenshots/30-app-settings-power.png" width="140" alt="MaxManager — لكل تطبيق · الطاقة"></a><br><sub><b>لكل تطبيق · الطاقة</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/31-app-settings-tune.png"><img src="docs/screenshots/31-app-settings-tune.png" width="140" alt="MaxManager — لكل تطبيق · ضبط"></a><br><sub><b>لكل تطبيق · ضبط</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>مجالات التحكّم</b> · ٨ إطارات</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/07-control-hub.png"><img src="docs/screenshots/07-control-hub.png" width="140" alt="MaxManager — التحكّم"></a><br><sub><b>التحكّم</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/08-control-lanes.png"><img src="docs/screenshots/08-control-lanes.png" width="140" alt="MaxManager — مسارات التحكّم"></a><br><sub><b>مسارات التحكّم</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/09-control-tools.png"><img src="docs/screenshots/09-control-tools.png" width="140" alt="MaxManager — أدوات التحكّم"></a><br><sub><b>أدوات التحكّم</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/10-control-tools-2.png"><img src="docs/screenshots/10-control-tools-2.png" width="140" alt="MaxManager — أدوات أخرى"></a><br><sub><b>أدوات أخرى</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/11-control-hub-2.png"><img src="docs/screenshots/11-control-hub-2.png" width="140" alt="MaxManager — التحكّم (٢)"></a><br><sub><b>التحكّم (٢)</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/12-hub-display.png"><img src="docs/screenshots/12-hub-display.png" width="140" alt="MaxManager — العرض"></a><br><sub><b>العرض</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/13-hub-responsiveness.png"><img src="docs/screenshots/13-hub-responsiveness.png" width="140" alt="MaxManager — الاستجابة"></a><br><sub><b>الاستجابة</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/14-hub-power.png"><img src="docs/screenshots/14-hub-power.png" width="140" alt="MaxManager — الطاقة"></a><br><sub><b>الطاقة</b></sub></td>
  </tr>
</table>

</details>

<details>
<summary><b>المعالج والرسوميات</b> · ٥ إطارات</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/15-cpu-cores.png"><img src="docs/screenshots/15-cpu-cores.png" width="140" alt="MaxManager — أنوية المعالج"></a><br><sub><b>أنوية المعالج</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/16-core-limits.png"><img src="docs/screenshots/16-core-limits.png" width="140" alt="MaxManager — حدود الأنوية"></a><br><sub><b>حدود الأنوية</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/17-cpu-preference-tweaks.png"><img src="docs/screenshots/17-cpu-preference-tweaks.png" width="140" alt="MaxManager — التحسينات"></a><br><sub><b>التحسينات</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/18-gpu-studio-profiles.png"><img src="docs/screenshots/18-gpu-studio-profiles.png" width="140" alt="MaxManager — أنماط الرسوميات"></a><br><sub><b>أنماط الرسوميات</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/19-gpu-studio-live.png"><img src="docs/screenshots/19-gpu-studio-live.png" width="140" alt="MaxManager — الرسوميات الحيّ"></a><br><sub><b>الرسوميات الحيّ</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>الذاكرة والعرض</b> · إطاران</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/20-memory-zram.png"><img src="docs/screenshots/20-memory-zram.png" width="140" alt="MaxManager — مدير ZRAM"></a><br><sub><b>مدير ZRAM</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/21-display-resolution.png"><img src="docs/screenshots/21-display-resolution.png" width="140" alt="MaxManager — الدقّة"></a><br><sub><b>الدقّة</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>البطارية والشحن</b> · ٤ إطارات</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/22-power-charging.png"><img src="docs/screenshots/22-power-charging.png" width="140" alt="MaxManager — الشحن"></a><br><sub><b>الشحن</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/23-bypass-check.png"><img src="docs/screenshots/23-bypass-check.png" width="140" alt="MaxManager — فحص التجاوز"></a><br><sub><b>فحص التجاوز</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/24-doze.png"><img src="docs/screenshots/24-doze.png" width="140" alt="MaxManager — وضع Doze"></a><br><sub><b>وضع Doze</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/25-sleep-policy.png"><img src="docs/screenshots/25-sleep-policy.png" width="140" alt="MaxManager — سياسة الخمول"></a><br><sub><b>سياسة الخمول</b></sub></td>
  </tr>
</table>

</details>

<details>
<summary><b>الإعدادات والأدوات</b> · ١١ إطارًا</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/32-settings-root.png"><img src="docs/screenshots/32-settings-root.png" width="140" alt="MaxManager — الإعدادات"></a><br><sub><b>الإعدادات</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/33-color-palette.png"><img src="docs/screenshots/33-color-palette.png" width="140" alt="MaxManager — لوحة الألوان"></a><br><sub><b>لوحة الألوان</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/34-logs.png"><img src="docs/screenshots/34-logs.png" width="140" alt="MaxManager — السجلات"></a><br><sub><b>السجلات</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/35-max-backup.png"><img src="docs/screenshots/35-max-backup.png" width="140" alt="MaxManager — النسخ الاحتياطي"></a><br><sub><b>النسخ الاحتياطي</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/36-backup-plan.png"><img src="docs/screenshots/36-backup-plan.png" width="140" alt="MaxManager — خطة النسخ"></a><br><sub><b>خطة النسخ</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/37-backup-apps.png"><img src="docs/screenshots/37-backup-apps.png" width="140" alt="MaxManager — تطبيقات النسخ"></a><br><sub><b>تطبيقات النسخ</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/38-permissions.png"><img src="docs/screenshots/38-permissions.png" width="140" alt="MaxManager — الأذونات"></a><br><sub><b>الأذونات</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/39-permissions-app.png"><img src="docs/screenshots/39-permissions-app.png" width="140" alt="MaxManager — أذونات تطبيق"></a><br><sub><b>أذونات تطبيق</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/40-permissions-2.png"><img src="docs/screenshots/40-permissions-2.png" width="140" alt="MaxManager — الأذونات (٢)"></a><br><sub><b>الأذونات (٢)</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/41-activity-launcher.png"><img src="docs/screenshots/41-activity-launcher.png" width="140" alt="MaxManager — الأنشطة"></a><br><sub><b>الأنشطة</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/42-set-edit.png"><img src="docs/screenshots/42-set-edit.png" width="140" alt="MaxManager — محرّر الخصائص"></a><br><sub><b>محرّر الخصائص</b></sub></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

<details>
<summary><b>الشبكة والتخزين و HUD</b> · ٦ إطارات</summary>

<table>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/43-network-detail.png"><img src="docs/screenshots/43-network-detail.png" width="140" alt="MaxManager — الشبكة"></a><br><sub><b>الشبكة</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/44-network-scheduler.png"><img src="docs/screenshots/44-network-scheduler.png" width="140" alt="MaxManager — مجدول الشبكة"></a><br><sub><b>مجدول الشبكة</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/45-storage-detail.png"><img src="docs/screenshots/45-storage-detail.png" width="140" alt="MaxManager — التخزين"></a><br><sub><b>التخزين</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/46-fps-overlay.png"><img src="docs/screenshots/46-fps-overlay.png" width="140" alt="MaxManager — طبقة FPS"></a><br><sub><b>طبقة FPS</b></sub></td>
  </tr>
  <tr>
    <td align="center" width="25%"><a href="docs/screenshots/47-fps-overlay-metrics.png"><img src="docs/screenshots/47-fps-overlay-metrics.png" width="140" alt="MaxManager — مقاييس HUD"></a><br><sub><b>مقاييس HUD</b></sub></td>
    <td align="center" width="25%"><a href="docs/screenshots/48-fps-overlay-source.png"><img src="docs/screenshots/48-fps-overlay-source.png" width="140" alt="MaxManager — مصدر HUD"></a><br><sub><b>مصدر HUD</b></sub></td>
    <td align="center" width="25%"></td>
    <td align="center" width="25%"></td>
  </tr>
</table>

</details>

> **الملتقط ٤٨ من ٤٨ إطارًا** · والخيارات الإضافيّة ٠. والإطار غير الملتقط يغيب من الشبكة أعلاه ولا يظهر مكسورًا؛ و<a href="docs/screenshots/">مجلّد اللقطات</a> يحملها كلّها.
<!-- screenshots:end -->

وكل إطار هنا **لقطة حقيقية من جهاز**، مأخوذة بحسب العقد في
**[`docs/screenshots/`](docs/screenshots/)**: صور PNG بدقة 1162×2480، ودون 400 كيلوبايت
للإطار، وخيار شريط حالة واحد عبر كل الإطارات، وسمة داكنة في اللقطات كلها، مع نسخ `-light` و`-ar`. والشبكة
**مولَّدة من الإطارات الموجودة** — `tools/screenshot_gallery.py` لا تكتب `<img>` إلا لملفّ PNG موجود
فعلًا، فالإطار الذي لم يُلتقط **غائب لا مكسور**، والإطار المُسقَط باسمه الصحيح يظهر في أول تشغيل
للمولّد.

والرسوم في هذه الصفحة — مسار الكتابة، ودورة Max Atlas، وحلقة Max AI، والمجالات التسعة — مرسومة من
سلوك التطبيق ونصوصه ورمزه لا من لقطات، وكل ادّعاء عن شاشة هنا مكتوب من كلمات الواجهة نفسها.

والواجهة مرسومة بقواعد لا بذوق، وهذه القواعد مكتوبة قيمةً قيمة في **[DESIGN.md](DESIGN.md)** —
مع بوابة (`tools/design_doc.py`) تُسقط البناء حين تختلف الوثيقة والشيفرة.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="لماذا-هكذا"></a>

## <img src="docs/assets/ic-layers.svg?v=2" width="22" height="22" align="absmiddle" alt="ثلاث طبقات"> لماذا بُني هكذا

<p align="center"><img src="docs/assets/control-plane.svg?v=2" width="100%" alt="مسار كتابة واحد: الشاشة، والحكم، وسجلّ الملكية، والتحقّق والرجوع، ثم واجهة النواة — والضابط الذي مساره غير مُثبَت هنا يُوسم كذلك"></p>

ثلاث طبقات، لا تتداخل:

1. **[Max Atlas](#max-atlas)** يقرّر **كيف** يمكن لشيء أن يعمل على هذا الجهاز: أي الواجهات موجودة،
   وأي المسارات تصلها، وما الذي نجح فعلًا في المرة السابقة.
2. **مسار التحكّم** هو الطريق الوحيد الذي يكتب: حكم واحد، وسجلّ ملكية فلا يتزاحم كاتبان على
   مقبض واحد، وتحقّق بقراءة القيمة، ورجوع حين لا يستقرّ الكتابة.
3. **[Max AI](#max-ai)** يقرّر **ما** يجب أن يتغيّر و**متى**: أصغر تغيير يمكن أن يسدّ الفجوة، يُقاس
   أثره بعده. مطفأ حتى تشغّله.

وقاعدة واحدة تغطي الثلاثة: **التغيير يُكتب بمسار واحد، يُثبَّت بقراءته، ويُفحص لاحقًا ضدّ الانزلاق
الصامت.** فإن لم يستقرّ أُخبرت — مع محاولة رجوع — بدل أن تُعرض عليك علامة صحّ.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="max-atlas"></a>

## <img src="docs/assets/ic-atlas.svg?v=2" width="22" height="22" align="absmiddle" alt="Max Atlas"> Max Atlas — سبب أن أي شيء يعمل على هاتفك أنت

<p align="center"><img src="docs/assets/atlas-cycle.svg?v=2" width="100%" alt="Max Atlas: اكتشف، افهم، ارسم الخريطة، تكيّف، نفّذ، تحقّق، تعلّم — ما يعمل هنا يُثبَت هنا"></p>

هاتفان من الطراز نفسه قد يكشفان واجهات نواة مختلفة؛ ونواتان قد تسمّيان الواجهة نفسها بوحدات
مختلفة، وتسمحان بكتابتها أو لا. Max Atlas يسألك كل واجهة: هل هي **هنا**؟ وما اسمها؟ وبأي وحدة
تتحدّث؟ وهل يمكن كتابتها؟ — ثم يتذكّر الجواب.

وما تشعر به من ذلك:

1. **الضوابط التي لا يمكن أن تعمل لا تُعرض.** لا مفاتيح ميتة.
2. **كل ضابط موصوف بما هو عليه:** يعمل ومُثبَت هنا · مسار موجود لكنه غير مُثبَت هنا · للقراءة فقط ·
   موجود لكن هذه النسخة لا تستطيع التحكّم به · أثبتَت غيابه · لا تلمسه أبدًا (قاعدة سلامة) · أو
   **مجهول**.
3. **الغياب يُثبَت لا يُفترض.** قراءة فشلت ليست غيابًا؛ والقائمة وحدها التي تفتقر فعلًا إلى الاسم تُحسب «ليس هنا».
4. **يتحسّن على جهازك.** ما نجح وما فشل، وكم يبقى كلٌّ منهما صحيحًا، محفوظ — فالتشغيلة الثانية ليست
   التجربة نفسها.

<details>
<summary><b>كيف يُثبَت هذا</b> دون أن يصير هاتفك منصّة الاختبار</summary>

الاكتشاف يجري ضمن ميزانية صريحة (عمليات، مدخلات، بايتات، وقت)، وحين يوقف حدٌّ مسحًا يقول التقرير
«حدٌّ أوقفه» — لا «الجهاز لم يكن لديه ما يقوله». ويمكن تسجيل تشغيلة حقيقية على جهاز بوصفها
**fixture**، وتُعاد تلك الـfixture عبر واجهة القراءة نفسها، فـ«يحتاج جهازًا» لا يبقى عذرًا دائمًا
لمنطق لم يُختبر. والمعرفة تأتي من كتالوج مُراجَع نتحمّل مسؤوليته؛ والمفردات المجتمعية قد *تقترح*
مسارًا لكنها لا تمنحه أبدًا.

</details>

الصفحة الكاملة: **[docs/max-atlas.md](docs/max-atlas.md)**.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="max-ai"></a>

## <img src="docs/assets/ic-ai.svg?v=2" width="22" height="22" align="absmiddle" alt="Max AI"> Max AI — تغيير واحد مقيس في كل مرّة

<p align="center"><img src="docs/assets/max-ai.svg?v=2" width="100%" alt="Max AI: راقب، قرّر، اسأل، تحقّق، تذكّر — تغيير واحد مقيس في كل مرّة، وقائمة بما لن يفعله أبدًا"></p>

Max AI يراقب سلوك الجهاز فعليًّا — السرعة والحرارة والبطاقة والضغط على الذاكرة والتطبيق الظاهر —
وحين تقول القراءات إن شيئًا يجب أن يتغيّر، يغيّر **شيئًا واحدًا**، ثم يقيس هل كان ذلك مفيدًا. إنه
حلقة لا إعداد جاهز:

- <img src="docs/assets/ic-notice.svg?v=2" width="20" height="20" align="absmiddle" alt="راقب"> **راقب** — يقرأ هذا الجهاز: الحرارة والحمل والبطاقة والذاكرة والتطبيق النشط. *لا تلاحظ شيئًا:
  يراقب لا يتصرّف.*
- <img src="docs/assets/ic-decide.svg?v=2" width="20" height="20" align="absmiddle" alt="قرّر"> **قرّر** — مقابل هدفك (سرعة أو توازن أو بطاقة)، يختار *أصغر* تغيير يمكن أن يسدّ الفجوة. *مضبوط واحد
  يتحرك لا ثمانية.*
- <img src="docs/assets/ic-ask.svg?v=2" width="20" height="20" align="absmiddle" alt="اسأل"> **اسأل** — طبقة سلامة بأولوية مطلقة تقول نعم أو لا قبل أي كتابة. *لا تُلمس واجهة محميّة أبدًا،
  المحرّك مُشغَّلًا كان أو مطفأً.*
- <img src="docs/assets/ic-verify.svg?v=2" width="20" height="20" align="absmiddle" alt="تحقّق"> **تحقّق** — تُقرأ القيمة، ثم يُقاس الأثر بعد نافذة استجابة. *التغيير الذي لم يستقرّ لا يُحسب فوزًا.*
- <img src="docs/assets/ic-remember.svg?v=2" width="20" height="20" align="absmiddle" alt="تذكّر"> **تذكّر** — تُسجَّل النتيجة كحلقة كاملة مقيسة. *يثق بما أصاب، ويزيل ثقته بما أخطأ.*

**لماذا ليس إعدادًا جاهزًا:** الإعداد الجاهز يطبّق الأرقام نفسها على كل جهاز ولا يكتشف أبداً إن كانت
قد نفعت. أمّا Max AI فلا يتحدّث إلا بمفردات Max Atlas على هاتفك أنت، وانتصاراته مقيسة لا مُتوقَّعة،
ويعرف متى يتوقّف — فحين تفتح لعبة لها ملفّها الخاصّ يتنحّى ويظلّ يراقب السلامة وحدها.

**وما لن يفعله أبدًا:** كتابة واجهة محميّة · ادّعاء تغيير لم يقسه · اختراع قراءة · إخفاء فشل. وكل حلقة
تبقى سجلًّا تفتحه: ما رآه، وما أراده، وما غيّره، وما فعله الجهاز بعده، وما تعلّمه.

**وهو مطفأ حتى تشغّله.** التحكّم اليدويّ هو الحالة الافتراضية، والملفّ الشخصيّ الذي تختاره يبقى خطًّا
أساسيًّا يدويًّا — لا أمرًا إلى المحرّك.

<details>
<summary><b>للمشكّكين:</b> كيف يبقى القرار صادقًا</summary>

لا يُحسب القرار إلا حين نُفِّذ عبر مسار الكتابة الوحيد **و**تحقّق. المحرّك يحتفظ بسجلّ ملكية فلا
يتزاحم كاتبان على مقبض واحد، وبنموذج ثقة فلا يُصدَّق مصدر أخطأ بالقدر نفسه، وبدفتر حلقات كاملة لا
ملخّص نوايا. وإذا ألغى المستخدم تغييرًا بيده، ذلك يُسجَّل رفضًا مقيسًا — لا ضجيجًا.

</details>

الصفحة الكاملة: **[docs/max-ai.md](docs/max-ai.md)**.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="ما-تتحكم-فيه"></a>

## <img src="docs/assets/ic-sliders.svg?v=2" width="22" height="22" align="absmiddle" alt="الضوابط"> ما تتحكم فيه

<p align="center"><img src="docs/assets/domains.svg?v=2" width="100%" alt="تسعة مجالات ضبط: المعالج، وبطاقة الرسوم، والذاكرة، والعرض، والاستجابة، والحرارة، والطاقة، والتخزين والمترجم، والشبكة"></p>

تسعة مجالات، لكل منها واجهته الخاصة. والسطر تحت كل اسم هو **وصف التطبيق نفسه** للمجال كما في
الواجهة حرفيًّا.

- <img src="docs/assets/ic-cpu.svg?v=2" width="20" height="20" align="absmiddle" alt="المعالج"> **المعالج (CPU)** — *الأنوية والحكّام وتسريع المزوّد وتفضيلات النواة.* تشغيل الأنوية أو إيقافها،
  وتثبيت مجموعات الجدولة على العناقيد، وحدّ أدنى وأقصى لكل عنقود، واختيار الحكّام، وتعديل تفضيلات
  النواة.
- <img src="docs/assets/ic-gpu.svg?v=2" width="20" height="20" align="absmiddle" alt="بطاقة الرسوم"> **بطاقة الرسوم (GPU)** — *ترددات بطاقة الرسوم ومعاملات المزوّد الخاصة بالرسوم.* ترددات جاهزة وحدود
  يدوية، وحكّام بطاقة الرسوم، وسياسة طاقة أنوية الشيدر، ومسار تسريع المزوّد، وتجاوز مُوثَّق لاختناق
  الحرارة.
- <img src="docs/assets/ic-memory.svg?v=2" width="20" height="20" align="absmiddle" alt="الذاكرة"> **الذاكرة** — *الضغط وسلوك الذاكرة الافتراضية وswappiness.* تحديد حجم ZRAM أو إيقافه، واختيار محرّك
  الضغط، وضبط swappiness والاسترداد. والمحرّك يقرأ **ضغط توقّف الذاكرة** لا نسبة الامتلاء — فالجهاز
  الممتلئ الخامل يحتاج عكس ما يحتاجه المتوقّف.
- <img src="docs/assets/ic-display.svg?v=2" width="20" height="20" align="absmiddle" alt="العرض"> **العرض** — *معدّل التحديث واللون ومقياس اللوحة.* معدّل التحديث، وقنوات اللون، والتشبّع، ونطاق الألوان
  واستجابة HDR، ومنحنيات السطوع، والضوء الليلي، ومقاييس الحركة، ومهلة الشاشة.
- <img src="docs/assets/ic-touch.svg?v=2" width="20" height="20" align="absmiddle" alt="الاستجابة"> **الاستجابة** — *اللمس وإيقاع الإطارات وزمن الجدولة.* أخذ عيّنات اللمس وتنعيمه، والضغط المزدوج
  للاستيقاظ، ومعاملات FPS GO / GED، والجدولة الواعية بالإطارات.
- <img src="docs/assets/ic-thermal.svg?v=2" width="20" height="20" align="absmiddle" alt="الحرارة"> **الحرارة** — *الحرارات والاختناق والمعاملات الحرارية.* حرارات المناطق الحيّة، وسياسة الحرارة، وما
  يُخنق الجهاز الآن.
- <img src="docs/assets/ic-battery.svg?v=2" width="20" height="20" align="absmiddle" alt="الطاقة"> **الطاقة** — *الشحن والتخطي والنوم وصحة البطاقة.* حدود تيار الشحن، وسقف شحن يبطئ تآكل البطاقة،
  والشحن بالتخطيّ، والغوص القاسي، وقائمة الانتظار، وصحة البطاقة.
- <img src="docs/assets/ic-storage.svg?v=2" width="20" height="20" align="absmiddle" alt="التخزين والمترجم"> **التخزين والمترجم** — *وضع التجميع وصحة التخزين.* إعادة تجميع ART بفلتر مختار، وإعادة ضبط الحالة
  المجمَّعة، وصحة التخزين.
- <img src="docs/assets/ic-network.svg?v=2" width="20" height="20" align="absmiddle" alt="الشبكة"> **الشبكة** — *جدولة الحركة وحالة الربط.* خوارزمية احتقان TCP، والفتح السريع/SACK/ECN، وملفات SYN،
  وإعادة استخدام المقابس، ومعاملات مجدول الإدخال/الإخراج، وحالة الربط.

وأي شيء لا تكشفه جهازك في هذه المجالات **لا يُذكر أصلًا**.

### تطبيقًا واحدًا

افتح **التطبيقات**، واختر تطبيقًا، وامنحه معاملته الخاصة دون لمس ما عداه: ملفّ الأداء (طاقة · متوازن ·
ألعاب · أداء · مخصّص) · معدّل التحديث · دقة العرض · سقف حراري · حكّام المعالج وبطاقة الرسوم (فقط ما
تبلّغه نواتك، وفقط الحكّام الذين تدعمهم **كل** سياسات المعالج) · قفل أولوية الواجهة · تعزيز أولوية
الإدخال/الإخراج · إعادة ضبط خاصة بالتطبيق.

وكل تطبيق يعرض **حالته الفعليّة** بعبارات واضحة: التحكّم الخاص مطفأ · يستعمل الملفّ العام · تجاوز
التطبيق نشط — وحين تتقدّم لعبة لها ملفّها الخاصّ **يتحوّل Max AI إلى المراقبة فقط**.

### الملفّات الشخصية

الملفّ الشخصي هو مجموعة سلوك مسمّاة تطبّقها وتضبطها وتحفظها وتتشاركها: **طاقة** (بارد وموفّر)،
**متوازن** (الخطّ الأساسي اليومي)، **ألعاب** (بطاقة الرسوم في نطاقها الأعلى لإيقاع إطارات أثبت)،
**أداء** (القدرة كاملة ما سمح العتاد)، **مخصّص** (لك).

وأمران يجعلان الملفّات أزيد من علامات مرجعية:

- **تُشارَك، والمصدر يسافر مع الرقم.** عند التصدير تحمل كل قيمة مصدرها: قيمة مُضمَّنة، أو قيمة
  غيّرتها، أو قياس *ادّعاه* من صدّره. وعند الاستيراد يقول التطبيق بالضبط ما قبله وما رفضه، والملفّ
  القادم من شريحة أخرى يقول ذلك: القياس هناك ليس قياسًا هنا.
- **متاحة من إعدادات السريعة.** بلاطة تبدّل الملفّ دون فتح التطبيق، وبلاطة ثانية تقود الشحن بالتخطيّ.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="المراقبة"></a>

## <img src="docs/assets/ic-pulse.svg?v=2" width="22" height="22" align="absmiddle" alt="قراءات حيّة"> المراقبة والقياس والتشخيص

- <img src="docs/assets/ic-pulse.svg?v=2" width="20" height="20" align="absmiddle" alt="Max Live"> **Max Live** — الصورة الحيّة: القراءات الحالية، وما يُسمح للأتمتة بفعله الآن ولماذا، وما ستفعله بعد
  ذلك، وهل يمكن التراجع عنه.
- <img src="docs/assets/ic-phone.svg?v=2" width="20" height="20" align="absmiddle" alt="الرئيسية"> **الرئيسية** — حالة الجهاز، والتطبيق النشط، والملفّ الجاري، والحرارات والتخزين في نظرة.
- <img src="docs/assets/ic-display.svg?v=2" width="20" height="20" align="absmiddle" alt="طبقة FPS"> **طبقة FPS** — عدّاد قابل للسحب فوق أي لعبة (FPS والمعالج والذاكرة)، بطريقة قراءة احتياطية، ووسم
  **Vulkan/OpenGL** حين تُصيِّر اللعبة كذلك.
- <img src="docs/assets/ic-cpu.svg?v=2" width="20" height="20" align="absmiddle" alt="مراقب العمليات"> **مراقب العمليات** — المعالج والذاكرة لكل عملية، وإيقاف قسري، وSIGKILL، وطبقة عائمة.
- <img src="docs/assets/ic-doc.svg?v=2" width="20" height="20" align="absmiddle" alt="عارض السجلّات"> **عارض السجلّات** — logcat حيّ بتصفية وبحث، وتقرير قابل للمشاركة **معجمه مكتوب في ملفّ السجلّ نفسه**.
- <img src="docs/assets/ic-verify.svg?v=2" width="20" height="20" align="absmiddle" alt="التشخيص"> **التشخيص** — مركز تشخيص حيّ، وصحّة مسار كل ضابط، وطبقة أزرق قابلة لإعادة الإنتاج، وتقرير دعم تختار
  أنت إرساله.
- <img src="docs/assets/ic-question.svg?v=2" width="20" height="20" align="absmiddle" alt="لماذا لم تعمل"> **«لماذا لم تعمل؟»** — لإعداد خاصّ بتطبيق: ما أراده، وما تحتفظ به العتادة، وأين تنظر بعد ذلك.

ولا شيء هنا يتصل بخادم. وتقرير الدعم يُبنى محليًّا ويُصغَّر، ولا يغادر الجهاز إلا حين ترسله أنت.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="اللغات"></a>

## <img src="docs/assets/ic-globe.svg?v=2" width="22" height="22" align="absmiddle" alt="اللغات"> اللغات

<p align="center"><img src="docs/assets/locales.svg?v=2" width="100%" alt="٨٤ لغة، والاتجاه من اليمين إلى اليسار مواطن أوّل"></p>

- **٨٤ لغة** زائد الإنجليزية؛ والمنتقي يتبع لغة النظام دون إعادة تشغيل.
- **فاتح وداكن**، بلون مفتاح قابل للسمات وشاشة لوحة ألوان مخصّصة.
- **الاتجاه RTL مفروض ببوابة** لا بأمل — العربية والفارسية والعبرية والأردية مُضمَّنة.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="المتطلبات"></a>

## <img src="docs/assets/ic-checklist.svg?v=2" width="22" height="22" align="absmiddle" alt="المتطلبات"> المتطلبات

| | |
| --- | --- |
| **أندرويد** | 10 أو أحدث (API 29)، مبنيًّا على API 37 |
| **الجذر** | Magisk أو KernelSU أو KernelSU Next — والوحدة هي المسار المدعوم. وShizuku يمنح وصول مستوى ADB بلا جذر، وبعض الأدوات تعمل به |
| **المعمارية** | `arm64-v8a` و`armeabi-v7a` |
| **الشرائح** | سلوكيات مخصّصة لـ Snapdragon وMediaTek وExynos وTensor وUnisoc. وما عداها يعمل بما تكشفه نواتك |
| **خارج النطاق** | لا وعود أداء، ولا فروق benchmarks: رقمٌ قيس على جهاز ليس ادّعاءً عن جهازك |

والجواب الحقيقي عن *«هل يعمل على هاتفي؟»* هو خريطة القدرات داخل التطبيق على جهازك أنت. والتفاصيل في
**[docs/compatibility.md](docs/compatibility.md)**.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="التثبيت"></a>

## <img src="docs/assets/ic-download.svg?v=2" width="22" height="22" align="absmiddle" alt="التثبيت"> التثبيت

MaxManager يأتي **وحدة بلا نظام** (systemless) — لا شيء في `/system` يُعدَّل دائمًا، والإلغاء يُعيد
كل شيء.

1. نزّل `MaxManager-v1.0-module.zip` من **[الإصدارات](https://github.com/nader295/Max-Manger/releases/latest)** وافلشه في **Magisk** أو **KernelSU** (أو مدير جذر متوافق).
2. أعد التشغيل.
3. افتح **MaxManager** وامشِ في **الإعداد** الذي يشرح ما يكشفه *جهازك*.

والإصدار نفسه يحمل **`MaxManager-checksums.txt`** — بصمة للحزمة وبصمة لكل ما فيها — فتُتحقّق من
التنزيل قبل تفليشه؛ والأمران في **[docs/releases/v1.0.md](docs/releases/v1.0.md)**. وإذا فشلت
الوحدة في بلوغ إقلاع
مستقرّ مرّتين متتاليتين تُعطّل نفسها وتقول ذلك في وصفها.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="لمطوّري-الروم"></a>

## <img src="docs/assets/ic-cube.svg?v=2" width="22" height="22" align="absmiddle" alt="مطوّرو الروم"> لمطوّري الروم

<p align="center"><img src="docs/assets/integration.svg?v=2" width="100%" alt="ثلاثة مسارات للدمج — الوحدة بلا نظام، ودمج AOSP من android/aosp، وKernelSU Next — والأسماء الثلاثة التي يجب أن تتفق: مسار الثنائي وخدمة init ووسوم SELinux"></p>

عدّة الدمج **غير منشورة هنا** — المصدر مغلق. وتُسلَّم لمطوّري الروم **بطلب كتابي**: ملفّات Soong،
وخدمة init، ونطاق sepolicy، وقائمة صلاحيات مُمتَزَجة، والوحدة نفسها مُحزَّمة لـKernelSU Next.

**ما تحصل عليه:** تطبيق تحكّم مُمتَزَج، وخمسة ثنائيات أصلية (خدمة الجهاز، وملفات الشرائح، وحارس
الحرارة، ومهيّئ أدوات، ومحمّل ألعاب)، ووحدة تُثبَّت وتُزال دون تعديل دائم في `/system`.

**وما تحتاجه:** نسخة موقّعة منصّة ومُمتَزَجة للتطبيق؛ والثنائي على `/system/bin/sys.maxmanager-service`؛
وخدمة init؛ وقواعد sepolicy. وثلاثة أسماء يجب أن تتفق حرفيًّا — مسار الثنائي وخدمة init ووسم SELinux —
والرسم أعلاه يعرضها.

> **الإذن أولًا.** MaxManager **برمجيات مملوكة**. والعدّة هنا ليقيّمها المنظّمون ويدمجوها **بإذن
> كتابي** من صاحب الحقوق — [`LICENSE`](LICENSE) لا تمنح حقًّا بخلاف ذلك. اسأل أولًا عبر
> [الدعم](#الدعم).

ابدأ من هنا: **[docs/rom-integration.md](docs/rom-integration.md)** — ثلاثة مسارات للدمج، وقائمة التحقّق،
وتعارضان وجداهما في العدّة وأُبلِّغ عنهما بدل تلميعهما.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="ما-لن-يفعله"></a>

## <img src="docs/assets/ic-shield.svg?v=2" width="22" height="22" align="absmiddle" alt="لا تُلمس"> ما لن يفعله

أجزاء التطبيق التي لا تستطيع إطفاءها، ولن تودّ ذلك:

- **لا كتابات على النواة من الشاشة.** كل تعديل يمرّ بحكم واحد بسجلّ ملكية ودفتر — فيصير «من غيّر هذا،
  ومتى، وماذا حدث بعد» قابلاً للجواب.
- **لا قراءات مُصنَّعة.** القيمة المجهولة تُعرض `status_unknown`، لا `0` معقولًا.
- **لا نجاح لم يُتحقَّق منه.** قراءة بعد كل كتابة؛ والانزلاق يُفحص لاحقًا.
- **نقاط الانعطاف الحراري لا تُكتب أبدًا** على أي جهاز. قاعدة لا قيد.
- **قائمة «لا تلمس» مُراجَعة** تحرس الواجهات التي يجب ألّا تُكتب، بمطابقة مقاطع عن قصد فلا تتسلل
  متغيّرات المزوّدين.
- **لا قياس عن بُعد، ولا حسابات، ولا رفع صامت.**

وحين يكون للصدق حدّ: **لا شيء في هذا المستودع يدّعي سلوك عتاد لم يقسه.**
[`docs/verification.md`](docs/verification.md) يذكر ما أُثبِت هنا، وما يعمل على أي جهاز بلا جهاز، وما
**يحتاج هاتفًا** — مكتوبًا «غير مُتحقَّق في هذه البيئة» لا نجاحًا. والجملة قاعدة في هذا المشروع لا
مراوغة.

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="الوثائق"></a>

## <img src="docs/assets/ic-doc.svg?v=2" width="22" height="22" align="absmiddle" alt="الوثائق"> الوثائق

هذه الصفحة هي الجولة. والجواب الذي تصل إليه بعدها في **[`docs/`](docs/README.md)**:

| الصفحة | بسطر واحد |
| --- | --- |
| [features.md](docs/features.md) | كل قدرة، ووظيفتها، وأين هي في التطبيق |
| [max-ai.md](docs/max-ai.md) | محرّك القرار: الهدف والسلامة والقياس والدفتر والتعلّم |
| [max-atlas.md](docs/max-atlas.md) | محرّك التكيّف، مرحلة مرحلة |
| [rom-integration.md](docs/rom-integration.md) | مسارات الدمج، وعدّة AOSP، وSELinux، والتحقّق |
| [compatibility.md](docs/compatibility.md) | إصدارات أندرويد، والمعماريات، ومديرو الجذر، والشرائح — وما هو خارج النطاق |
| [profiles.md](docs/profiles.md) | سلوكيات الشرائح والتنفيذيات الأصلية للوحدة |
| [thermal.md](docs/thermal.md) | حارس الحرارة: دمج المناطق، والسياسة، والتوقّع، والتعلّم |
| [architecture.md](docs/architecture.md) | كيف تلتفّق التطبيق والحراس وواجهات النواة |
| [releases/v1.0.md](docs/releases/v1.0.md) | ملاحظات إصدار ‎v1.0‎، وكيف تتحقّق من التنزيل |
| [verification.md](docs/verification.md) | كيف يُقاس كل ادّعاء هنا — وما لا يمكن قياسه |
| [faq.md](docs/faq.md) | الأسئلة التي تتكرّر |
| [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) | مكوّنات الطرف الثالث مع إشعاراتها |

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="الأسئلة"></a>

## <img src="docs/assets/ic-question.svg?v=2" width="22" height="22" align="absmiddle" alt="الأسئلة"> الأسئلة الشائعة

<details>
<summary><b>هل يحتاج إلى جذر؟</b></summary>

نعم، لمسار التحكّم كاملًا: هو وحدة Magisk/KernelSU، والتطبيق يصل إلى النواة عبر جسر جذر واحد
مُدقَّق. وShizuku (مستوى ADB بلا جذر) يُكتشف أيضًا ويُفعّل عدة أدوات قراءة وكتابة.

</details>

<details>
<summary><b>هل Max AI مُشغَّل افتراضيًّا؟</b></summary>

لا. التحكّم اليدويّ هو الحالة الافتراضية، ولا شيء يُفعّل نفسه. وحين تُشغّله تبقى طبقة السلامة بأولوية
مطلقة.

</details>

<details>
<summary><b>ماذا يحدث إذا ساء شيء؟</b></summary>

تُقرأ القيم بعد كتابتها، ويُعرض عدم التطابق مع محاولة رجوع، وحارس الانزلاق يعيد الفحص لاحقًا،
والمثبِّت يُعطّل نفسه إن فشل في الإقلاع مرّتين.

</details>

<details>
<summary><b>لماذا تُعرض القيمة المجهولة <code>status_unknown</code> لا ٠؟</b></summary>

لأنّ `0` ادّعاء. والتطبيق يقول *مجهول* حين لا يعلم، بدل أن يعرض صفراً يبدو معقولًا.

</details>

<details>
<summary><b>هل يرسل بياناتي إلى أي مكان؟</b></summary>

لا قياس عن بُعد ولا رفع صامت. وتقرير التشخيص يُبنى محليًّا ويُصغَّر، ولا يغادر جهازك إلا إذا سلّمت
الملفّ بنفسك.

</details>

<details>
<summary><b>كيف أزيله تمامًا؟</b></summary>

أزل الوحدة من مدير الجذر. لم يُعدَّل شيء في `/system` تعديلًا دائمًا.

</details>

<details>
<summary><b>لماذا الرخصة مملوكة؟</b></summary>

اختيار المشروع نفسه، مذكور في [`LICENSE`](LICENSE). المستودع العامّ ليس هو المشروع مفتوح المصدر.
ومكوّنات الطرف الثالث تحتفظ برخصها وتُفهرس في [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md).

</details>

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="الدعم"></a>

## <img src="docs/assets/ic-bubble.svg?v=2" width="22" height="22" align="absmiddle" alt="الدعم"> الدعم

- **تيليجرام:** [@ROBINHOOD_GROUP_RODIN](https://t.me/ROBINHOOD_GROUP_RODIN) — بلاغات الأفكار والبناء.
- **البلاغات:** من فضلك اذكر الجهاز، والروم، ومدير الجذر، وما عرضه التطبيق. وإن قال
  `status_unknown` فقل ذلك — إنه حقيقة عن جهازك لا خطأ عليك إصلاحه أولًا.

<a id="الرخصة"></a>

## <img src="docs/assets/ic-seal.svg?v=2" width="22" height="22" align="absmiddle" alt="الرخصة"> الرخصة

**مملوكة.** حقوق النشر (C) 2026 **Nader Magdy**. جميع الحقوق محفوظة. انظر [`LICENSE`](LICENSE) للبنود
الكاملة — لا يُمنح أي حقّ استعمال أو نسخ أو تعديل أو توزيع دون إذن كتابي سابق من صاحب الحقوق.

ومكوّنات الطرف الثالث الموجودة في هذا المستودع أو المبنيّ عليها تحتفظ **برخصها هي**
(Apache-2.0 لـ`archdaemon/` و`thermalcore/`، وBSD-3-Clause لـ`vmtouch` المضمَّن، وغيرها)؛
وإشعاراتها في [`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md).

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>

---

<a id="credits"></a>

## <img src="docs/assets/ic-credit.svg?v=2" width="22" height="22" align="absmiddle" alt="الفضل"> Credits

‏MaxManager لم يُكتب وحده. هذه الأعمال نشكره عليها — وكلّ إشعار تفرضه رخصتها يبقى في
[`THIRD_PARTY_NOTICES.md`](THIRD_PARTY_NOTICES.md)، وهو القائمة الملزمة.

| المشروع | صاحب الحقوق | الرخصة |
| --- | --- | --- |
| [AZenith](https://github.com/Liliya2727/AZenith) | (C) 2025-2026 Zexshia | Apache-2.0 |
| [Encore Tweaks](https://github.com/Rem01Gaming/encore) | (C) 2024-2025 Rem01Gaming | Apache-2.0 |
| [Rianixia-ThermalCore](https://github.com/ryanistr/Rianixia-ThermalCore) | (C) 2025-2026 ryanistr | Apache-2.0 |
| [VMTouch](https://github.com/hoytech/vmtouch) | (c) 2009-2023 Doug Hoyte and contributors | BSD-3-Clause |

<sub><b>اسمك غير موجود في القائمة؟</b> إن كان لك عمل يُستخدم هنا ولم يُذكر أعلاه، راسلني في
الخاص — أو تجدني في [المجموعة](https://t.me/ROBINHOOD_GROUP_RODIN) — وسيُضاف.</sub>

<p align="right"><sub><a href="#top">↑ أعلى الصفحة</a></sub></p>
