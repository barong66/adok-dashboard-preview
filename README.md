# Adok.ai Dashboard — preview

Статический мокап редизайна дашборда adok.ai. Концепция — **compact cockpit**: всё на одном экране, контекст у каждой цифры, интерактив без перезагрузок. Основан на [asg/support#118](https://gitlab.as12as.com/asg/support/-/work_items/118), плюс улучшения по результатам брейншторма.

## Дизайн-принципы

- **Контекст у каждой цифры** — где сейчас vs где должна быть (vs avg, vs prev period, vs last week)
- **Алерты на главной** — issues не прячутся в notifications, а видны полосой сразу под top bar
- **График в `$`** — деньги, а не impressions; импрешнс как secondary tab
- **Один разрез на виджет** — Revenue by date/format · Revenue by Traffic Sources · Revenue by Websites — по таску #118, не объединяем
- **Сортировка вместо ручного поиска** — клик по любому заголовку колонки

## Виджеты сверху вниз

### 1. Alerts strip _(новое)_
Полоса под top bar, **появляется только если есть issues**. Без issues — нет полосы. Источники: anti-adblock domain down, creative pending review, invoice voided, low balance, KYC pending. Есть `Review →` и dismiss.

### 2. Income header — 4 карточки + sparklines _(переработано)_
Today / Yesterday / This month / Last 30 days. Убраны «7 days» и «Previous month» — дублируют. На каждой карточке:

- `$value` крупно
- Δ% vs сравнимый период (зелёная ↑ / оранжевая ↓ / красная ↓ при ≤−15%)
- мини-sparkline под значением
- **цветная боковая полоса** слева: signal anomaly (зелёная если ≥+1%, серая если ±1%, оранжевая ≤−5%, красная ≤−15%)
- hover-tooltip: «Today $142 vs same weekday avg $135.10»

### 3. Revenue chart — `$` как default _(переработано)_
Заменяет нынешний impressions-чарт.

- **Metric tabs**: `Revenue $` (default) · Impressions · Requests · eCPM
- **Period tabs**: 24h · 7d · 30d · Custom
- **Stacked area** по 8 ad-форматам с фиксированными цветами (Popunder фиолет / Banner синий / In-video зелёный / Slider оранж / In-Page Push красный / Interstitial бирюза / OutStream сиреневый / Direct Link амбер)
- **Hover-tooltip** с разбивкой по форматам в той же метрике + Total
- **Chip-легенда** снизу с toggle on/off по каждому формату

### 4. Revenue by date/format _(оставлен по #118 + улучшение)_
Та же таблица, плюс колонка `vs Prev` — Δ% относительно предыдущего дня, окрашена зелёным/красным. Все колонки сортируемые.

### 5. Revenue by Traffic Sources _(NEW per #118 + улучшения)_
`Source · Total · UV · PPV · eCPM · Δ% · Trend`. Δ% это eCPM week-over-week. Trend — 7-точечный sparkline eCPM. Сортировка по любой колонке.

### 6. Revenue by Websites _(NEW per #118 + улучшения)_
`Website · Total · Revenue · eCPM · Δ% · Trend`. Δ% это Revenue WoW. Trend — sparkline revenue. Сортируется.

### 7. Top movers _(новое)_
Где деньги выросли, где упали — для opportunity-job.

- **Dim selector**: Website · Traffic source · Format
- **Period selector**: vs Yesterday · vs Last week
- 2 колонки: ↑ Top growers (3 строки) | ▼ Top decliners (3 строки)
- Каждая строка: `Name · Δ$ · Δ%`
- Фильтр шумов: items с очень маленьким абс. изменением скрыты

## Источник правды по верстке

- [asg/vue-front/src/apps/adok/layout/components/Sidebar.vue](https://gitlab.as12as.com/asg/vue-front/-/blob/master/src/apps/adok/layout/components/Sidebar.vue)
- [asg/vue-front/src/apps/adok/views/dashboard/components/Incomes.vue](https://gitlab.as12as.com/asg/vue-front/-/blob/master/src/apps/adok/views/dashboard/components/Incomes.vue)
- [asg/vue-front/src/apps/adok/views/dashboard/components/RevenueByDate.vue](https://gitlab.as12as.com/asg/vue-front/-/blob/master/src/apps/adok/views/dashboard/components/RevenueByDate.vue)
- Скриншот живого дашборда от пользователя — единственный источник по виджетам, отсутствующим в master

## Что выдумано

Все цифры — семплы. Today/Yesterday/30d значения и таблица `Revenue by date/format` взяты с реального скриншота. Остальное — реалистичный fake (Traffic Sources, Websites, alerts, chart timeseries).

Один файл, без сборки и зависимостей.
