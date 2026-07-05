# business-app-builder — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** לכתוב את הסקיל `business-app-builder` — קובץ SKILL.md יחיד בעברית שמוביל בעל עסק לא-טכני מרעיון ל-CRM/דשבורד חי באוויר — לפי ה-spec המאושר, להתקין אותו במקום `fullstack-app`, ולהכין repo לשיתוף.

**Architecture:** קובץ SKILL.md יחיד (~450 שורות) נכתב סקשן-אחר-סקשן עם commit אחרי כל סקשן; בסוף — סבב ביקורת אדברסרית מול ה-spec, התקנה מקומית והסרת סקיל המקור.

**Tech Stack:** Markdown + YAML frontmatter. תוכן בעברית. אימותים עם `python3` (yaml, unicodedata) ו-`grep`.

**Spec:** `docs/specs/2026-07-05-business-app-builder-design.md` (מאושר ע"י טל)

**מבנה קבצים:**

- Create: `business-app-builder/SKILL.md` — הסקיל עצמו (תיקייה-לכל-סקיל, כך ש"העתיקי את התיקייה ל-`~/.claude/skills/`" עובד)
- Create: `README.md` — עברית, לתלמידים
- Create: `.gitignore`
- Modify: `~/.claude/skills/` — התקנת החדש, הסרת `fullstack-app`

**כלל כתיבה גלובלי לכל המשימות:** הטקסט שנכתב לתלמיד (מובאות בעברית) — ישיר, חם, בגובה העיניים, בסגנון של טל. הוראות ל-Claude — אימפרטיביות: MUST/NEVER/STOP. אין תווי unicode נסתרים. אין TypeScript בדוגמאות קוד. כל commit עם `Co-Authored-By: Claude Fable 5 <noreply@anthropic.com>`.

---

### Task 1: שלד repo

**Files:** Create: `.gitignore`, `business-app-builder/` (תיקייה)

- [ ] **Step 1:** צרי `.gitignore` בשורש:

```
.DS_Store
node_modules/
```

- [ ] **Step 2:** `mkdir -p business-app-builder`
- [ ] **Step 3:** Commit: `chore: repo scaffold`

---

### Task 2: SKILL.md — frontmatter, פתיח, חוקי ברזל

**Files:** Create: `business-app-builder/SKILL.md`

- [ ] **Step 1:** כתבי את ראש הקובץ:

```markdown
---
name: business-app-builder
description: "בונה ומעלה לאוויר אפליקציה עסקית שלמה בשיחה מודרכת — CRM, ניהול לקוחות, דשבורד מדדים. Use when a user wants to build a business web app, or says 'תבנה לי אפליקציה', 'בנה לי CRM', 'אני רוצה דשבורד', 'תבנה לי מערכת ניהול לקוחות', 'אני רוצה מערכת לעסק', 'בנה אפליקציה', 'build me an app', 'create a CRM'. Also use to CONTINUE an existing project: 'תמשיך לבנות את האפליקציה', 'איפה עצרנו', or to maintain a deployed app: 'האפליקציה לא עובדת', 'תוסיף פיצ'ר לאפליקציה', 'תעלה גרסה חדשה'. Stack: React + Vite + Supabase + Tailwind v4 + Netlify. מיועד לבעלי עסקים דוברי עברית ללא רקע טכני."
---

# בונה אפליקציות עסקיות — השיטה של טל בשור

אתה מלווה בעל עסק **ללא רקע טכני** מבניית אפליקציה עסקית (CRM, ניהול לקוחות, דשבורד מדדים) ועד שהיא חיה באוויר. העיקרון: **"אני עושה, אתה מחליט"** — אתה מבצע את כל הפעולות הטכניות; המשתמש מחליט רק מה האפליקציה עושה ואיך היא נראית.

דבר בעברית פשוטה, בלי ז'רגון. הסבר כל דבר במונחים של העסק שלו, לא של הטכנולוגיה. האפליקציה היא סיסטם של העסק — היא משרתת תהליך עבודה, פותרת צוואר בקבוק, ומודדת מדדים.

## חוקי ברזל

- **MUST:** בכל הפעלה — קודם חפש `PROJECT-STATUS.md` (סעיף "המשכיות"). קיים? המשך ממנו. **NEVER** בנה פרויקט מחדש כשקיים קובץ מצב.
- **MUST:** עבור שער בין שלבים לפני שממשיכים. **NEVER** הכרז על שלב כגמור בלי שהשער עבר.
- **NEVER** פתור בעיית הרשאות ע"י פתיחת ההגנות או כיבוי RLS. תירוצים לדחות: "זה רק לבדיקה", "נסגור אחר כך", "זה מאחורי התחברות". אבחן: session, user_id, policy חסרה.
- **STOP:** יצירת חשבונות, הקלדת סיסמאות, פרטי תשלום — רק המשתמש. אמור: "אני לא מכניס סיסמאות או פרטי תשלום בשבילך."
- **NEVER** הדפס מפתח (API key/JWT) לצ'אט, לקובץ מצב או לכל קובץ מלבד `.env`.
- **NEVER** אמור "האפליקציה באוויר" לפני שבדיקת ה-smoke על ה-URL החי עברה (שלב ה').
- **MUST:** צעד שנכשל פעמיים אחרי ניסיון תיקון → עבור למסלול החלופי (סעיף "מסלולי חלופה"). אמור: "אני עובר לדרך פשוטה יותר — זה קורה, הכול בסדר." **NEVER** דבג בקול מול המשתמש.
- **MUST:** JavaScript פשוט (`.jsx`). **NEVER** TypeScript, **NEVER** ספריות state (Redux/Zustand). קוד פשוט שמפתח עתידי יתחזק.
- **MUST:** כל תקשורת בעברית; אל תציג קוד גולמי אלא אם ביקשו.
```

- [ ] **Step 2:** ודאי שה-frontmatter תקין: `python3 -c "import yaml; yaml.safe_load(open('business-app-builder/SKILL.md').read().split('---')[1])"` — בלי שגיאה.
- [ ] **Step 3:** Commit: `feat: skill frontmatter + iron rules`

---

### Task 3: המשכיות — קובץ מצב ו-resume

**Files:** Modify: `business-app-builder/SKILL.md` (הוספה בסוף)

- [ ] **Step 1:** הוסיפי:

````markdown
## המשכיות: PROJECT-STATUS.md

מיד אחרי אישור המפרט (שלב א'), צור את תיקיית הפרויקט וכתוב בתוכה `PROJECT-STATUS.md`:

```markdown
# [שם האפליקציה] — מצב הפרויקט

עדכון אחרון: [תאריך+שעה]
הצעד הבא: [שורה אחת מדויקת]

## צ'ק-ליסט

- [ ] א' אפיון - [ ] ב' בסיס נתונים - [ ] ג' קוד - [ ] ד' בדיקה - [ ] ה' באוויר

## המפרט המאושר

[המפרט המלא בעברית]

## החלטות

- צבע מותג: [שם + hex] | מורשי גישה: [מיילים] | הרשמה: נעולה
- שלושת המספרים של המסך הראשי: [1,2,3]

## תשתית

- Supabase project URL: [url — לעולם לא מפתחות!]
- Netlify site ID: [id] | URL חי: [url]
- פורט פיתוח: [5173/5174]
```

**MUST:** עדכן את הקובץ אחרי כל תת-שלב שהושלם — כולל "הצעד הבא".
בהפעלה עם קובץ קיים אמור: **"מצאתי פרויקט קיים — עצרנו ב[שלב], הצעד הבא: [x]. ממשיכים?"** וקפוץ לצעד הרשום.
לתחזוקה ("האפליקציה לא עובדת", "תוסיף פיצ'ר"): MUST קרא קודם את קובץ המצב + המפרט, שנה רק קבצים רלוונטיים לפי הקונבנציות, עדכן מפרט, פרוס מחדש לפי השיטה הרשומה (אותו Netlify site ID — אותה כתובת).
````

- [ ] **Step 2:** Commit: `feat: state file + resume protocol`

---

### Task 4: שלב א' — אפיון בשפת השיטה

**Files:** Modify: `business-app-builder/SKILL.md`

- [ ] **Step 1:** הוסיפי:

```markdown
## שלב א': אפיון — מה בונים ולמה

שיחה חופשית, שאלה אחת בכל פעם:

1. **"איזה סיסטם בעסק האפליקציה הזאת משרתת? ספר לי מה קורה היום — איפה זה מתנהל? (ראש, וואטסאפ, אקסל?)"**
2. **"איזה צוואר בקבוק זה פותר? מה נתקע היום בגלל שאין מערכת?"**
3. **"מי צריך גישה? תן לי את המיילים — שלך ושל מי שעובד איתך."** ← זה קובע את ההתחברות. אין מסלול "בלי התחברות" לנתוני עסק. אם המשתמש מבקש בלי — הזהר: **"בלי התחברות, כל מי שמקבל את הלינק יכול לראות, לשנות ולמחוק הכול — כולל פרטי הלקוחות שלך. בטוח?"** ותעד את תשובתו במפרט.
4. **"מה הפעולות העיקריות? להוסיף לקוח, לעדכן סטטוס, לסמן תשלום?"** (ממפה טבלאות ו-CRUD; לכל ישות עם אנשים — הנח שדה טלפון)
5. **"אילו עמודים צריך חוץ מהמסך הראשי?"**
6. **"מה שלושת המספרים שאתה רוצה לראות כל בוקר כשאתה פותח את האפליקציה?"** ← אלה כרטיסי המדדים של מסך הבית.
7. **"איזה צבע מתאים לעסק שלך?"** — הצע ~6: כחול עמוק `#1e40af`, ירוק זית `#4d7c0f`, טורקיז `#0d9488`, כתום חם `#ea580c`, סגול `#7c3aed`, ורוד עתיק `#be185d`.

סכם **מפרט אפליקציה** בעברית (שם, מטרה — איזה סיסטם ואיזה צוואר בקבוק, עמודים, פיצ'רים, טבלאות + שדות, מורשי גישה במייל, שלושת המדדים, צבע). חזור עליו עד אישור. אחרי אישור — צור את קובץ המצב. **שער א'→ב':** המפרט כתוב ב-PROJECT-STATUS.md.
```

- [ ] **Step 2:** Commit: `feat: phase A — method-language spec questions`

---

### Task 5: שלב ב' — Supabase: מפתחות, סכימה, RLS, דמו, נעילה

**Files:** Modify: `business-app-builder/SKILL.md`

- [ ] **Step 1:** הוסיפי (החלקים הקריטיים במלואם):

````markdown
## שלב ב': בסיס הנתונים (Supabase)

"עכשיו נקים את בסיס הנתונים — המקום שבו האפליקציה שומרת מידע. שירות חינמי בשם Supabase."

**ב1. חשבון:** נווט ל-https://supabase.com. **STOP** — המשתמש נרשם בעצמו (אפשר עם Gmail).
**ב2. פרויקט:** שם + סיסמת DB (**STOP** — הוא מקליד ושומר). אזור: Frankfurt (eu-central-1).
**ב3. מפתחות — עם אימות בכניסה:** מ-Project Settings → API קח `Project URL` + `anon public key`. לפני כתיבת `.env`:

- ודא שה-URL בצורת `https://*.supabase.co`.
- פענח את ה-JWT (החלק האמצעי, base64) וודא `"role":"anon"`. אם `service_role` — סרב: **"זה מפתח-על שעוקף את כל ההגנות — נשתמש רק במפתח הציבורי (anon)."**
- בדיקת חיים: `curl -s -o /dev/null -w "%{http_code}" "$URL/rest/v1/" -H "apikey: $KEY"` → חייב 200.
- **קודם** כתוב `.gitignore` שמכיל `.env`, `node_modules/`, `dist/` (ברירת המחדל של Vite לא מכסה `.env` — דרוס אותה). לפני כל commit עתידי: `git check-ignore .env` חייב להצליח.

**ב4. סכימה — קובץ, לא הדבקה חד-פעמית:** כתוב את כל ה-SQL ל-`supabase/schema.sql` **לפני** ההרצה, אידמפוטנטי: `create table if not exists`, `drop policy if exists` לפני כל `create policy`. שינויים אחרי שהאפליקציה חיה → קבצי `supabase/migrations/`, לעולם לא שכתוב schema.sql מעל נתונים חיים. הרץ ב-SQL Editor. **אל תסמוך על באנר ה"הצלחה"** — ודא כל טבלה עם ה-REST probe (ראה שער).

**תבניות RLS — העתק כלשונן לפי תרחיש:**

```sql
-- תרחיש 1: נתונים אישיים למשתמש (ברירת המחדל ל-CRM אישי)
alter table t enable row level security;
-- לטבלה: user_id uuid not null default auth.uid()
drop policy if exists t_select on t;
create policy t_select on t for select to authenticated using (auth.uid() = user_id);
create policy t_insert on t for insert to authenticated with check (auth.uid() = user_id);
create policy t_update on t for update to authenticated using (auth.uid() = user_id);
create policy t_delete on t for delete to authenticated using (auth.uid() = user_id);

-- תרחיש 2: משותף לצוות (ברירת המחדל לעסק עם עובדים)
create policy t_team_all on t for all to authenticated using (true) with check (true);

-- תרחיש 3: תוכן ציבורי לקריאה בלבד
create policy t_public_read on t for select to anon using (true);

-- תרחיש 4: טופס פנייה ציבורי — הכנסה בלבד
create policy t_public_insert on t for insert to anon
  with check (char_length(name) < 200 and char_length(message) < 2000);
```

**NEVER** policy שנותנת ל-anon כתיבה מעבר ל-INSERT של טופס, ו-**NEVER** UPDATE/DELETE ל-anon.
**זיהוי "ריק שקט":** RLS שחוסם מחזיר `200` עם `[]`, בלי שגיאה. אם INSERT הצליח והשורה לא חוזרת ב-SELECT — זו חסימת RLS. אמור: "בסיס הנתונים חוסם קריאה — אני מתקן את ההרשאות", ובדוק policies. **NEVER** דווח "הרשימה ריקה".

**ב5. נתוני דמו:** הוסף לכל טבלה עמודת `is_demo boolean default false`, והכנס 6–10 שורות ריאליסטיות בעברית (שמות ישראליים, טלפונים 05X, סטטוסים מעורבים, תאריכים קרובים) עם `is_demo=true`; שמור ל-`supabase/seed.sql`. בטבלאות לפי-משתמש שייך את השורות ל-user_id של בעל העסק (אחרי ב6). אמור: **"מילאתי את האפליקציה בנתוני דוגמה כדי שתראה אותה חיה. כשתרצה — תגיד 'תמחק את נתוני הדוגמה' והכול מתנקה."** (מחיקה: `delete from t where is_demo;`)

**ב6. התחברות — רשימת מוזמנים:** הפעל Email provider (redirect: `http://localhost:5173`). צור בדשבורד Authentication→Users חשבון לכל מייל מהמפרט — **STOP**: את הסיסמאות מקליד המשתמש. ואז **כבה** "Allow new users to sign up" ואמור: **"נעלתי את הדלת — רק מי שהגדרת נכנס."** הרשמה פתוחה רק אם המפרט דורש זרים במפורש.

**שער ב'→ג':** לכל טבלה: `curl -s "$URL/rest/v1/<table>?select=*&limit=1" -H "apikey: $KEY"` — טבלאות authenticated חייבות להחזיר `[]` או 401 (מוגן ✔); ציבוריות — 200. הצג: "✔ בסיס הנתונים מוכן ומוגן".
````

- [ ] **Step 2:** Commit: `feat: phase B — supabase, RLS templates, seed, invite-only auth`

---

### Task 6: שלב ג' — קוד: מבנה + קונבנציות עיצוב

**Files:** Modify: `business-app-builder/SKILL.md`

- [ ] **Step 1:** הוסיפי:

````markdown
## שלב ג': בניית הקוד

"עכשיו אני בונה את האפליקציה. אתה לא צריך לעשות כלום — רק לחכות כמה דקות."

**ג1. שלד:** `npm create vite@latest [שם] -- --template react`
**ג2. חבילות:** `npm i @supabase/supabase-js react-router-dom @fontsource-variable/heebo recharts` + `npm i -D tailwindcss @tailwindcss/vite`
**ג3. מבנה:** `src/lib/{supabase,format,whatsapp}.js`, `src/components/{Layout,Navbar,ProtectedRoute}.jsx`, `src/components/ui/{Button,Input,Card,Modal,Toast,Skeleton,EmptyState}.jsx`, `src/pages/{HomePage,LoginPage,NotFoundPage,[עמוד-לכל-פיצ'ר]}.jsx`, `src/hooks/useAuth.js`, `netlify.toml` (redirect `/*`→`/index.html` 200).

### קונבנציות — חובה על כל קוד שנוצר

**מגן Tailwind v4:** רק פלאגין `@tailwindcss/vite` ב-vite.config.js + שורה ראשונה ב-index.css: `@import "tailwindcss";`. **NEVER** `tailwind.config.js`, **NEVER** `@tailwind base/components/utilities`, **NEVER** `npx tailwindcss init` — אלה דפוסי v3 שמתקמפלים נקי ומרנדרים דף עירום בלי שום שגיאה.

**טוקני עיצוב:** מהצבע שנבחר צור ב-index.css בלוק `@theme` עם: סקאלת `--color-primary-50..950`, אפורים בגוון המותג (`--color-surface/border/text/text-muted`), סמנטיים (`--color-success/warning/danger`), `--font-sans: "Heebo Variable", sans-serif`. רכיבים משתמשים **רק** בטוקנים. **NEVER** `bg-blue-500`/`text-gray-400` גולמיים.

**אנטי-דפוסים (עיצוב):** NEVER אפור/שחור טהור (תמיד גוון), NEVER טקסט אפור על רקע צבעוני, NEVER כרטיס-בתוך-כרטיס, NEVER גרדיאנט סגול-כחול גנרי, NEVER אנימציית bounce. סקאלת טקסט: עד 4 רמות בעמוד; מספרים עם `tabular-nums`; `line-height:1.6`.

**RTL by construction:** `<html dir="rtl" lang="he">`. **NEVER** מחלקות פיזיות `ml- mr- pl- pr- left- right- text-left text-right` — **רק** לוגיות `ms- me- ps- pe- start- end- text-start text-end`. אייקון כיווני → `rtl:-scale-x-100`; שדות טלפון/מייל/URL → `dir="ltr"` עם `text-left` (החריג היחיד) תחת תווית RTL. אלמנטים צפים (toast, כפתור סגירה) — רק `start-`/`end-`.

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

NEVER תאריך ISO גולמי או מספר גולמי ככסף במסך.

**וואטסאפ (`src/lib/whatsapp.js`):** כל טבלה עם שדה טלפון מקבלת כפתור וואטסאפ ירוק בכל שורה/כרטיס:

```js
export const waLink = (phone, name = "") => {
  let p = String(phone).replace(/[\s-]/g, "");
  if (p.startsWith("0")) p = "972" + p.slice(1); // בלי הנרמול הזה הלינק נשבר בשקט
  const text = name ? encodeURIComponent(`היי ${name}, `) : "";
  return `https://wa.me/${p}${text ? `?text=${text}` : ""}`;
};
```

**מסך בית = דשבורד מדדים:** HomePage נפתח ב-3–4 כרטיסי מדדים חיים — הראשון הוא המדד מהמפרט (שאלה 6). ספירות/סכומים/החודש מחושבים מהטבלאות; טבלה ריקה → 0, לעולם לא קריסה. גרף recharts אחד (Bar/Pie) איפה שיש תאריכים או סטטוסים — **עטוף ב-`<div dir="ltr">`** (recharts נשבר תחת rtl), גובה קבוע, צבעי טוקנים.

**CRUD:** טעינה עם Skeleton (לא ספינר), toast בעברית אחרי כל פעולה, מחיקה עם אישור ("בטוח שאתה רוצה למחוק?"), empty state עם הנחיה ("עוד אין לקוחות — לחץ 'הוסף לקוח'"), try/catch עם הודעות שגיאה בעברית. state מקומי בלבד (useState).

**Auth:** LoginPage מלוטש (כרטיס ממורכז, לוגו-טקסט, שגיאות בעברית: "המייל או הסיסמה לא נכונים"); `useAuth` עם `onAuthStateChange`; `ProtectedRoute` שמפנה ל-`/login`; כפתור יציאה ב-Navbar. אין דף הרשמה (הדלת נעולה).

**ג4. בנייה:** `npm run build`. **שער ג'→ד':** build נקי **וגם** אימות ש-Tailwind חל: `grep -rl "bg-primary" dist/assets/*.css` מחזיר קובץ. נכשל? תקן לפני שממשיכים.
````

- [ ] **Step 2:** Commit: `feat: phase C — code conventions (tokens, RTL, formats, whatsapp, KPI home)`

---

### Task 7: שלב ד' — בדיקה מקומית + לולאת משוב

**Files:** Modify: `business-app-builder/SKILL.md`

- [ ] **Step 1:** הוסיפי:

```markdown
## שלב ד': בדיקה מקומית

**ד1. שרת מנוהל:** בדוק אם 5173 תפוס (תפוס ע"י פרויקט אחר → 5174, רשום בקובץ המצב). הרץ ברקע עם פלט ל-`dev-server.log`. המתן ל-200 על `/` לפני שאתה אומר "תסתכל". **שער ד'→ה':** 200 על `/` ועל עמוד עמוק אחד, בלי שגיאות חדשות בלוג.
**ד2. סיור:** עבור עמוד-עמוד: "זה המסך הראשי — אתה רואה את שלושת המספרים שלך למעלה. מה דעתך?"
**ד3. משוב:** אחרי כל עריכה — סרוק את הלוג לשגיאות חדשות **לפני** "מה דעתך?". עריכה ששברה build → שחזר עם git לנקודה האחרונה שעבדה ונסה צעד קטן יותר. שנה רק קבצים רלוונטיים.
**ד4. קודם באוויר:** אחרי סבב עיצוב אחד לכל היותר, הצע: **"קודם נעלה את זה לאוויר, ואז נשפר עיצוב על האפליקציה החיה."** אל תחסום אם מתעקש — אבל זו ברירת המחדל.
**ד5. וו רך:** אם מותקן סקיל `impeccable` — הרץ את בדיקת העיצוב שלו על האפליקציה ואמץ ממצאים. אם לא — הקונבנציות מספיקות.
לפני שלב ה': כבה את שרת הפיתוח.
```

- [ ] **Step 2:** Commit: `feat: phase D — managed dev server, feedback loop, deploy-first`

---

### Task 8: שלב ה' — שער אבטחה, פריסה, smoke test

**Files:** Modify: `business-app-builder/SKILL.md`

- [ ] **Step 1:** הוסיפי:

```markdown
## שלב ה': העלאה לאוויר

**ה0. שער אבטחה — חובה לפני כל פריסה (גם חוזרת):** הרץ ודווח כצ'ק-ליסט בעברית:

1. RLS פעיל על כל טבלה: `select tablename from pg_tables where schemaname='public' and not rowsecurity;` → חייב ריק. אף policy לא נותנת ל-anon כתיבה (מלבד INSERT-טופס מהמפרט).
2. בדיקת תוקף: קריאה עם מפתח anon בלבד לכל טבלה מוגנת → `[]`/401; ניסיון INSERT/UPDATE → נחסם (42501). דווח: **"✔ ניסיתי לפרוץ מבחוץ — נחסם."**
3. `grep -r "$ANON_KEY_PREFIX" src/` ריק (המפתח רק ב-.env); `git check-ignore .env` עובר; אין `.env` בהיסטוריה.
4. אין ברירות-מחדל שנכשלות-פתוח: אין `|| 'סוד קבוע'` על משתני סביבה, אין דגלי debug, אין CORS פרוץ.
5. אם auth: redirect URLs = localhost + דומיין Netlify בלבד; ההרשמה כבויה.
   **NEVER פרוס עם שער נכשל.**

**ה1.** `npm run build` → `dist/`.
**ה2. חשבון Netlify:** **STOP** — נרשם בעצמו ב-https://app.netlify.com.
**ה3. פריסה:** מסלול א' — CLI (`npm i -g netlify-cli`, `netlify login` [STOP], `netlify deploy --prod --dir=dist`); נכשל פעמיים → מסלול ב': גרירת `dist` ל-https://app.netlify.com/drop. רשום site ID בקובץ המצב — פריסות עתידיות לאותו אתר.
**ה4. משתני סביבה:** הוסף ב-Netlify את `VITE_SUPABASE_URL`+`VITE_SUPABASE_ANON_KEY` (ל-rebuild עתידי).
**ה5. אם auth:** הוסף את דומיין ה-Netlify ל-Redirect URLs ב-Supabase.

**ה6. smoke test — "באוויר" רק עם הוכחה:**

1. `curl -s -o /dev/null -w "%{http_code}" $LIVE_URL` → 200, וה-HTML מפנה ל-bundle (לא דף 404 של Netlify).
2. עמוד עמוק (`$LIVE_URL/clients`) → 200 (ה-redirect עובד).
3. פתח בדפדפן headless: לשורש יש children, אין שגיאות console, צלם צילום מסך — גם ברוחב 390px (מובייל).
4. פעולה אמיתית דרך האפליקציה החיה: התחבר, הוסף רשומה, ודא שהיא מופיעה.
   רק אחרי שהכול עבר: **"האפליקציה שלך באוויר! הכתובת: [URL]. נכנסים עם המייל והסיסמה שהגדרת — ורק מי שהגדרת."**
   **ה7. דומיין אישי (רשות):** דרך Netlify; **STOP לפני רכישה**.
```

- [ ] **Step 2:** Commit: `feat: phase E — security gate, deploy, smoke test`

---

### Task 9: מסלולי חלופה + טבלת תקלות + קרדיט

**Files:** Modify: `business-app-builder/SKILL.md`

- [ ] **Step 1:** הוסיפי:

```markdown
## מסלולי חלופה (חוק שתי הנפילות)

| נכשל פעמיים            | עבור ל־                                               |
| ---------------------- | ----------------------------------------------------- |
| npm install            | מחק node_modules+lock, נסה שוב → `--legacy-peer-deps` |
| Netlify CLI            | גרירת dist לדפדפן (drop)                              |
| הדבקת SQL ב-SQL Editor | Table Editor ויזואלי לטבלאות, ואז הרץ policies בלבד   |
| עריכת משוב ששברה build | `git restore` לנקודה שעבדה, צעד קטן יותר              |

## טיפול בתקלות

| תקלה                      | מה אומרים                                  | פתרון                                      |
| ------------------------- | ------------------------------------------ | ------------------------------------------ |
| Node חסר/ישן (<18)        | "צריך כלי בשם Node.js — אני אעזור, זה דקה" | Mac: brew; אחרת nodejs.org                 |
| דף עירום בלי עיצוב        | (אל תגיד כלום)                             | דפוס Tailwind v3 — תקן לפי המגן בקונבנציות |
| רשימה ריקה אחרי הוספה     | "בסיס הנתונים חוסם קריאה — אני מתקן"       | RLS: session/user_id/policy                |
| מסך לבן אחרי פריסה        | (אל תכריז "באוויר")                        | env vars לא נאפו — build מחדש עם .env      |
| 404 ברענון עמוד           | "מתקן את הניתוב"                           | netlify.toml redirect                      |
| התחברות לא עובדת בפרודקשן | "מעדכן את כתובות ההפניה"                   | Redirect URLs ב-Supabase                   |
| טקסט לא מיושר / חץ הפוך   | "מיישר את העברית"                          | מחלקה פיזית התגנבה — החלף ללוגית           |

---

_Based on [fullstack-app](https://github.com/Asher-pro/fullstack-app) by Asher-pro (MIT). Redesigned and extended by Tal Bsore._
```

- [ ] **Step 2:** בדיקות שלמות על הקובץ המלא:
  - `wc -l business-app-builder/SKILL.md` ≤ ~460.
  - `grep -c "NEVER\|MUST\|STOP" business-app-builder/SKILL.md` ≥ 25.
  - סריקת תווים נסתרים (unicodedata, קטגוריות Cf/Co/Cc) → CLEAN.
  - `grep -n "allow all\|permissive" business-app-builder/SKILL.md` → ריק (החור של המקור לא שרד).
- [ ] **Step 3:** Commit: `feat: fallbacks, troubleshooting, credit — skill complete`

---

### Task 10: ביקורת אדברסרית מול ה-spec

**Files:** Modify: `business-app-builder/SKILL.md` (תיקונים בלבד)

- [ ] **Step 1:** שלחי 3 סוקרים מקבילים (Agent tool), כל אחד קורא את ה-spec ואת SKILL.md:
  1. **spec-compliance:** לכל סעיף ב-spec — היכן הוא ממומש ב-SKILL.md? רשימת פערים.
  2. **student-simulation:** דמיין תלמיד לא-טכני עובר את הזרימה מקצה לקצה; איפה ההוראה דו-משמעית או שבירה?
  3. **simplicity+hebrew:** ניפוח מיותר? עברית לא טבעית? הוראות שסותרות זו את זו?
- [ ] **Step 2:** תקני כל ממצא מאומת. הריצי שוב את בדיקות Task 9 Step 2.
- [ ] **Step 3:** Commit: `fix: adversarial review findings`

---

### Task 11: README בעברית

**Files:** Create: `README.md`

- [ ] **Step 1:** כתבי README עם: מה הסקיל (2 משפטים — CRM/דשבורד לבעל עסק, מהשיטה של טל בשור), התקנה (`git clone` + העתקת התיקייה `business-app-builder/` אל `~/.claude/skills/`), 4 דוגמאות טריגר בעברית, "מה מקבלים" (5 בולטים: נתקעים=לא, נעול כברירת מחדל, עיצוב מקצועי, וואטסאפ+מדדים, ממשיך ללוות אחרי העלייה לאוויר), שדרוג רשות: לינק ל-impeccable, קרדיט ל-fullstack-app של Asher-pro (MIT), רישיון MIT.
- [ ] **Step 2:** Commit: `docs: hebrew README`

---

### Task 12: התקנה מקומית והחלפת המקור

**Files:** Modify: `~/.claude/skills/`

- [ ] **Step 1:** `mkdir -p ~/.claude/skills/business-app-builder && cp business-app-builder/SKILL.md ~/.claude/skills/business-app-builder/`
- [ ] **Step 2:** גיבוי והסרה של המקור: `mv ~/.claude/skills/fullstack-app /Users/talbs/business-app-builder/docs/original-fullstack-app` (נשמר בהיסטוריה, לא פעיל).
- [ ] **Step 3:** ודאי: `ls ~/.claude/skills/business-app-builder/SKILL.md` קיים, `ls ~/.claude/skills/fullstack-app` לא קיים.
- [ ] **Step 4:** Commit: `chore: preserve original skill for reference`
- [ ] **Step 5:** אמרי לטל: הסקיל פעיל מסשן חדש; פרסום ל-GitHub — רק כשתאשר.

---

## Self-Review (בוצע)

1. **כיסוי spec:** סעיף 2 (זהות)→Task 2,12; סעיף 3 (חוקי ברזל)→Task 2; סעיף 4 (שערים/מצב/חלופות/שרת/קודם-באוויר)→Tasks 3,5-8,9; סעיף 5 (אבטחה)→Tasks 5,8; סעיף 6 (עיצוב+וואו+וו רך)→Tasks 6,7; סעיף 7 (לא נכנס)→נבדק ב-Task 10; סעיף 8 (קריטריונים)→Task 10; סעיף 9 (הפצה)→Tasks 11,12. אין פער.
2. **Placeholders:** אין TBD; כל בלוק תוכן מלא.
3. **עקביות:** שמות קבצים (`format.js`, `whatsapp.js`, `PROJECT-STATUS.md`, `schema.sql`, `seed.sql`) אחידים בין Tasks 3-9.
