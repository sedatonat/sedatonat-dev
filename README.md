# sedatonat.dev

Personal hub at **https://sedatonat.dev** — a single static page linking the
projects I build and write: Swift/iOS notes, an AI-built news outlet, a supply
chain portal, a glossary, a book and a photography site.

## Stack

No build step, no dependencies. One `index.html` with inline CSS and JS,
served by GitHub Pages from the `main` branch.

| File | Purpose |
|---|---|
| `index.html` | The whole site — markup, styles, script, JSON-LD |
| `404.html` | Custom not-found page, same design tokens |
| `favicon.svg` | Theme-aware mark (light fill in dark mode) |
| `apple-touch-icon.png` | 180×180 iOS home-screen icon |
| `og.png` | 1200×630 social share card |
| `sitemap.xml`, `robots.txt` | Crawling |
| `CNAME` | Custom domain |

## Language

English is the default and the language of all metadata. Turkish is applied
client-side from `data-tr` attributes; visitors can switch with the `TR` / `EN`
control in the header and the choice is remembered in `localStorage`.

## Local preview

```sh
python3 -m http.server 8000
```

## License

Code is MIT (see `LICENSE`). Text and images are © Sedat Onat.
