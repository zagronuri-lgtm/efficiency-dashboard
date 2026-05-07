# חיבור urizagron.com ל-Netlify — מדריך מהיר

## חלק א': העלאת האתר ל-Netlify (5 דקות)

### צעד 1: הכן תיקייה לפריסה
שמור את 2 הקבצים האלה בתיקייה אחת על המחשב:
- `landing.html` → **שנה את שמו ל-`index.html`** (חשוב! זה הופך אותו לדף הראשי)
- `traffic-diversion.html` → השאר כך

מבנה התיקייה צריך להיראות:
```
my-site/
├── index.html              (שהיה landing.html)
└── traffic-diversion.html
```

### צעד 2: העלה ל-Netlify
1. גש ל-[app.netlify.com/drop](https://app.netlify.com/drop)
2. גרור את **התיקייה כולה** (לא קבצים בודדים) לתוך החלון
3. תקבל URL זמני, כמו `https://amazing-curie-abc123.netlify.app`
4. בדוק שהאתר עובד — פתח את ה-URL ותראה את דף הנחיתה
5. לחץ על **"Claim your site"** והירשם / התחבר

---

## חלק ב': חיבור הדומיין urizagron.com (10 דקות)

### צעד 3: הוסף את הדומיין ב-Netlify
1. בלוח הבקרה של Netlify, לחץ על האתר שלך
2. **Domain settings** → **Add custom domain**
3. הקלד: `urizagron.com`
4. אשר את הבעלות (Netlify יראה הוראות)
5. הוסף גם את `www.urizagron.com` כ-domain alias

### צעד 4: עדכן DNS ב-Namecheap
לאחר שהוספת את הדומיין ב-Netlify, תקבל **A Record** ו-**CNAME**.

**אופציה A — שינוי Nameservers (מומלץ, פשוט יותר):**
1. ב-Netlify: Domain settings → ראה את ה-Netlify DNS nameservers (לדוגמה: `dns1.p01.nsone.net`, `dns2.p01.nsone.net`...)
2. ב-Namecheap: גש ל-[ap.www.namecheap.com/domains/list](https://ap.www.namecheap.com/domains/list)
3. ליד `urizagron.com` לחץ **MANAGE**
4. תחת **NAMESERVERS** בחר **Custom DNS**
5. הדבק את 4 ה-nameservers של Netlify
6. לחץ על הסימון ירוק לשמירה

**אופציה B — A Record + CNAME (משאיר Namecheap DNS):**
ב-Namecheap → MANAGE → **Advanced DNS**:
| Type | Host | Value | TTL |
|---|---|---|---|
| A Record | @ | 75.2.60.5 | Automatic |
| CNAME | www | YOUR-SITE-NAME.netlify.app | Automatic |

### צעד 5: המתן ל-DNS propagation
- בדרך כלל **5-30 דקות**, לפעמים עד 24 שעות
- בדוק [whatsmydns.net](https://whatsmydns.net) → הקלד `urizagron.com`
- כשרוב הדגלים ירוקים — מוכן

### צעד 6: HTTPS אוטומטי
Netlify ינפיק תעודת SSL חינם דרך Let's Encrypt **אוטומטית** ברגע שה-DNS עובד. לא צריך לעשות כלום.

---

## חלק ג': הקמת מיילים @urizagron.com (אופציונלי, 5 דקות)

הדף שלך מציג `hello@urizagron.com` ו-`sales@urizagron.com`. כדי לקבל מיילים שם:

### אופציה הכי זולה — Cloudflare Email Routing (חינם):
1. הרשם ל-[Cloudflare](https://cloudflare.com) חינם
2. הוסף את `urizagron.com` (תצטרך להעביר nameservers — אבל אז לא משתמשים ב-Netlify DNS, יש קצת התנגשות)

### אופציה פשוטה יותר — ImprovMX (חינם):
1. גש ל-[improvmx.com](https://improvmx.com)
2. הוסף את `urizagron.com` ותגדיר forwarding: `hello@urizagron.com → your.real.email@gmail.com`
3. ImprovMX יראה לך MX records להוסיף ב-Namecheap → Advanced DNS

### אופציה מקצועית — Google Workspace:
$6/חודש למשתמש, נותן לך תיבת Gmail מלאה כמו `hello@urizagron.com`.

---

## מה יקרה אחרי כל זה
- `https://urizagron.com` → דף הנחיתה (TransitDivert)
- `https://urizagron.com/traffic-diversion.html` → האפליקציה עצמה (זה מה שתשלח ללקוחות אחרי קנייה)
- `hello@urizagron.com` → מיילים נכנסים אליך

---

## סטטוס נוכחי לבדיקה
- [ ] Netlify Drop בוצע, יש URL זמני
- [ ] urizagron.com מחובר ב-Netlify
- [ ] DNS עודכן ב-Namecheap
- [ ] הדומיין עולה עם HTTPS
- [ ] Stripe Payment Links נוצרו
- [ ] הקישורים עודכנו ב-`index.html`
- [ ] מיילים מועברים אליך

ברגע שכל הסעיפים מסומנים — אתה אונליין ומוכן למכירה.
