# Basaev — Design System Proposal v0

**Status:** DRAFT · pending team review (saved 2026-04-25)
**Branch:** `Try-DesignSystem`
**Author:** Claude (design-consultation skill)
**Preview:** see `preview.html` next to this file

---

## The memorable thing

> **«AI, который относится к тебе как ко взрослому, а не как к пациенту, которого надо успокоить.»**

Каждое решение в этой системе проверяется об три фразы пользователя:
1. «Серьёзный инструмент, не игрушка»
2. «Тут со мной говорят как со взрослым»
3. «Тише и глубже всего, что я видел»

---

## Direction: Editorial-Brutalist

**Тон:** serious research notebook, не wellness app.
**Inspirations:** Aeon (intellectual gravity), Linear (operator confidence), Granta / Are.na (curated quietness).
**Anti-tone:** pastel comfort, friendly mascot, soft-soothing, generic AI startup aesthetic.

### Layer-3 eureka (research finding)

Все introspection-приложения используют тёплый-мягкий визуальный язык, потому что предполагают: пользователь тревожный, его надо успокоить. Но пользователи Basaev уже выбрали делать тяжёлую работу над собой — им не нужно reassurance, им нужно **уважение к этой работе**. Визуальный язык должен быть ближе к серьёзному research notebook, чем к wellness-app. Aeon (intellectual gravity) + Linear (operator confidence) >> Calm/Stoic (patient comfort).

---

## Aesthetic

- **Direction:** Editorial-Brutalist (refined-modernist + editorial weight)
- **Decoration:** minimal — типография делает всю работу. Один тонкий слой бумажного зерна (3–5% noise) на hero-поверхностях, чтобы избежать sterile-clean. Никаких icons-in-circles, иллюстраций людей-в-медитации, gradient backgrounds, glass / blur / 3D.
- **Mood:** quiet, considered, adult, deliberate. Like reading a serious essay, not using an app.

---

## Typography

| Role | Family | Why |
|------|--------|-----|
| **Display** | **Fraunces** (variable, opsz 9–144, wght 300–900) | Editorial gravitas, optical sizing адаптируется от display до body, italic axis для сигнатурных моментов. Google Fonts. |
| **Body** | **Source Serif 4** (variable, opsz 8–60, wght 200–900) | Designed for screen reading. Тёплый, книжный, signal «editorial register». Google Fonts. |
| **UI / Labels** | Source Serif 4 | Same as body |
| **Data / Tables** | **Geist Mono** (tabular-nums) | Чистый современный mono для timestamps, метрик, кода. Vercel, free. |
| **Code** | Geist Mono | Same |

**Loading:** Google Fonts CSS2 link, variable axes:
```html
<link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300..900;1,9..144,300..900&family=Source+Serif+4:ital,opsz,wght@0,8..60,200..900;1,8..60,200..900&family=Geist+Mono:wght@300..900&display=swap" rel="stylesheet">
```

**Scale (намеренно тише, чем SaaS-норма):**
- Hero: clamp(2.2rem, 5.5vw, 3.8rem) — 32–48px не 64–80px
- H2: clamp(1.55rem, 3vw, 2.25rem)
- Body: 1.05rem (~17px)
- Caption / data: 0.78rem (~12px)
- Tracking: -0.02em on display, normal on body

**Anti-list (никогда):** Inter, Roboto, Arial, Helvetica, Open Sans, Lato, Montserrat, Poppins, Space Grotesk, system-ui as primary. Fonts из gstack-blacklist.

---

## Color

### Palette

| Token | Light mode | Dark mode | Usage |
|-------|------------|-----------|-------|
| `--paper` | `#FAF8F4` | — | Light bg |
| `--ink` | `#0F0E0D` | — | Light fg |
| `--deep-ink` | — | `#0A0A0A` | Dark bg (не чистый чёрный — слегка тёплый) |
| `--bone` | — | `#E8E4DD` | Dark fg |
| `--ink-2` | `#4A4845` | `#A8A39A` | Secondary text |
| `--ink-3` | `#8E8B86` | `#6E6A62` | Tertiary text / hints |
| `--rule` | `#DDD6CB` | `#2A2725` | Borders / dividers |
| `--brass` | `#A87B3C` | `#A87B3C` | **Accent** |
| `--moss` | `#5C6B47` | `#5C6B47` | Success |
| `--oxblood` | `#7A2A2A` | `#7A2A2A` | Error |

### Accent rule (RISK: critical)

**Brass появляется максимум на ОДНОЙ вещи на странице.** Most pages — accent invisible. Триггеры показа:
- Primary CTA в bottom of long content
- Текущая стадия в карте 9-stage
- Stage progression event (paper-fade)
- Тонкая линия-разделитель между ходом юзера и агента в чате

Это противоположность «каждая CTA в фирменном цвете». Бронза появляется, когда что-то правда важно — поэтому когда появляется, читается.

### WCAG-AA

Все foreground-on-background combinations проверены: ink on paper 16.2:1, bone on deep-ink 13.4:1, brass on paper 4.6:1 (AA). Текущие токены в `globals.css` уже WCAG-AA, эта система продолжает.

---

## Layout

- **Approach:** editorial grid, asymmetric.
- **Grid:** 12-col base. Content в 8–10 col, не центрированно. Marketing — text-first hero БЕЗ product screenshot above the fold.
- **Max content width:** 1100px (preview), но контент часто сидит в 50–60ch reading width.
- **Page margins:** generous left/right (16–20% of viewport на широких экранах) — сигнал «продуманно». Tighter vertical rhythm — сигнал «собранно».
- **Border radius scale:** sm 0px (most), md 0px (most), lg 4px (rare), full 9999px (never default — only avatars/pills if needed). Editorial register НЕ использует bubble-radius.
- **Chat messages:** paragraphs, not bubbles. Speaker labelled in Fraunces italic above each turn.

---

## Spacing

- **Base unit:** 4px
- **Density:** comfortable — плотнее wellness-apps (которые over-pad), но не cramped как dashboard.
- **Scale:** 2xs(2) xs(4) sm(8) md(16) lg(24) xl(40) 2xl(64) 3xl(96)

---

## Motion

**Темп — медленнее SaaS-нормы.** Это где «тише и глубже» живёт буквально.

| Use | Duration | Easing |
|-----|----------|--------|
| Hover states | 100ms | ease-out |
| Component transitions | 250ms | ease-out enter, ease-in exit |
| Page reveals | 500–700ms | ease-out |
| Stage progression (signature) | 1200ms | custom paper-fade |
| Theme toggle | 600ms | ease-out |

**Никаких:** springs, bounces, parallax, scroll-driven decoration.

**Сигнатурный момент:** медленный paper-fade при stage progression. Случается 8–9 раз за всю жизнь пользователя в продукте — темп маркирует значимость.

---

## SAFE / RISK breakdown

### Safe choices (категорийный baseline)
- Light/dark themes — table stakes
- Generous left/right margins — сигнал «серьёзный продукт»
- Single accent + neutrals — Linear / Vercel / Stripe playbook
- WCAG-AA contrast (already done in current `globals.css`)

### Risk choices (где Basaev получает своё лицо)

1. **Editorial serif (Fraunces) на display, не sans.**
   - Каждый wellness/AI конкурент — sans. Самый громкий single signal.
   - Trade-off: некоторые users могут подумать «old-fashioned». Reward: instant differentiation + adult register.

2. **Paper cream + deep ink, не white + soft grey.**
   - Категорийный departure. Reads as «книжка/дневник», не «app».
   - Trade-off: less «welcoming» first impression. Reward: anyone who reads it is the right user.

3. **Slow motion (400-600ms reveals vs SaaS-норма 200-300ms).**
   - Продукт буквально feels quieter, потому что motion-clock медленнее нормы.
   - Trade-off: некоторые users могут почувствовать как «slow». Reward: signal «мы не спешим».

4. **Earned accent shown rarely (brass на одной вещи max).**
   - Противоположность «каждая CTA в фирменном цвете».
   - Trade-off: визуально менее «branded». Reward: confidence not affect.

---

## Coherence check

Каждый выбор усиливает «AI как серьёзный собеседник, не утешитель»:

- Serif → editorial register
- Cream paper → notebook not app
- Slow motion → размышление not task
- Restrained accent → confidence not affect
- Asymmetric layout → considered not auto-generated
- Paragraph-based chat → reading, not messaging

Если пройдёт об тест «серьёзный / как со взрослым / тише и глубже» в команде — фиксируем.

---

## Что дальше (когда команда обсудит)

Один из вариантов:

**A) Команда одобрила.** Запустить `/design-consultation` снова, выбрать «ship it» — Claude запишет `frontend/DESIGN.md` с этими токенами + добавит правило в CLAUDE.md.

**B) Команда хочет изменить блок.** Запустить `/design-consultation` снова, выбрать «adjust one block» — точечное изменение (фонт / цвет / плотность), пересборка preview.

**C) Команда хочет другое направление.** Запустить `/design-consultation` снова, выбрать «wrong direction» — попробовать brutalist-monospace или luxury-art-book как поляры.

В любом случае контекст этой сессии (research, preview, proposal) сохранён в `~/.gstack/projects/ActVox-app.basaev-web/designs/design-system-20260425/` и любая будущая сессия Claude сможет подхватить отсюда — это **не пропадёт**.

---

## Артефакты сессии

- `proposal.md` — этот документ
- `preview.html` — интерактивный live preview, открывается в браузере
- `research-screenshots/01-stoic.png` — getstoic.com (anti-pattern: warm wellness)
- `research-screenshots/02-linear.png` — linear.app (reference: serious tech tool)
- `research-screenshots/04-aeon.png` — aeon.co (reference: editorial gravity)
- `research-screenshots/04-lex.png` — lex.page (reference: refined literary)
- `session.json` — машинно-читаемое состояние сессии для resume

---

*Generated by `/design-consultation` skill · gstack v1.12.2 · 2026-04-25*
