
# أسم المشروع Open WebUI 🌐

## 📖 وصف المشروع
مشروع **Open WebUI** عبارة عن منصة ذكاء اصطناعي مفتوحة المصدر، قابلة للتخصيص ومصممة لتعمل بالكامل دون الحاجة للاتصال بالإنترنت (Offline). المنصة تتيح لك تشغيل نماذج لغوية متعددة (LLMs) باستخدام Ollama أو واجهات برمجة التطبيقات المتوافقة مع OpenAI. 

تتميز المنصة بدعم مدمج لتقنية RAG (للتفاعل مع المستندات والملفات)، وتوليد وتحرير الصور، والمكالمات الصوتية والمرئية، والبحث في الويب، بالإضافة إلى نظام صلاحيات قوي يتيح التحكم بالوصول للمستخدمين (RBAC)، وتدعم العمل بسلاسة على أجهزة الكمبيوتر والهواتف الذكية.

---

## 🚀 طرق التثبيت والتشغيل

### 🐍 أولاً: التثبيت باستخدام بايثون (Python pip)
تُعد هذه الطريقة مثالية للمطورين، ولكن يُشترط أن يكون لديك إصدار **Python 3.11** لتجنب أي مشاكل في التوافق.

**1. تثبيت المنصة:**
افتح موجه الأوامر (Terminal) ونفذ الأمر التالي:
```bash
pip install open-webui
```

**2. تشغيل الخادم:**
بعد اكتمال التثبيت، يمكنك بدء تشغيل المنصة عبر الأمر:
```bash
open-webui serve
```
> **ملاحظة:** يمكنك الوصول إلى الواجهة بعد التشغيل عبر الرابط: [http://localhost:8080](http://localhost:8080)

---

### 🐳 ثانياً: التثبيت السريع باستخدام دوكر (Docker)
تُعد هذه الطريقة الأكثر استقراراً وأماناً لبيئات الإنتاج. اختر الأمر الذي يتناسب مع إعدادات جهازك:

**1. الإعداد الافتراضي (Ollama مثبت على نفس الجهاز)**
إذا كان محرك Ollama يعمل محلياً على جهازك، استخدم هذا الأمر لربط الحاوية به:
```bash
docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

**2. الاتصال بخادم Ollama خارجي**
إذا كان Ollama مثبتاً على خادم أو جهاز آخر، قم بتعديل الرابط في الأمر التالي للاتصال به:
```bash
docker run -d -p 3000:8080 -e OLLAMA_BASE_URL=[https://example.com](https://example.com) -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

**3. التثبيت بدعم تسريع الرسومات (Nvidia GPU)**
للحصول على أداء فائق باستخدام كرت الشاشة (يتطلب تثبيت `Nvidia CUDA toolkit` مسبقاً):
```bash
docker run -d -p 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda
```

**4. الاستخدام مع واجهة برمجة تطبيقات OpenAI فقط**
إذا كنت ترغب باستخدام نماذج OpenAI فقط (بدون Ollama)، استبدل `your_secret_key` بمفتاحك السري:
```bash
docker run -d -p 3000:8080 -e OPENAI_API_KEY=your_secret_key -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

---

### 📦 ثالثاً: التثبيت بالحزمة المدمجة (Open WebUI + Ollama)
توفر هذه الطريقة حاوية واحدة تضم المنصة ومحرك Ollama معاً لتبسيط عملية الإعداد.

**1. مع دعم كرت الشاشة (GPU):**
```bash
docker run -d -p 3000:8080 --gpus=all -v ollama:/root/.ollama -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama
```

**2. للعمل على المعالج العادي (CPU) فقط:**
```bash
docker run -d -p 3000:8080 -v ollama:/root/.ollama -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:ollama
```

> **ملاحظة:** عند استخدام أي من أوامر Docker أعلاه، ستتمكن من الوصول إلى واجهة المنصة عبر الرابط: [http://localhost:3000](http://localhost:3000)
