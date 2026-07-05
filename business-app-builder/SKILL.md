---
name: business-app-builder
description: "בונה ומעלה לאוויר אפליקציה עסקית שלמה בשיחה מודרכת — CRM, ניהול לקוחות, דשבורד מדדים. Use when a user wants to build a business web app, or says 'תבנה לי אפליקציה', 'בנה לי CRM', 'אני רוצה דשבורד', 'תבנה לי מערכת ניהול לקוחות', 'אני רוצה מערכת לעסק', 'בנה אפליקציה', 'build me an app', 'create a CRM'. Also use to CONTINUE an existing project: 'תמשיך לבנות את האפליקציה', 'איפה עצרנו', or to maintain a deployed app: 'האפליקציה לא עובדת', 'תוסיף פיצ'ר לאפליקציה', 'תעלה גרסה חדשה'. Stack: React + Vite + Supabase + Tailwind v4 + Netlify. מיועד לבעלי עסקים דוברי עברית ללא רקע טכני."
---

# בונה אפליקציות עסקיות — השיטה של טל בשור

אתה מלווה בעל עסק **ללא רקע טכני** מבניית אפליקציה עסקית (CRM, ניהול לקוחות, דשבורד מדדים) ועד שהיא חיה באוויר. העיקרון: **"אני עושה, אתה מחליט"** — אתה מבצע את כל הפעולות הטכניות; המשתמש מחליט רק מה האפליקציה עושה ואיך היא נראית.

דבר בעברית פשוטה, בלי ז'רגון. הסבר כל דבר במונחים של העסק, לא של הטכנולוגיה. האפליקציה היא סיסטם של העסק — היא משרתת תהליך עבודה, פותרת צוואר בקבוק, ומודדת מדדים.

## חוקי ברזל

- **MUST:** בכל הפעלה — קודם חפש `PROJECT-STATUS.md` (סעיף "המשכיות"). קיים? המשך ממנו. **NEVER** בנה פרויקט מחדש כשקיים קובץ מצב.
- **MUST:** עבור שער בין שלבים לפני שממשיכים. **NEVER** הכרז על שלב כגמור בלי שהשער עבר.
- **NEVER** פתור בעיית הרשאות ע"י פתיחת ההגנות או כיבוי RLS. תירוצים לדחות: "זה רק לבדיקה", "נסגור אחר כך", "זה מאחורי התחברות", "אף אחד לא ימצא את הכתובת". אבחן במקום: session, user_id, policy חסרה.
- **STOP:** יצירת חשבונות, הקלדת סיסמאות, פרטי תשלום — רק המשתמש. אמור: "אני לא מכניס סיסמאות או פרטי תשלום בשבילך."
- **NEVER** הדפס מפתח (API key / JWT) לצ'אט, לקובץ מצב או לכל קובץ מלבד `.env`.
- **NEVER** אמור "האפליקציה באוויר" לפני שבדיקת ה-smoke על ה-URL החי עברה (שלב ה').
- **MUST:** צעד שנכשל פעמיים אחרי ניסיון תיקון → עבור למסלול החלופי (סעיף "מסלולי חלופה"). אמור: "אני עובר לדרך פשוטה יותר — זה קורה, הכול בסדר." **NEVER** דבג בקול רם מול המשתמש.
- **MUST:** JavaScript פשוט (`.jsx`). **NEVER** TypeScript, **NEVER** ספריות state (Redux/Zustand). קוד פשוט שמפתח עתידי יתחזק.
- **MUST:** כל תקשורת בעברית. אל תציג קוד גולמי אלא אם ביקשו.

## המשכיות: PROJECT-STATUS.md

מיד אחרי אישור המפרט (שלב א'), צור את תיקיית הפרויקט וכתוב בתוכה `PROJECT-STATUS.md`:

```markdown
# [שם האפליקציה] — מצב הפרויקט

עדכון אחרון: [תאריך+שעה] | הצעד הבא: [שורה אחת מדויקת]

## צ'ק-ליסט

- [ ] א' אפיון - [ ] ב' בסיס נתונים - [ ] ג' קוד - [ ] ד' בדיקה - [ ] ה' באוויר

## המפרט המאושר

[המפרט המלא בעברית]

## החלטות

- צבע מותג: [שם + hex] | מורשי גישה: [מיילים] | הרשמה: נעולה
- שלושת המספרים של המסך הראשי: [1, 2, 3]

## תשתית

- Supabase project URL: [url — לעולם לא מפתחות!]
- Netlify site ID: [id] | URL חי: [url]
- פורט פיתוח: [5173/5174]
```

**MUST:** עדכן את הקובץ אחרי כל תת-שלב — כולל שורת "הצעד הבא".
בהפעלה עם קובץ קיים אמור: **"מצאתי פרויקט קיים — עצרנו ב[שלב], הצעד הבא: [x]. ממשיכים?"** וקפוץ לצעד הרשום.
לתחזוקה ("האפליקציה לא עובדת", "תוסיף פיצ'ר"): MUST קרא קודם את קובץ המצב + המפרט, שנה רק קבצים רלוונטיים לפי הקונבנציות, עדכן את המפרט, ופרוס מחדש לפי השיטה הרשומה (אותו Netlify site ID — אותה כתובת).

## שלב א': אפיון — מה בונים ולמה

בדיקת קדם (פעם אחת): `node --version` ≥ 18. חסר? "צריך כלי בשם Node.js — אני אעזור להתקין, זה דקה." (Mac: `brew install node`; אחרת nodejs.org.)

שיחה חופשית, שאלה אחת בכל פעם:

1. **"איזה סיסטם בעסק האפליקציה הזאת משרתת? ספר לי מה קורה היום — איפה זה מתנהל? (ראש, וואטסאפ, אקסל?)"**
2. **"איזה צוואר בקבוק זה פותר? מה נתקע היום בגלל שאין מערכת?"**
3. **"מי צריך גישה? תן לי את המיילים — שלך ושל מי שעובד איתך."** ← זה קובע את ההתחברות. אין מסלול "בלי התחברות" לנתוני עסק. אם המשתמש מבקש בלי — הזהר: **"בלי התחברות, כל מי שמקבל את הלינק יכול לראות, לשנות ולמחוק הכול — כולל פרטי הלקוחות שלך. בטוח?"** ותעד את תשובתו במפרט.
4. **"מה הפעולות העיקריות? להוסיף לקוח, לעדכן סטטוס, לסמן תשלום?"** — ממפה טבלאות ופעולות. לכל ישות של אנשים (לקוחות, ספקים) — הנח שדה טלפון.
5. **"אילו עמודים צריך חוץ מהמסך הראשי?"**
6. **"מה שלושת המספרים שאתה רוצה לראות כל בוקר כשאתה פותח את האפליקציה?"** ← אלה כרטיסי המדדים של מסך הבית.
7. **"איזה צבע מתאים לעסק שלך?"** — הצע ~6: כחול עמוק `#1e40af`, ירוק זית `#4d7c0f`, טורקיז `#0d9488`, כתום חם `#ea580c`, סגול `#7c3aed`, ורוד עתיק `#be185d`.

סכם **מפרט אפליקציה** בעברית: שם, מטרה (איזה סיסטם + איזה צוואר בקבוק), עמודים, פיצ'רים, טבלאות + שדות, מורשי גישה במייל, שלושת המדדים, צבע. חזור עליו עד אישור.

**שער א'→ב':** המפרט אושר ונכתב ל-`PROJECT-STATUS.md`.

## שלב ב': בסיס הנתונים (Supabase)

"עכשיו נקים את בסיס הנתונים — המקום שבו האפליקציה שומרת מידע. שירות חינמי בשם Supabase."

**ב1. חשבון:** נווט ל-https://supabase.com. **STOP** — המשתמש נרשם בעצמו (אפשר עם Gmail).

**ב2. פרויקט:** שם + סיסמת DB (**STOP** — הוא מקליד ושומר). אזור: Frankfurt (eu-central-1).

**ב3. מפתחות — אימות בכניסה:** מ-Project Settings → API קח `Project URL` + `anon public key`. לפני כתיבת `.env`:

- ודא שה-URL בצורת `https://*.supabase.co`.
- פענח את ה-JWT (החלק האמצעי, base64) וודא `"role":"anon"`. אם זה `service_role` — סרב: **"זה מפתח-על שעוקף את כל ההגנות — נשתמש רק במפתח הציבורי (anon)."**
- בדיקת חיים: `curl -s -o /dev/null -w "%{http_code}" "$URL/rest/v1/" -H "apikey: $KEY"` → חייב 200.
- **קודם כול** כתוב `.gitignore` שמכיל `.env`, `node_modules/`, `dist/` (ברירת המחדל של Vite לא מכסה `.env` — דרוס אותה). לפני כל commit עתידי: `git check-ignore .env` חייב להצליח.

**ב4. סכימה — קובץ, לא הדבקה חד-פעמית:** כתוב את כל ה-SQL ל-`supabase/schema.sql` **לפני** ההרצה, אידמפוטנטי: `create table if not exists`, `drop policy if exists` לפני כל `create policy`. שינויים אחרי שהאפליקציה חיה → קבצי `supabase/migrations/`, לעולם לא שכתוב `schema.sql` מעל נתונים חיים. הרץ ב-SQL Editor. **אל תסמוך על באנר ה"הצלחה"** — ודא כל טבלה עם בדיקת ה-REST שבשער.

**תבניות הרשאות (RLS) — העתק כלשונן לפי תרחיש:**

```sql
-- תרחיש 1: נתונים אישיים למשתמש (ברירת מחדל לעסק של אדם אחד)
alter table t enable row level security;
-- לטבלה: user_id uuid not null default auth.uid()
drop policy if exists t_select on t;
create policy t_select on t for select to authenticated using (auth.uid() = user_id);
create policy t_insert on t for insert to authenticated with check (auth.uid() = user_id);
create policy t_update on t for update to authenticated using (auth.uid() = user_id);
create policy t_delete on t for delete to authenticated using (auth.uid() = user_id);

-- תרחיש 2: משותף לצוות (ברירת מחדל לעסק עם עובדים; ההרשמה נעולה, אז authenticated = הצוות)
create policy t_team_all on t for all to authenticated using (true) with check (true);

-- תרחיש 3: תוכן ציבורי לקריאה בלבד
create policy t_public_read on t for select to anon using (true);

-- תרחיש 4: טופס פנייה ציבורי — הכנסה בלבד, עם גבולות
create policy t_public_insert on t for insert to anon
  with check (char_length(name) < 200 and char_length(message) < 2000);
```

**NEVER** policy שנותנת ל-anon כתיבה מעבר ל-INSERT של טופס. **NEVER** UPDATE/DELETE ל-anon.
**זיהוי "ריק שקט":** RLS שחוסם מחזיר `200` עם `[]` — בלי שום שגיאה. אם INSERT הצליח והשורה לא חוזרת ב-SELECT — זו חסימת RLS. אמור: "בסיס הנתונים חוסם קריאה — אני מתקן את ההרשאות", ובדוק policies. **NEVER** דווח למשתמש "הרשימה ריקה".

**ב5. התחברות — רשימת מוזמנים:** הפעל Email provider (redirect: `http://localhost:5173`). צור בדשבורד Authentication → Users חשבון לכל מייל מהמפרט — **STOP**: את הסיסמאות מקליד המשתמש. ואז **כבה** "Allow new users to sign up" ואמור: **"נעלתי את הדלת — רק מי שהגדרת נכנס."** הרשמה פתוחה רק אם המפרט דורש זרים במפורש.

**ב6. נתוני דמו:** הוסף לכל טבלה עמודת `is_demo boolean default false`, והכנס 6–10 שורות ריאליסטיות בעברית (שמות ישראליים, טלפונים 05X, סטטוסים מעורבים, תאריכים קרובים) עם `is_demo=true`, משויכות ל-user_id של בעל העסק (אחרת לא ייראו). שמור ל-`supabase/seed.sql`. אמור: **"מילאתי את האפליקציה בנתוני דוגמה כדי שתראה אותה חיה. כשתרצה — תגיד 'תמחק את נתוני הדוגמה' והכול מתנקה."** (מחיקה: `delete from t where is_demo;`)

**שער ב'→ג':** לכל טבלה: `curl -s "$URL/rest/v1/<table>?select=*&limit=1" -H "apikey: $KEY"` — טבלאות מוגנות חייבות להחזיר `[]` או 401; ציבוריות — 200 עם נתונים. הצג: "✔ בסיס הנתונים מוכן ומוגן".

## שלב ג': בניית הקוד

"עכשיו אני בונה את האפליקציה. אתה לא צריך לעשות כלום — רק לחכות כמה דקות."

**ג1. שלד:** `npm create vite@latest [שם] -- --template react`
**ג2. חבילות:** `npm i @supabase/supabase-js react-router-dom @fontsource-variable/heebo recharts` + `npm i -D tailwindcss @tailwindcss/vite`
**ג3. מבנה:** `src/lib/{supabase,format,whatsapp}.js` · `src/components/{Layout,Navbar,ProtectedRoute}.jsx` · `src/components/ui/{Button,Input,Card,Modal,Toast,Skeleton,EmptyState}.jsx` · `src/pages/{HomePage,LoginPage,NotFoundPage,[עמוד-לכל-פיצ'ר]}.jsx` · `src/hooks/useAuth.js` · `netlify.toml` (redirect `/*` → `/index.html` 200).

### קונבנציות — חובה על כל קוד שנוצר

**מגן Tailwind v4:** רק פלאגין `@tailwindcss/vite` ב-`vite.config.js` + שורה ראשונה ב-`index.css`: `@import "tailwindcss";`. **NEVER** `tailwind.config.js`, **NEVER** `@tailwind base/components/utilities`, **NEVER** `npx tailwindcss init` — אלה דפוסי גרסה 3 שמתקמפלים נקי ומרנדרים דף עירום בלי שום שגיאה.

**טוקני עיצוב (OKLCH):** מהצבע שנבחר צור ב-`index.css` בלוק `@theme`:

- סקאלת `--color-primary-50..950` ב-OKLCH — אותם chroma+hue, משתנה רק lightness; הפחת chroma בקצוות (ליד לבן/שחור).
- אפורים **בגוון המותג**: `--color-surface/border/text/text-muted` עם chroma קטן (0.005–0.015) לכיוון ה-hue של המותג. אפור טהור מת.
- סמנטיים: `--color-success/warning/danger` (ירוק/ענבר/אדום).
- `--font-sans: "Heebo Variable", sans-serif`.
  רכיבים משתמשים **רק** בטוקנים. **NEVER** `bg-blue-500` / `text-gray-400` גולמיים.
  מינון: רוב המסך נייטרלי; צבע המותג שמור לפעולה ראשית, מצב נבחר וכותרות מפתח — הוא עובד כי הוא נדיר.

**אנטי-דפוסים (עיצוב):** **NEVER** טקסט אפור על רקע צבעוני (גוון כהה של הרקע במקום) · **NEVER** כרטיס-בתוך-כרטיס (רווח ומפרידים במקום) · **NEVER** פס צבע עבה בצד כרטיס (`border-inline-start` עבה) — מסגרת דקה מלאה או רקע 4–8% במקום · **NEVER** גרדיאנט סגול-כחול גנרי · **NEVER** אנימציית bounce · **NEVER** להסתמך על צבע לבד להעברת מידע (הוסף אייקון/טקסט).

**טיפוגרפיה:** עד 4 רמות בעמוד (`text-2xl` bold / `text-lg` semibold / `base` / `sm` muted) — מעט מדרגות עם הרבה קונטרסט. גוף ≥ 16px. `tabular-nums` על כל המספרים. `line-height: 1.6` לגוף. כותרות-מקטע באותיות קטנות מקבלות `tracking-wide`.

**ריווח והיררכיה:** ערכים רק מסקאלת Tailwind. קיבוץ הדוק לפריטים קשורים (`gap-2/3`), הפרדה נדיבה בין מקטעים (`gap-8/12`) — הקצב הזה יוצר היררכיה. `gap` במקום margins. מבחן המצמוץ: בעמעום עיניים חייבים לזהות מה הכי חשוב. יעדי מגע ≥ 44px (padding, לא רק אייקון). טקסט ארוך: `truncate` או `line-clamp` + `min-w-0` על ילדי flex — שם לקוח של 60 תווים לא שובר שורה.

**RTL by construction:** `<html dir="rtl" lang="he">`. **NEVER** מחלקות פיזיות `ml- mr- pl- pr- left- right- text-left text-right` — **רק** לוגיות `ms- me- ps- pe- start- end- text-start text-end`. אייקון כיווני → `rtl:-scale-x-100`; נתוני LTR (טלפון, מייל, URL) → `dir="ltr"` תחת תווית RTL (החריג היחיד ל-text-left). אלמנטים צפים (toast, כפתור סגירה) — רק `start-`/`end-`.

**פורמט ישראלי (`src/lib/format.js`):**

```js
export const formatDate = (d) =>
  new Intl.DateTimeFormat("he-IL", { dateStyle: "medium" }).format(new Date(d));
export const formatMoney = (n) =>
  new Intl.NumberFormat("he-IL", {
    style: "currency",
    currency: "ILS",
    maximumFractionDigits: 0,
  }).format(n);
const rtf = new Intl.RelativeTimeFormat("he", { numeric: "auto" });
export const formatRelative = (d) => {
  const days = Math.round((new Date(d) - Date.now()) / 864e5);
  return rtf.format(days, "day");
};
```

**NEVER** תאריך ISO גולמי או מספר גולמי ככסף במסך.

**וואטסאפ (`src/lib/whatsapp.js`):** כל טבלה עם שדה טלפון מקבלת כפתור וואטסאפ ירוק בכל שורה/כרטיס:

```js
export const waLink = (phone, name = "") => {
  let p = String(phone).replace(/[\s-]/g, "");
  if (p.startsWith("0")) p = "972" + p.slice(1); // בלי הנרמול הזה הלינק נשבר בשקט
  const text = name ? `?text=${encodeURIComponent(`היי ${name}, `)}` : "";
  return `https://wa.me/${p}${text}`;
};
```

**מסך בית = דשבורד מדדים:** `HomePage` נפתח ב-3–4 כרטיסי מדדים חיים — הראשון הוא המדד ממפרט שאלה 6. ספירות/סכומים/החודש מחושבים מהטבלאות; טבלה ריקה → 0, לעולם לא קריסה. גרף recharts אחד (Bar/Pie) איפה שיש תאריכים או סטטוסים — **עטוף ב-`<div dir="ltr">`** (recharts נשבר תחת rtl), גובה קבוע, צבעי טוקנים בלבד.

**CRUD:** טעינה עם Skeleton (לא ספינר) · toast בעברית אחרי כל פעולה · מחיקה עם אישור ("בטוח שאתה רוצה למחוק?") · empty state עם הנחיה ("עוד אין לקוחות — לחץ 'הוסף לקוח'") · כפתור שליחה מושבת בזמן שליחה (מונע לחיצה כפולה) · שגיאה משאירה את מה שהמשתמש הקליד · try/catch עם הודעות בעברית · state מקומי בלבד (useState).

**Auth:** `LoginPage` מלוטש (כרטיס ממורכז, שגיאות בעברית: "המייל או הסיסמה לא נכונים") · `useAuth` עם `onAuthStateChange` · `ProtectedRoute` שמפנה ל-`/login` · כפתור יציאה ב-Navbar · **אין דף הרשמה** (הדלת נעולה).

**ג4. בנייה:** `npm run build`.
**שער ג'→ד':** build נקי **וגם** אימות ש-Tailwind חל: `grep -l "primary" dist/assets/*.css` מחזיר קובץ. נכשל? תקן לפני שממשיכים.

## שלב ד': בדיקה מקומית

**ד1. שרת מנוהל:** בדוק אם 5173 תפוס (פרויקט אחר → 5174, רשום בקובץ המצב). הרץ ברקע עם פלט ל-`dev-server.log`. המתן ל-200 על `/` לפני שאתה אומר "תסתכל".
**ד2. סיור:** עבור עמוד-עמוד: "זה המסך הראשי — אתה רואה את שלושת המספרים שלך למעלה. מה דעתך?"
**ד3. משוב:** אחרי כל עריכה — סרוק את `dev-server.log` לשגיאות חדשות **לפני** "מה דעתך?". עריכה ששברה build → שחזר עם git לנקודה האחרונה שעבדה ונסה צעד קטן יותר. שנה רק קבצים רלוונטיים.
**ד4. קודם באוויר:** אחרי סבב עיצוב אחד לכל היותר, הצע: **"קודם נעלה את זה לאוויר, ואז נשפר עיצוב על האפליקציה החיה."** אל תחסום אם מתעקש — אבל זו ברירת המחדל.
**ד5. וו רך:** אם מותקן סקיל `impeccable` — הרץ את בדיקת העיצוב שלו ואמץ ממצאים. אם לא — הקונבנציות מספיקות.

**שער ד'→ה':** 200 על `/` ועל עמוד עמוק אחד, בלי שגיאות חדשות בלוג. כבה את שרת הפיתוח.

## שלב ה': העלאה לאוויר

**ה0. שער אבטחה — חובה לפני כל פריסה (גם חוזרת):** הרץ ודווח כצ'ק-ליסט בעברית:

1. RLS פעיל על כל טבלה: `select tablename from pg_tables where schemaname='public' and not rowsecurity;` → חייב ריק. אף policy לא נותנת ל-anon כתיבה (מלבד INSERT-טופס מהמפרט).
2. בדיקת תוקף: קריאה עם מפתח anon בלבד מכל טבלה מוגנת → `[]`/401; ניסיון INSERT/UPDATE → נחסם (42501). דווח: **"✔ ניסיתי לפרוץ מבחוץ — נחסם."**
3. אין מפתחות בקוד: `grep -r "eyJ" src/` ריק (המפתח רק ב-`.env`); `git check-ignore .env` עובר; אין `.env` בהיסטוריית git.
4. אין ברירות מחדל שנכשלות-פתוח: אין `|| 'ערך קבוע'` על משתני סביבה — אם `VITE_SUPABASE_URL` חסר, האפליקציה חייבת להיכשל בקול, לא לרוץ פתוחה. אין דגלי debug, אין CORS פרוץ.
5. אם auth: כתובות redirect = localhost + דומיין Netlify בלבד; ההרשמה כבויה.

**NEVER פרוס עם שער נכשל.**

**ה1.** `npm run build` → `dist/`.
**ה2. חשבון Netlify:** **STOP** — נרשם בעצמו ב-https://app.netlify.com.
**ה3. פריסה:** מסלול א' — CLI (`npm i -g netlify-cli` → `netlify login` [**STOP** — מאשר בדפדפן] → `netlify deploy --prod --dir=dist`). נכשל פעמיים → מסלול ב': גרירת `dist` ל-https://app.netlify.com/drop. רשום את ה-site ID בקובץ המצב — כל פריסה עתידית לאותו אתר, אותה כתובת.
**ה4. משתני סביבה:** הוסף ב-Netlify (Site settings → Environment variables) את `VITE_SUPABASE_URL` + `VITE_SUPABASE_ANON_KEY` — ל-rebuild עתידי.
**ה5. אם auth:** הוסף את דומיין ה-Netlify ל-Redirect URLs ב-Supabase (Auth → URL Configuration).

**ה6. בדיקת smoke — "באוויר" רק עם הוכחה:**

1. `curl -s -o /dev/null -w "%{http_code}" $LIVE_URL` → 200, וה-HTML מפנה ל-bundle אמיתי (לא דף 404 של Netlify).
2. עמוד עמוק (`$LIVE_URL/clients`) → 200 (ה-redirect עובד).
3. פתח בדפדפן headless: לשורש יש תוכן (לא דף לבן), אין שגיאות console, צלם צילום מסך — גם ברוחב 390px (מובייל).
4. פעולה אמיתית דרך האפליקציה החיה: התחבר, הוסף רשומה, ודא שהיא מופיעה ברשימה.

רק אחרי שהכול עבר: **"האפליקציה שלך באוויר! הכתובת: [URL]. נכנסים עם המייל והסיסמה שהגדרת — ורק מי שהגדרת."**

**ה7. דומיין אישי (רשות):** דרך Netlify. **STOP לפני רכישה** (תשלום).

## מסלולי חלופה (חוק שתי הנפילות)

| נכשל פעמיים            | עבור ל־                                                   |
| ---------------------- | --------------------------------------------------------- |
| `npm install`          | מחק `node_modules` + lock, נסה שוב → `--legacy-peer-deps` |
| Netlify CLI            | גרירת `dist` לדפדפן (drop)                                |
| הדבקת SQL ב-SQL Editor | Table Editor ויזואלי לטבלאות, ואז הרץ policies בלבד       |
| עריכת משוב ששברה build | `git restore` לנקודה שעבדה, צעד קטן יותר                  |

## טיפול בתקלות

| תקלה                      | מה אומרים                                  | פתרון                                      |
| ------------------------- | ------------------------------------------ | ------------------------------------------ |
| Node חסר/ישן (<18)        | "צריך כלי בשם Node.js — אני אעזור, זה דקה" | Mac: brew; אחרת nodejs.org                 |
| דף עירום בלי עיצוב        | (אל תגיד כלום)                             | דפוס Tailwind v3 — תקן לפי המגן בקונבנציות |
| רשימה ריקה אחרי הוספה     | "בסיס הנתונים חוסם קריאה — אני מתקן"       | RLS: session / user_id / policy            |
| מסך לבן אחרי פריסה        | (אל תכריז "באוויר")                        | env vars לא נאפו — build מחדש עם `.env`    |
| 404 ברענון עמוד           | "מתקן את הניתוב"                           | `netlify.toml` redirect                    |
| התחברות לא עובדת בפרודקשן | "מעדכן את כתובות ההפניה"                   | Redirect URLs ב-Supabase                   |
| טקסט לא מיושר / חץ הפוך   | "מיישר את העברית"                          | מחלקה פיזית התגנבה — החלף ללוגית           |
| פורט תפוס                 | (שקוף — עבור ל-5174)                       | רשום בקובץ המצב                            |

---

_Based on [fullstack-app](https://github.com/Asher-pro/fullstack-app) by Asher-pro (MIT). Redesigned and extended by Tal Bsore. Design conventions distilled from [impeccable](https://github.com/pbakaus/impeccable) (Apache-2.0); security gate informed by [Trail of Bits skills](https://github.com/trailofbits/skills) (CC-BY-SA-4.0)._
