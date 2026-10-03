# خدمة التفسير — API ثابت

خدمة استعلام فورية لـ**41 طبعة تفسير عربية**. أرسل طلب HTTP واحد واستقبل كل ما تحتاج — بلا تحميل ولا مفاتيح ولا حدود عملية.

## الاستعلام الرئيسي: تفسير آية من كل الطبعات في رد واحد

```
GET https://medmrf-10.github.io/tfsr/api/ayah/<سورة>/<آية>.json.gz
```

مثال — آية الكرسي من الـ41 تفسيراً دفعة واحدة:

```bash
curl -s https://medmrf-10.github.io/tfsr/api/ayah/2/255.json.gz | gunzip
```

الرد:

```json
{"s":2,"a":255,"tafsir":{
  "ar-tafsir-ibn-kathir":   {"g":"2:255","f":"2:255","t":"2:255","x":"<نص التفسير كاملاً>"},
  "ar-tafsir-al-tabari":    {...},
  "tafsir-al-razi":         {...},
  "... (41 طبعة)":           {}
}}
```

الحقول داخل كل طبعة: `g` مفتاح المقطع المجمَّع · `f`/`t` من آية إلى آية · `x` نص التفسير (HTML).

## الطبعات الـ41

قائمة كاملة بالطبعات وأرقامها: `GET /api/index.json` — وميتاداتا كل طبعة: `GET /api/editions/<slug>.json.gz`

الطبعة تُعنون بـ`slug` مثل: `ar-tafsir-ibn-kathir`, `ar-tafsir-al-tabari`, `tafsir-al-razi`, `ar-tafseer-al-qurtubi`, `al-alusi`, `al-bahr-al-muhit`, `tafsir-jalalayn`, `adwa-al-bayan` (الشنقيطي), `tafsir-fe-zalul-quran-syed-qatab`, `al-basit`, `al-kashshaf`…

## قاعدة البيانات الكاملة

`releases/` — `tafsir.db.gz` (SQLite، 610MB): نفس البيانات بفهارس بحث كامل النص (FTS5 مُجرّدة الحركات/الألف/الياء) + مرافق `query.py` بدوال جاهزة.

## ملاحظة الضغط

كل الملفات `.json.gz` — فك الضغط: `curl -s <url> | gunzip` أو بايثون `gzip.open`.
