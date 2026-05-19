# Adok.ai Dashboard — preview

Статический мокап нового дашборда adok.ai по [asg/support#118](https://gitlab.as12as.com/asg/support/-/work_items/118).

**Принцип:** взят живой дашборд (sidebar, top bar, шапка доходов, график activity, таблица Revenue by date/format) и воспроизведён 1:1 в HTML/CSS — потом применены изменения из таска.

## Применённые правки из #118

**Оставлено как есть (pixel-aligned):**

- Sidebar: `Dashboard / TRAFFIC / ADVERTISING / EXTRA TOOLS / MORE`
- Top bar (Activity, search, balance, user)
- Шапка с 6 карточками дохода (Today / Yesterday / 7d / This month / Prev month / 30d)
- Activity chart (Impressions / Requests + фильтр по ad type)
- Таблица **Revenue by date/format**

**Удалено** (per #118 — «много информации, что больше путает»):

- Revenue by demand source
- Marketplace Revenue (с кнопками Manage Flat deals / Marketplace settings / Invite advertiser)
- Top GEOs by revenue
- Ad Network's Top by CPM
- Traffic by Websites
- Traffic by SubID

**Добавлено** (per #118):

- **Revenue by Traffic Sources** — `Traffic Source | Total | UV | PPV | eCPM`
- **Revenue by Websites** — `Website | Total | Revenue | eCPM`

## Данные

Цифры в шапке и в таблице Revenue by date/format взяты со скрина живого дашборда. В двух новых таблицах — выдуманные семплы, чтобы показать вид.

## Источник правды

Исходники Vue: [asg/vue-front/src/apps/adok](https://gitlab.as12as.com/asg/vue-front/-/tree/master/src/apps/adok). Стили для шапки — [Incomes.vue](https://gitlab.as12as.com/asg/vue-front/-/blob/master/src/apps/adok/views/dashboard/components/Incomes.vue), для таблицы — [RevenueByDate.vue](https://gitlab.as12as.com/asg/vue-front/-/blob/master/src/apps/adok/views/dashboard/components/RevenueByDate.vue).

Один файл, без сборки и зависимостей.
