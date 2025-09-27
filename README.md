<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>توثيق تفعيل اليوم الوطني – معرض صور/فيديو + طباعة + QR</title>
  <link href="https://fonts.googleapis.com/css2?family=Noto+Naskh+Arabic:wght@400;700&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
  <style>
    html{font-size:18px}
    body{font-family:'Noto Naskh Arabic', serif; background: linear-gradient(135deg,#1e3c72,#2a5298);}
    @page{size:A4;margin:14mm}
    @media print{
      .no-print{display:none !important}
      .card{break-inside:avoid;page-break-inside:avoid}
      .print-block{page-break-after:auto}
      body{background:white}
    }
    video{max-height:280px}
    .section-title{background:linear-gradient(to right,#a18cd1,#fbc2eb);color:white;padding:6px 12px;border-radius:8px;margin-bottom:8px;box-shadow:0 3px 6px rgba(0,0,0,0.2)}
    .signature-box{border:2px solid #a18cd1;padding:12px;border-radius:12px;background:#fff0f6;box-shadow:0 4px 10px rgba(0,0,0,0.1)}
    .toast{position:fixed;inset-inline-end:12px;inset-block-start:12px;background:#111827;color:#fff;padding:10px 14px;border-radius:10px;box-shadow:0 6px 16px rgba(0,0,0,.25);z-index:9999}
  </style>
</head>
<body class="text-gray-900">
  <header class="no-print bg-gradient-to-r from-purple-700 to-pink-500 text-white border-b sticky top-0 z-30 shadow-lg">
    <div class="max-w-6xl mx-auto px-4 py-3 flex flex-col gap-2 md:flex-row md:items-center md:justify-between">
      <h1 class="text-2xl font-bold">توثيق تفعيل اليوم الوطني</h1>
      <div class="flex flex-wrap items-center gap-2">
        <label class="inline-flex items-center gap-2 px-3 py-2 border rounded-lg bg-white text-gray-700 cursor-pointer">
          <input id="fileInput" class="hidden" type="file" accept="image/*,video/*" multiple>
          <span>إضافة وسائط</span>
        </label>
        <button onclick="openUrlAdder()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">إضافة عبر رابط</button>
        <button onclick="openPageQR()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">إنشاء QR لهذه الصفحة</button>
        <button onclick="window.print()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">طباعة كمستند</button>
        <button onclick="exportManifest()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">تصدير قائمة الوسائط</button>
        <button onclick="importManifest()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">استيراد قائمة</button>
        <button onclick="runDiagnostics()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">تشخيص</button>
        <button onclick="openPublishSettings()" class="px-3 py-2 border rounded-lg bg-white text-gray-700">إعدادات النشر</button>
      </div>
    </div>
  </header>

  <section class="max-w-6xl mx-auto px-4 mt-6 print-block">
    <div class="bg-white border-4 border-purple-400 rounded-2xl p-6 shadow-xl grid md:grid-cols-2 gap-6">
      <div>
        <div class="section-title">اسم المدرسة:</div>
        <div contenteditable="true" class="mt-1 p-2 border rounded">ابتدائية عون بن الحارث للطفولة المبكرة</div>
      </div>
      <div>
        <div class="section-title">البرنامج:</div>
        <div contenteditable="true" class="mt-1 p-2 border rounded">توثيق تفعيل اليوم الوطني</div>
      </div>
      <div>
        <div class="section-title">التاريخ الهجري / الميلادي:</div>
        <div contenteditable="true" class="mt-1 p-2 border rounded">الأربعاء 2 ربيع الآخر 1447هـ - الخميس 3 ربيع الآخر 1447هـ / الموافق .. - .. 2025م</div>
      </div>
      <div>
        <div class="section-title">الموقع/الوحدة/الفصل:</div>
        <div contenteditable="true" class="mt-1 p-2 border rounded">—</div>
      </div>
      <div class="md:col-span-2">
        <div class="section-title">وصف مختصر:</div>
        <div id="shortDesc" contenteditable="true" class="mt-1 p-2 border rounded bg-gradient-to-r from-purple-50 to-pink-100">تم تنفيذ فعاليات اليوم الوطني على مدى يومين متتاليين (الأربعاء والخميس)، وشملت عروضًا مرئية، أنشطة طلابية، وفقرات متنوعة عززت قيم المواطنة والانتماء الوطني.</div>
      </div>
    </div>
  </section>

  <main class="max-w-6xl mx-auto px-4 my-6">
    <div id="gallery" class="grid sm:grid-cols-2 lg:grid-cols-3 gap-4"></div>
  </main>

  <section class="max-w-6xl mx-auto px-4 my-6 print-block">
    <div class="signature-box grid md:grid-cols-2 gap-4">
      <div>إعداد رائدة النشاط: <span class="font-bold">ابتسام دغريري</span></div>
      <div>منسقة الإذاعة: <span class="font-bold">إلهام الثقفي</span></div>
      <div>وكيلة شؤون الطلاب: <span class="font-bold">آمال الأحمدي</span></div>
      <div>مديرة المدرسة: <span class="font-bold">أريج الغامدي</span></div>
    </div>
  </section>

  <!-- نافذة QR عام للصفحة -->
  <div id="qrModal" class="fixed inset-0 bg-black/50 items-center justify-center hidden">
    <div class="bg-white rounded-xl p-5 w-[90%] max-w-md">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-xl font-bold">رمز QR للرابط</h2>
        <button class="no-print text-gray-600" onclick="closeQR()">إغلاق</button>
      </div>
      <div id="qrBox" class="flex items-center justify-center p-4"></div>
      <div class="text-sm break-all text-gray-600" id="qrLink"></div>
    </div>
  </div>

  <!-- نافذة QR لوسيط محدد -->
  <div id="itemQRModal" class="fixed inset-0 bg-black/50 items-center justify-center hidden">
    <div class="bg-white rounded-xl p-5 w-[90%] max-w-md">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-xl font-bold">رمز QR للشاهد</h2>
        <button class="no-print text-gray-600" onclick="closeItemQR()">إغلاق</button>
      </div>
      <div id="itemQRBox" class="flex items-center justify-center p-4"></div>
      <div class="text-sm break-all text-gray-600" id="itemQRLink"></div>
    </div>
  </div>

  <!-- نافذة عرض وسيط -->
  <div id="viewer" class="fixed inset-0 bg-black/80 items-center justify-center hidden">
    <div class="bg-white rounded-xl w-[95%] h-[90%] p-3 flex flex-col">
      <div class="flex items-center justify-between pb-2 border-b">
        <div class="font-bold">معاينة</div>
        <div class="flex items-center gap-2 no-print">
          <button id="downloadBtn" class="px-3 py-1 border rounded">تنزيل</button>
          <button onclick="closeViewer()" class="px-3 py-1 border rounded">إغلاق</button>
        </div>
      </div>
      <div class="flex-1 overflow-auto flex items-center justify-center p-2">
        <img id="viewImg" class="max-h-full max-w-full hidden" alt="" />
        <video id="viewVid" class="max-h-full max-w-full hidden" controls></video>
      </div>
    </div>
  </div>

  <input id="manifestInput" type="file" accept="application/json" class="hidden" />

  <script>
    // عناصر DOM
    const fileInput = document.getElementById('fileInput');
    const gallery = document.getElementById('gallery');

    // إنشاء بطاقة للصور/الفيديو
    function createCard(obj){
      const isVideo = obj.type?.startsWith('video') || /\.(mp4|webm|ogg)(\?|$)/i.test(obj.url);
      const card = document.createElement('article');
      card.className = 'card bg-white border rounded-xl overflow-hidden shadow-sm';

      const mediaWrap = document.createElement('div');
      mediaWrap.className = 'relative bg-gray-100';

      if(isVideo){
        const vid = document.createElement('video');
        vid.src = obj.url; vid.className = 'w-full'; vid.controls = false;
        vid.dataset.name = obj.name || '';
        vid.addEventListener('click', ()=> openViewer(obj));
        mediaWrap.appendChild(vid);
      } else {
        const img = document.createElement('img');
        img.src = obj.url; img.alt = obj.caption || ''; img.className = 'w-full cursor-pointer';
        img.dataset.name = obj.name || '';
        img.addEventListener('click', ()=> openViewer(obj));
        mediaWrap.appendChild(img);
      }

      const body = document.createElement('div');
      body.className = 'p-3 space-y-2';

      const caption = document.createElement('div');
      caption.contentEditable = true;
      caption.className = 'border rounded p-2 min-h-[3rem]';
      caption.textContent = obj.caption || '';
      caption.addEventListener('input', ()=> obj.caption = caption.textContent);

      const meta = document.createElement('div');
      meta.className = 'grid grid-cols-2 gap-2 no-print';

      const qrBtn = document.createElement('button');
      qrBtn.className = 'px-2 py-1 border rounded';
      qrBtn.textContent = 'QR لهذا الشاهد';
      qrBtn.addEventListener('click', ()=> openItemQR(obj.url));

      const removeBtn = document.createElement('button');
      removeBtn.className = 'px-2 py-1 border rounded text-red-700';
      removeBtn.textContent = 'حذف';
      removeBtn.addEventListener('click', ()=> card.remove());

      meta.append(qrBtn, removeBtn);
      body.append(caption, meta);
      card.append(mediaWrap, body);
      gallery.prepend(card);
    }

    // إدراج ملفات محلية
    fileInput.addEventListener('change', (e)=>{
      const files = Array.from(e.target.files || []);
      files.forEach(f=>{
        const url = URL.createObjectURL(f);
        createCard({url, type: f.type, name: f.name});
      });
      fileInput.value = '';
    });

    // إدراج عبر روابط
    function openUrlAdder(){
      const txt = prompt('الصق رابط صورة أو فيديو (يمكن عدّة روابط كل سطر)');
      if(!txt) return;
      txt.split(/\n|\r/).map(s=>s.trim()).filter(Boolean).forEach(u=> createCard({url:u}));
    }

    // عارض الوسائط
    const viewer = document.getElementById('viewer');
    const viewImg = document.getElementById('viewImg');
    const viewVid = document.getElementById('viewVid');
    const downloadBtn = document.getElementById('downloadBtn');

    function openViewer(obj){
      viewImg.classList.add('hidden');
      viewVid.classList.add('hidden');
      downloadBtn.onclick = ()=> downloadMedia(obj.url);
      if(obj.type?.startsWith('video') || /\.(mp4|webm|ogg)(\?|$)/i.test(obj.url)){
        viewVid.src = obj.url; viewVid.classList.remove('hidden');
      } else {
        viewImg.src = obj.url; viewImg.classList.remove('hidden');
      }
      viewer.classList.remove('hidden');
      viewer.classList.add('flex');
    }
    function closeViewer(){
      viewer.classList.add('hidden');
      viewer.classList.remove('flex');
      viewVid.pause();
    }
    function downloadMedia(url){
      const a = document.createElement('a'); a.href = url; a.download = '';
      document.body.appendChild(a); a.click(); a.remove();
    }

    // QR للصفحة
    const qrModal = document.getElementById('qrModal');
    const qrBox = document.getElementById('qrBox');
    const qrLink = document.getElementById('qrLink');

    function openPageQR(){
      qrBox.innerHTML = '';
      const configured = localStorage.getItem('PUBLIC_URL');
      const link = configured || location.href;
      new QRCode(qrBox, {text: link, width: 220, height: 220});
      qrLink.textContent = link;
      qrModal.classList.remove('hidden');
      qrModal.classList.add('flex');
      if(!configured && location.protocol === 'file:'){
        toast('QR يشير لمسار محلي. حددي رابطًا عامًا من إعدادات النشر.');
      }
    }
    function closeQR(){
      qrModal.classList.add('hidden');
      qrModal.classList.remove('flex');
    }

    // QR لعنصر
    const itemQRModal = document.getElementById('itemQRModal');
    const itemQRBox = document.getElementById('itemQRBox');
    const itemQRLink = document.getElementById('itemQRLink');

    function openItemQR(url){
      itemQRBox.innerHTML = '';
      let link = url || '';
      const isLocal = /^(blob:|data:|file:)/i.test(link) || link.length>2000;
      if(isLocal){
        const base = localStorage.getItem('PUBLIC_URL');
        if(!base){ alert('الرابط محلي/طويل. حددي رابطًا عامًا من إعدادات النشر أولاً.'); return; }
        let fname='';
        try{ fname=new URL(link).pathname.split('/').pop(); }catch{ fname=String(link).split('/').pop(); }
        if(!fname || /^(blob:|data:|file:)/i.test(link)){
          fname = prompt('اسم الملف داخل assets/ (مثال: photo1.jpg)'); if(!fname) return;
        }
        fname = fname.split('?')[0].replace(/[^\w\-\.\u0600-\u06FF]+/g,'_');
        link = base.replace(/\/$/,'') + '/assets/' + fname;
      }
      new QRCode(itemQRBox, {text: link, width: 220, height: 220});
      itemQRLink.textContent = link;
      itemQRModal.classList.remove('hidden');
      itemQRModal.classList.add('flex');
    }
    function closeItemQR(){
      itemQRModal.classList.add('hidden');
      itemQRModal.classList.remove('flex');
    }

    // تصدير/استيراد قائمة الوسائط
    function exportManifest(){
      const cards = [...document.querySelectorAll('#gallery .card')];
      const items = cards.map(c=>{
        const media = c.querySelector('img,video');
        const caption = c.querySelector('[contenteditable]')?.textContent?.trim() || '';
        return { url: media?.src || '', caption, name: media?.dataset?.name || '' };
      });
      const blob = new Blob([JSON.stringify(items, null, 2)], {type:'application/json'});
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = 'national-day-manifest.json';
      a.click();
    }
    const manifestInput = document.getElementById('manifestInput');
    function importManifest(){ manifestInput.click(); }
    manifestInput.addEventListener('change', async (e)=>{
      const f = e.target.files?.[0]; if(!f) return;
      const text = await f.text();
      try{
        const list = JSON.parse(text);
        list.forEach(item=> createCard(item));
      }catch(err){ alert('ملف غير صالح'); }
      manifestInput.value = '';
    });

    // سحب وإفلات + تشخيص
    document.addEventListener('dragover', e=>{ e.preventDefault(); });
    document.addEventListener('drop', e=>{
      e.preventDefault();
      const files = Array.from(e.dataTransfer.files || []);
      files.forEach(f=> createCard({url:URL.createObjectURL(f), type:f.type, name:f.name}));
    });

    function toast(msg){
      const t = document.createElement('div'); t.className='toast'; t.textContent=msg; document.body.appendChild(t);
      setTimeout(()=> t.remove(), 3000);
    }
    function runDiagnostics(){
      const ok = name => typeof window[name]==='function';
      const tests = [
        ['openUrlAdder', ok('openUrlAdder')],
        ['openPageQR', ok('openPageQR')],
        ['exportManifest', ok('exportManifest')],
        ['importManifest', ok('importManifest')],
        ['createCard', ok('createCard')],
      ];
      const img1='data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mP8/5+hHgAHrALt1c2yNQAAAABJRU5ErkJggg==';
      createCard({url:img1, caption:'اختبار', type:'image/png', name:'test.png'});
      const pass = document.querySelectorAll('#gallery .card').length>0 && tests.every(t=>t[1]);
      console.log('Diagnostics', tests, 'gallery>0', pass);
      toast(pass?'OK':'فشل التشخيص، تحققي من Console');
    }
  </script>

  <!-- نافذة إعدادات النشر -->
  <div id="publishModal" class="fixed inset-0 bg-black/50 items-center justify-center hidden">
    <div class="bg-white rounded-xl p-5 w-[90%] max-w-lg">
      <div class="flex items-center justify-between mb-3">
        <h2 class="text-xl font-bold">إعدادات النشر العام</h2>
        <button class="no-print text-gray-600" onclick="closePublishSettings()">إغلاق</button>
      </div>
      <p class="text-sm text-gray-600 mb-3">أدخلي رابط الاستضافة العام (مثال: https://althaqafi.github.io/national-day/). سيُستخدم لتقصير روابط QR.</p>
      <label class="block text-sm mb-1">الرابط العام للموقع</label>
      <input id="publicUrlInput" type="url" class="w-full border rounded p-2 mb-3" placeholder="https://yourname.github.io/national-day/" value="https://althaqafi.github.io/national-day/">
      <div class="flex gap-2 justify-end">
        <button class="px-3 py-2 border rounded" onclick="savePublicUrl()">حفظ</button>
      </div>
    </div>
  </div>

  <script>
    // إعدادات النشر
    const publishModal = document.getElementById('publishModal');
    const publicUrlInput = document.getElementById('publicUrlInput');
    function openPublishSettings(){
      publicUrlInput.value = localStorage.getItem('PUBLIC_URL') || publicUrlInput.value || '';
      publishModal.classList.remove('hidden');
      publishModal.classList.add('flex');
    }
    function closePublishSettings(){
      publishModal.classList.add('hidden');
      publishModal.classList.remove('flex');
    }
    function savePublicUrl(){
      const val = publicUrlInput.value.trim();
      if(val && !/^https?:\/\//i.test(val)){ alert('أدخلي رابطًا يبدأ بـ https://'); return; }
      if(val){ localStorage.setItem('PUBLIC_URL', val); } else { localStorage.removeItem('PUBLIC_URL'); }
      closePublishSettings();
      toast('تم حفظ رابط النشر');
    }
  </script>
</body>
</html>
