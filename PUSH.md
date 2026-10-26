# להעלות את הריפו ל-GitHub

הריפו כאן שלם: 11 קורסים, 11 PDF, מערכת העיצוב, הסקריפטים וה-GitHub Action.
38 קבצים, 9 קומיטים, עובר את שער האיכות.

`github.com/zilberz-hue/academy` כבר קיים ומחובר ל-Netlify, אבל יש בו רק
קבצי שורש — תיקיות `courses/`, `assets/`, `pdf/` ו-`scripts/` לא עלו בגרירה.
לכן דף הבית מציג 11 קורסים וכל הקישורים מחזירים 404.

הפקודה למטה מחליפה את מה שבריפו במה שכאן, ומסדרת את זה בפעם אחת.

## הדרך הקצרה — טרמינל

```bash
unzip academy.zip
cd repo
git push --force origin main
```

זה הכול. ה-remote כבר מוגדר ל-`https://github.com/zilberz-hue/academy.git`,
אין מה להוסיף ואין מה לקנפג.

`--force` נדרש כי ההיסטוריות נפרדו: בריפו יש 3 קומיטים של העלאות ידניות, וכאן 9.
לא מאבדים שום דבר — כל מה שהעלית ידנית קיים כאן בגרסה מעודכנת יותר.

אם git מבקש הזדהות, שם המשתמש הוא `zilberz-hue` והסיסמה היא **Personal Access Token**
(לא סיסמת החשבון): `github.com/settings/tokens` → Generate new token (classic) → הרשאת `repo`.

## בלי טרמינל — GitHub Desktop

1. להתקין: `desktop.github.com`
2. להיכנס עם חשבון `zilberz-hue`
3. `File → Add local repository` ולבחור את תיקיית `repo` שפרקת מה-zip
4. ללחוץ `Push origin`. אם הוא מתלונן על היסטוריה שונה — `Repository → Repository settings`
   ואז force push, או פשוט להריץ את הפקודה מהסעיף הקודם מתוך `Repository → Open in Terminal`

## אחרי הדחיפה — פעם אחת בלבד

ב-GitHub: `Settings → Actions → General → Workflow permissions` → **Read and write permissions** → Save.

בלי זה ה-Action ירוץ אבל לא יוכל לקמט חזרה את `index.html` ואת `pdf/`.

## ומכאן זה אוטומטי

```
git push  →  GitHub Action  →  index + PDF + שער איכות  →  קומיט  →  Netlify
```

כל דחיפה שנוגעת ב-`courses/`, `assets/`, `courses.json` או `scripts/`:

1. מרעננת את `index.html` מ-`courses.json`
2. בונה קובץ עצמאי לכל קורס עם הגופנים מוטמעים
3. מרנדרת מחדש את כל 11 ה-PDF
4. **מריצה את שער האיכות** — אפס שגיאות JS, רקע קלף, גופן Assistant, בדיוק אינדקס
   אחד גלוי, hero עם לוגו, מספר יחידות תואם, אין גלילה אופקית, כל קישור בדף הבית תקין
5. מקמטת את התוצרים עם `[skip ci]`

אם משהו שבור — הבנייה נופלת, הקומיט לא נכנס, והאתר נשאר על הגרסה הקודמת.

להרצת השער מקומית, לפני דחיפה: `npm run check`

## לעדכן תוכן מכאן והלאה

לערוך את הקובץ ב-`courses/`, לדחוף, וזהו. לא להריץ build ולא לייצר PDF ביד —
ה-Action עושה את זה. עיצוב שמשותף לכל הקורסים נמצא ב-`assets/tizon.css` ורק שם.
