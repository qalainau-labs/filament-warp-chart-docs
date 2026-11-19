# Changelog

All notable changes to `qalainau/filament-warp-chart` are documented here.

## [1.0.1] - 2026-11-20

### Fixed

- Japanese and Chinese (Simplified and Traditional) texts no longer put a space between a name or a number and the characters next to it: “予算の95%” instead of “予算 の 95%” in tooltips, the text for screen readers, the share of a target and the flow bands. Korean keeps the space between words.

## [1.0.0] - 2026-11-20

### Added

- `WarpChart`, a schema component: bar (also horizontal and stacked), line, area, bar and line together, pie, donut and a big number. It goes anywhere a schema goes: forms, infolists, pages, action modals.
- Data from an Eloquent query (`->query()`, `->relationship()`, `->tableQuery()`), grouped per day, week, month, quarter or year, by a column or by a `BelongsTo`, with count, sum, average, lowest and highest. Days are cut in the viewer's timezone, also across daylight saving changes. The same results on SQLite, MySQL, MariaDB and PostgreSQL.
- Data you build yourself (`->data()`), from a `ChartData` or the array shape of Filament's chart widget; with `Get $get` it follows the form as people type.
- Drill-down (`->drillDown()`, `->drillToRecords()`): click a bar to see what is behind it, level by level, down to a list of the records with links.
- Comparison with the previous year or the previous period, and budget or target lines (`->compareToPreviousYear()`, `->compareToPreviousPeriod()`, `->target()`).
- Linked charts (`->selectable()`, `->reactsTo()`): clicking a value in one chart refetches the others. A Livewire event `warp-chart-selected` lets tables and other components follow.
- `WarpChartWidget` for dashboards (reads the dashboard filters), `WarpChartAction` and `WarpChartBulkAction` to open a chart in a modal from a table row, the table header or the selected rows.
- Charts are redrawn whenever Livewire renders the page with new data, drawn only once they are visible (hidden tabs, opening modals), and follow the width of their container. Light and dark mode, keyboard access, a data table for screen readers.
- Colors in order or by name (`->colors(['Paper' => '#eda100'])`), so a category has the same color in every chart. “Other” is always gray.
- The day, week or month that is not over yet is drawn paler and its tooltip says so.
- `->js()`: data worked out in the browser from the fields of the form, so a chart follows every keystroke without a request. `->dataLabels()`: the values written on the bars.
- `->exportable()`: an Export menu with the chart as a PNG image, its data as CSV, and printing (to save a PDF), all made in the browser.
- `->pivot()`: a chart of a Warp Pivot (1.8 or later) — its rows as categories and drill-down levels, its columns as series, its values as what is measured.
  - When the rows are dates (`sold_on:month`, also day, week, quarter and year), the periods without a value are filled with 0, so the axis does not jump (2025-12, then 2026-03). With `->period()` the whole period is filled, otherwise everything between the first and the last period of the data.
- A value axis in a currency without decimals (`->money('JPY')`, `->money('KRW')`, or `->money('USD', 0)`) counts in whole numbers, also when there is nothing to draw (no more ¥0.2, ¥0.4). Currencies with decimals such as USD are unchanged.
- A chart that can be clicked says so in one line above it (`->hints(false)` to hide), and a chart with one series names its value axis (`->valueLabel()`).
- Actual against target: `->bullet()` (a row per category with a bar, a target line and the share reached) and `->gauge()` (a half-circle meter, one per category side by side), with `->bands([60, 90])` and `->maxValue()`. Lay one out per rep with `->groupByRelation('salesRep')` and a target per rep.
- `->rangeSelector()`: a small chart of the whole period under a date chart; drag across it to choose the period above, with the mouse, by touch or with the keyboard. With a name, the chosen period goes to other charts (`->followRange('period')`) and, through `warp-chart-selected`, to any Livewire component (`ChartRequest::parseRange()`).
- `->treemap()`: the shares of the total as tiles that drill down like bars.
- `->heatmap()`: rows × columns in shades of one color. `->perWeekdayAndHour('ordered_at')` (and `Dimension::weekday()`, `Dimension::hour()`) counts the busy hours of the week in the viewer's timezone, on all four databases.
- `->sankey()` with `->flow('source', 'stage', 'outcome')`: records flowing from step to step; click a band or a box to list its records. `ChartData::flow()` for your own flows.
- Filament multi-tenancy: query charts are scoped to the current tenant.
- Ten languages: English, Japanese, German, French, Spanish, Italian, Brazilian Portuguese, Korean, simplified and traditional Chinese.
- **Static analysis**: the setting methods of the plugin class are declared as returning the plugin, so `$panel->plugin(…::make()->…())` passes Larastan.
