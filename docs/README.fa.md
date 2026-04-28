# Project Planner — مهارت هوش مصنوعی برای OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** یک مهارت برای عامل OpenCode است که فرآیند حرفه‌ای برنامه‌ریزی پروژه را قبل از تولید کد اعمال می‌کند و تحلیل نیازمندی‌ها، طراحی معماری، تفکیک وظایف و پیگیری پیشرفت را تضمین می‌نماید.

## ویژگی‌ها

- **برنامه‌ریزی اجباری** — هر وظیفه تولید کد ابتدا باید برنامه‌ریزی شود، مگر اینکه کاربر صریحاً از آن صرف‌نظر کند
- **طبقه‌بندی دامنه** — شناسایی خودکار نوع پروژه (Web/CLI/Library/Mobile) با اعمال بهترین روش‌های مربوطه
- **تحلیل نیازمندی‌ها** — ۱۴ بعد برای شفاف‌سازی نیازمندی‌ها + سه سطح اولویت (P0/P1/P2)
- **ارزیابی ریسک** — شناسایی، رتبه‌بندی و استراتژی‌های کاهش برای ۶ دسته ریسک
- **طراحی معماری** — نمودار لایه‌ای ASCII + مدل داده + قراردادهای API
- **تفکیک وظایف** — گراف وابستگی‌ها + مسیر بحرانی + تخمین زمان
- **پیگیری پیشرفت** — ثبت هر مرحله + خلاصه نقاط عطف
- **عدم تداخل** — فایل‌های پیکربندی سایر افزونه‌های IDE را تغییر نمی‌دهد

## نصب

### روش ۱: نصب سراسری (توصیه شده)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### روش ۲: نصب در سطح پروژه

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## پیکربندی

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "permission": {
    "skill": {
      "project-planner": "allow"
    }
  }
}
```

## گردش کار

درخواست کاربر → شناسایی وظیفه تولید کد → صرف‌نظر از برنامه‌ریزی؟ → طبقه‌بندی دامنه → تحلیل نیازمندی‌ها → طراحی فنی → تفکیک وظایف → اجرای وظیفه‌محور

خروجی‌ها: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## سازگاری

فایل‌های پیکربندی سایر افزونه‌ها شامل `.vscode/`، `.cursor/`، `.continue/`، `.github/`، `.idea/` را تغییر نمی‌دهد.

## مجوز

MIT
