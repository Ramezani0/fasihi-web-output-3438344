# Fasihi CRM — بسته کامل برای ChatGPT / Engineering
**تاریخ:** 2026-09-11  
**PO:** امیرحسین رمضانی  
**نمایندگی:** بیمه کارآفرین کد **۳۰۴۵** — خانم فاطمه فصیحی  
**سورس CRM:** https://github.com/Ramezani0/fasihi-crm (ریپوی اصلی؛ visibility را PO از Settings عوض می‌کند)  
**بریف Public (بدون لاگین):** https://github.com/Ramezani0/fasihi-web-output-3438344  
**Release tarball UI:** https://github.com/Ramezani0/fasihi-crm/releases/tag/web-output-3438344

این سند همان چیزی است که باید به ChatGPT بدهی: محصول، استک، داده، قفل‌ها، هویت بصری، استقرار، و فایل بیلد.

---

## ۱) این Release چیست

Nitro / TanStack Start production `.output` برای دیپلوی UI روی VPS.

| فیلد | مقدار |
|--|--|
| فایل | `fasihi-web-output-3438344.tar.gz` |
| تگ | `web-output-3438344` |
| Commit | `34383440e33c82efcd2ede61441b6dbbf6ce77c4` (`main`) — `ui: پرداخت بصری زمرد/طلا — پک branded lux در public/assets/lux` |
| Rebase روی | `2510e704` (Outlet + slim `/api/customers` + `/api/policies/lite`) |
| حجم | **25783738** بایت |
| SHA-256 | `d0ef5060b1351fcd652a638685691c500fe5046f95c1bd622681ed519cb3e72f` |
| ورود سرور | `.output/server/index.mjs` |
| Nitro | `NITRO_PRESET=bun bun run build` — بدون این preset بیلد `cloudflare-module` می‌شود و روی `$PORT` گوش نمی‌دهد |
| بیلد | `bun install --frozen-lockfile` سپس `NITRO_PRESET=bun bun run build` |

**دانلود tarball:**  
https://github.com/Ramezani0/fasihi-crm/releases/download/web-output-3438344/fasihi-web-output-3438344.tar.gz  
اگر ریپوی `fasihi-crm` هنوز Private باشد این URL لاگین/`gh` می‌خواهد. بریف کامل بدون لاگین اینجاست:  
https://raw.githubusercontent.com/Ramezani0/fasihi-web-output-3438344/main/FASIHI_CRM_CHATGPT_BRIEF.md

**checksum sidecar:**  
https://github.com/Ramezani0/fasihi-crm/releases/download/web-output-3438344/fasihi-web-output-3438344.sha256

```bash
curl -fsSL -o fasihi-web-output-3438344.tar.gz \
  https://github.com/Ramezani0/fasihi-crm/releases/download/web-output-3438344/fasihi-web-output-3438344.tar.gz
test "$(stat -c '%s' fasihi-web-output-3438344.tar.gz)" = 25783738
echo 'd0ef5060b1351fcd652a638685691c500fe5046f95c1bd622681ed519cb3e72f  fasihi-web-output-3438344.tar.gz' | sha256sum -c
```

یا:

```bash
gh release download web-output-3438344 --repo Ramezani0/fasihi-crm --pattern 'fasihi-web-output-3438344.tar.gz'
```

**فقط فرانت.** از این tarball جایگزین نکن: `vps/app.py`، Postgres، یا Caddyfile. API زنده را از `2510e70` نگه دار. دیپلوی خودکار نشده. DB را wipe نکن.

استخراج از `/opt/fasihi/web`. داخل آرشیو: `.output/...`  
برند: `.output/public/brand/` (`karafarin-256.png`, `karafarin-logo.png`)  
لوکس: `.output/public/assets/lux/` — ۲۲ PNG stamped؛ بج = لوگو + رقم `3045` فقط.

---

## ۲) محصول

**CRM فصیحی** — سامانه فارسی RTL مدیریت مشتریان، بیمه‌نامه‌ها و اقساط برای نمایندگی ۳۰۴۵ بیمه کارآفرین.

- دامنه تولید: https://www.fasihicrm.ir
- دمو Lovable (قدیمی‌تر): https://fasihi-crm.lovable.app
- Lovable project: `b03d0b17-2002-4c2d-a2ca-9ecb7d4b9b9c`
- Latest known Lovable commit: `1f166b9f`
- سورس: partial frontend export از Lovable (~80 فایل؛ کامل در برابر ~107 نیست) + API پایتون روی VPS

**عنوان:** CRM فصیحی  
**زیرعنوان:** مدیریت هوشمند بیمه‌نامه، اقساط و مشتریان — نمایندگی ۳۰۴۵ بیمه کارآفرین  
**فوتر:** نمایندگی بیمه کارآفرین کد ۳۰۴۵ — خانم فاطمه فصیحی | CRM فصیحی  
**تگ‌لاین:** اقساط معوق، یادآوری تمدید، گزارش مدیریتی

PO کارگزاری / شبکه فروش بیمه کارآفرین است؛ فقط دولوپر نیست.

---

## ۳) استک

| لایه | انتخاب |
|--|--|
| Frontend | TanStack Start + React 19 + Tailwind 4 + shadcn/ui + Bun |
| روت‌ها | `src/routes/` — `html[lang=fa][dir=rtl]` — فونت Vazirmatn |
| ۳D | Three.js + R3F + Drei — **فقط** ورود (`/`) و هیروی داشبورد |
| Backend | `vps/app.py` — stdlib HTTP + psycopg — `0.0.0.0:8088` |
| DB | Postgres 16 (`fasihi-db`) |
| Edge | Caddy — `/api/*` و `/data*` → API؛ `/` → web `:3000` |
| کانتینرها | `fasihi-caddy`, `fasihi-db` (127.0.0.1:5432), `fasihi-api` (:8088), `fasihi-web` (:3000, bun nitro) |

اجرای محلی:

```
bun install
cp .env.example .env
bun run dev
```

رمز دمو از `VITE_DEMO_PASSWORD`. اگر خالی باشد هر رمز غیرخالی برای `ceo` / `manager` / `sales` / `accounting` قبول است. **رمز را در گیت نگذار.** چیپ ورود فقط username است.

---

## ۴) ماژول‌ها

1. Dashboard — تمدید، معوق، KPI + هیرو ۳D  
2. مشتریان (بیمه‌گذاران)  
3. بیمه‌نامه‌ها  
4. اقساط / بدهی  
5. تمدید  
6. پایپلاین فروش  
7. گزارش‌ها  
8. کاربران / نقش‌ها (ceo, manager, sales, accounting)  
9. **پرونده ۳۶۵** — `/customers/$customerId`  
10. وظایف، اعلان‌ها، تنظیمات، حسابرسی (از export Lovable)

ثبت مشتری، پرداخت قسط، ورود CSV و تبدیل پایپلاین هنوز **در حافظه مرورگر** است (API نوشتنی برای CRM ندارد). SMS اسکلت است.

---

## ۵) FACT داده (۲۰۲۶-۰۹-۱۱) — این اعداد درست‌اند

| متریک | قبل از import ۱۸ فایل | بعد از فاز ۱–۷ |
|--|--|--|
| customers | 1352 | **1526** |
| policies | 3499 | **9446** |
| installments | 3112 | **27485** |

- `customers.legal_entity_id` هست (شناسه ۱۱رقمی حقوقی)
- `source_system` باید دقیق رشتهٔ `fasihicrm` باشد
- فاز ۸ (وصول کلی تجمیعی ~۳۴ ردیف) = **HOLD**
- ۱۸ فایل import شده؛ لود جدید لازم نیست
- تصمیم UL: آخرین نسخه per کد رایانه → policies (+2332)؛ همه ۱۲۷۰۹ تراکنش → تاریخچه اقساط/الحاقیه
- split ستون `نام-کدملی` قبل از ورود
- یکی از جفت تاخیر۷۰۰؛ یکی از پزشکان xlsx/csv
- بدون wipe / حذف کور؛ upsert با ON CONFLICT
- شناسه و موبایل string با صفر اول
- تلفن روی همه رکوردها اجباری نیست
- duplicate detection کور حذف نکند

UI فاز ۲ (`a5b5be8`): store از `GET /api/data`؛ اگر API نیاید mock. mutation هنوز local.

---

## ۶) زیرساخت

**VPS داده (بک‌آپ / میزبان قدیمی داده):** `95.38.182.128` — Ubuntu 24.04، ~1GB RAM، `/opt/fasihi`  
**VPS اعلام‌شده برای دامنه / باکس جدید:** `185.204.197.49` — SSH publickey-only  
اعتبار DB فقط روی VPS در `/opt/fasihi/db.env` (chmod 600) — **هرگز commit نشود.**

DNS (2026-09-11): `@` و `www` عمومی گاهی به `185.10.75.58` (cPanel 404) می‌روند. اپ وقتی Host به `95.38.182.128` بخورد سالم است. فیکس: Cloudflare A `@` + `www` = `95.38.182.128`، proxy **off**.

`vps/Caddyfile` در گیت ممکن است نسبت به `/opt/fasihi/Caddyfile` زنده کهنه باشد.

تاریخچه git را force-push / rebase / amend نکن — Lovable به گیت وصل است.

---

## ۷) قفل سخت — نقض = شکست

1. بدون wipe / TRUNCATE / حذف کور / re-import مگر PO صریحاً بگوید  
2. `source_system = fasihicrm`  
3. CSV: UTF-8-SIG؛ صفر اول موبایل اختراع یا حذف نشود  
4. اولویت: حفظ داده > پایداری > صحت > سرعت > UX > ظاهر  
5. اسرار، CSV خام مشتری، پسورد در گیت نیست  
6. ۳D فقط login + dashboard hero — جداول Three.js نگیرند  
7. `prefers-reduced-motion` / بدون WebGL → SVG/PNG ثابت  
8. RTL باید سریع بماند  
9. edit in place؛ اپ موازی نساز  
10. این tarball فقط UI است — API/DB/Caddy را از آن عوض نکن  

باگ‌های mapping شناخته‌شده را با wipe درست نکن: kind (سواری→شخص ثالث نمایشی؛ API گاهی kind ناشناس را `عمر و سرمایه‌گذاری` می‌کند)، `holder_name`، `computer_code`، شهر خالی = `—`، وضعیت فارسی.

---

## ۸) هویت بصری قفل‌شده (PO)

خواسته: زیباترین سایت CRM بیمه کارآفرین ایران — زمرد + طلا، نوشته طلایی، تم تیره/روشن، لوگوی رسمی همه‌جا.

| نقش | مقدار |
|--|--|
| زمرد رسمی | `#007440` |
| طلای لوگو | `#FCBC00` |
| عنوان تیره | `#E8C547` روی `#050806` |
| عنوان روشن | `#8F6E12` روی `#F4EFE0` |
| کارت تیره / روشن | `#121C16` / `#FFFCF4` |
| متن تیره / روشن | `#F3EAD2` / `#143322` |
| لوگو | `public/brand/karafarin-logo.png` |
| تم | `html.dark` / `html.light` — کلید `fasihi-theme` |

لوکس branded (۲۲ PNG در `public/assets/lux/`): بج گوشه = لوگو + رقم `3045` فقط؛ نه متن «کد ۳۰۴۵» و نه پنل تیره پشت بج. متن زنده UI با CSS (`title-extrude` / Vazirmatn) است.

۵ سطح ۳D سبک RTL-safe: login hero، dashboard KPI orbs، pipeline CSS funnel، dossier badge، insurance field cards. **جداول بدون canvas.**

---

## ۹) API (خلاصه)

Base URL مرورگر: `VITE_API_BASE_URL` (خالی = same-origin). هلپر: `src/lib/api.ts`. CORS GET/OPTIONS. `Cache-Control: no-store`.

- `GET /api/health` — liveness + counts  
- `GET /api/data` — snapshot برای store (customers / policies / installments + optional `legalEntityId`)  
- `GET /data` — HTML dump برای ops  
- `GET /api/sms/status` — اسکلت Iran Payamak (بدون راز)  
- `POST /api/sms/send` — stub؛ Postgres را لمس نمی‌کند  

اگر API قطع شود UI به `buildDemoData()` برمی‌گردد و کرش نمی‌کند.

فاز ۲ بعداً slim کرد: `/api/customers` fields + `/api/policies/lite` تا پرونده ۳۶۵ واقعاً رندر شود (`2510e70`, `#26`). gzip/timeout روی `/api/data` (`#21`).

---

## ۱۰) فازها و تاریخچه ساخت (هرچه گفته شد)

**Vision v2 (از صفر UI، داده بماند):**  
معماری + ۳D login/hero + ناوبری → وصل ماژول‌ها به `/api/*` → فیکس mapping + QA → DNS دامنه؛ مهاجرت اختیاری به 185.204 بعداً.

**کارهای انجام‌شده روی main (نمونه commit):**

- VISION-V2 از صفر UI، Postgres بماند  
- Agency 3045 briefing  
- Phase 1: شل ۳D، ناوبری، قرارداد API  
- Skip Three.js اگر WebGL نباشد  
- Restore role chips username-only  
- Phase 2: hydrate store از `GET /api/data` (`a5b5be8`)  
- بسته رسمی ۱۸ فایل import (1526/9446/27485)  
- هویت Karafarin emerald/gold + theme + 3D hero  
- پرونده ۳۶۵ + اسکلت SMS + ۵ سطح ۳D  
- seed قوانین بیمه برای ماژول دانش  
- fix `/api/data` timeout + gzip  
- enrich پرونده ۳۶۵ + SMS  
- dossier Outlet + slim customers API  
- slim `/api/customers` + policies/lite  
- **این بیلد:** پرداخت بصری زمرد/طلا — پک branded lux در `public/assets/lux` (`3438344`)

**گام‌های بعدی (از بریف‌ها):**

1. DNS `@`/`www` → میزبان سالم  
2. parity سورس Lovable (~80 → ~107) قبل از UI بزرگ  
3. mutation پایدار روی API (الان local)  
4. QA counts روی دامنه بدون reimport  
5. auth واقعی  
6. SMS یادآوری بعد از پایداری  
7. پرونده ۳۶۵: نمایش `legal_entity_id` + تاریخچه UL  
8. cutover به `185.204.197.49` فقط با دستور PO و کلید نصب‌شده  

---

## ۱۱) مسیر تحویل این فایل (FACT این agent)

Engineering نمی‌تواند artifact را از VM ایجنت Cursor خودکار بکشد.

1. Release asset از قبل روی تگ `web-output-3438344` بود (ریپو Private بود).  
2. دانلود با `gh release download` تأیید شد: size `25783738` و sha256 بالا.  
3. کپی VM: `/tmp/fasihi-web-output-3438344.tar.gz` (همان hash).  
4. کلید disposable ed25519 ساخته شد برای scp به `root@185.204.197.49:/tmp/fasihi-web-output-3438344.tar.gz` — **منتظر AUTHORIZED** تا DevOps pubkey را نصب کند. scp نشده.  
   Pubkey: `ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOqntH0PH8KQ7mF2ORWom3vsE8tnuGarFbTSiMQfxBjq`  
5. PO خواست لینک GitHub + تمام توضیحات ساخت CRM برای ChatGPT، و فایل Public شود.  
   - بریف کامل روی ریپوی Public گذاشته شد: https://github.com/Ramezani0/fasihi-web-output-3438344  
   - خود `fasihi-crm` را توکن ایجنت نتوانست Public کند (403 visibility). PO باید از GitHub → Settings → Danger zone → Change visibility → Public بزند تا لینک tarball بدون لاگین کار کند.

توکن GitHub / URL امضاشده را چاپ نکن.

---

## ۱۲) دستور به ChatGPT

تو مهندس ارشد Fasihi CRM هستی. اسکفلد جدید نساز. تاریخچه را force-push نکن.

1. tarball را از لینک Public بالا بگیر و sha256 را چک کن.  
2. فقط `.output` را روی `fasihi-web` بگذار؛ API/DB/Caddy را عوض نکن.  
3. منبع حقیقت کد: همین ریپو + `docs/CHATGPT_HANDOFF.md` + `AGENCY.md` + `CURSOR.md` + `VISION-V2.md` + `docs/ARCHITECTURE.md` + `docs/DESIGN_EMERALD_GOLD.md` + `docs/LUX_ART_PLACEMENT.md`.  
4. اگر اعداد بین فایل‌ها فرق داشت، FACT این سند و `docs/CHATGPT_HANDOFF.md` برنده است: **1526 / 9446 / 27485**.  
5. حدس را از FACT جدا بنویس. رمز نگذار. اگر نمی‌دانی بگو نمی‌دانم.
