# Ganakah — calculators and converters (Android and iPhone)

One Expo (React Native) project builds the Android app and the iPhone app. No server and no login. Everything is worked out on the phone and saved on the phone; the only thing that goes online is the currency converter, to fetch exchange rates (it falls back to saved rates when offline).

**10 languages:** English, தமிழ், हिन्दी, తెలుగు, മലയാളം, ಕನ್ನಡ, मराठी, ગુજરાતી, ଓଡ଼ିଆ, বাংলা — pick one with the 🌐 button on Home or in Settings.

## What is in the app

**Main calculators**

| Tool | What it does |
|---|---|
| Calculator | + − × ÷, shop-style % (200+10% = 220), ±, memory (MC MR M+ M−), GT (grand total of every = result; long-press to clear), history, Copy. **+ GST / − GST keys** with a rate row (5, 18, 40% first, then 0.25, 1.5, 3%): shows taxable value, CGST, SGST and total. Amount in words under every result. |
| Scientific | sin cos tan and inverses, sinh cosh tanh, log, ln, log₂, 10ˣ, eˣ, x², x³, xʸ, √, ∛, ʸ√x, n!, nCr, nPr, mod, 1/x, \|x\|, π, e, Ans, brackets, DEG/RAD/GRAD, history. Clear errors such as "Cannot divide by 0". |
| GST HSN Finder | Search 21,935 HSN and 681 SAC codes by code (8471, 8471 30 10) or words (laptop, hotel room, retreaded tyre), with All / Goods / Services filters. Each code shows its GST rate with CGST / SGST / IGST, the other rates and conditions under the same code, notification basis, RCM note and the 01-11-2026 change; badges for "Check conditions", RCM and changed codes; breadcrumb to chapter and heading; copy, share, star, recent searches; quick add / remove GST on any amount. A code not in the list shows the nearest heading and the residual 18% entry. |
| Income tax | Two tabs, like the e-filing portal's calculator. **Basic:** year, taxpayer, residential status, age, total taxable income as per the new regime, old-regime-only exemptions and Chapter VI-A deductions; the old-regime income is worked out. **Advanced:** income head by head, as below. **Matches the Income Tax Department's own calculator** for salary and slab cases (checked on 53 cases, see below). Individual or HUF; resident, RNOR or non-resident (no rebate or senior slabs for non-residents). Business and profession separately, from books or presumptive 44AD (6% / 8%) and 44ADA (50%) with turnover limits; let-out house property (municipal tax, 30% standard deduction, loan interest, ₹2L loss set-off in old regime, none in new); other sources split into savings interest, FD/RD interest, dividends, family pension (one-third up to ₹15,000 / ₹25,000) and other income. Tax Year 2026-27 (Income-tax Act 2025 — rebate shown as s.156, standard deduction as s.19(1)), FY 2025-26 and FY 2024-25. New vs old regime side by side with the saving, age groups, standard deduction, 80C, 80CCD(1B), 80D, 80TTA/TTB, HRA, home-loan interest, professional tax, employer NPS, rebate with marginal relief, surcharge with marginal relief, 4% cess, slab working. |

**Mutual funds & investing:** SIP (step-up, year-by-year table), SWP (monthly withdrawal, how long the money lasts, safe withdrawal amount), goal planner (SIP needed for a target, with inflation and existing savings), lump sum, CAGR, XIRR (real return from your own dated investments), MF capital gains tax (equity, debt bought on/after 1 Apr 2023, gold/international), PPF (default 7.1%), inflation, **NPS** (corpus, maximum lump sum and minimum annuity under the PFRDA exit rules as amended 16-12-2025 — 80/20 for All Citizen / Corporate, 60/40 for Government, full withdrawal up to ₹8 lakh — and monthly pension), **EPF** (12% + 12% with the EPS share on wages up to ₹25,000 from 17-09-2026, interest 8.25% on the monthly running balance, year-by-year table), **Sukanya Samriddhi** (default 8.2%, 15 years of deposits, maturity at 21 years, year-by-year table), **Retirement** (corpus needed for inflation-linked expenses, monthly SIP needed).

**Money:** Loan EMI with three tabs — Personal loan, Home loan (property value and down payment, RBI loan-to-value check, year-1 interest and principal for the old-regime deductions) and Car loan (on-road price and down payment) — each with an optional processing fee plus 18% GST, the amount you receive, the effective rate with the fee, and a year-by-year table; fixed deposit, recurring deposit, simple interest (rate per year or per month), percentage, discount, profit & margin, gold & jewellery price, HRA exemption, amount in words (lakh/crore or million), bill split & tip, which pack is cheaper.

**Unit converter:** 💱 **live currency** (166 currencies, rates updated daily from ExchangeRate-API with the ECB as backup, search any currency, swap, works offline with the last saved rates); length; area & land (cent, ground, ankanam, guntha, acre, hectare, sq ft, sq yard…); weight (tola, sovereign, quintal…); volume; temperature; speed; time; data; pressure (psi, bar); energy (kWh); power (hp, AC ton); fuel economy; angle. Shows the value in every unit at once; tap a row to convert from it.

**Everyday:** age (exact, next birthday), days between dates (inclusive option, working days), add or subtract days/months/years (due dates), BMI, trip fuel cost, total & average of a list, number systems (binary, octal, hex, Roman).

Home screen: search (works in English and in the chosen language), long-press any tool to add it to Favourites. The **☰ menu** (top-right) opens Settings, grouped like a phone settings page: an app card with the version; **Preferences** — Language (its own page: 10 languages) and Theme (its own page: Same as phone / Light / Dark and 7 colour themes — Ink blue, Ledger green, Maroon, Peacock teal, Saffron, Violet, Graphite); **Saved on this phone** — clear calculator history, clear favourites (tap twice to confirm); **About** — privacy, data sources, disclaimer and version.

```
ganakah/
  App.js                 screens and the Back button
  src/logic/             the calculations (no app code; tested by test/logic.test.js)
    expr.js              calculator expression reader (no eval)
    gst.js               GST add / remove, CGST / SGST / IGST split
    hsn.js               HSN/SAC search, lookup, conditions, CGST/SGST split
  src/data/hsn.json      HSN/SAC rate master, generated by npm run hsn (do not edit)
  data/HSN_SAC_GST_Rates.xlsx   the master in Excel (source of hsn.json)
  scripts/build-hsn.mjs  Excel -> src/data/hsn.json
    incomeTax.js         slabs, rebate, surcharge, cess, HRA — one table per year
    capitalGains.js      mutual fund capital gains (s.111A, 112A, 112, 50AA)
    currency.js          live rates (fetch + backup), bundled rates for offline use
    units.js finance.js dates.js numberWords.js format.js
  src/tools/simpleTools.js   every form-style tool (EMI, SIP, age…) in one list
  src/screens/           Home, Calculator, Scientific, GST, Income tax, Unit converter, Settings, FormTool
  src/theme.js           colour themes (add one by copying an entry in THEMES)
  src/i18n/              languages: one file per language (ta.js, hi.js…), English text is the key
  scripts/i18n-keys.mjs  lists every string; --missing shows what is not translated yet
  test/logic.test.js     306 checks
```

## 1. Run the tests (no install needed)

Needs Node.js 20.10 or newer.

```bash
cd ganakah
npm test
```

You should see **306 passed, 0 failed**.

## 2. Try it on your phone

```bash
cd ganakah
npm run setup        # installs Expo and the matching package versions (once)
npm start            # expo start --dev-client
```

Testing uses the **development build "Ganakah (dev)"**, not Expo Go. Make it once (and again after any native change: a package with native code, `app.json` plugins, permissions, icon, splash, name or app ID):

```bash
eas build -p android --profile development
```

Install the APK from the link EAS shows, open it, and scan the QR code from `npm start` (phone and computer on the same Wi-Fi). Screen, logic and translation changes load without a rebuild. `npm run start:go` still opens the app in Expo Go for a quick look, as long as no native package outside Expo Go is added. `npm run web` opens it in the browser.

EAS profiles (`eas.json`): **development** (dev client, APK), **preview** (APK for testers), **production** (AAB for Google Play, build number raised by EAS; `appVersionSource: remote`).

## 3. Build the real apps

```bash
npm install -g eas-cli
eas login
eas init
```

Before the first build, check the app IDs and icons in **Publishing** below.

- **Android test APK:** `eas build -p android --profile preview`, then install the APK on any Android phone.
- **Google Play:** `eas build -p android --profile production`, then `eas submit -p android`. A new personal developer account must run a closed test (12+ testers, 14 days) before the public listing.
- **App Store:** `eas build -p ios --profile production`, then `eas submit -p ios` (Apple Developer Program membership).

The app collects no personal data and has no permissions, so the privacy policy can say exactly that.

## Publishing

| Item | Value |
|---|---|
| Android package | `in.saraswathytaxedge.ganakah` |
| iOS bundle identifier | `in.saraswathytaxedge.ganakah` |
| Version | 1.4.0 (`app.json` and `package.json`; EAS raises the build number by itself) |
| Privacy policy | https://apps.saraswathytaxedge.com/ganakah/privacy.html |
| Support | support@saraswathytaxedge.com (support URL for Apple: https://apps.saraswathytaxedge.com/) |

The app IDs can **never change** after the first upload to either store. The links shown in the app are kept in one file, `src/links.js`.

**Icons.** `assets/icon.svg` is the master (navy #041853 ground, red double ledger rule, white ₹ drawn as paths, 2×2 keys in red, white, green and grey; the script reads the background colour from it). After changing it, run:

```bash
npm run icons
```

`scripts/make-icons.mjs` (dev-only package `@resvg/resvg-js`) writes `assets/icon.png` (1024, no transparency), `assets/adaptive-icon.png` (foreground inside the centre 66%), `assets/splash-icon.png`, `assets/favicon.png` (48), plus `site/favicon.png` and `site/ganakah/icon.png` for the website, and the Google Play feature graphics `store/feature-graphic-en.png` and `store/feature-graphic-ta.png` (1024×500). The feature graphics have text, so the script draws them with headless Chrome or Edge (resvg cannot shape Tamil); if neither is installed it skips them with a warning. `icon.png` and the feature graphics are written without an alpha channel, as the stores require. If you change the background colour in `icon.svg`, change the two `#041853` values in `app.json` too.

**Splash screen.** Set in `app.json` under the `expo-splash-screen` plugin: `assets/splash-icon.png`, 200 px wide, on `#041853` in light and dark mode. Expo Go shows its own splash; the real one appears in the development, preview and production builds.

**Store texts.** `store/listing-en.md` and `store/listing-ta.md`: names, descriptions with character counts, the 8 screenshots to take, the category, and the Play Console and App Store Connect answers.

**Privacy website (GitHub Pages).** The `site/` folder is the whole website:

1. On GitHub, create (or open) the **public** repository `saraswathytaxedge/apps-site`.
2. Copy everything inside `site/` (`index.html`, `CNAME`, `favicon.png`, the `ganakah/` folder) to the root of that repository and push to `main`.
3. In that repository: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main`, folder `/ (root)` → Save.**
4. Same page, **Custom domain:** `apps.saraswathytaxedge.com` → Save. (The `CNAME` file already holds it.)
5. At your domain provider, in the DNS records for `saraswathytaxedge.com`, add: **Type `CNAME`, Name/Host `apps`, Value/Target `saraswathytaxedge.github.io`** (TTL default). Do not add A records for `apps`.
6. Wait until GitHub's DNS check on the Pages screen turns green (minutes to a few hours), then tick **Enforce HTTPS**.
7. Open https://apps.saraswathytaxedge.com/ganakah/privacy.html on the phone and check that both English and தமிழ் show.

When the privacy text changes, edit `site/ganakah/privacy.html` here, change the effective date, and copy it to `apps-site` again.

## GST HSN Finder

**Source:** `data/HSN_SAC_GST_Rates.xlsx`, the owner's HSN/SAC master, **as on 01-11-2026** (Notes sheet, line 1). Sheets `HSN_MSTR` (21,935 codes; 4,093 need a condition check; 93 changed on 01-11-2026) and `SAC_MSTR` (681 codes; 280 need a check; 16 changed). The Notes sheet lists the notifications applied: goods 9/2025-CT(R) as amended, Nil 10/2025-CT(R) as amended by 03/2026, services 11/2017 and 12/2017-CT(R) as amended, and RCM 4/2017, 13/2017 and 17/2017-CT(R) as amended.

The app never reads the Excel. `npm run hsn` (`scripts/build-hsn.mjs`) reads both sheets by header name and checks the counts against the Summary in the Notes sheet. It then writes `src/data/hsn.json` (about 1.9 MB, loaded only when the finder opens). Descriptions, conditions and notification text are shown in English, as in the official list.

The build corrects and lists 7 codes in the current Excel: "2307 00" and "2514 00" (spaces), and 30559, 3074330, 40210, 5119110 and 90121 (lost leading zero). Each is a duplicate of a correctly typed row with the same rate. Fixing them in the Excel is recommended.

**How to update** (after a CBIC rate notification): replace `data/HSN_SAC_GST_Rates.xlsx` with the new master (same column headers; update Notes line 1 and the Summary), then run, one per line:

```bash
npm install
npm run hsn
npm test
```

`npm run hsn` stops with an error if a header is missing or renamed, or if the counts differ from the Summary. Never edit `src/data/hsn.json` by hand.

## Updating tax rates each year

All rates are in one table at the top of `src/logic/incomeTax.js` (`TAX_YEARS`). After each Budget, add a new year at the top of the list, copy the slabs, rebate and standard deduction from incometax.gov.in, add a test for it in `test/logic.test.js`, and run `npm test`. GST rates are the lists at the top of `src/logic/gst.js`. Capital gains rates are at the top of `src/logic/capitalGains.js`. The PPF rate is a default in the PPF tool (`src/tools/simpleTools.js`); the government reviews it every quarter (7.1% for Oct–Dec 2026). Sukanya Samriddhi (`SSY_RULES`, 8.2%), EPF (`EPF_RULES`: 8.25%, wage ceiling ₹25,000) and the NPS exit split (`NPS_RULES`) are at the end of `src/logic/finance.js`, each with its source and date.

**Checked against the official calculator (11 Nov 2026).** The Income & Tax Calculator on the e-filing portal (eportal.incometax.gov.in, Income Tax Act 2025, Tax Year 2026-27) gave exactly the same tax as the app in all 53 cases tried:

| Case | Portal | App |
|---|---|---|
| New regime, income ₹5L–₹6Cr (12 levels), Basic Calculator | same | same |
| New regime ₹12.5L (marginal relief on rebate, Advanced Calculator) | ₹52,000 | ₹52,000 |
| New regime ₹12.1L / ₹13L | ₹10,400 / ₹78,000 | same |
| New regime ₹51L / ₹1.02Cr / ₹2.05Cr / ₹5.1Cr (surcharge relief) | ₹12,27,200 / ₹31,57,440 / ₹71,93,680 / ₹1,93,44,000 | same |
| Old regime, below 60 / 60–79 / 80+, five income levels each | e.g. ₹10L: ₹1,17,000 / ₹1,14,400 / ₹1,04,000 | same |
| Salary with standard deduction: new ₹12.75L, ₹13L, ₹18L; old ₹10L, ₹5.5L | ₹0, ₹26,000, ₹1,50,800; ₹1,06,600, ₹0 | same |

**Added later — not yet checked on the portal (fill in the Portal column after checking, Tax Year 2026-27, resident individual below 60 unless stated):**

| Case | Portal | App |
|---|---|---|
| Rent ₹12L, old regime (30% standard deduction → ₹8.4L) | | ₹83,720 |
| Salary ₹10L + let-out house: rent ₹1.2L, interest ₹5L, old regime (loss set off only ₹2L) | | ₹65,000 |
| Same, new regime (house property loss not set off) | | ₹0 (total income ₹9,25,000) |
| 44AD: ₹1Cr by bank + ₹10L cash, old regime (income ₹6.8L) | | ₹50,440 |
| 44ADA: ₹40L receipts, new regime (income ₹20L) | | ₹2,08,000 |
| HUF, other income ₹7L, new regime (no rebate) | | ₹15,600 |
| Non-resident, other income ₹12L, new regime (no rebate) | | ₹62,400 |
| Non-resident aged 60–79, ₹5L, old regime (no senior slab, no rebate) | | ₹13,000 |
| Basic tab: new-regime income ₹7,50,000, nothing else (old regime income ₹7,50,000) | | new ₹0, old ₹65,000 |
| Basic tab: new-regime income ₹13,00,000, exemptions ₹2,00,000, VI-A ₹1,50,000 (old ₹9,50,000) | | new ₹78,000, old ₹1,06,600 |

The portal's Basic Calculator says it skips marginal relief; the Advanced Calculator includes it inside "Rebate u/s 156", which is how the app shows it too. Rates were first taken from incometax.gov.in ("Salaried Individuals for AY 2026-27") on 10 Nov 2026. Budget 2026 did not change the slabs, so Tax Year 2026-27 uses the same figures. From Tax Year 2026-27 the Income-tax Rules 2026 give 50% HRA in eight cities (Delhi, Mumbai, Kolkata, Chennai, Bengaluru, Hyderabad, Pune, Ahmedabad); earlier years use the four metros.

## Languages

Every piece of text goes through `tr('English text')`. Each language file in `src/i18n/` maps the English text to the translation; anything missing simply shows in English, so the app never breaks.

- Check coverage: `node scripts/i18n-keys.mjs --missing` (add `-v` to list the missing strings). Right now every language has all strings except SIP, SWP, XIRR, CAGR, BMI, PPF, GST, X and Y, which stay in English on purpose.
- Tax and finance short forms (GST, CGST, TDS, EMI, NPS, HRA, LTCG, section numbers) and unit names (km, acre, cent…) are kept in English, the way people use them on bills and forms.
- Amount in words stays in English ("Rupees … Only") because that is what cheques and invoices use.
- `npm test` checks that every translation keeps the same `{placeholders}` as the English text.
- The translations were written by Claude. **Ask a native speaker to read through each language before publishing**, especially the tax screen.

## Live currency rates

- Main source: ExchangeRate-API open access (`open.er-api.com`, no key, 166 currencies, updates once a day). Its terms ask for the credit link "Rates by Exchange Rate API", which the currency screen shows.
- Backup: Frankfurter (`api.frankfurter.dev`, European Central Bank rates, about 30 currencies). Used only if the main source fails; currencies it lacks keep their last saved rate.
- The app refreshes when the screen opens and the rates are more than 6 hours old, or when you press Refresh. With no internet it shows the last saved rates and says from when. Today's rates (11 Nov 2026, 1 USD = ₹93.96) are bundled so it works even on first launch offline.
- These are mid-market reference rates. Banks and cards add a margin, and the screen says so.

## Hand test before you build

1. **Calculator:** 1200 + 10 % = → 1,320. Press **+ GST 18%** → 1,557.60 with CGST ₹118.80 and SGST ₹118.80. Type 1180, press **− GST 18%** → 1,000. Open History.
2. **Scientific:** sin(30) = 0.5 in DEG; switch to RAD and check sin(π÷2) = 1. nCr(5,2) = 10. 2 ÷ 0 shows "Cannot divide by 0".
3. **GST HSN Finder:** search 8471 30 10 → 18%; open it, type 1,000 → total ₹1,180 (CGST ₹90 + SGST ₹90); search isabgol → Nil with the 01-11-2026 change note.
4. **Income tax:** salary 13,00,000 → new regime ₹26,000 (marginal relief). Other income 51,00,000 → new regime ₹12,27,200 (surcharge relief ₹41,000). Compare one real client computation with the department's calculator.
5. **Units:** 1 acre = 100 cent; 1 ground = 2,400 sq ft.
6. **Everyday:** your own date of birth in Age; 04-08-2026 + 30 days = 03-09-2026.
7. **Mutual funds:** SWP with ₹20 lakh, ₹15,000 a month, 8%, 15 years (press Try an example) and check the year table. MF capital gains example: equity bought 15-03-2024, sold 10-11-2026, ₹4,00,000 → ₹6,20,000 gives tax ₹12,350. XIRR with one of your own fund statements against the XIRR shown by your fund house or CAS.
8. **Themes:** 🎨 Theme → pick each colour theme in light and dark; reopen the app and check the choice is kept.
9. **Currency:** open 💱 Currency (live) with internet on: the "Rates updated" time should be today. Turn on flight mode, reopen: it should say "No internet" and still convert. Search "dirham", pick AED, press ⇄.
10. **Languages:** 🌐 → pick each language; open Calculator, GST, Income tax and Currency and check nothing is cut off. Reopen the app and check the language is kept.
11. Android: the phone's Back button goes back one screen. Turn on dark mode in the phone and check the app follows (Auto).

## What was tested

- `npm test`: live currency (parsing both sources, fallback to the backup, offline, cross rates), translations (same placeholders in every language), SWP, goal SIP, CAGR, XIRR, PPF, inflation, MF capital gains (equity long/short, the 12-month edge, debt at slab, gold fund), expression reader (order of operations, %, brackets, trig in degrees, errors), Indian number formatting, GST add/remove/invoice, income tax for all three years (rebate, marginal relief, surcharge relief, senior slabs, deduction caps), HRA, units, EMI, SIP, FD, RD, dates, number to words, and every form tool with its example values.
- Every screen was clicked through in a headless browser, and Home, Income tax, Currency and Calculator were screenshotted in all 10 languages with web stand-ins for the phone parts: all checks above passed, no errors. **Not yet run in Expo Go or on a real phone**; expect small layout fixes on the first run.
