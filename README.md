# Haoran Zhang — personal site

A single-page personal portfolio. Plain HTML + CSS, **no build step, no dependencies** — which is
what makes it cheap to host (GitHub Pages, free) and easy to change later.

Live at: **https://ricardoran.github.io**

## What's inside

```
.
├── index.html      all page content (bilingual: every string exists twice, .en and .zh)
├── style.css       all styling; design tokens at the top in :root
├── assets/
│   ├── favicon.svg
│   ├── og.png         1200x630 social preview card
│   └── resume.pdf     linked from the sidebar (public download)
├── .nojekyll       tells GitHub Pages to serve files as-is (no Jekyll processing)
└── README.md
```

## Editing content

Everything lives in `index.html`. Text is written as two siblings:

```html
<span class="en">Selected Work</span><span class="zh">精选项目</span>
```

Only the language matching `<html data-lang="…">` is displayed; the other one is hidden by CSS
(`[data-lang="en"] .zh { display: none }`). To change a sentence, edit both siblings — or delete
the `<span>` of the language you don't use and remove the toggle.

Section order in `index.html`: sidebar (intro, quick facts, links) → About → Selected Work →
Experience → Education → Toolbox.

### Common changes

| Want to… | Do this |
| --- | --- |
| Change name / role / blurb | sidebar block at the top of `<body>` |
| Add a project card | copy one `<article class="card">` inside `.cards`, keep the `<header>` + `<p>` + `.tags` structure |
| Change the accent color | `--accent` / `--accent-soft` in `:root` (and the `[data-theme="dark"]` block) |
| Change the monogram | the `<div class="monogram">HZ</div>` text |
| Replace the résumé PDF | overwrite `assets/resume.pdf` — it is served publicly, so keep that in mind |
| Add analytics | one `<script>` before `</body>` |
| Change social preview image | replace `assets/og.png` (1200×630) |

## Local preview

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

Just opening `index.html` in a browser works too — there is no build.

## Deploy

The repo is published with GitHub Pages from the `main` branch, root folder.
Any push to `main` goes live in about a minute:

```bash
git add -A && git commit -m "Update content" && git push
```

## Custom domain (optional, the only paid part)

Domain registration costs money — a `.com` is about **$10.5–11.2 / year** at
[Cloudflare Registrar](https://www.cloudflare.com/products/registrar/) (at-cost, same price on renewal).
GitHub Pages itself and its automatic HTTPS are free; only the domain is paid.

To move from `ricardoran.github.io` to e.g. `haoranzhang.com`:

1. Buy the domain, then in its DNS add `A` records for the apex
   (185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153)
   and a `CNAME` for `www` → `ricardoran.github.io`.
2. In the repo: Settings → Pages → Custom domain → enter the domain (this writes a `CNAME` file).
3. Tick **Enforce HTTPS** once the certificate is issued (usually a few minutes).
4. Update the absolute URLs in `index.html`: `og:url`, `og:image`, `twitter:image` and the JSON-LD `url`.

Free alternative: a subdomain from a service like [is-a.dev](https://github.com/is-a-dev) — no cost,
but it lives on someone else's domain and can disappear if that project stops.


---

## 中文说明

- 整站就是 `index.html` + `style.css` 两个文件，没有构建步骤，改完直接 push 就重新发布。
- 文案都是中英成对出现：`<span class="en">English</span><span class="zh">中文</span>`，改的时候两边一起改。
- 颜色在 `style.css` 顶部的 `:root` 里（`--accent` 是主题色），深色模式在 `[data-theme="dark"]` 里。
- 本地预览：`python3 -m http.server 8000`，然后打开 `http://localhost:8000`。
- 发布：`git push` 推 `main` 分支即可，GitHub Pages 会自动更新。
- 简历已挂在侧边栏，指向 `assets/resume.pdf`；换版本直接覆盖同名文件即可（这个 PDF 是公开可下载的，换之前注意里面的手机号等信息）。
