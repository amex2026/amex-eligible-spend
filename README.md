# Amex Eligible Spend

A single-file, offline calculator for American Express **eligible spend**.

**[Open the tool](https://amex2026.github.io/amex-eligible-spend/)** — or download
`index.html` and double-click it. Nothing to install.

## What it does

Drop an American Express *Account Activity* PDF onto the page and it reports how much
of the statement counts as eligible spend.

> **Rule:** a transaction is eligible only if reward points are attached to it.
> Points can be negative (a return or merchant credit debits points), and those
> amounts subtract from the total. Anything with no points — payments, membership
> fees, bank transfers, statement credits, and still-pending charges — is excluded
> and listed separately.

Output: eligible charges, point-debited refunds, **net eligible spend**, net points,
the excluded list, and a downloadable per-transaction CSV. Multiple PDFs at once give
a combined total.

## Privacy

Everything runs in your browser. The PDF is never uploaded — there is no server, no
network request, and no analytics.

Don't take my word for it — verify it yourself in 30 seconds:

1. **Go offline.** Turn off WiFi, open the file, drop in a PDF. It still works. Data
   that never leaves the machine can't be exfiltrated.
2. **Watch the network.** `F12` → Network tab → drop in a PDF → zero requests.
3. **Read it.** `Ctrl+U`, or open it in any text editor. Search for `fetch`,
   `XMLHttpRequest`, `script src`, or `http` — there are none. It's 20 KB total.

Trust in a tool like this comes down to three things: it runs offline (your data
stays put), the source is readable (auditable), and what runs is what you read (it's
a local file). This one is all three.

## How it works

The PDF is decoded in plain JavaScript with no libraries: object-graph parsing,
`FlateDecode` via the browser's built-in `DecompressionStream`, `/ObjStm` expansion,
and `ToUnicode` CMap decoding. That is why the whole tool is ~20 KB and has zero
dependencies.

As a self-check it compares the number of parsed transactions against the count of
dollar-amount lines found in the PDF text, and warns instead of silently reporting a
wrong total.

## Browser support

Chrome / Edge 80+, Firefox 113+, Safari 16.4+ (requires `DecompressionStream`).

## License

MIT
