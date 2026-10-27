# TouchDesigner + Claude Code

این ریپو Claude Code را با پلاگین رسمی [touchdesigner-mcp](https://github.com/8beeeaaat/touchdesigner-mcp) به TouchDesigner وصل می‌کند.
فایل `.claude/settings.json` بازارچهٔ `touchdesigner-mcp` و پلاگین `touchdesigner` را برای این پوشه فعال می‌کند.
پلاگین خودش سرور MCP را همراه دارد، پس `.mcp.json` جداگانه لازم نیست (و نباید اضافه شود).

## پیش‌نیازها

- TouchDesigner (نسخهٔ جدید)
- Node.js نسخهٔ 22.18 به بالا، 24.x یا 26 به بالا (نسخه‌های فرد مثل 23 و 25 پشتیبانی نمی‌شوند)
- Claude Code روی **همان کامپیوتری** که TouchDesigner روی آن اجرا می‌شود

## راه‌اندازی

1. فایل `touchdesigner-mcp-td.zip` را از
   [آخرین نسخه](https://github.com/8beeeaaat/touchdesigner-mcp/releases/latest/download/touchdesigner-mcp-td.zip)
   دانلود و از حالت فشرده خارج کنید. ساختار پوشه را تغییر ندهید.
2. فایل `mcp_webserver_base.tox` را داخل پروژهٔ TouchDesigner بکشید (مثلاً در `/project1`).
   WebServer DAT داخل آن باید روی `http://127.0.0.1:9981` روشن باشد.
3. این ریپو را روی کامپیوتر خودتان clone کنید و داخل پوشه‌اش `claude` را اجرا کنید.
4. پوشه را trust کنید و نصب بازارچه و پلاگین `touchdesigner` را تأیید کنید.
   اگر پیشنهادی نیامد، دستی نصب کنید:

   ```bash
   claude plugin marketplace add 8beeeaaat/touchdesigner-mcp
   claude plugin install touchdesigner@touchdesigner-mcp
   ```

5. یک جلسهٔ تازه باز کنید و `/touchdesigner:setup` را بزنید تا اتصال بررسی شود.

اگر می‌خواهید از اپ Claude Code (موبایل یا وب) کار کنید، داخل همین پوشه `claude remote-control` را اجرا کنید.

## دستورها

| دستور | کار |
|---|---|
| `/touchdesigner:launch [tox-path]` | اجرای TouchDesigner با کامپوننت MCP و صبر تا اتصال برقرار شود |
| `/touchdesigner:setup` | بررسی و تعمیر اتصال |
| `/touchdesigner:debug [node-path]` | بررسی خطاهای نودها |
| `/touchdesigner:snapshot [top-path]` | گرفتن تصویر از خروجی یک TOP |
| `/touchdesigner:overview [root-path]` | گزارش ساختار پروژه |
| `/touchdesigner:perf [root-path]` | اندازه‌گیری زمان cook و پیدا کردن کندترین نودها |

بقیه کارها را می‌توانید عادی بنویسید، مثلاً «یک noise TOP بساز و به level TOP وصل کن».

## تنظیمات

اگر TouchDesigner روی آدرس یا پورت دیگری است، موقع فعال شدن پلاگین مقدارش را وارد کنید، یا:

```bash
claude plugin install touchdesigner@touchdesigner-mcp \
  --config touchdesigner_host=http://192.168.1.100 \
  --config touchdesigner_port=9982
```

`touchdesigner_host` فقط پروتکل و نام میزبان است، بدون پورت و بدون `/` آخر.
بعد از تغییر تنظیمات `/reload-plugins` را بزنید یا جلسهٔ تازه باز کنید.

## رفع مشکل

| مشکل | بررسی |
|---|---|
| `get_td_info` خطا می‌دهد یا ابزارها timeout می‌شوند | TouchDesigner باز است؟ `.tox` وارد شده؟ WebServer DAT روی پورت درست روشن است؟ `/touchdesigner:setup` را بزنید |
| ابزارها در `/mcp` نیستند | بعد از فعال کردن پلاگین، Claude Code را دوباره باز کنید؛ ببینید `npx` به npm دسترسی دارد |
| تصویر snapshot سیاه است | خطای نودهای بالادست (`/touchdesigner:debug`) یا رزولوشن صفر TOP |
