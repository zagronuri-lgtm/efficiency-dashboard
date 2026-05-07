# איך מתחילים למכור — מדריך 30 דקות

## מה יש לך עכשיו
1. **`landing.html`** — דף מכירה מקצועי באנגלית עם 3 חבילות מחיר
2. **`traffic-diversion.html`** — האפליקציה עצמה שאתה מוכר
3. **כפתורי קנייה** — מוכנים לחיבור ל-Stripe

## 5 צעדים להעלות את זה אונליין ולהתחיל לקבל כסף

### 1. דומיין (5 דקות, ~$12/שנה)
- היכנס ל-[Namecheap](https://namecheap.com) או [Cloudflare](https://cloudflare.com/products/registrar)
- חפש שם זמין (לדוגמה: `transitdivert.com`, `busdivert.io`, `mydivert.app`)
- קנה את הדומיין

### 2. Hosting חינם (5 דקות)
**אופציה הכי פשוטה — Netlify Drop:**
1. גש ל-[netlify.com/drop](https://app.netlify.com/drop)
2. גרור את התיקייה שמכילה `landing.html` ו-`traffic-diversion.html`
3. שנה את שם הקובץ הראשי ל-`index.html` (במקום `landing.html`)
4. תקבל URL זמני — לדוגמה `https://random-name.netlify.app`
5. בהגדרות Netlify, חבר את הדומיין שקנית בצעד 1

**או GitHub Pages (חינם אם המאגר ציבורי):**
- בהגדרות המאגר ב-GitHub: Settings → Pages → Source: main → Save

### 3. Stripe Payment Links (10 דקות)
1. צור חשבון [Stripe](https://stripe.com) — מהיר ובחינם
2. עבור ל-[Payment Links](https://dashboard.stripe.com/payment-links)
3. צור 2 payment links:
   - **Single Planner** — $499 one-time
   - **Department** — $1,499 one-time
4. לכל אחד הגדר:
   - שם מוצר
   - מחיר one-time
   - אסוף email (חשוב!)
   - הגדר success URL: `https://yourdomain.com/thank-you.html` (נצטרך ליצור)
5. העתק את ה-URLs

### 4. עדכן את `landing.html` (3 דקות)
פתח את הקובץ, חפש את השורה:
```js
const STRIPE_LINKS = {
    single:     'https://buy.stripe.com/REPLACE_WITH_YOUR_LINK_SINGLE',
    department: 'https://buy.stripe.com/REPLACE_WITH_YOUR_LINK_DEPARTMENT'
};
```
החלף את הקישורים ב-URLs האמיתיים מ-Stripe.

החלף גם את כתובות המייל:
- `hello@transitdivert.com` → המייל שלך
- `sales@transitdivert.com` → המייל שלך

### 5. דף תודה + מסירת המוצר (5 דקות)
צור קובץ פשוט בשם `thank-you.html`:
```html
<!DOCTYPE html>
<html>
<head><title>Thank You!</title></head>
<body style="font-family: sans-serif; max-width: 600px; margin: 5rem auto; padding: 2rem;">
    <h1>🎉 Thank you for your purchase!</h1>
    <p>You'll receive an email within 5 minutes with:</p>
    <ul>
        <li>Your TransitDivert app file</li>
        <li>Setup instructions</li>
        <li>Anthropic API key setup guide</li>
    </ul>
    <p>Questions? Email <a href="mailto:hello@yourdomain.com">hello@yourdomain.com</a></p>
</body>
</html>
```

**הכי פשוט להתחיל:** אחרי כל קנייה, Stripe ישלח לך מייל. תשלח ידנית את `traffic-diversion.html` ללקוח (אפשר לאוטמט אחר כך).

**אוטומציה (אופציונלי):** השתמש ב-[Zapier](https://zapier.com) — Stripe → Gmail → שלח אוטומטית את הקובץ.

## חוקים חשובים שלא לשכוח

### חובה לפני שאתה מוכר
- [ ] **Privacy Policy** + **Terms of Service** — חובה לפי GDPR/CCPA. השתמש ב-[Termly](https://termly.io) חינם
- [ ] **Refund Policy** — Stripe דורש מדיניות ברורה
- [ ] **Tax** — אם אתה בארה"ב, הצטרף ל-[Stripe Tax](https://stripe.com/tax) (אוטומטי)
- [ ] **בעלות על הקוד** — וודא שאין בעיית IP (ראה הערה בתחילת השיחה)

### לפי בקשת לקוחות (לא חובה מההתחלה)
- חשבונית מע"מ (אם בישראל) → השתמש ב-Green Invoice / iCount
- חוזה SaaS / EULA רשמי
- DPA (Data Processing Agreement)

## השקעה כוללת לחודש הראשון

| פריט | מחיר |
|---|---|
| דומיין | $12/שנה |
| Hosting (Netlify) | חינם |
| Stripe | 2.9% + 30¢ לעסקה (רק כשמוכרים) |
| Termly Privacy/Terms | חינם |
| Anthropic API (לבדיקות) | $20-50 לחודש |
| **סה"כ קבוע** | **~$15** |

אם תמכור 5 לקוחות בחודש הראשון ב-$499:
- הכנסות: $2,495
- עמלת Stripe: ~$75
- **רווח נטו: ~$2,400**

## מה בא אחר כך
- **חודש 1-2:** הוצא post ב-LinkedIn לחבריך בתעשייה. שלח email לצוותי planning ב-5 רשויות שאתה מכיר.
- **חודש 3:** אם יש 5+ לקוחות מרוצים — בקש קייסים / המלצות.
- **חודש 6:** אם הגעת ל-$5K MRR, שקול לשפר את המוצר ולעלות מחיר.
- **שנה 1:** אם זה עובד, אז כדאי להתחיל לחשוב על SaaS אמיתי (ראה `ARCHITECTURE-SAAS.md`).

הצלחה! 🚀
