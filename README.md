# Ain Shams Medicine – registration tracker

A shared, bilingual (English / Arabic) checklist for a new international student at the Faculty of Medicine, Ain Shams University (2026–2027). Family members sign in with Google and can:

- tick steps as they are done (the next pending step is highlighted);
- **add, edit, reorder and delete steps** (✎ Edit on any step, or ＋ Add a step here under any section);
- **add, edit and remove map places** (paste a Google Maps link or coordinates), which then appear on the scaled map and in the step location list;
- comment on any step.

Every change records the person's name and the date/time automatically (shown in Cairo time).

**Status:** personal family tool, not an official university resource. Always confirm details with the faculty.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app. The built-in starting plan is the `STEPS` list inside it; everything the family adds or edits is saved in Firebase |
| `config.js` | **Paste your Firebase config here** |
| `firestore.rules` | Security rules: only listed Google accounts can read or write |

## Privacy

GitHub Pages sites are **public** on a normal GitHub account, even if the repo is private. The page itself contains only the general plan (no passport numbers, names of the student, or addresses of where she lives). The ticks and comments are stored in Firebase and can only be read by the Google accounts you list in `firestore.rules`. Don't put passport numbers or other ID numbers in comments.

## Setup (about 15 minutes)

### 1. Create the Firebase project (free "Spark" plan)
1. Go to https://console.firebase.google.com → **Add project** → any name (e.g. `asu-tracker`) → Google Analytics off → Create.
2. **Build → Authentication → Get started → Sign-in method → Google → Enable** → choose a support email → Save.
3. **Build → Firestore Database → Create database** → Production mode → location `europe-west` (or any) → Enable.
4. **Firestore → Rules** tab → replace everything (if you set it up before, paste the new version: it adds steps and places) with the contents of `firestore.rules`, put each family member's Gmail address in the list, then **Publish**.
5. **Project settings (gear) → General → Your apps → Web (`</>`)** → register an app (no hosting) → copy the values (apiKey, authDomain, projectId, …) into `config.js`.

The Firebase web config is not a secret; access is controlled by the rules in step 4.

### 2. Put it on GitHub Pages
1. On github.com: **New repository** → name `asu-tracker` → Public (required for free Pages) → do **not** add a README → Create.
2. From inside this folder:
   ```bash
   git remote add origin https://github.com/<your-username>/asu-tracker.git
   git branch -M main
   git add config.js && git commit -m "Add Firebase config"
   git push -u origin main
   ```
   (Or use **Add file → Upload files** on github.com and drag all the files in.)
3. Repo **Settings → Pages → Source: Deploy from a branch → `main` / root → Save**. After a minute the site is at `https://<your-username>.github.io/asu-tracker/`.

### 3. Allow sign-in from your site
Firebase → **Authentication → Settings → Authorized domains → Add domain** → `<your-username>.github.io`.

### 4. Share
Send the link to the people you listed in the rules. They open it, press **Sign in with Google**, and can tick and comment. Anyone not on the list sees the plan but no ticks or comments.

To add someone later: add their Gmail to `firestore.rules` in the Firebase console and Publish. No need to touch GitHub.

## Try it without Firebase
Leave `apiKey` empty in `config.js` and double-click `index.html`. It runs in **demo mode**: everything saves only in that browser.

---

## بالعربي (مختصر)
1. أنشئ مشروعاً مجانياً في Firebase، وفعّل تسجيل الدخول بحساب جوجل، وأنشئ قاعدة Firestore.
2. انسخ محتوى `firestore.rules` إلى تبويب Rules وأضف بريد جيميل لكل فرد من العائلة، ثم Publish.
3. انسخ إعدادات تطبيق الويب إلى ملف `config.js`.
4. ارفع الملفات إلى مستودع على GitHub وفعّل GitHub Pages.
5. أضف النطاق `<اسم المستخدم>.github.io` إلى Authorized domains في Firebase.
6. أرسل الرابط للعائلة؛ كل شخص يسجل الدخول بحساب جوجل، ويمكنه تعليم الخطوات وإضافة خطوات جديدة وتعديلها وترتيبها وحذفها، وإضافة مواقع للخريطة، والتعليق. الاسم ووقت التعديل يُسجلان تلقائياً.
