# Project Planner — OpenCode کے لیے AI اسکل

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

**project-planner** ایک OpenCode Agent اسکل ہے جو کوڈ جنریشن سے پہلے پیشہ ورانہ منصوبہ بندی کے عمل کو لازمی قرار دیتا ہے، جس سے ضروریات کے تجزیہ، آرکیٹیکچر ڈیزائن، کاموں کی تقسیم اور پیشرفت کی نگرانی کو یقینی بنایا جاتا ہے۔

## خصوصیات

- **لازمی منصوبہ بندی** — کوڈ جنریشن کے کسی بھی کام کو پہلے منصوبہ بندی سے گزرنا ہوگا، جب تک کہ صارف واضح طور پر اسے چھوڑ نہ دے
- **ڈومین کی درجہ‌بندی** — پروجیکٹ کی قسم کی خودکار شناخت (Web/CLI/Library/Mobile) اور متعلقہ بہترین طریقوں کا اطلاق
- **ضروریات کا تجزیہ** — 14 جہتوں میں ضروریات کی وضاحت + ترجیح کی تین سطحیں (P0/P1/P2)
- **خطرے کی تشخیص** — 6 اقسام کے خطرات کی شناخت، درجہ‌بندی اور تخفیف کی حکمت عملی
- **آرکیٹیکچر ڈیزائن** — ASCII پرت‌بندی خاکہ + ڈیٹا ماڈل + API معاہدے
- **کاموں کی تقسیم** — انحصار گراف + اہم راستہ + وقت کا تخمینہ
- **پیشرفت کی نگرانی** — ہر مرحلے کی ریکارڈنگ + سنگ میل کا خلاصہ
- **صفر تنازع** — دیگر IDE پلگ انز کی کنفیگریشن فائلیں تبدیل نہیں کرتا

## تنصیب

### طریقہ 1: عالمی تنصیب (تجویز کردہ)

```bash
# Windows PowerShell
Copy-Item -Path "path/to/project-planner" -Destination "$env:USERPROFILE\.config\opencode\skills\project-planner" -Recurse

# macOS / Linux
cp -r ./project-planner ~/.config/opencode/skills/project-planner
```

### طریقہ 2: پروجیکٹ کی سطح پر تنصیب

```bash
mkdir -p .opencode/skills
cp -r path/to/project-planner .opencode/skills/project-planner
```

## ترتیبات

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

## کام کا طریقہ کار

صارف کی درخواست → کوڈ جنریشن کے کام کی شناخت → منصوبہ‌بندی چھوڑیں؟ → ڈومین کی درجہ‌بندی → ضروریات کا تجزیہ → تکنیکی ڈیزائن → کاموں کی تقسیم → کام کے مطابق عملدرآمد

پیداوار: `memory/project-planner/plan.md` → `design.md` → `tasks.md` → `progress.md`

## مطابقت

دیگر پلگ انز کی `.vscode/`، `.cursor/`، `.continue/`، `.github/`، `.idea/` کنفیگریشن فائلوں میں ترمیم نہیں کرتا۔

## لائسنس

MIT
