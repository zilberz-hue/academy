# להעלות את הריפו ל-GitHub

הריפו כבר מאותחל, עם branch `main` ושני קומיטים. נשאר רק להצמיד אותו ל-GitHub.

## 1. ליצור ריפו ריק

פתח: https://github.com/new?name=academy

- **Owner**: zilberz-hue
- **Repository name**: academy
- **Private** (מומלץ — אפשר לפתוח אחר כך)
- אל תסמן "Add a README", "Add .gitignore" או "Choose a license" — הריפו כבר מכיל אותם,
  וסימון ייצור קונפליקט בדחיפה הראשונה.

## 2. לדחוף

```bash
cd academy
git remote add origin https://github.com/zilberz-hue/academy.git
git push -u origin main
```

אם SSH מוגדר אצלך, השורה האמצעית היא:

```bash
git remote add origin git@github.com:zilberz-hue/academy.git
```

## 3. לחבר ל-Netlify

Netlify → Add new site → Import an existing project → GitHub → `academy`.

| שדה | ערך |
|---|---|
| Branch to deploy | `main` |
| Build command | *(ריק)* |
| Publish directory | `.` |

`netlify.toml` שבריפו כבר מגדיר את זה, אז אפשר פשוט ללחוץ Deploy.

## 4. מכאן זה אוטומטי

אחרי שני השלבים האלה אין יותר עבודה ידנית:

```
git push  →  GitHub Action  →  index + PDF + שער איכות  →  קומיט  →  Netlify
```

כל דחיפה שמשנה תוכן קורס מרעננת את דף הבית ואת כל קבצי ה-PDF, עוברת שער
שבודק את עשרת הקורסים בדפדפן, ורק אז עולה לאוויר. אם משהו שבור — הבנייה
נופלת והאתר נשאר על הגרסה הקודמת.

להרצת השער מקומית: `npm run check`
