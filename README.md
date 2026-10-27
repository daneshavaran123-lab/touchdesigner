# TouchDesigner + Claude Code

این ریپو Claude Code را از طریق [touchdesigner-mcp](https://github.com/8beeeaaat/touchdesigner-mcp) به TouchDesigner وصل می‌کند.
فایل `.mcp.json` سرور MCP را برای همین پوشه تعریف می‌کند.

## پیش‌نیازها

- TouchDesigner (نسخهٔ جدید)
- Node.js نسخهٔ 22.18 به بالا، 24.x یا 26 به بالا (نسخه‌های فرد مثل 23 و 25 پشتیبانی نمی‌شوند)
- Claude Code روی **همان کامپیوتری** که TouchDesigner روی آن اجرا می‌شود

## راه‌اندازی

1. فایل `touchdesigner-mcp-td.zip` را از
   [آخرین نسخه](https://github.com/8beeeaaat/touchdesigner-mcp/releases/latest/download/touchdesigner-mcp-td.zip)
   دانلود و از حالت فشرده خارج کنید. ساختار پوشه را تغییر ندهید.
2. فایل `mcp_webserver_base.tox` را داخل پروژهٔ TouchDesigner بکشید (مثلاً در `/project1/mcp_webserver_base`).
3. مطمئن شوید WebServer DAT داخل آن روشن است. پورت پیش‌فرض `9981` است.
   برای دیدن لاگ‌ها Textport را باز کنید (`Alt+T`).
4. این ریپو را روی کامپیوتر خودتان clone کنید و داخل پوشه‌اش `claude` را اجرا کنید.
   Claude Code سرور `touchdesigner` را از `.mcp.json` پیشنهاد می‌دهد؛ آن را تأیید کنید.
5. با دستور `/mcp` بررسی کنید که سرور `touchdesigner` وصل شده است.

اگر می‌خواهید از اپ Claude Code (موبایل یا وب) کار کنید، داخل همین پوشه `claude remote-control` را اجرا کنید.

## نکته‌ها

- **ویندوز:** اگر سرور وصل نشد، در `.mcp.json` مقدار `command` را `cmd` بگذارید و `"/c", "npx"` را به اول `args` اضافه کنید.
- اگر TouchDesigner روی پورت یا آدرس دیگری است، مقدار `--host` و `--port` را در `.mcp.json` عوض کنید.
- اگر اتصال قطع شود، کلاینت خطا را ۶۰ ثانیه نگه می‌دارد و بعد دوباره امتحان می‌کند.

## ابزارهایی که Claude در دسترس دارد

ساخت و حذف نود (`create_td_node`، `delete_td_node`)، خواندن و تغییر پارامترها
(`get_td_node_parameters`، `update_td_node_parameters`)، فهرست نودها (`get_td_nodes`)،
اجرای پایتون داخل TouchDesigner (`execute_python_script`)، بررسی خطاها (`get_td_node_errors`)،
گرفتن تصویر از TOPها (`get_top_image`) و ابزارهای دیگر.
