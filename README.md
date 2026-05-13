# Private-translate-action
GitHub Actions workflows to translate text or files with Google Translate and save/delete translation files inside your repository.

> **🔒 Privacy Notice**: This repository processes text or files you provide (e.g., via workflow inputs or existing files) and stores translation results in the `docs/translation/` folder. If you plan to translate **sensitive, private, or confidential information**, please **make your fork of this repository private** to prevent unintended exposure. Public repositories will make all translation files publicly visible.

## ✨ Workflows

### 1. `Translate with Google Translate`
- **Trigger**: Manual (`workflow_dispatch`)
- **Inputs**:
  - `input_type` – Choose between:
    - `text` – Translate a multi-line text you provide manually.
    - `file` – Translate an existing file from your repository.
  - `text` – (Required if `input_type = text`) The text you want to translate (supports multiple lines).
  - `source_file` – (Required if `input_type = file`) Path to the file in the repo to translate, e.g., `docs/lyrics.txt` or `README.md`.
  - `target_lang` – Target language code, e.g., `es` (Spanish), `fa` (Farsi), `de`, `zh`, `ja`.
  - `output_file_suffix` – (Only for file input) Suffix added to the output filename. Example: `"_translated"` → `input_translated_fa.txt`.
- **What it does**:
  1. For text input: translates the provided text.
  2. For file input: reads the file from the repository and translates its entire content while preserving all line breaks/formatting.
  3. Output is always saved under `docs/translation/`:
     - **Text mode** → `docs/translation/translation_<timestamp>_to_<lang>.txt` (contains original + translation).
     - **File mode** → `docs/translation/<basename><suffix>_<lang>.txt` (contains only the translation plus a comment line with the source file path). If a file with the same name already exists, a timestamp is automatically inserted to avoid overwriting.
  4. The new translation file is automatically committed and pushed to the repository.

### 2. `Delete All Translations`
- **Trigger**: Manual (`workflow_dispatch`)
- **Inputs**:
  - `confirm` – You must type `"yes"` to confirm deletion.
- **What it does**:
  - Deletes the entire `docs/translation/` folder and all translation files inside it.
  - Commits and pushes the removal.

## 🚀 How to use

1. Go to the **Actions** tab of your repository.
2. Select the workflow you want to run (e.g., `Translate with Google Translate`).
3. Click **Run workflow**, choose the input type (`text` or `file`), fill in the required inputs, and confirm.
4. After completion, the translated file will appear in the `docs/translation/` folder (or all files will be deleted if you ran the delete workflow).

## ⚙️ Requirements

- **Permissions**: The workflows need `contents: write`. Enable this in:
  `Settings → Actions → General → Workflow permissions → Read and write permissions`
- **Dependencies**: The translate workflow installs `deep-translator` (unofficial Google Translate API) on each run.

## 📝 Notes

- The `[skip ci]` flag is added to commit messages to prevent recursive workflow runs.
- For heavy or production use, consider switching to the official [Google Cloud Translation API](https://cloud.google.com/translate).
- Multi‑line text and files work fine: line breaks are preserved in both input modes.

## 🧹 Clean up

Run the **Delete All Translations** workflow any time you want to remove all generated translation files from the `docs/translation/` folder.

---

## 📖 توضیحات به فارسی

**🔒 نکته حریم خصوصی**: این مخزن متن یا فایل‌هایی که شما ارائه می‌دهید (مثلاً از طریق ورودی‌های workflow یا فایل‌های موجود در مخزن) را پردازش کرده و نتایج ترجمه را در پوشه `docs/translation/` ذخیره می‌کند. اگر قصد ترجمه **اطلاعات حساس، خصوصی یا محرمانه** را دارید، لطفاً **فورک خود را خصوصی (private) کنید** تا از دسترسی ناخواسته جلوگیری شود. مخازن عمومی تمام فایل‌های ترجمه را در معرض دید عموم قرار می‌دهند.

این مخزن شامل دو workflow برای GitHub Actions است که متن یا فایل را با استفاده از **Google Translate** (از طریق کتابخانه `deep-translator`) ترجمه کرده و نتیجه را مستقیماً در مخزن شما ذخیره می‌کند.

### 🧠 workflow اول: ترجمه با Google Translate
- **نحوه اجرا**: دستی (`workflow_dispatch`)
- **ورودی‌ها**:
  - `input_type` – انتخاب بین:
    - `text` – ترجمه متن چندخطی که دستی وارد می‌کنید.
    - `file` – ترجمه یک فایل موجود در مخزن.
  - `text` – (در صورت انتخاب `text` الزامی است) متنی که می‌خواهید ترجمه شود (چند خطی را پشتیبانی می‌کند).
  - `source_file` – (در صورت انتخاب `file` الزامی است) مسیر فایل در مخزن برای ترجمه، مثلاً `docs/lyrics.txt` یا `README.md`.
  - `target_lang` – کد زبان مقصد، مثلاً `es` (اسپانیایی)، `fa` (فارسی)، `de`، `zh`، `ja`.
  - `output_file_suffix` – (فقط برای ورودی فایل) پسوندی که به نام فایل خروجی اضافه می‌شود. مثال: `"_translated"` → `input_translated_fa.txt`.
- **عملکرد**:
  1. برای ورودی متن: متن ارائه‌شده را ترجمه می‌کند.
  2. برای ورودی فایل: فایل را از مخزن خوانده و تمام محتوای آن را با حفظ خطوط و قالب‌بندی ترجمه می‌کند.
  3. خروجی همیشه در مسیر `docs/translation/` ذخیره می‌شود:
     - **حالت متن** → `docs/translation/translation_<timestamp>_to_<lang>.txt` (شامل اصل و ترجمه).
     - **حالت فایل** → `docs/translation/<basename><suffix>_<lang>.txt` (فقط شامل ترجمه به همراه یک خط توضیح با مسیر فایل اصلی). اگر فایلی با همین نام از قبل وجود داشته باشد، یک زمان‌سنج خودکار به نام اضافه می‌شود تا از بازنویسی جلوگیری شود.
  4. فایل ترجمه جدید به‌طور خودکار commit و به مخزن push می‌شود.

### 🗑️ workflow دوم: حذف همه ترجمه‌ها
- **نحوه اجرا**: دستی (`workflow_dispatch`)
- **ورودی‌ها**:
  - `confirm` – برای تأیید حذف باید `"yes"` را تایپ کنید.
- **عملکرد**:
  - کل پوشه `docs/translation/` و تمام فایل‌های درون آن را حذف می‌کند.
  - حذف را commit و push می‌کند.

### 🚀 نحوه استفاده

1. به برگه **Actions** مخزن خود بروید.
2. workflow مورد نظر (مثلاً `Translate with Google Translate`) را انتخاب کنید.
3. روی **Run workflow** کلیک کنید، نوع ورودی (`text` یا `file`) را انتخاب کنید، ورودی‌های لازم را پر کنید و تأیید کنید.
4. پس از اتمام، فایل ترجمه‌شده در پوشه `docs/translation/` ظاهر می‌شود (یا در صورت اجرای workflow دوم، همه فایل‌ها حذف می‌شوند).

### ⚙️ پیش‌نیازها

- **دسترسی‌ها**: workflowها به `contents: write` نیاز دارند. این را در مسیر زیر فعال کنید:
  `Settings → Actions → General → Workflow permissions → Read and write permissions`
- **وابستگی‌ها**: workflow ترجمه در هر بار اجرا، کتابخانه `deep-translator` (API غیررسمی Google Translate) را نصب می‌کند.

### 📝 نکات

- پرچم `[skip ci]` به پیام commit اضافه می‌شود تا از اجرای مجدد workflow جلوگیری شود.
- برای استفاده سنگین یا تولیدی، بهتر است از [API رسمی Google Cloud Translation](https://cloud.google.com/translate) استفاده کنید.
- متن چند خطی و فایل‌ها به درستی کار می‌کنند: خطوط در هر دو حالت ورودی حفظ می‌شوند.

### 🧹 پاکسازی

هر زمان خواستید همه فایل‌های ترجمه را از پوشه `docs/translation/` حذف کنید، workflow **Delete All Translations** را اجرا کنید.
