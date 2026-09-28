# Third-Party Notices — MaxManager

هذا الملفّ قائمة **ما ليس مملوكًا لنا ويدخل التوزيع** — بإشعاره ورخصته. وما عدا ذلك يحكمه `LICENSE`
وحده.

**ووظيفته واحدة: أن يقول ما أضفناه.** فلا يُثقل بذكر **منهجٍ** أُلهمنا منه ولا مشروعٍ **لم يُنقل منه
كود**، ولا بسرد تاريخ التنقية وأدلّة الأدوات — فسجلّ الإزالة وإعادة التأليف والدلائل المقيسة في
`docs/PROVENANCE.md` وفي `docs/ai/HANDOFF.md`، وهما موضع الإثبات.

والقائمة **مقيسة لا مكتوبة من الذاكرة**: مصدرها `python3 tools/license_audit.py --json` الذي يقرأ
ترويسة كلّ ملفّ متعقَّب، وترويسة ELF لكلّ ثنائية، وتتبّعات Gradle (٤٢) وصناديق Cargo (١٠٨). ومن قرأ
رقمًا هنا يستطيع إعادة اشتقاقه بالأمر نفسه.

**وعلاقة هذا الملفّ بقسم `Credits` في `README.md`:** يُذكر هناك اسم العمل وحقّ النشر والرخصة
**إعلانًا للفضل**، ولا يُنقل إليه نصّ الإشعار. وهذا الملفّ يبقى **وحده** المرجع الملزم، ووحده موضع
النصّ الكامل للرخصة. ولا تُعاد كتابة ملكية مؤلّف خارجي ولا تُنسب ملفاته إلى المشروع.

## 1. مكوّنات مشمولة في الشجرة

| المكوّن | ما استُعمل منه | الترخيص | حقوق النشر |
| --- | --- | --- | --- |
| **AZenith** `github.com/Liliya2727/AZenith` | صاحب ترويسة `Copyright (C) 2026-2027 Zexshia` التي تحملها **٢٤٧ ملفًا** في `manager/` و`archdaemon/` (ومجموعة `archdaemon/` يصنّفها التدقيق بـ«Encore Daemon (via AZenith)») | Apache-2.0 | Copyright (C) 2025-2026 Zexshia |
| **Encore Tweaks** `github.com/Rem01Gaming/encore` | أساس خدمة `archdaemon/` (٤٠ ملفًا في الوحدة؛ منها ١٤ ملفّ C ومعه `mainfiles/verify.sh` و`AppMonitor.kt` **تحمل ترويسته صراحةً**) | Apache-2.0 | Copyright (C) 2024-2025 Rem01Gaming |
| **Rianixia-ThermalCore** `github.com/ryanistr/Rianixia-ThermalCore` | محرّك الإدارة الحرارية `thermalcore/` (١٦ ملفّ Rust؛ منها ٣ تُسمّي أصله: `main.rs` · `monitor.rs` · `android_ffi.rs`) | Apache-2.0 | Copyright (C) 2025-2026 ryanistr |
| **Android Open Source Project** `source.android.com/license` | بنية مساحة المستخدم وسياسة SELinux؛ أدوات الإقلاع/الصور (`binutils/` · `android/aosp/`) | Apache-2.0 | Copyright (C) The Android Open Source Project |
| **VMTouch** `github.com/hoytech/vmtouch` | **كود مُضمَّن ومُعدَّل**: `preloadbin/jni/main.c` هو vmtouch 1.4.1 (**٩٩٫٧٪ مطابقة — فارق ٣ أسطر**) يُبنى منه `sys.maxmanager-preloadbin` | BSD-3-Clause | Copyright (c) 2009-2023 Doug Hoyte and contributors |

## 2. الإشعارات المحفوظة في ملفّاتها — ولا تُنسخ هنا

- **Apache-2.0 محفوظ كما هو في ٢٨١ ملفًّا** داخل `manager/app` يحمل في ترويسته اسم مؤلّف خارجي
  (`Zexshia` ٢٤٧ · `MaxManager contributors` ٣٢ · `Rapli` ١ · `KowX` ١). وهي تبقى على رخصتها مع
  إشعارها **كما هي**: لا تُعاد كتابتها ولا تُنسب إلى ملكية المشروع — لأن إشعار Apache-2.0 شرط بقاء،
  ولا يُمحى بانتقال الملفّ إلى مجلّد آخر. والتفصيل في `docs/PROVENANCE.md` (حالة
  `APACHE_HEADER_RETAINED`)، وأسماء هؤلاء المؤلّفين في قسم `Credits` بـ`README.md`.
- **vmtouch يُحفظ إشعاره كاملًا في ترويسة ملفّه** (الشرط الأول من BSD-3-Clause: تبقى حقوق النشر
  وقائمة الشروط وإخلاء المسؤولية في المصدر)، فلا يُعاد نسخه هنا ليَشِيخ: الملفّ `preloadbin/jni/main.c`
  يحمل حقوق النشر والرخصة وتعديلات MaxManager، و`preloadbin/README.md` هو README vmtouch الأصلي
  بسطر حقوقه.

## 3. مكتبات تُبنى معها (لا نسخ مصدري في المستودع)

تُقرأ من ملفات البناء والكتالوج، وتُراجَع عند كل تحديث إصدار:

- **تبعيات Gradle (٤٢)** — التوزيع المقيس: `Apache-2.0` (٣٦) · `MIT` (٤، تُشحن) · واثنتان **لا
  تُشحنان** فهما `testImplementation` وحدهما: `junit:junit` (`EPL-1.0`) و`org.json:json`
  (`Public-Domain`). وترخيص `EPL-1.0` **مُعلَن لا مسكوت عنه**: ضعيف الترابط وبمستوى الملفّ،
  والاعتماد عليه في نطاق الاختبار فقط. القائمة بأسمائها في `build/license-report.json`.
- **صناديق Cargo (١٠٨)** — التوزيع المقيس: `MIT OR Apache-2.0` (١٠٣) · `Apache-2.0` (٤) · `Zlib` (١).

## 4. كيف يُتحقّق من هذه القائمة — بأمر، لا بوصف

```sh
python3 tools/license_audit.py --assert       # لا GPL في مسار الإصدار، ولا أصل مُخفى بترويسة ملكية
python3 tools/license_audit.py --self-test    # يقيس الأداة نفسها
```

وتُشغَّلان في CI ضمن خطوة «Contract gates» **قبل** البناء الثقيل، فتنكشف عودة أيّ مكوّن GPL في ثوانٍ.
ونتائج التدقيق الحيّة — بالأرقام والحالات — في `docs/PROVENANCE.md`،
و`docs/AUTHENTICITY.md` لقياس استقلال النصّ عن الأصل المرجعي.
