# PROVENANCE — أصل كل ملف ورخصته وما يجب عمله

> **مُولَّد آليًّا — لا يُحرَّر يدويًّا:**
> `python3 tools/license_audit.py --provenance`
> （و`build/license-report.json` هو نفس القياس بصيغة يقرؤها CI）

**الطريقة:** يُصنَّف كل ملف متعقّب في git من **ترويسته الفعلية** (أول 30 سطرًا) لا من اسمه ولا من مجلّده. ومن لا ترويسة له يُصنَّف بعائلة وحدته ويُكتب ذلك صراحةً في عمود الدليل. والأصول وتراخيصها ومراجعها مقيّدة في جدول `SOURCES` داخل الأداة، فكل حكم هنا قابل لإعادة الاشتقاق بأمر واحد.

## الخلاصة

| المقياس | العدد |
| --- | --- |
| ملفات متعقّبة | 2825 |
| ملفات مشتقّة من GPL | **0** |
| منها داخل مسار الإصدار | **0** |
| ملفات مجهولة الترخيص | 0 |
| ملفات مملوكة (MaxManager) | 2369 |
| ملفات برخصة طرف ثالث حُرّة | 456 |
| تبعيات Gradle | 43 |
| صناديق Cargo | 108 |
| ثغرات ABI | 0 |
| تناقضات ترويسة (GPL + Apache-2.0) | 0 |

## بوابة GPL (PHASE 10)

| السؤال | الجواب |
| --- | --- |
| GPL source in MaxManager-owned code | **NO** |
| GPL dependency | **NO** |
| GPL native binary | **NO** |
| GPL code in APK | **NO** |
| GPL-derived source remaining | **NO** |
| GPL declared in body — pending diff review | **NO** |
| Unknown-license component | **NO** |
| Hidden origin under a proprietary header | **NO** |

**وما دام أيٌّ منها `YES` فالتنظيف غير مكتمل** — والأداة تُفشل CI (`--assert`) عند `gpl_code_in_apk = YES` أو `gpl_native_binary = YES` أو `gpl_dependency = YES` أو `hidden_origin_under_proprietary_header = YES` (إشعار رخصة مُمحى بترويسة ملكية).

## الإزالة وإعادة التأليف — سجل التغيير، والحالة النهائية المقيسة

قائمة ما أُزيل وما أُعيد تأليفه — بالأرقام التي قُيست وقت التنفيذ — في `docs/ai/HANDOFF.md` (جولات التنقية)، **وهنا موضع الإثبات**: لا يُسرد تاريخ التنقية في `THIRD_PARTY_NOTICES.md` (وظيفته ذكر ما أضفناه لا ما أزلناه بأمر المالك). ولا يُعاد كتابة الأرقام التاريخية هنا (تُنسخ فتنحرف)؛ وما يُقاس في هذا الملف هو **الحالة الراهنة**: مشتقّ من GPL = 0، وGPL في مسار الإصدار = 0، ومجهول الترخيص = 0.

وحالة «استقلال النصّ» عن أصل GPL **لا تُدَّعى من هذا الجدول**: تُقاس بأداة مستقلة مقابلةً للأصل (`tools/upstream_similarity.py --assert --upstream …`)، ونتيجتها وبقاياها المُعلَنة تُطبع في كل تشغيل.

## أ‌) ملفات مشتقّة من GPL — تُعاد كتابتها أو تُحذف

لا شيء. ✅

## ج) ملفات بلا أصل خارجي مُعلَن

العدد: **2336** ملفًا (موارد، أيقونات، خطوط، بيانات، ومصادر بترويسة ملكية داخلية بلا ذكر أصل خارجي). وتفصيلها الكامل في `build/license-report.json`.

## د) التبعيات الخارجية

### Gradle

| COORDINATE | SCOPE | SHIPPED | LICENSE |
| --- | --- | --- | --- |
| `androidx.activity:activity-compose:1.11.0` | implementation | نعم | Apache-2.0 |
| `androidx.appcompat:appcompat:1.8.0` | implementation | نعم | Apache-2.0 |
| `androidx.compose.animation:animation` | implementation | نعم | Apache-2.0 |
| `androidx.compose.animation:animation-core` | implementation | نعم | Apache-2.0 |
| `androidx.compose.foundation:foundation` | implementation | نعم | Apache-2.0 |
| `androidx.compose.material3:material3:1.4.0` | implementation | نعم | Apache-2.0 |
| `androidx.compose.material:material` | implementation | نعم | Apache-2.0 |
| `androidx.compose.material:material-icons-extended` | implementation | نعم | Apache-2.0 |
| `androidx.compose.ui:ui` | implementation | نعم | Apache-2.0 |
| `androidx.compose.ui:ui-text-google-fonts` | implementation | نعم | Apache-2.0 |
| `androidx.compose.ui:ui-tooling-preview` | implementation | نعم | Apache-2.0 |
| `androidx.compose:compose-bom:2025.10.01` | implementation | نعم | Apache-2.0 |
| `androidx.documentfile:documentfile:1.1.0` | implementation | نعم | Apache-2.0 |
| `androidx.hilt:hilt-navigation-compose:1.2.0` | implementation | نعم | Apache-2.0 |
| `androidx.lifecycle:lifecycle-runtime-compose:2.9.4` | implementation | نعم | Apache-2.0 |
| `androidx.lifecycle:lifecycle-service:2.9.4` | implementation | نعم | Apache-2.0 |
| `androidx.lifecycle:lifecycle-viewmodel-compose:2.9.4` | implementation | نعم | Apache-2.0 |
| `androidx.media3:media3-exoplayer:1.3.0` | implementation | نعم | Apache-2.0 |
| `androidx.media3:media3-ui:1.3.0` | implementation | نعم | Apache-2.0 |
| `androidx.navigation:navigation-compose:2.9.4` | implementation | نعم | Apache-2.0 |
| `androidx.transition:transition:1.7.1` | implementation | نعم | Apache-2.0 |
| `com.github.Fox2Code.AndroidANSI:library-ktx:1.2.1` | implementation | نعم | MIT |
| `com.github.Fox2Code.AndroidANSI:library:1.2.1` | implementation | نعم | MIT |
| `com.github.jeziellago:compose-markdown:0.7.2` | implementation | نعم | MIT |
| `com.github.topjohnwu.libsu:core:6.0.0` | implementation | نعم | Apache-2.0 |
| `com.github.topjohnwu.libsu:io:6.0.0` | implementation | نعم | Apache-2.0 |
| `com.github.topjohnwu.libsu:service:6.0.0` | implementation | نعم | Apache-2.0 |
| `com.github.yalantis:ucrop:2.2.11-native` | implementation | نعم | Apache-2.0 |
| `com.google.dagger:hilt-android:2.59.2` | implementation | نعم | Apache-2.0 |
| `com.google.dagger:hilt-compiler:2.59.2` | ksp | نعم | Apache-2.0 |
| `com.materialkolor:material-kolor:5.0.0-alpha07` | implementation | نعم | MIT |
| `dev.chrisbanes.haze:haze-android:2.0.0-alpha02` | implementation | نعم | Apache-2.0 |
| `dev.chrisbanes.haze:haze-blur-materials:2.0.0-alpha02` | implementation | نعم | Apache-2.0 |
| `dev.chrisbanes.haze:haze-blur:2.0.0-alpha02` | implementation | نعم | Apache-2.0 |
| `dev.rikka.shizuku:api:13.1.5` | implementation | نعم | Apache-2.0 |
| `dev.rikka.shizuku:provider:13.1.5` | implementation | نعم | Apache-2.0 |
| `io.coil-kt:coil-compose:2.7.0` | implementation | نعم | Apache-2.0 |
| `io.coil-kt:coil-gif:2.7.0` | implementation | نعم | Apache-2.0 |
| `junit:junit:4.13.2` | testImplementation | لا (اختبار) | EPL-1.0 |
| `me.zhanghai.android.appiconloader:appiconloader-coil:1.5.0` | implementation | نعم | Apache-2.0 |
| `org.jetbrains.kotlinx:kotlinx-serialization-json:1.11.0` | implementation | نعم | Apache-2.0 |
| `org.json:json:20260814` | testImplementation | لا (اختبار) | Public-Domain |
| `org.lsposed.hiddenapibypass:hiddenapibypass:6.1` | implementation | نعم | Apache-2.0 |

### Cargo

| CRATE | VERSION | LOCAL | LICENSE |
| --- | --- | --- | --- |
| `android_system_properties` | 0.1.5 | لا | MIT OR Apache-2.0 |
| `autocfg` | 1.5.1 | لا | MIT OR Apache-2.0 |
| `bincode` | 2.0.1 | لا | MIT OR Apache-2.0 |
| `bincode_derive` | 2.0.1 | لا | MIT OR Apache-2.0 |
| `bitflags` | 2.10.0 | لا | MIT OR Apache-2.0 |
| `bumpalo` | 3.19.0 | لا | MIT OR Apache-2.0 |
| `bytes` | 1.12.1 | لا | MIT OR Apache-2.0 |
| `cc` | 1.2.43 | لا | MIT OR Apache-2.0 |
| `cesu8` | 1.1.0 | لا | MIT OR Apache-2.0 |
| `cfg-if` | 1.0.5 | لا | MIT OR Apache-2.0 |
| `cfg_aliases` | 0.2.1 | لا | MIT OR Apache-2.0 |
| `chrono` | 0.4.42 | لا | MIT OR Apache-2.0 |
| `combine` | 4.6.8 | لا | MIT OR Apache-2.0 |
| `core-foundation-sys` | 0.8.7 | لا | MIT OR Apache-2.0 |
| `crc32fast` | 1.5.2 | لا | MIT OR Apache-2.0 |
| `equivalent` | 1.0.2 | لا | MIT OR Apache-2.0 |
| `find-msvc-tools` | 0.1.4 | لا | MIT OR Apache-2.0 |
| `flate2` | 1.1.10 | لا | MIT OR Apache-2.0 |
| `futures-core` | 0.3.31 | لا | MIT OR Apache-2.0 |
| `glob` | 0.3.3 | لا | MIT OR Apache-2.0 |
| `hashbrown` | 0.17.1 | لا | MIT OR Apache-2.0 |
| `iana-time-zone` | 0.1.64 | لا | MIT OR Apache-2.0 |
| `iana-time-zone-haiku` | 0.1.2 | لا | MIT OR Apache-2.0 |
| `indexmap` | 2.14.2 | لا | MIT OR Apache-2.0 |
| `inotify` | 0.11.0 | لا | MIT OR Apache-2.0 |
| `inotify-sys` | 0.1.5 | لا | MIT OR Apache-2.0 |
| `itoa` | 1.0.18 | لا | MIT OR Apache-2.0 |
| `jni` | 0.21.1 | لا | MIT OR Apache-2.0 |
| `jni-sys` | 0.4.1 | لا | MIT OR Apache-2.0 |
| `jni-sys-macros` | 0.4.1 | لا | MIT OR Apache-2.0 |
| `js-sys` | 0.3.82 | لا | MIT OR Apache-2.0 |
| `lazy_static` | 1.5.0 | لا | MIT OR Apache-2.0 |
| `libc` | 0.2.177 | لا | MIT OR Apache-2.0 |
| `log` | 0.4.34 | لا | MIT OR Apache-2.0 |
| `matrixmultiply` | 0.3.11 | لا | MIT OR Apache-2.0 |
| `maxmanager-profilesettings` | 1.0.0 | نعم | Apache-2.0 |
| `maxmanager-utilityconf` | 1.0.0 | نعم | Apache-2.0 |
| `maxmanager_native` | 0.1.0 | نعم | Apache-2.0 |
| `memchr` | 2.8.3 | لا | MIT OR Apache-2.0 |
| `mio` | 1.1.0 | لا | MIT OR Apache-2.0 |
| `ndarray` | 0.15.6 | لا | MIT OR Apache-2.0 |
| `nix` | 0.30.1 | لا | MIT OR Apache-2.0 |
| `ntapi` | 0.4.1 | لا | MIT OR Apache-2.0 |
| `num-complex` | 0.4.6 | لا | MIT OR Apache-2.0 |
| `num-integer` | 0.1.47 | لا | MIT OR Apache-2.0 |
| `num-traits` | 0.2.19 | لا | MIT OR Apache-2.0 |
| `objc2-core-foundation` | 0.3.2 | لا | MIT OR Apache-2.0 |
| `objc2-io-kit` | 0.3.2 | لا | MIT OR Apache-2.0 |
| `once_cell` | 1.21.3 | لا | MIT OR Apache-2.0 |
| `pin-project-lite` | 0.2.16 | لا | MIT OR Apache-2.0 |
| `proc-macro2` | 1.0.107 | لا | MIT OR Apache-2.0 |
| `quote` | 1.0.47 | لا | MIT OR Apache-2.0 |
| `rawpointer` | 0.2.1 | لا | MIT OR Apache-2.0 |
| `rianixia-thermalcore` | 2.0.0 | نعم | Apache-2.0 |
| `rustversion` | 1.0.22 | لا | MIT OR Apache-2.0 |
| `ryu` | 1.0.20 | لا | MIT OR Apache-2.0 |
| `same-file` | 1.0.6 | لا | MIT OR Apache-2.0 |
| `serde` | 1.0.229 | لا | MIT OR Apache-2.0 |
| `serde_core` | 1.0.229 | لا | MIT OR Apache-2.0 |
| `serde_derive` | 1.0.229 | لا | MIT OR Apache-2.0 |
| `serde_json` | 1.0.151 | لا | MIT OR Apache-2.0 |
| `shlex` | 1.3.0 | لا | MIT OR Apache-2.0 |
| `signal-hook` | 0.3.18 | لا | MIT OR Apache-2.0 |
| `signal-hook-registry` | 1.4.6 | لا | MIT OR Apache-2.0 |
| `socket2` | 0.6.1 | لا | MIT OR Apache-2.0 |
| `syn` | 3.0.6 | لا | MIT OR Apache-2.0 |
| `sysinfo` | 0.37.2 | لا | MIT OR Apache-2.0 |
| `thiserror` | 1.0.69 | لا | MIT OR Apache-2.0 |
| `thiserror-impl` | 1.0.69 | لا | MIT OR Apache-2.0 |
| `tokio` | 1.48.0 | لا | MIT OR Apache-2.0 |
| `typed-path` | 0.12.3 | لا | MIT OR Apache-2.0 |
| `unicode-ident` | 1.0.26 | لا | MIT OR Apache-2.0 |
| `unty` | 0.0.4 | لا | MIT OR Apache-2.0 |
| `virtue` | 0.0.18 | لا | MIT OR Apache-2.0 |
| `walkdir` | 2.5.0 | لا | MIT OR Apache-2.0 |
| `wasi` | 0.11.1+wasi-snapshot-preview1 | لا | MIT OR Apache-2.0 |
| `wasm-bindgen` | 0.2.105 | لا | MIT OR Apache-2.0 |
| `wasm-bindgen-macro` | 0.2.105 | لا | MIT OR Apache-2.0 |
| `wasm-bindgen-macro-support` | 0.2.105 | لا | MIT OR Apache-2.0 |
| `wasm-bindgen-shared` | 0.2.105 | لا | MIT OR Apache-2.0 |
| `winapi` | 0.3.9 | لا | MIT OR Apache-2.0 |
| `winapi-i686-pc-windows-gnu` | 0.4.0 | لا | MIT OR Apache-2.0 |
| `winapi-util` | 0.1.11 | لا | MIT OR Apache-2.0 |
| `winapi-x86_64-pc-windows-gnu` | 0.4.0 | لا | MIT OR Apache-2.0 |
| `windows` | 0.61.3 | لا | MIT OR Apache-2.0 |
| `windows-collections` | 0.2.0 | لا | MIT OR Apache-2.0 |
| `windows-core` | 0.62.2 | لا | MIT OR Apache-2.0 |
| `windows-future` | 0.2.1 | لا | MIT OR Apache-2.0 |
| `windows-implement` | 0.60.2 | لا | MIT OR Apache-2.0 |
| `windows-interface` | 0.59.3 | لا | MIT OR Apache-2.0 |
| `windows-link` | 0.2.1 | لا | MIT OR Apache-2.0 |
| `windows-numerics` | 0.2.0 | لا | MIT OR Apache-2.0 |
| `windows-result` | 0.4.1 | لا | MIT OR Apache-2.0 |
| `windows-strings` | 0.5.1 | لا | MIT OR Apache-2.0 |
| `windows-sys` | 0.61.2 | لا | MIT OR Apache-2.0 |
| `windows-targets` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows-threading` | 0.1.0 | لا | MIT OR Apache-2.0 |
| `windows_aarch64_gnullvm` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows_aarch64_msvc` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows_i686_gnu` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows_i686_gnullvm` | 0.53.1 | لا | MIT OR Apache-2.0 |
| `windows_i686_msvc` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows_x86_64_gnu` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows_x86_64_gnullvm` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `windows_x86_64_msvc` | 0.42.2 | لا | MIT OR Apache-2.0 |
| `zip` | 8.6.0 | لا | MIT OR Apache-2.0 |
| `zlib-rs` | 0.6.8 | لا | Zlib |
| `zmij` | 1.0.23 | لا | MIT OR Apache-2.0 |

## هـ) الثنائيات ومعمارياتها

| FILE | ARCH | ORIGIN | LICENSE | ACTION |
| --- | --- | --- | --- | --- |
| `manager/gradle/wrapper/gradle-wrapper.jar` | — | MaxManager app | Proprietary (All rights reserved) | **ATTRIBUTE** |

## و) حدود هذا التدقيق

* الحكم مبنيّ على **ما هو مُعلَن في الترويسة**، لا على تشابه دلالي يُقاس بالـdiff. فملف بلا ترويسة قد يكون مُشتقًّا وهو غير معروف — وهذا احتمال يُدار بالمراجعة البشرية لا يُدَّعى نفيه. ولذلك تُفصل حالة `GPL_REFERENCED` عن `GPL_DERIVED`: الأولى **دعوى استقلال** لم تُختبر بعد، والثانية **إقرار بأصل**.
* الاسم في الترويسة يُحتسب أصلًا **فقط** إذا جاء في سطر يحمل سياق نسبة (مأخوذ · مبني على · حقوق · رخصة). بلا هذا الشرط كانت ثوابت مسارات مثل `/data/data/com.termux/files/usr/bin` تُصنّف ملفاتها «مشتقّة من Termux» — وهي إيجابية كاذبة أُزيلت بقياس لا بتقدير.
* `docs/` و`tools/` تُصنَّفان بعائلة وحدتهما ولا يُستنتج أصلهما من أسماء مشاريع تُذكر فيهما وصفًا؛ فلا يظهر نثر الأدوات «مشتقًّا» من كل من يُسمّى فيه.
* ما لا أصل خارجي له ولا عائلة وحدة معروفة يُصنَّف **افتراضًا مُعلَنًا**: رخصة المستودع، بحالة `REPO_DEFAULT`. وهذا افتراض عن نطاق المشروع لا قياس — يُكتب كما هو ولا يُقدَّم كإثبات.
* وبيانات المستودع (`devices.db` · `socs.json` · `maxmanagerApplist.json`) **لا** تدخل في ذلك الافتراض العام، ولا تبقى `Unknown`: تُقرأ من جدول `DECLARED_DATA_ASSETS` بدليل مكتوب بجانب كل سطر (حالة `DATA_ASSET_DECLARED`) — والقياس الذي أعلنها: لا نظير لها في أي أصل خارجي مُدقَّق (ZKM ٤٤٣ ملفًا · vtools · أشجار raw)، وأُضيفت في الالتزام الأول `581fe5d`. وحدّه معلَن: هذا ينفي ما فُحص لا كل شيء في العالم.
* لا تصل الأداة إلى الشبكة: التراخيص من جدول مُنتقى بسند، وما ليس فيه يُكتب `Unknown`.
* جدول `DEP_LICENSES` يغطّي التبعيات المستعملة اليوم؛ وإضافة تبعية جديدة بدون سطر له تظهر `Unknown` لا `Apache-2.0`.

## ز) جدول الملفات المصدرية الكامل

| FILE | ORIGIN | LICENSE | STATUS | ACTION |
| --- | --- | --- | --- | --- |
| `.github/scripts/build_developer_bundle.sh` | MaxManager CI | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `.github/scripts/changelog.sh` | MaxManager CI | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `.github/scripts/compile_zip.sh` | MaxManager CI | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `.github/scripts/generatesha256.sh` | MaxManager CI | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `.github/scripts/telebot.sh` | MaxManager CI | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `.github/scripts/verify.sh` | MaxManager CI | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/aosp/Android.bp` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/aosp/BoardConfig.mk` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/aosp/maxmanager.rc` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/aosp/product-inclusion.mk` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/aosp/sepolicy/maxmanager.te` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/kernelsu/action.sh` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/kernelsu/customize.sh` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/kernelsu/service.sh` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `android/kernelsu/uninstall.sh` | MaxManager platform integration | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/jni/Android.mk` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/Application.mk` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/Main.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/include/MaxManager.h` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/AppLoader/AppLoader.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/AppLoader/StatusMonitor.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/AppLoader/VisibleApps.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/BinaryCLI/BinaryCLI.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/BinaryCLI/BypassCompatibility.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/BinaryCLI/CLIUtility.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/BypassCharge/ChargingNodes.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/BypassCharge/ChargingUtility.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/ConfigHandler/RefreshRateHandler.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/ConfigHandler/RenderingHandler.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/ConfigHandler/ResolutionChanger.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/ConfigHandler/StateHandler.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/FileUtility/FileHandler.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/FileUtility/LockFile.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/GamePreload/GamePreload.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/InotifyHandler/InotifyWatcher.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/MaxManagerUtility/AppPriority.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/MaxManagerUtility/DaemonUtility.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/MaxManagerUtility/ModuleIntegrity.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/PidTracker/PidTracker.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/ShellUtility/ExecuteCommand.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/ShellUtility/ExecuteDirect.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/ShellUtility/SystemvUtility.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/StartupInit/ConfigLoader.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/StartupInit/DaemonContext.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/StartupInit/DaemonStartup.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/StartupInit/PropValidator.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/System/System.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/SystemLogger/SystemLogger.c` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `archdaemon/jni/src/SystemProfile/PerAppKernel.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/SystemProfile/PerAppThermal.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/SystemProfile/ProfileUtility.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/jni/src/SystemProfile/SystemProfiles.c` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `archdaemon/tests/broadcast.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/cli_profile.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/file_protocols.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/host/fopen_router.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/host/host.h` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/host/props.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/host/shim/host_prelude.h` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/host/shim/sys/system_properties.h` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/host/stubs.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `archdaemon/tests/parity_test.c` | MaxManager (host parity tests) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/chipsets/exynos.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/chipsets/mediatek.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/chipsets/mod.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/chipsets/snapdragon.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/chipsets/tensor.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/chipsets/unisoc.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/main.rs` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `binprofiles/src/plan.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/profiles/mod.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binprofiles/src/props.rs` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `binprofiles/src/utils/mod.rs` | MaxManager binprofiles | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binutils/src/main.rs` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `binutils/src/utils/logger.rs` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `binutils/src/utils/mod.rs` | MaxManager binutils | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `binutils/src/utils/plan.rs` | MaxManager binutils | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `mainfiles/action.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/customize.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/post-fs-data.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/preferenced-tweaks.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/props.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/service.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/uninstall.sh` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `mainfiles/verify.sh` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/build.gradle.kts` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/proguard-rules.pro` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/debug/java/nd/max/ui/component/StudioPreviews.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/aidl/nd/max/core/ipc/IRootNodeService.aidl` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/assets/devices.db` | MaxManager declared data asset | Proprietary (All rights reserved) | DATA_ASSET_DECLARED | KEEP |
| `manager/app/src/main/assets/socs.json` | MaxManager declared data asset | Proprietary (All rights reserved) | DATA_ASSET_DECLARED | KEEP |
| `manager/app/src/main/java/nd/max/AppMonitor.kt` | Encore Tweaks | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/AppMonitorLogger.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/MainActivity.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/MaxManagerApplication.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/MaxManagerPaths.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/MaxManagerProps.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/PerAppRefreshRateController.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/RefreshRate.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/TileService/BypassChgTileService.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/TileService/ProfileTileService.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/XiaomiVendorFeatures.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasBackendProvider.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasCapabilityMap.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasCapabilityState.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasCatalog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasCommunityBank.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasControlIntent.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasDeviceIdentity.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasDeviceProfile.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasDiscovery.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasEvidenceStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasFailureLedger.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasFileReadTransport.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasFileStoreIo.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasFixture.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasFixtureRecorder.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasFreshness.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasModels.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasPlatformProvider.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasProbeSchedule.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasRepository.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasResolver.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasRoutePlanner.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/AtlasSafetyPolicy.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/atlas/MaxAtlas.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioBackendLadder.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioBackendMeasurement.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioCapabilities.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioCapabilityProbe.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioDeviceCatalog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioDynamicsModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioDynamicsParam.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEffectBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEffectKind.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEffectLibraryStaging.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEffectProbe.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEffectSession.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEffectsXml.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEngineCapability.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioEqModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioInventory.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioKnobVerdict.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioMixerBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioMixerModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioPresetController.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioProfileStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioProfileV2.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioRoutingBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSoundPreset.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSpectrumCapture.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSpectrumModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioStreamBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioStreamCatalog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioStreamVerdict.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioStrengthModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSystemEffectBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSystemEffectsModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSystemModuleModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/AudioSystemVerdict.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/DolbyDapProtocol.kt` | DolbyUI (Lunaris AOSP) | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/core/audio/MaxFxControlBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/MaxFxModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/VendorAudioAdapter.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/VendorAudioBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/VendorAudioDiscovery.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/audio/VendorAudioModel.kt` | DolbyUI (Lunaris AOSP) | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/core/audio/VendorEffectSession.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/daemon/DaemonControl.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/daemon/DaemonSupervisor.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/daemon/ModuleWatchman.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/di/AppModule.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/di/DataModule.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/AtlasDoctor.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/AtlasReportExporter.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/AtlasSupportReport.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/DeviceBlueprint.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/diagnostics/DiagnosticCenter.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/diagnostics/HardwareRouteHealth.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/LogCodeGlossary.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/LogDiagnosticReport.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/LogEventLine.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/LogHeader.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/diagnostics/LogSettingsDigest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/CockpitModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameLibrary.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameLibraryAccess.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameLobbyMeta.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameProfileDocument.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameProfilePersistence.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameProfileRepository.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameSessionPanel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/GameSpaceRepository.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/LobbyModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/PanelClocks.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/main/java/nd/max/core/gamespace/PanelControls.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/main/java/nd/max/core/gamespace/PanelDevice.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/main/java/nd/max/core/gamespace/PanelHandleMath.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/gamespace/PanelToggles.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AdaptiveProfileEngine.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasAdapters.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasAdaptiveExecutor.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasDiscoveredControl.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasGpuAdapters.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasPrivilegedReadTransport.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasRouteMemory.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/AtlasRouteMemoryFactory.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ChargingHardwareBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ContextData.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ControlOwnership.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/CpuHardwareBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/DeviceStateCollector.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/DeviceWriteRecording.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/DriftGuard.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/GpuCeilingPolicy.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/GpuHardwareBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/GpuTweakPersistence.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareCapability.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareCapabilityResolver.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareControlArbiter.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareControlKey.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareDataSource.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareRepairExecutor.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareRepairModels.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareRuntime.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/HardwareVerification.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ManualControlLocks.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/MemoryPressureReader.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/MtkGpuFixedIndex.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/MtkGpuOppTable.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/PerAppControlRegistry.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/PerAppFrequencyController.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/PerAppHardwareStatus.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/PerAppRecoveryStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/PlatformCeilingAuthority.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/PredictiveSafety.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ProfileApplier.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/ReadOnlyProbeAccess.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/RootFileAccess.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/RouteEvidenceFacts.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/SharedControlStorage.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/SharedHardwareOwnershipStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ThermalCeilingRouter.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ThermalCurve.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ThermalGuard.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/VerifiedControl.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/hardware/WriteVerification.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/hardware/ZramHardwareBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/ipc/RootNodeChannel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/ipc/RootNodeService.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ArchiveBridge.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ArchivePacket.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ContextBridge.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/PredictorBridge.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ProbeBridge.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ProbePacket.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/PropBridge.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ScanBridge.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/jni/ScanPacket.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/CoalescingCycleRunner.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/ControlOutcomeModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/ControlPlane.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/ControlRegistry.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/CpuCeilingKnobs.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/CredibilityStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/DynamicIntentLearner.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiCadence.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiEngine.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiEpisode.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiInsights.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiJournal.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiJournalCodec.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiModels.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiThermalBudget.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MaxAiThermalCurve.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MemoryStall.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/MinimalPlanner.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/Objective.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/ResponseModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/SafetyEngine.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/SafetyGovernor.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/ThermalCapDistribution.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/maxai/TrustModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/AppStatusProtocol.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/ChipsetIdentity.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/ChipsetMatcher.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/EventLog.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/platform/ForegroundAppResolver.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/FpsMonitorUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/HardwareUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/platform/HudSession.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/platform/ProcessFeed.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/ProcessWatch.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/platform/PropertyUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/platform/SensorInventory.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/platform/SensorMonitorUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/platform/ThermalUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/privilege/PrivilegeLevel.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/privilege/PrivilegeManager.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/privilege/ShizukuGateway.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/core/recommendation/RecommendationModels.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/recommendation/RecommendationTextClassifier.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/CopgTag.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/PerAppDeviceModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SampleDevice.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofApplyBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofApplyEngine.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofBarrierStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofCapabilityMatrix.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofConfigTransaction.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofConfigurationRepository.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofCopgBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofCopgContract.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofDeviceCatalog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofEngineAdapter.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofEngineGate.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofEngineRegistry.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofExistingPerApp.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofFileTransaction.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofFpsTargets.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofGlobalBackend.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofGlobalContract.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofIdentityModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofProfile.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofProfileStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofRecoveryModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/spoof/SpoofRecoveryStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/core/threading/DispatcherProvider.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/data/datasources/HardwareDataSourceImpl.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/receiver/MaxManagerReceiver.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/receiver/ModuleWatchReceiver.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/service/FpsOverlayService.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/service/GamePanelService.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/service/OverlayForeground.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/service/ProcessOverlayService.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/activitylauncher/ActivityIndex.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/activitylauncher/ActivityLauncherScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/activitylauncher/ActivityLauncherViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/AboutAppsComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/AccessibilitySemantics.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/AdaptiveLayout.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/AmbientGlowCycle.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/AmbientMotifOverlay.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/AppIconComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/BottomSheetComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/CapabilityMatrixCard.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/ConfigBackupFlow.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/ContentStateComponents.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/DecisionHierarchy.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/DialogComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/ExpressiveListComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileBottomBars.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileCompressDialog.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileDrawerContent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileEditorDialog.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileEntryList.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FilePropertiesDialog.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileSearchDialog.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/FileWindowChrome.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/GamePanelCockpit.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/GamePanelHandle.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/GamePanelSurface.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/main/java/nd/max/ui/component/GaugeComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/HomeComponents.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/HudSurface.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/LiveGraphComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/LobbyCarousel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/LobbyMotion.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/LobbyVisuals.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxAiEntryButton.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxAiShortcut.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxControls.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxDesignSystem.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxDeviceInfoShortcut.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxFeedback.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxInteractionComponents.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/MaxMotion.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/ModuleBackupComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/NeuralClockWave.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/NeuralDashboardKit.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/NeuralPill.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/NeuralSparkline.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/PowerCoreCard.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/PrivilegePanel.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/ProcessSurface.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/PulseArt.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/PulseFieldEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/RefreshRateComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/RendererComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/RouteVerdictLabel.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/ScreenChrome.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/SensorInventoryCard.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/SettingsHeaderComponent.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/component/StudioButtons.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/StudioComponents.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/StudioSectionHeader.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/component/WarningBanner.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxAiCinematics.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxAudioVisuals.kt` | DolbyUI (Lunaris AOSP) | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/ui/design/MaxBar.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxCard.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxCardShell.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxCommandMenu.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxCondition.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxContextMenu.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxControlRows.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxCurvePlot.kt` | DolbyUI (Lunaris AOSP) | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/ui/design/MaxDialogs.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxDomainCard.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxDrawer.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxFloatingNotice.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxHelp.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxMetric.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxProgressStrip.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxScreenScaffold.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxScrollToTop.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxSearchField.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxStructure.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxTabStrip.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxTabbedDialog.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/design/MaxTokens.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/design/MaxViewMenu.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/ActivityCardSettings.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/ApplistScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/AtlasDiagnosticsSection.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/mainscreens/ControlLayoutModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/ControlScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/DiagnosticsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/mainscreens/GetStartedScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeCapacityCards.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeCommandDeck.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeDashboardComponents.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeDeckModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeDeckSettingsSheet.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeFormat.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeGuideBanners.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeGuideModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/HomeScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/LegacyTweakComponents.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/mainscreens/LegendaryHomeDashboard.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/MaxAiPresentation.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/MaxAiRuntimeStatus.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/MaxAiScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/MaxLiveScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/ScreenFinderModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/ScreenFinderSheet.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/SettingsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/mainscreens/StoryboardHome.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/StoryboardModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/mainscreens/UnifiedActivityModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/navigation/LaunchRoutes.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/navigation/MaxDestinationCatalog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/navigation/MaxDestinations.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/navigation/MaxNavActions.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/navigation/MaxNavBar.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/navigation/MaxNavGraph.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/overlay/OverlayWindow.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/overlay/SilkDragController.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/settings/AppLanguage.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/settings/LanguagePicker.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/settings/SettingsPreference.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/settings/SettingsViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/AboutScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/AppSettingsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/AppSpoofSection.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/BypassChargeScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/BypassCheckScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/ChargingScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/ColorSchemeScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/ConfigBackupScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/CpuCoreControlScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/CustomThemeScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/DebloatFreezeScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoAudioFacts.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoCollect.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoEntryPoints.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoFacts.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoFormat.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoHero.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoHeroModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DeviceInfoScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/Dex2oatScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/DisplayStudioScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/DozeModeScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/EmulatorHubScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/FasSettingsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerActions.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerCommands.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerDialogs.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerPanes.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerPersistence.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerSelection.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FileManagerState.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FpsGoSettingsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/FpsOverlayScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/GameLobbyManageDialog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/GameLobbyScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/GameProfileDialog.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/GovSettingsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/GpuStudioScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/HmaCompanionScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/LogsViewerScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/LogsViewerSections.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/MaxBackupHubScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/MaxBackupPickerScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/MaxBackupRecentItem.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/MaxBackupScheduleSection.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/MaxBackupScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/MaxBackupSystemSection.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/ModuleHealthScreen.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/NetworkDetailScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/NetworkSchedulerScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/PermissionsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/PluginsScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/PreferencedTweakScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/PrivilegeScreen.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/ProcessManagerScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/ResolutionScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/SetEditScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/StorageDetailScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/ThermalDetailScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/TouchBoostScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/UltraCleanerScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/ZramManagerScreen.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioBackendSection.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioCapabilitySection.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioEngineSections.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioPresetResources.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioSoundPresetsSection.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioStudioHero.kt` | DolbyUI (Lunaris AOSP) | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioStudioScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioStudioTabBar.kt` | DolbyUI (Lunaris AOSP) | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/AudioSystemSections.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/audio/MaxFxSection.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/subscreens/hubs/MaxDomainHubScreen.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/theme/Fonts.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/theme/MaxTypography.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/theme/Shape.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/theme/Theme.kt` | KowX | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/theme/Type.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ActivityCardPreferences.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/ApkInspector.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/AppConfigUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/AppOpsBatch.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/AppOpsUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/AppVersionUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/BackgroundGovernanceUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/BackupManagerUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/BannerImageUtil.kt` | Rapli | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/BatteryHealthUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/BootHistoryUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ChargeLedger.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ClockMeterModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ClockWaveModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ConfigBackupInventory.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/CoreClockMath.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/CpuTopologyUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/CrashLogUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/DebloatFreezeUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/DeviceNameUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/Dex2oatUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/DisplayUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/DozeModeUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/FileActionModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileArchiveEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileBookmarkModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileClipboardModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileConflictModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileDeleteModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileHomeModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileOpenModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileOperationRunner.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FilePermissionModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FilePermissionOps.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileSearchEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileSearchFilters.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileSearchPlan.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileStore.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileSystemEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileSystemModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileTarCodec.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileTaskModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FileWindowModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/FpsOverlayPrefs.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/GamePanelPrefs.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/HardwareChoice.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/HomeActivityModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/HomeDeckStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/InstallSourceUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/LoadHistory.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/LogUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MainThreadStallDetector.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupCounts.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupFavorites.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupFolders.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupRetention.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupSchedule.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupScheduler.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupStorage.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupSystemEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxBackupSystemModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxPrefsBundle.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MaxSearch.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/MemoryBoostEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/MemoryLedger.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ModuleHealthUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ModuleInventory.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/MtkUtils.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/PerAppKernelUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/PermissionPolicy.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/PluginContract.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/PluginDirectory.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/PrivilegedShell.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ProcessOverlayPrefs.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/ProfilePresetStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/ProfileSharing.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/RebootUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/RefreshRatesUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/RootMount.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/RootUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/SELinuxCheckerUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ScreenUsageStore.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/SetEditUtil.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/SettingsVisibilityUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/SpectrumModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/StorageHealthUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/StorageScanModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/StorageUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/StoryboardSources.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/util/ThermalModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/UltraCleanEngine.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/UltraCleanModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/VersionIdentity.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/WallpaperUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/XiaomiVendorHalUtil.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/util/ZramPlatformUtil.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/AppSettingsViewmodel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/ApplistViewmodel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/AtlasViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/AudioStudioUiState.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/AudioStudioViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/ChargingViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/CpuCoreControlViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/DebloatFreezeViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/Dex2oatViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/DisplayStudioViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/DozeModeViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/GameSpaceViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/GpuStudioViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/HomeActivityViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/HomeDashboardViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/HomeViewmodel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/LogsLineParser.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/LogsViewerViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/MaxAiViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/NetworkSchedulerViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/ProcessManagerViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/ResolutionViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/SetEditViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/SettingViewmodel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/SpoofStudioViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/TouchBoostViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/TweakViewmodel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/main/java/nd/max/ui/viewmodel/UltraCleanerViewModel.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/main/java/nd/max/ui/viewmodel/ZramViewModel.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/architecture/LayeringArchitectureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/AppStatusProtocolContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/BroadcastContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/ContractFixtures.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/DaemonCliContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/ExecOwnershipContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/FilePathsContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/FileProtocolContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/ModuleWatchmanContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/PerAppHardwareStatusContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/RootNodeContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/RootNodeSemanticsContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/SharedControlPlaneContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/contract/SystemPropertiesContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasArchitectureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasBackendProviderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasCapabilityMapTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasCatalogTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasChildScopeTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasCommunityBankTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasCompletionTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasDeviceIdentityTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasDeviceProfileTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasFailureLedgerTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasFileReadTransportTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasFixtureRecorderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasFixtureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasFreshnessTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasHarnessTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasPlatformProviderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasRealReadIntegrationTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasResolverTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasRoutePlannerTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/AtlasSafetyPolicyTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/MaxAtlasTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/support/AtlasBudgets.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/support/AtlasCanaries.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/support/AtlasClock.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/support/AtlasFakeTransport.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/atlas/support/AtlasSourceGuard.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioBackendLadderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioCapabilitiesTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioDynamicsModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioEffectsXmlTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioEngineCapabilityTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioEqModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioKnobVerdictTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioMixerSpectrumTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioProfileV2Test.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioSoundPresetTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioStreamCatalogTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioStreamVerdictTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioSystemEffectsModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioSystemModuleModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/AudioSystemVerdictTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/DolbyDapProtocolTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/MaxFxModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/audio/VendorAudioModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/daemon/DaemonControlTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/daemon/DaemonSupervisorTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/daemon/ModuleWatchmanTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/AtlasDoctorTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/AtlasSupportReportTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/DiagnosticCenterTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/HardwareRouteHealthTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/LogCodeGlossaryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/LogDiagnosticReportTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/LogEventLineTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/diagnostics/LogHeaderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/CockpitModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/GameLibraryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/GameLobbyMetaTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/GameProfileDocumentTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/GameProfilePersistenceTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/GameSessionPanelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/LobbyModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/PanelHandleMathTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/gamespace/PanelTogglesTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasAdapterRegistryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasAdaptiveExecutorTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasAdaptiveReadTransportTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasDiscoveredControlTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasGpuAdaptersTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasRouteMemoryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/AtlasRouteMemoryWiringTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/CeilingRaiseTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ChargingHardwareBackendTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ControlPlaneArchitectureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/CpuAvailableFrequencySnapTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/CpuProvenRangeTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/GpuCeilingPolicyTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/GpuControlModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/HardwareControlArbiterTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/HardwareControlArbiterVerificationTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/HardwareRepairExecutorTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/HardwareVerificationTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ManualControlLocksTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/MemoryPressureReaderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/PerAppControlRegistryRetargetTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/PerAppControlRegistryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/PerAppHardwareStatusTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/PlatformCeilingAuthorityTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ReadOnlyProbeAccessTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/RecordedDeviceWriteTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/RootFileAccessDiscoveryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/RootFileAccessNativeMergeTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ThermalCeilingRouterTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ThermalCurveTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/ThermalGuardTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/hardware/WriteVerificationTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/core/jni/ArchivePacketTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/jni/LogPacketTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/jni/ProbePacketTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/jni/PropBridgeTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/jni/ScanPacketTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/CoalescingCycleRunnerTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/ControlOutcomeModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/ControlRegistryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/CpuCeilingKnobsAtlasTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiCadenceTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiInsightsTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiInterruptSafetyTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiJournalCodecTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiMasterSwitchTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiThermalBudgetTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MaxAiThermalCurveTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MemoryStallTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/MinimalPlannerTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/ObjectiveTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/ResponseModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/maxai/ThermalCapDistributionTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/platform/ChipsetIdentityTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/platform/ChipsetPartCodeLineTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/platform/ForegroundAppResolverTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/platform/HudSessionTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/platform/ProcessFeedTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/recommendation/RecommendationTextClassifierTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/CopgTagTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/PerAppDeviceModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofApplyBackendTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofCapabilityMatrixTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofCopgContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofDeviceCatalogTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofEngineAdapterTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofEngineGateTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofEngineRegistryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofExistingPerAppTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofFileTransactionTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofFpsTargetsTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofIdentityModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofProfileTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/core/spoof/SpoofRecoveryModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/component/BottomSheetKeyboardTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/component/UserScaleRequestsTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/design/MaxCardSizeTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/design/MaxViewMenuContractTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/design/OutcomeFromCodeNotWordingTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/mainscreens/ActiveObjectiveTest.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/test/java/nd/max/ui/mainscreens/ApplistPresentationArchitectureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/ControlLayoutModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/HomeDeckModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/MaxAiPresentationTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/MaxAiTimelineFilterTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/MaxLivePresentationArchitectureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/ScreenFinderTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/ScreenUsageLedgerTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/StoryboardModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/mainscreens/UnifiedActivityModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/navigation/AtlasReadOnlyEntryTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/navigation/LaunchRouteTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/navigation/MergedDestinationCleanupTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/navigation/SettingsDestinationReachabilityTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/subscreens/DetailScreensLanguageContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/subscreens/DeviceInfoControlConvergenceTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/subscreens/DeviceInfoFactsTest.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/test/java/nd/max/ui/subscreens/DeviceInfoFormatTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/subscreens/DeviceInfoModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/subscreens/DeviceInfoShortcutEntryTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/subscreens/DeviceInfoShortcutOrdersTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/subscreens/FileManagerCompressModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/subscreens/FileManagerSelectionTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ApkDigestsTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/BackgroundGovernanceUtilTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/BootHistoryUtilTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ChargeLedgerTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ClockMeterModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ClockWaveTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/ConfigBackupInventoryTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/CoreClockMathTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/CrashLogUtilTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/EventLogResultTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileActionModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/FileArchiveEngineTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileBookmarkModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileClipboardModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileConflictModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileDeleteModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileHomeModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileOpenPlanTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FilePermissionModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FilePermissionOpsTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileSearchEngineTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileSearchFiltersTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileSearchPlanTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileStoreTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileSystemModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/FileTarCodecTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileTaskModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FileWindowModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/FpsMonitorParseTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/GpuCeilingChoiceTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/HardwareChoiceTest.kt` | MaxManager app | Proprietary (All rights reserved) | REPO_DEFAULT | ADD_COPYRIGHT_HEADER |
| `manager/app/src/test/java/nd/max/ui/util/HealthParsersTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/HomeActivityModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/InstallSourceUtilTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/LoadHistoryTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MainThreadStallDetectorTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupCountsTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupFavoritesTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupRetentionTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupSchedulePlanTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupStorageTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupSystemPermissionsTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/MaxBackupSystemTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/MaxSearchTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/MemoryLedgerTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ModuleHealthUtilTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/PermissionPolicyTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/PluginContractTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/ProfileSharingTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/RootMountTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ScreenOpenLatencyTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/SensorInventoryTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/SetEditUtilTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/SetEditValueKindTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/SpectrumModelTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/StorageScanModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/StorageScanNativeMappingTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/ThermalModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/ThermalZoneBatchTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/UltraCleanModelTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/util/VersionIdentityTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/util/ZramPlatformUtilTest.kt` | MaxManager contributors | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/app/src/test/java/nd/max/ui/viewmodel/AtlasPresentationTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/viewmodel/DashboardPulseLatencyTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/viewmodel/HomeTemperaturePolicyTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/viewmodel/LogsLineParserTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/viewmodel/MaxAiPresentationArchitectureTest.kt` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/app/src/test/java/nd/max/ui/viewmodel/ViewModelInstantiationTest.kt` | Zexshia | Apache-2.0 | APACHE_HEADER_RETAINED | REVIEW |
| `manager/build.gradle.kts` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/settings.gradle.kts` | MaxManager app | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/archive.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/contextual_engine.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/digital_twin.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/lib.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/logparse.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/power_predictor.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/probe.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/rl_agent.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/scan.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `manager/src/main/rust/src/sysprop.rs` | MaxManager (native engine) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/aidl/android/hardware/audio/effect/AcousticEchoCanceler.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/AutomaticGainControlV1.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/AutomaticGainControlV2.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/BassBoost.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Capability.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/CommandId.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/DefaultExtension.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Descriptor.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Downmix.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/DynamicsProcessing.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/EnvironmentalReverb.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Equalizer.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Flags.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/HapticGenerator.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/IEffect.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/IFactory.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/LoudnessEnhancer.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/NoiseSuppression.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Parameter.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/PresetReverb.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Processing.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Range.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/State.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/VendorExtension.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Virtualizer.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Visualizer.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/audio/effect/Volume.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/Ashmem.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/MappableFile.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/NativeHandle.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/fmq/GrantorDescriptor.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/fmq/MQDescriptor.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/fmq/SynchronizedReadWrite.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/hardware/common/fmq/UnsynchronizedWrite.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioAttributes.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioChannelLayout.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioConfig.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioConfigBase.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioContentType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioDevice.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioDeviceAddress.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioDeviceDescription.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioDeviceType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioDualMonoMode.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioEncapsulationMetadataType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioEncapsulationMode.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioEncapsulationType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioFlag.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioFormatDescription.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioFormatType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioGain.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioGainConfig.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioGainMode.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalAttributesGroup.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalCapCriterion.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalCapCriterionType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalEngineConfig.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalProductStrategy.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalVolumeCurve.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioHalVolumeGroup.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioInputFlags.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioIoFlags.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioLatencyMode.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioMMapPolicy.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioMMapPolicyInfo.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioMMapPolicyType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioMode.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioOffloadInfo.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioOutputFlags.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPlaybackRate.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPort.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPortConfig.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPortDeviceExt.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPortExt.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPortMixExt.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioPortMixExtUseCase.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioProductStrategyType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioProfile.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioSource.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioStandard.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioStreamType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioUsage.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/AudioUuid.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Boolean.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Byte.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Double.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/ExtraAudioDescriptor.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Float.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Int.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Long.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/MicrophoneDynamicInfo.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/MicrophoneInfo.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/PcmType.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/android/media/audio/common/Void.aidl` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/aidl/gen.sh` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/include/maxfx_effect_abi.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/jni/Android.mk` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/jni/Application.mk` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_aidl.cpp` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_dsp.c` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_dsp.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_effect.c` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_effect.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_props.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/src/maxfx_props_android.c` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/tests/dsp_test.c` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/tests/props_stub.c` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_auto_utils.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_enums.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_interface_utils.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_internal_logging.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_parcel_utils.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_parcelable_utils.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_stability.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libbinder_ndk_cpp/android/binder_to_string.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/base/fmq/MQDescriptorBase.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/compat/android-base/logging.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/android-base/unique_fd.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/cutils/ashmem.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/cutils/native_handle.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/logging_surface_test.cpp` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/native_handle_shim.cpp` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/utils/Errors.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/utils/Log.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/compat/utils/SystemClock.h` | MaxManager (repository default) | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `maxfx/third_party/libfmq/include/fmq/AidlMQDescriptorShim.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/AidlMQDescriptorShimBase.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/AidlMQDescriptorShimCpp.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/AidlMessageQueue.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/AidlMessageQueueBase.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/AidlMessageQueueCpp.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/ConvertMQDescriptors.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/EventFlag.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/MessageQueue.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/include/fmq/MessageQueueBase.h` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/src/EventFlag.cpp` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxfx/third_party/libfmq/src/FmqInternal.cpp` | Android Open Source Project | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `maxmanagerApplist.json` | MaxManager declared data asset | Proprietary (All rights reserved) | DATA_ASSET_DECLARED | KEEP |
| `preloadbin/jni/Android.mk` | MaxManager preloadbin | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `preloadbin/jni/Application.mk` | MaxManager preloadbin | Proprietary (All rights reserved) | NO_HEADER | KEEP |
| `preloadbin/jni/main.c` | VMTouch | BSD-3-Clause | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/android_ffi.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/constants.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/context.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/cooling.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/cpu.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/effectiveness.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/learning.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/lib.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/main.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/monitor.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/policy_manager.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/prediction.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/simulator.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/state.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/thermal_zones.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `thermalcore/src/utils.rs` | Rianixia-ThermalCore | Apache-2.0 | APACHE_DERIVED | REWRITE_FOR_IDENTITY |
| `tools/bundle_contract.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/code_health.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/dead_modules.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/design_doc.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/design_tokens.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/fetch_maxfx_aidl.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/gen_readme_assets.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/i18n_coverage.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/i18n_translate.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/jni_symbols.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/kt_balance.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/license_audit.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/log_gate.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/maxfx_contract.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/publish_docs_repo.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/read_image_text.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/readme_assets.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/repo_audit.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/resource_compile.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/rtl_guard.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/screenshot_gallery.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/sepolicy_matrix.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/source_manifest.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/svg_review.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/test_atlas_jvm.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/test_maxai_jvm.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
| `tools/upstream_similarity.py` | MaxManager tooling | Proprietary (All rights reserved) | PROSE_SCOPE | KEEP |
