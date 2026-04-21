# 🧠 مصنع الاختبارات الذكية - دليل الإعداد

## 📦 محتويات المشروع

```
kids-quiz-pwa/
├── index.html              # التطبيق الرئيسي (كل شيء في ملف واحد)
├── manifest.json           # إعدادات PWA
├── sw.js                   # Service Worker للعمل Offline
├── flowise-quiz-flow.json  # قالب Flowise جاهز للاستيراد
└── README.md               # هذا الملف
```

---

## 🚀 طريقة التشغيل السريع

### 1. تشغيل محلي
```bash
# تثبيت خادم بسيط
npx serve .

# أو بـ Python
python -m http.server 8080
```

ثم افتح: `http://localhost:8080`

### 2. نشر على الإنترنت (مجاني)
```bash
# Netlify Drop - اسحب المجلد إلى netlify.com/drop
# أو Vercel
npx vercel

# أو GitHub Pages
git init && git add . && git commit -m "init"
git push origin main
# فعّل GitHub Pages من الإعدادات
```

---

## 🔑 إعداد مفاتيح API

### OpenAI (DALL-E + GPT-4)
1. اذهب إلى: https://platform.openai.com/api-keys
2. أنشئ مفتاح جديد
3. في التطبيق: تبويب "إدارة المفاتيح" → إضافة مفتاح OpenAI

### ElevenLabs (Text-to-Speech)
1. اذهب إلى: https://elevenlabs.io/app/settings/api-keys
2. انسخ مفتاح API
3. في التطبيق: تبويب "إدارة المفاتيح" → إضافة مفتاح ElevenLabs
4. ابحث عن Voice ID عربي من: https://elevenlabs.io/voice-library

**أصوات عربية موصى بها:**
- `21m00Tcm4TlvDq8ikWAM` - Rachel (متعدد اللغات)
- ابحث في المكتبة عن "Arabic" لصوت أفضل

### Google Gemini (بديل لـ GPT-4)
1. اذهب إلى: https://aistudio.google.com/app/apikey
2. أنشئ مفتاح وأضفه للتطبيق

---

## 📊 هيكل ملف CSV لـ CapCut

```csv
رقم_السؤال,السؤال,الخيار_أ,الخيار_ب,الخيار_ج,الخيار_د,الإجابة_الصحيحة,نص_الإجابة,اسم_ملف_الصورة,اسم_ملف_الصوت,بروبت_الصورة,التعليق_الصوتي
1,"ما هو أكبر كوكب في المجموعة الشمسية؟","المريخ","زحل","المشتري","الأرض","c","المشتري","q1_image.png","q1_audio.mp3","Pixar 3D giant planet Jupiter...","هل تعرف أكبر كواكب مجموعتنا؟"
```

### استيراد في CapCut:
1. افتح CapCut Desktop
2. New Project → اختر Template للمسابقة
3. من القائمة العلوية: **Batch Edit**
4. **Import CSV** → ارفع الملف
5. استبدل الصور بملفات `q1_image.png, q2_image.png...`
6. استبدل الصوت بملفات `q1_audio.mp3, q2_audio.mp3...`
7. **Batch Generate** → ينتج الفيديوهات تلقائياً! 🎬

---

## ⚡ إعداد Flowise (Backend Low-Code)

```bash
# تثبيت Flowise
npm install -g flowise
flowise start

# أو بـ Docker
docker run -d -p 3000:3000 flowiseai/flowise
```

1. افتح: `http://localhost:3000`
2. Chatflows → **Import Chatflow**
3. ارفع: `flowise-quiz-flow.json`
4. أدخل مفاتيح OpenAI و ElevenLabs في الـ nodes
5. انسخ **Prediction URL**
6. في التطبيق: تبويب Flowise Guide → أدخل الـ URL

---

## 🔄 منطق تبديل المفاتيح التلقائي

```javascript
// الخوارزمية المستخدمة في التطبيق:
// 1. ابدأ بأول مفتاح بحالة "active"
// 2. إذا جاء خطأ 429 → علّم المفتاح كـ "limit"
// 3. انتقل للمفتاح التالي بحالة "active"
// 4. أعد المحاولة تلقائياً
// 5. إذا انتهت كل المفاتيح → أبلغ المستخدم

// أضف 3+ مفاتيح لكل خدمة لضمان الاستمرارية
```

---

## 📱 ميزات PWA

| الميزة | الوصف |
|--------|-------|
| ✅ Offline-First | عرض المشاريع السابقة بدون إنترنت |
| ✅ IndexedDB | تخزين محلي لجميع المشاريع |
| ✅ Service Worker | Cache ذكي للأصول |
| ✅ Install Banner | تثبيت كتطبيق على الجهاز |
| ✅ RTL Support | واجهة عربية كاملة |
| ✅ Push Notifications | إشعار عند اكتمال التوليد |

---

## 🎨 أمثلة على بروبتات الصور

للحيوانات:
```
Pixar 3D animation style, cute happy lion with big expressive eyes, 
jungle background, bright vivid colors, soft lighting, child-friendly, 
white background, high quality render, 4k
```

للفضاء:
```
Pixar 3D animation style, cute cartoon planet Jupiter with funny face, 
stars and space background, glowing colors, adorable, child-friendly,
high quality 3D render
```

---

## 🛠️ التخصيص

### تغيير نموذج GPT
في الكود: ابحث عن `claude-sonnet-4-20250514` وغيّر حسب الحاجة

### تغيير ستايل الصور
في `imageStyle` select، يمكن إضافة خيارات جديدة مثل:
- `anime` - أنمي ياباني
- `realistic` - واقعي
- `storybook` - كتاب قصص

### إضافة لغات جديدة
في `dialect` select، أضف اللهجة واضبط الـ System Prompt

---

## 📞 الدعم والمساهمة

هذا التطبيق مفتوح المصدر، يمكنك تطويره وإضافة:
- [ ] دعم Stable Diffusion محلي
- [ ] تصدير مباشر للـ Google Drive
- [ ] قوالب مسابقات جاهزة
- [ ] مزامنة سحابية للمشاريع

---
بُني بـ ❤️ لدعم منشئي محتوى الأطفال العرب
