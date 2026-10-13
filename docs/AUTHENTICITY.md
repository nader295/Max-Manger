# AUTHENTICITY — قياس استقلال النصّ عن أصول GPL المُزالة

مُولَّد بـ`python3 tools/upstream_similarity.py --write-doc docs/AUTHENTICITY.md --upstream build/audit/zkm-raw --upstream build/audit/vtools-raw`. لا يُكتب بيد.

## 1. الطريقة — ماذا يُقاس بالضبط

تقارن الأداة كل ملف مصدري عندنا بكل ملف في نسخة الأصل المرجعي، بثلاثة مقياسين **مختلفين** — فلا يُخفى أحدهما بالآخر:

| المقياس | ما يقيسه | لماذا هو مستقلّ |
| --- | --- | --- |
| `code` | احتواء رموز البنية (تسميات الدوال والمتغيرات، بعد تجريد التعليقات و`package`/`import`) | يقيس **بنية التعبير** لا النصّ: نسخة مُعاد تسميتها تبقى مكشوفة |
| `raw` | التطابق النصّي الحرفي | يكشف النقل الحرفي ولو غُيّرت الأسماء |
| `lit` | الحرفيات المشتركة (نصوص، أرقام مسارات) | تُفصل عن الاثنين: هي **بيانات** لا تعبير، فلا تُحسب تشابهًا |

السقوف: `code ≥ 0.3` أو مقطع مسمّى ≥ 6 أسطر متتالية ⇒ ملف «يستحق النظر».

## 2. ما قيس في هذه الجولة

- `scanned` = **569**
- `upstream_files` = **146**
- ملفات أصل مرجعي مُحمّلة: **146**

## 3. النتيجة

**لا ملف بلغ السقف بلا سبب مكتوب.** ✅ وهذا ما تقوله البوابة بـ`--assert` (exit 0).

وبلغ السقف 4 ملفًا، وكلّها **بقايا مُعلَنة**: API الأطر تفرض صياغة واحدة، والاسم الذي يفرضه الـAPI ليس نقل تعبير. وكل سبب مكتوب **أدناه في المخرجات** وفي جدول الكود `DECLARED_RESIDUE` نفسه — فلا يُخفي إعلانٌ رقمًا:

| FILE | code | raw | run | الأصل |
| --- | --- | --- | --- | --- |
| `manager/app/src/main/java/nd/max/ui/theme/Type.kt` | 0.471 | 0.231 | 3 | `zkm-raw/kotlin/com/zuan/kernelmanager/ui/theme/Type.kt` |
| `manager/app/src/main/java/nd/max/ui/process/MyLifecycleOwner.kt` | 0.347 | 0.278 | 2 | `zkm-raw/kotlin/com/zuan/kernelmanager/ui/terminal/FloatingTerminalService.kt` |
| `manager/app/src/main/java/nd/max/service/FpsOverlayService.kt` | 0.243 | 0.124 | 7 | `zkm-raw/kotlin/com/zuan/kernelmanager/services/FpsOverlayService.kt` |
| `manager/app/src/main/java/nd/max/service/ProcessOverlayService.kt` | 0.199 | 0.124 | 7 | `zkm-raw/kotlin/com/zuan/kernelmanager/services/FpsOverlayService.kt` |

### أسباب البقايا (منقولة من جدول الكود — تُقرأ ولا تُقدَّر)

- **`manager/app/src/main/java/nd/max/ui/theme/Type.kt`** — صيغة باني Material 3: `TextStyle(fontFamily=…, fontSize=…)` — نفس الـAPI تفرض نفس الأسطر؛ وأصل الملف القياسي ٢٤ سطرًا ويحمل لونًا واحدًا بخطّ النظام، وهذا الملف لوحة كاملة بخطوط المشروع
- **`manager/app/src/main/java/nd/max/ui/process/MyLifecycleOwner.kt`** — تمثيل `SavedStateRegistryOwner` يدويًّا: `LifecycleRegistry(this)` و`SavedStateRegistryController.create(this)` وتجاوزان — لا صياغة ثانية لها في AndroidX
- **`manager/app/src/main/java/nd/max/service/FpsOverlayService.kt`** — تصريحات عقد Compose داخل نافذة عائمة بلا نشاط (windowManager · overlayView · layoutParams · سجل الحالة · مخزن الViewModel) — أسماؤها يفرضها الـAPI، ونفس السبب أدناه
- **`manager/app/src/main/java/nd/max/service/ProcessOverlayService.kt`** — نفس عقد الخدمة السابقة حرفيًّا (الخدمتان تشتركان فيه داخليًّا  أيضًا) — توحيده في وحدة مشتركة عملٌ له مشروعُه لا يُدسّ في جولة تحقّق، والوحدة المُشتركة تُنشأ عند أوّل تعديل وظيفي على إحدى الخدمتين

## 4. حدود هذا القياس

* يقيس **التشابه النصّي** لا الأصل القانوني. ملفّان قد يشتركان في صياغة ويختلفان في الأصل، والعكس — ولذلك يُقرأ مع `docs/PROVENANCE.md` (الذي يحكم من الترويسة).
* البقايا المُعلَنة **لا تُسقِط البوابة لكنها تُطبع في كل تشغيل**، والجدول في الكود (`DECLARED_RESIDUE`) لا يقبل إضافة بلا سبب مكتوب.
* الإعلان يصف API الأطر (Material 3 · AndroidX · عقد خدمة Compose) لا نقل تعبير — وكل ما كان نقلًا تعبيريًّا حقيقيًّا أُعيد تأليفه ولم يُدرج.
