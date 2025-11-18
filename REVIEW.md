# Review Follow-up

The previously reported issues in `matrix_v7.pine` have been addressed:

1. **Daily high/low repainting** – Replaced the `request.security(..., lookahead_on)` call with on-chart accumulation logic so the current day high/low evolve with each intraday bar instead of leaking the completed daily bar. Seeded the previous-day range with a non-repainting daily request to keep the "Previous Day" dashboard row populated even when the chart has limited history.
2. **`useCloseForPx` toggle** – Added a proper alternative (`hl2`) so the comparison logic meaningfully reacts to the "Use close for comparisons" input across the dashboard, filters, and alert logic.
