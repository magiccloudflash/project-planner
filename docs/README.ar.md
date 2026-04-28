# Project Planner — مهارة ذكاء اصطناعي لـ OpenCode

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** هي مهارة لعامل OpenCode تفرض عملية تخطيط احترافية للمشروع قبل إنشاء الكود، مما يضمن تحليل المتطلبات وتصميم البنية وتقسيم المهام وتتبع التقدم.

## الميزات

- **تخطيط إلزامي** — أي مهمة إنشاء كود يجب أن تمر بالتخطيط أولاً، إلا إذا تجاوزها المستخدم صراحةً
- **تصنيف المجال** — التعرف التلقائي على نوع المشروع (Web/CLI/Library/Mobile) مع تطبيق أفضل الممارسات المقابلة
- **تحليل المتطلبات** — 14 بُعداً لتوضيح المتطلبات + ثلاثة مستويات للأولوية (P0/P1/P2)
- **تقييم المخاطر** — تحديد وتصنيف واستراتيجيات تخفيف لـ 6 فئات من المخاطر
- **تصميم البنية** — رسم تخطيطي للطبقات ASCII + نموذج بيانات + عقود API
- **تقسيم المهام** — رسم بياني للتبعيات + المسار الحرج + تقدير الوقت
- **تتبع التقدم** — تسجيل كل خطوة + ملخص المراحل الرئيسية
- **صفر تعارض** — لا يعدل ملفات تكوين الإضافات الأخرى للبيئة التطويرية

## التثبيت

### الطريقة 1: التثبيت العام (موصى به)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### الطريقة 2: التثبيت على مستوى المشروع

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## الإعدادات

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

## سير العمل

طلب المستخدم → تحديد مهمة إنشاء الكود → تجاوز التخطيط؟ → تصنيف المجال → تحليل المتطلبات → التصميم الفني → تقسيم المهام → التنفيذ حسب المهمة

الملفات: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## التوافق

لا يعدل ملفات تكوين الإضافات الأخرى `.vscode/`، `.cursor/`، `.continue/`، `.github/`، `.idea/`.

## الترخيص

MIT
