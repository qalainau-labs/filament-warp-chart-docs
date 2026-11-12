# Changelog

All notable changes to `qalainau/filament-warp-chart` are documented here.

## [1.0.0] - 2026-11-12

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
- A chart that can be clicked says so in one line above it (`->hints(false)` to hide), and a chart with one series names its value axis (`->valueLabel()`).
- Filament multi-tenancy: query charts are scoped to the current tenant.
- Ten languages: English, Japanese, German, French, Spanish, Italian, Brazilian Portuguese, Korean, simplified and traditional Chinese.
