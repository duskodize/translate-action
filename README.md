# GitHub Actions Translation Tool

> **🔒 Privacy Notice**: This repository processes text you provide (e.g., via workflow inputs) and stores translation results in the `translation/` folder. If you plan to translate **sensitive, private, or confidential information**, please **make your fork of this repository private** to prevent unintended exposure. Public repositories will make all translation files publicly visible.

This repository provides two GitHub Actions workflows to translate text using **Google Translate** (via the `deep-translator` library) and store the results directly in your repo.

## ✨ Workflows

### 1. `Translate with Google Translate`
- **Trigger**: Manual (`workflow_dispatch`)
- **Inputs**:
  - `text` – The text you want to translate (supports multiple lines)
  - `target_lang` – Target language code, e.g., `es` (Spanish), `fa` (Farsi), `de`, `zh`, `ja`
- **What it does**:
  1. Translates the text using Google Translate.
  2. Creates a timestamped file in the `translation/` folder (e.g., `translation_20260512_143022_to_fa.txt`).
  3. The file contains: original text, target language, and the translated result.
  4. Commits and pushes the file back to the repository.

### 2. `Delete All Translations`
- **Trigger**: Manual (`workflow_dispatch`)
- **What it does**:
  - Deletes the entire `translation/` folder (or just its contents if you modify the script).
  - Commits and pushes the removal.

## 🚀 How to use

1. Go to the **Actions** tab of your repository.
2. Select the workflow you want to run (e.g., `Translate with Google Translate`).
3. Click **Run workflow**, fill in the inputs (for the translate workflow), and confirm.
4. After completion, the translated file will appear in the `translation/` folder (or all files will be deleted).

## ⚙️ Requirements

- **Permissions**: The workflows need `contents: write`. Enable this in:
  `Settings → Actions → General → Workflow permissions → Read and write permissions`
- **Dependencies**: The translate workflow installs `deep-translator` (unofficial Google Translate API) on each run.

## 📝 Notes

- The `[skip ci]` flag is added to commit messages to prevent recursive workflow runs.
- For heavy or production use, consider switching to the official [Google Cloud Translation API](https://cloud.google.com/translate).
- Multi‑line text works: you can paste several lines into the `text` field when triggering the workflow.

## 🧹 Clean up

Run the **Delete All Translations** workflow any time you want to remove all generated translation files from the repository.

---

## 📖 توضیحات به فارسی

**🔒 نکته حریم خصوصی**: این مخزن متنی که شما وارد می‌کنید را پردازش کرده و نتایج ترجمه را در پوشه `translation/` ذخیره می‌کند. اگر قصد ترجمه **اطلاعات حساس، خصوصی یا محرمانه** را دارید، لطفاً **فورک خود را خصوصی (private) کنید** تا از دسترسی ناخواسته جلوگیری شود. مخازن عمومی تمام فایل‌های ترجمه را در معرض دید عموم قرار می‌دهند.

این مخزن شامل دو workflow برای GitHub Actions است که متن را با استفاده از **Google Translate** (از طریق کتابخانه `deep-translator`) ترجمه کرده و نتیجه را مستقیماً در مخزن شما ذخیره می‌کند.

### 🧠 workflow اول: ترجمه با Google Translate
- **نحوه اجرا**: دستی (`workflow_dispatch`)
- **ورودی‌ها**:
  - `text` – متنی که می‌خواهید ترجمه شود (چند خطی را پشتیبانی می‌کند)
  - `target_lang` – کد زبان مقصد، مثلاً `es` (اسپانیایی)، `fa` (فارسی)، `de`، `zh`، `ja`
- **عملکرد**:
  1. متن را با Google Translate ترجمه می‌کند.
  2. یک فایل با زمان‌‌انداز در پوشه `translation/` می‌سازد (مثل `translation_20260512_143022_to_fa.txt`).
  3. فایل شامل: متن اصلی، زبان مقصد و نتیجه ترجمه است.
  4. فایل را به مخزن commit و push می‌کند.

### 🗑️ workflow دوم: حذف همه ترجمه‌ها
- **نحوه اجرا**: دستی (`workflow_dispatch`)
- **عملکرد**:
  - کل پوشه `translation/` (یا فقط محتویات آن در صورت تغییر اسکریپت) را حذف می‌کند.
  - حذف را commit و push می‌کند.

### 🚀 نحوه استفاده

1. به برگه **Actions** مخزن خود بروید.
2. workflow مورد نظر (مثلاً `Translate with Google Translate`) را انتخاب کنید.
3. روی **Run workflow** کلیک کنید، ورودی‌ها را پر کنید (برای workflow ترجمه) و تأیید کنید.
4. پس از اتمام، فایل ترجمه‌شده در پوشه `translation/` ظاهر می‌شود (یا در صورت اجرای workflow دوم، همه فایل‌ها حذف می‌شوند).

### ⚙️ پیش‌نیازها

- **دسترسی‌ها**: workflowها به `contents: write` نیاز دارند. این را در مسیر زیر فعال کنید:
  `Settings → Actions → General → Workflow permissions → Read and write permissions`
- **وابستگی‌ها**: workflow ترجمه در هر بار اجرا، کتابخانه `deep-translator` (API غیررسمی Google Translate) را نصب می‌کند.

### 📝 نکات

- پرچم `[skip ci]` به پیام commit اضافه می‌شود تا از اجرای مجدد workflow جلوگیری شود.
- برای استفاده سنگین یا تولیدی، بهتر است از [API رسمی Google Cloud Translation](https://cloud.google.com/translate) استفاده کنید.
- متن چند خطی کار می‌کند: می‌توانید چند خط را در فیلد `text` جایگذاری کنید.

### 🧹 پاکسازی

هر زمان خواستید همه فایل‌های ترجمه را از مخزن حذف کنید، workflow **Delete All Translations** را اجرا کنید.
