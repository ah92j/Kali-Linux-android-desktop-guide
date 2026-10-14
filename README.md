<h1 dir="rtl" align="right">تشغيل Kali Linux على أندرويد من الصفر</h1>

<p dir="rtl" align="right"><strong>Termux + Kali NetHunter Rootless + TigerVNC + VNC Viewer + Fluxbox + tint2 + iDesk + code-server</strong></p>

<p dir="rtl" align="right">هذا الدليل يشرح التثبيت خطوة بخطوة على هاتف أندرويد من دون روت، ثم إعداد سطح مكتب خفيف وفتح محرر شبيه بـ VS Code من المتصفح.</p>

<p dir="rtl" align="right"><strong>طريقة استخدام الدليل:</strong> اقرأ الشرح العربي أولًا. كل أمر موجود في صندوق مستقل ومحاذى من اليسار إلى اليمين. انسخ الأمر الموجود داخل الصندوق فقط، والصقه في التطبيق المحدد في الشرح. نفّذ الأوامر واحدًا تلو الآخر وانتظر انتهاء كل أمر قبل الانتقال إلى التالي. لا تلصق عنوان الصندوق أو نص الشرح داخل الطرفية.</p>

<p dir="rtl" align="right"><a href="README.en.md" dir="ltr">Read the English guide</a> · <a href="index.html" dir="ltr">صفحة الدليل</a></p>

<p dir="rtl" align="right"><strong>تنبيه:</strong> تختلف الحزم والتفاصيل قليلًا حسب إصدارات أندرويد وTermux وKali. لا يمكن ضمان عدم ظهور أي خطأ على كل جهاز. إذا ظهر خطأ، توقّف وانسخ نصه كما هو قبل تجربة أوامر أخرى.</p>

<h2 dir="rtl" align="right">النتيجة التي سنصل إليها</h2>

<ul dir="rtl" align="right">
<li>تشغيل Kali Linux داخل Termux من دون روت.</li>
<li>فتح سطح مكتب رسومي باستخدام TigerVNC وتطبيق VNC Viewer.</li>
<li>واجهة Fluxbox مع شريط tint2 واختصارات سطح المكتب عبر iDesk.</li>
<li>إنشاء مجلد عمل باسم <code dir="ltr">~/Desktop/Python</code>.</li>
<li>تشغيل code-server، وهو محرر شبيه بـ VS Code داخل متصفح الهاتف.</li>
</ul>

<h2 dir="rtl" align="right">قبل البدء</h2>

<ul dir="rtl" align="right">
<li>هاتف أندرويد ومساحة فارغة بعدة غيغابايت؛ يختلف الحجم النهائي حسب الإصدار والحزم.</li>
<li>اتصال إنترنت جيد، ويُفضّل إبقاء الهاتف على الشاحن أثناء تثبيت النظام.</li>
<li>ثبّت Termux من مصدر رسمي واحد فقط. لا تخلط النسخ والإضافات التي تأتي من مصادر ذات مفاتيح توقيع مختلفة.</li>
<li>هذا إعداد Rootless ولا يحتاج إلى روت، لكنه لا يوفر كل إمكانات Kali المثبت على جهاز حقيقي أو جهاز مروّت.</li>
<li>سنربط خادم VNC ومحرر code-server بعنوان الهاتف المحلي <code dir="ltr">127.0.0.1</code>، فلا تغيّر العنوان إلى <code dir="ltr">0.0.0.0</code>.</li>
</ul>

<h2 dir="rtl" align="right">الخطوة 1: تثبيت التطبيقات</h2>

<p dir="rtl" align="right">ثبّت Termux من أحد المصدرين التاليين، واختر مصدرًا واحدًا فقط:</p>

<ul dir="rtl" align="right">
<li><a href="https://f-droid.org/en/packages/com.termux/">Termux على F-Droid</a></li>
<li><a href="https://github.com/termux/termux-app/releases">إصدارات Termux الرسمية</a></li>
</ul>

<p dir="rtl" align="right">ثبّت أيضًا تطبيق VNC Viewer من متجر موثوق. سنستخدم TigerVNC داخل Kali مع VNC Viewer. لا تشغّل KeX بالتزامن مع إعداد TigerVNC اليدوي في هذا الدليل.</p>

<p dir="rtl" align="right"><strong>إذا كان Termux مثبتًا ويعمل لديك بالفعل، فلا تحذفه.</strong> حذفه قد يؤدي إلى حذف ملفات البيئة المحلية.</p>

<h2 dir="rtl" align="right">الخطوة 2: تجهيز Termux</h2>

<p dir="rtl" align="right">افتح تطبيق Termux الأصلي على أندرويد، وليس Terminal داخل Kali. نفّذ الأمر التالي لتحديث الحزم:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل تطبيق Termux الأصلي.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>pkg update &amp;&amp; pkg upgrade -y</code></pre>

<p dir="rtl" align="right">اسمح بالوصول إلى مجلدات الهاتف عند ظهور نافذة الإذن:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Termux. اضغط Allow / سماح إذا طلب أندرويد الإذن.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>termux-setup-storage</code></pre>

<p dir="rtl" align="right">ثبّت أداة تنزيل الملفات:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Termux.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>pkg install -y wget</code></pre>

<h2 dir="rtl" align="right">الخطوة 3: تثبيت Kali NetHunter Rootless</h2>

<p dir="rtl" align="right">نفّذ هذه الأوامر الثلاثة داخل Termux الأصلي، بالترتيب. انسخ كل صندوق على حدة وانتظر انتهاء الأمر قبل الانتقال إلى التالي.</p>

<p dir="rtl" align="right"><strong>الأمر الأول — تنزيل أداة التثبيت.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>wget -O install-nethunter-termux https://offs.ec/2MceZWr</code></pre>

<p dir="rtl" align="right"><strong>الأمر الثاني — السماح بتشغيل أداة التثبيت.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>chmod +x install-nethunter-termux</code></pre>

<p dir="rtl" align="right"><strong>الأمر الثالث — بدء التثبيت. اتبع الأسئلة التي تظهر على الشاشة وانتظر اكتمال التنزيل وفك الضغط.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>./install-nethunter-termux</code></pre>

<p dir="rtl" align="right">لا تغلق Termux بالقوة أثناء التثبيت. قد تستغرق العملية وقتًا، بحسب سرعة الاتصال والمساحة المتاحة.</p>

<p dir="rtl" align="right">بعد اكتمال التثبيت، ابدأ Kali بهذا الأمر:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Termux. بعد التنفيذ يجب أن تصبح داخل طرفية Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>nethunter</code></pre>

<h2 dir="rtl" align="right">الخطوة 4: تحديث Kali وتثبيت الحزم</h2>

<p dir="rtl" align="right">تأكد أنك داخل Kali. نفّذ تحديث النظام وانتظر اكتماله:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali بعد تنفيذ nethunter.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt update &amp;&amp; sudo apt full-upgrade -y</code></pre>

<p dir="rtl" align="right">ثبّت حزم سطح المكتب وخادم VNC والأدوات المطلوبة:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. يحتاج التنزيل إلى بعض الوقت.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt install -y fluxbox tint2 idesk xterm dbus-x11 tigervnc-standalone-server thunar feh adwaita-icon-theme x11-xserver-utils fonts-noto-core python3 python3-pip git curl wget ca-certificates xdg-utils</code></pre>

<p dir="rtl" align="right">إذا أظهر مدير الحزم خطأ بشأن اسم حزمة، لا تجرّب أسماء عشوائية ولا تتخطَّ الخطأ بصمت؛ أرسل نص الخطأ كاملًا للتحقق من اسم الحزمة المتوفر في إصدارك.</p>

<h2 dir="rtl" align="right">الخطوة 5: إنشاء مجلدات العمل وإعداد سطح المكتب</h2>

<p dir="rtl" align="right">أنشئ مجلدات الإعدادات ومجلد العمل باسم Python:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>mkdir -p ~/.config/tigervnc ~/.idesktop ~/.config/tint2 ~/.fluxbox ~/.local/bin ~/Desktop/Python</code></pre>

<p dir="rtl" align="right">أنشئ ملف بدء جلسة سطح المكتب. هذا الأمر يكتب ملف الإعداد كاملًا؛ انسخ الصندوق كله دفعة واحدة:</p>

<p dir="rtl" align="right"><strong>ملف تشغيل سطح المكتب — داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>cat &gt; ~/.config/tigervnc/xstartup &lt;&lt;&#x27;EOF&#x27;
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
xsetroot -solid &quot;#4b2e69&quot; 2&gt;/dev/null
exec dbus-launch --exit-with-session sh -c &#x27;tint2 &amp; idesk &amp; exec fluxbox&#x27;
EOF</code></pre>

<p dir="rtl" align="right">اسمح بتشغيل ملف الإعداد:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>chmod +x ~/.config/tigervnc/xstartup</code></pre>

<p dir="rtl" align="right">تستخدم هذه الإعدادات خلفية بنفسجية وFluxbox وtint2 وiDesk. إذا كان سطح المكتب لديك يعمل بالفعل بإعدادات مختلفة، احتفظ بنسخة منها قبل استبدالها.</p>

<h2 dir="rtl" align="right">الخطوة 6: إنشاء كلمة مرور VNC وتشغيل الخادم</h2>

<p dir="rtl" align="right">أنشئ كلمة مرور خاصة باتصال VNC. سيطلب منك الطرفية إدخال كلمة المرور وتأكيدها. لا ترسلها لأي شخص ولا تضعها في ملفات المشروع:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. إذا قال إن الأمر غير موجود، جرّب الأمر البديل التالي.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncpasswd ~/.config/tigervnc/passwd</code></pre>

<p dir="rtl" align="right"><strong>بديل عند عدم توفر tigervncpasswd.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>vncpasswd ~/.config/tigervnc/passwd</code></pre>

<p dir="rtl" align="right">شغّل خادم VNC على الشاشة رقم 1، واجعل الاتصال محليًا على الهاتف:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. إذا ظهرت رسالة بأن الجلسة تعمل بالفعل، لا تكرر التشغيل مباشرةً.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver :1 -localhost yes -geometry 1280x800 -depth 24</code></pre>

<p dir="rtl" align="right">إذا كانت جلسة قديمة عالقة أو تريد إعادة تشغيلها، أوقف العرض رقم 1 ثم شغّله من جديد:</p>

<p dir="rtl" align="right"><strong>إيقاف جلسة VNC القديمة — داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver -kill :1</code></pre>

<p dir="rtl" align="right"><strong>إعادة تشغيل جلسة VNC — داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver :1 -localhost yes -geometry 1280x800 -depth 24</code></pre>

<p dir="rtl" align="right">لا تستخدم طريقة KeX بالتوازي مع خادم TigerVNC اليدوي؛ اختر مسارًا واحدًا لتجنب تعارض الجلسات.</p>

<h2 dir="rtl" align="right">الخطوة 7: الاتصال من VNC Viewer</h2>

<ol dir="rtl" align="right">
<li>افتح تطبيق VNC Viewer على الهاتف.</li>
<li>أضف اتصالًا جديدًا.</li>
<li>في خانة العنوان اكتب <code dir="ltr">127.0.0.1:5901</code>.</li>
<li>اتصل وأدخل كلمة مرور VNC التي أنشأتها في الخطوة السابقة.</li>
</ol>

<p dir="rtl" align="right">إذا كان الاتصال ناجحًا، سترى سطح مكتب Fluxbox. اترك Termux يعمل في الخلفية أثناء استخدام VNC. إذا أغلق أندرويد Termux تلقائيًا، راجع إعدادات البطارية واسمح للتطبيق بالعمل في الخلفية إن كان الخيار متاحًا.</p>

<h2 dir="rtl" align="right">الخطوة 8: فهم الواجهة وإنشاء مجلد Python</h2>

<ul dir="rtl" align="right">
<li><strong>Fluxbox:</strong> مدير النوافذ والقوائم.</li>
<li><strong>tint2:</strong> شريط المهام.</li>
<li><strong>iDesk:</strong> يعرض الاختصارات التي نحددها كأيقونات على سطح المكتب.</li>
</ul>

<p dir="rtl" align="right">أنشأنا مجلد العمل مسبقًا. تأكد من وجوده:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. يجب أن يظهر مسار Desktop ومسار Python.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -ld ~/Desktop ~/Desktop/Python</code></pre>

<p dir="rtl" align="right">ملاحظة: iDesk لا يعرض المجلدات تلقائيًا مثل بعض بيئات سطح المكتب؛ إذا لم يظهر مجلد Python كأيقونة، فهذا لا يعني أن المجلد غير موجود. سننشئ اختصارًا للمحرر في خطوة منفصلة.</p>

<h2 dir="rtl" align="right">الخطوة 9: تثبيت code-server</h2>

<p dir="rtl" align="right">في هذه البيئة، تعطل VS Code المكتبي بسبب قيود PRoot على الوصول لبعض ملفات النظام. لذلك نستخدم code-server، وهو محرر شبيه بـ VS Code يعمل داخل متصفح الهاتف.</p>

<p dir="rtl" align="right">نزّل سكربت التثبيت الرسمي إلى ملف أولًا:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>curl -fsSL https://code-server.dev/install.sh -o /tmp/code-server-install.sh</code></pre>

<p dir="rtl" align="right">ثم شغّل سكربت التثبيت:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. قد يطلب كلمة مرور sudo لتثبيت الحزمة.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sh /tmp/code-server-install.sh</code></pre>

<p dir="rtl" align="right">تحقق من تثبيت البرنامج:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. يجب أن يظهر رقم الإصدار.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>code-server --version</code></pre>

<h2 dir="rtl" align="right">الخطوة 10: تشغيل المحرر وفتح مجلد Python</h2>

<p dir="rtl" align="right">انسخ الأمر التالي كاملًا داخل Kali. ينشئ مجلد العمل إذا لم يكن موجودًا، ثم يشغّل المحرر في الخلفية على الهاتف فقط:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. انسخ الأسطر الثلاثة كلها في عملية لصق واحدة.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>mkdir -p &quot;$HOME/Desktop/Python&quot;
nohup code-server --bind-addr 127.0.0.1:8080 &quot;$HOME/Desktop/Python&quot; &gt; &quot;$HOME/code-server.log&quot; 2&gt;&amp;1 &amp;
sleep 3</code></pre>

<p dir="rtl" align="right">اعرض كلمة المرور محليًا على شاشة الهاتف:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. لا تشارك كلمة المرور ولا تحفظها داخل المستودع العام.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>grep &#x27;^password:&#x27; &quot;$HOME/.config/code-server/config.yaml&quot;</code></pre>

<p dir="rtl" align="right">افتح متصفح الهاتف واكتب هذا العنوان في شريط العنوان:</p>

<p dir="rtl" align="right"><strong>العنوان داخل متصفح الهاتف، وليس داخل Terminal.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>http://127.0.0.1:8080</code></pre>

<p dir="rtl" align="right">أدخل كلمة المرور التي ظهرت في الطرفية. ستفتح واجهة شبيهة بـ VS Code، ومجلد العمل Python جاهز في المستكشف. أنشئ ملفًا جديدًا من Explorer إذا أردت كتابة برنامج.</p>

<p dir="rtl" align="right">إذا لم يفتح المحرر، اعرض آخر رسائل سجل التشغيل:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. أرسل نص الخطأ إن احتجت مساعدة.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tail -n 40 &quot;$HOME/code-server.log&quot;</code></pre>

<p dir="rtl" align="right">يبقى الخادم مربوطًا بـ <code dir="ltr">127.0.0.1</code> لأسباب أمنية. لا تغيّره إلى <code dir="ltr">0.0.0.0</code> إلا بعد فهم مخاطر كشف المحرر للأجهزة الأخرى.</p>

<h2 dir="rtl" align="right">الخطوة 11: إضافة أيقونة Python إلى سطح المكتب</h2>

<p dir="rtl" align="right">ينشئ الأمر التالي اختصارًا يفتح محرر code-server في المتصفح. يجب أن يكون code-server قد ثُبّت، لكن لا يلزم أن يكون مشغّلًا لحظة إنشاء الأيقونة.</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. انسخ الصندوق كاملًا كما هو.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>mkdir -p ~/.idesktop
ICON=&quot;$(find /usr/share/icons /usr/share/pixmaps -type f -iname &#x27;folder.png&#x27; -print -quit 2&gt;/dev/null)&quot;
if [ -z &quot;$ICON&quot; ]; then
  ICON=&quot;$(grep -hm1 &#x27;Icon:&#x27; ~/.idesktop/*.lnk 2&gt;/dev/null | sed &#x27;s/^[[:space:]]*Icon:[[:space:]]*//&#x27; | head -n 1)&quot;
fi
if [ -z &quot;$ICON&quot; ]; then
  echo &quot;No PNG icon found. Keep using code-server from the browser.&quot;
else
  cat &gt; ~/.idesktop/Python.lnk &lt;&lt;EOF
table Icon
  Caption: Python
  Command: xdg-open http://127.0.0.1:8080
  Icon: $ICON
  Width: 48
  Height: 48
  X: 180
  Y: 320
end
EOF
  echo &quot;Python shortcut created.&quot;
fi</code></pre>

<p dir="rtl" align="right">أعد تشغيل iDesk ليقرأ الاختصار:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. قد يختفي سطح المكتب لثوانٍ ثم تعود الأيقونات.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>pkill -x idesk 2&gt;/dev/null || true
nohup idesk &gt;/tmp/idesk.log 2&gt;&amp;1 &amp;</code></pre>

<p dir="rtl" align="right">عند ظهور أيقونة Python، انقر عليها مرتين. ستفتح عنوان المحرر في المتصفح. إذا لم يظهر الرمز، تحقق أولًا أن ملف الاختصار موجود:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -l ~/.idesktop/Python.lnk</code></pre>

<h2 dir="rtl" align="right">الخطوة 12: إخفاء شريط البحث في أعلى المحرر</h2>

<p dir="rtl" align="right">إذا كان الشريط الذي يغطي الجزء العلوي هو Command Center، افتح قائمة الأوامر داخل المحرر، وابحث عن <code dir="ltr">Preferences: Open User Settings (JSON)</code>. أضف الإعداد التالي داخل كائن JSON، ولا تحذف الإعدادات الأخرى الموجودة بالفعل:</p>

<p dir="rtl" align="right"><strong>إعداد JSON — أضف فاصلة بعده أو قبله حسب موقعه والإعدادات المحيطة.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>&quot;window.commandCenter&quot;: false</code></pre>

<p dir="rtl" align="right">إذا كنت تستخدم إعدادات فيها مفاتيح أخرى، تأكد من وضع فاصلة بين السطور؛ ملف JSON غير الصحيح قد يمنع قراءة الإعدادات.</p>

<h2 dir="rtl" align="right">اختياري: تجربة VS Code المكتبي</h2>

<p dir="rtl" align="right">هذه خطوة اختيارية وليست ضرورية؛ المسار الموصى به لهذا الهاتف هو code-server. في التجربة الموثقة هنا، ثُبّت VS Code المكتبي لكن تعطل أثناء التشغيل بسبب قيود PRoot على بعض ملفات النظام. إذا أردت تجربة تثبيته، نفّذ الأوامر التالية داخل Kali:</p>

<p dir="rtl" align="right"><strong>الأمر الأول — تثبيت أدوات إضافة المستودع.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt install -y wget gpg</code></pre>

<p dir="rtl" align="right"><strong>الأمر الثاني — إضافة مفتاح مستودع Microsoft الرسمي.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo gpg --dearmor -o /usr/share/keyrings/microsoft.gpg</code></pre>

<p dir="rtl" align="right"><strong>الأمر الثالث — إعداد المستودع الرسمي.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>printf &#x27;Types: deb\nURIs: https://packages.microsoft.com/repos/code\nSuites: stable\nComponents: main\nArchitectures: amd64,arm64,armhf\nSigned-By: /usr/share/keyrings/microsoft.gpg\n&#x27; | sudo tee /etc/apt/sources.list.d/vscode.sources &gt;/dev/null</code></pre>

<p dir="rtl" align="right"><strong>الأمر الرابع — تحديث قائمة الحزم وتثبيت VS Code.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>sudo apt update &amp;&amp; sudo apt install -y code</code></pre>

<p dir="rtl" align="right">إذا ظهرت أخطاء مثل <code dir="ltr">Failed to initialize cpuinfo</code> أو <code dir="ltr">Failed to read /proc/sys/fs/inotify/max_user_watches</code> أو <code dir="ltr">trace trap</code>، استخدم code-server بدل محاولة تعطيل العزل الأمني لـ Electron. لا ننصح بتشغيل VS Code مع تعطيل العزل كإعداد دائم.</p>

<h2 dir="rtl" align="right">تشغيل النظام يوميًا</h2>

<ol dir="rtl" align="right">
<li>افتح Termux الأصلي.</li>
<li>ابدأ Kali بالأمر التالي، إذا لم تكن داخل Kali بالفعل:</li>
</ol>

<p dir="rtl" align="right"><strong>أين؟ داخل Termux.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>nethunter</code></pre>

<p dir="rtl" align="right">إذا كان خادم VNC متوقفًا، شغّله داخل Kali:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali. لا تعِد تشغيله إذا كانت الجلسة تعمل بالفعل.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver :1 -localhost yes -geometry 1280x800 -depth 24</code></pre>

<p dir="rtl" align="right">افتح VNC Viewer واتصل بـ <code dir="ltr">127.0.0.1:5901</code>. إذا كان code-server متوقفًا، شغّله داخل Kali:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>nohup code-server --bind-addr 127.0.0.1:8080 &quot;$HOME/Desktop/Python&quot; &gt; &quot;$HOME/code-server.log&quot; 2&gt;&amp;1 &amp;</code></pre>

<p dir="rtl" align="right">بعدها افتح المتصفح على <code dir="ltr">http://127.0.0.1:8080</code>. لإيقاف جلسة VNC عند الانتهاء، نفّذ داخل Kali:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>tigervncserver -kill :1</code></pre>

<h2 dir="rtl" align="right">حل المشكلات الشائعة</h2>

<h3 dir="rtl" align="right">VNC Viewer لا يتصل</h3>

<p dir="rtl" align="right">تأكد أن الخادم يعمل وأن العنوان هو <code dir="ltr">127.0.0.1:5901</code>. إذا ظهرت رسالة أن الجلسة موجودة بالفعل، لا تنشئ عدة جلسات؛ استخدم أمر الإيقاف ثم شغّلها مجددًا عند الحاجة.</p>

<h3 dir="rtl" align="right">سطح المكتب فارغ أو لا تظهر الأيقونات</h3>

<p dir="rtl" align="right">افحص ملف بدء الجلسة وتأكّد من صلاحية تشغيله:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -l ~/.config/tigervnc/xstartup
cat ~/.config/tigervnc/xstartup</code></pre>

<p dir="rtl" align="right">قد لا يعرض iDesk المجلدات تلقائيًا؛ أنشئ اختصار Python كما في الخطوة 11.</p>

<h3 dir="rtl" align="right">code-server لا يفتح</h3>

<p dir="rtl" align="right">تحقق من الإصدار ثم راجع سجل التشغيل:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>code-server --version
tail -n 40 &quot;$HOME/code-server.log&quot;</code></pre>

<h3 dir="rtl" align="right">Thunar يتعطل عند فتح مجلد أو معاينة صورة</h3>

<p dir="rtl" align="right">في بعض بيئات PRoot، قد تتعطل معاينة الصور بسبب قيود sandbox الخاصة بـ bwrap أو Glycin. هذا لا يعني أن المجلد غير موجود. لا تعطّل sandbox افتراضيًا؛ تحقق من وجود المجلد باستخدام الأمر التالي:</p>

<p dir="rtl" align="right"><strong>أين؟ داخل Kali.</strong></p>
<pre dir="ltr" align="left" style="direction:ltr;text-align:left;white-space:pre;overflow-x:auto;"><code>ls -ld &quot;$HOME/Desktop&quot; &quot;$HOME/Desktop/Python&quot;</code></pre>

<h3 dir="rtl" align="right">أمر أو حزمة غير موجودة</h3>

<p dir="rtl" align="right">تأكد أولًا أنك تستخدم التطبيق الصحيح: أوامر <code dir="ltr">pkg</code> في Termux، وأوامر <code dir="ltr">apt</code> داخل Kali. انسخ نص الخطأ كاملًا وراجع المصادر الرسمية قبل تعديل الإعدادات.</p>

<h2 dir="rtl" align="right">ملاحظات الأمان</h2>

<ul dir="rtl" align="right">
<li>لا تشارك كلمة مرور VNC أو code-server ولا ترفع ملفات الإعدادات السرية.</li>
<li>أبقِ خادمي VNC وcode-server على عنوان <code dir="ltr">127.0.0.1</code> للاستخدام المحلي.</li>
<li>لا تعطّل عزل Electron أو Glycin كحل دائم لمجرد تجاوز خطأ.</li>
<li>لا تضع كلمات المرور أو السجلات الشخصية داخل مجلد عام.</li>
</ul>

<h2 dir="rtl" align="right">المصادر الرسمية</h2>

<ul dir="rtl" align="right">
<li><a href="https://www.kali.org/docs/nethunter/nethunter-rootless/">توثيق Kali NetHunter Rootless</a></li>
<li><a href="https://github.com/termux/termux-app#installation">طرق تثبيت Termux الرسمية</a></li>
<li><a href="https://f-droid.org/en/packages/com.termux/">Termux على F-Droid</a></li>
<li><a href="https://manpages.debian.org/trixie/tigervnc-standalone-server/tigervncserver.1.en.html">توثيق TigerVNC</a></li>
<li><a href="https://code-server.dev/">الموقع الرسمي لـ code-server</a></li>
</ul>

<hr>

<p dir="rtl" align="right"><strong>هذا دليل مجتمعي غير رسمي، وليس إصدارًا من Kali Linux أو Termux. راجع التوثيق الرسمي عند اختلاف الإصدارات.</strong></p>
