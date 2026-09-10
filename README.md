# 酒者蘇生 (SHUSYASOSEI) — EC Landing Page

Static landing page for the supplement **酒者蘇生** ("shusyasosei"), built from the
client-supplied design assets and the confirmation PDF (`確認用_酒者蘇生_ec_02`).

- Single file: `index.html` (inline CSS + JS, no build step, no dependencies)
- Assets: `assets/*.webp` (optimized from the original PNGs — ~936 KB total vs ~24 MB raw)
- Layout mirrors the design: **PC** = 3 columns (fixed left logo / center content / fixed
  right CTA sidebar); **mobile** = single content column + sticky bottom CTA bar.

## Structure (matches the confirmation PDF, top → bottom)

| Section | Source asset | Content |
|---|---|---|
| Hero | `hero-a.webp` / `hero-b.webp` (crossfade) | 翌朝、別人..? / 飲む前の仕込みで、翌朝スッキリ |
| 02 | `s02-*.webp` (composed in HTML) | こんなお悩みありませんか？ |
| 03 | `s03.webp` | 控えるではなく、整えるという選択を / 選ばれる理由 |
| 04 | `s04.webp` | 3大成分+15種をバランス配合 |
| 05 | `s05.webp` | 配合量が圧倒的に違う |
| 06 | `s06.webp` | 開発の想い STORY |
| 07 | `s07.webp` | そんな方のためにできたのが 酒者蘇生 |
| 08 | `s08.webp` | 贅沢配合のオリジナル処方 |
| 09 | `s09.webp` | 罪悪感なく楽しめる / 個包装で効率よく |
| 10 | `s10.webp` | おすすめの飲むタイミング |
| 11 | `s11-*.webp` + HTML text | 保証・特典 + footer |

Sections 03–10 are the client's final flattened section images (1980×2700), placed as-is
for pixel fidelity. Sections 02 and 11 had no flattened export, so they are composed from
the individual pieces + live text.

## TODO before publish (operator)

All links are placeholders (`href="#"`). Replace them — each `<a>` carries a `data-cta`
attribute so you can find/replace by purpose:

| `data-cta` | Where it appears | Point it to |
|---|---|---|
| `purchase` | ご購入はこちら (right rail + mobile sticky bar) | Shopify product / checkout URL |
| `line` | Official SNS (LINE icon) | 公式LINE URL |
| `instagram` | Official SNS (IG icon) | 公式Instagram URL |
| `wholesale` | 店舗様・卸販売はこちら（LINEでご案内いたします）(right rail + mobile sticky bar) | 卸売 inquiry — LINE URL / form |
| `tokushoho` | Footer | 特定商取引法に基づく表示 page |
| `privacy` | Footer | プライバシーポリシー page |

Also review/confirm: legal wording (栄養機能食品 claims), 薬機法 compliance of copy,
and the `© 2026, shushasosei` footer text.

## Preview / deploy

```bash
# local preview
cd ~/Workspace/AJARA/shusyasosei && python3 -m http.server 8080   # → http://localhost:8080

# deploy (static host — Cloudflare Pages example)
npx wrangler pages deploy . --project-name shusyasosei
```

## Notes

- Regenerate assets from the raw PNGs with `cwebp -sharp_yuv` (original in
  `~/Downloads/shusyasosei_ec_提出01/`). Composites 1600px wide q90; hero/text/buttons/
  logo near-native q92; backgrounds 1200px q82. Total ~2.7 MB.
- The PC center column is sized by viewport **height** (`--content: clamp(460px,78vh,700px)`)
  so the hero fits one screen without clipping; below 941px it switches to the mobile layout.
- Respects `prefers-reduced-motion` (disables hero crossfade + scroll reveal).
- No tracking / analytics wired yet — add before launch if needed.
