# cv — published build

Static build of `~/Projects/career/resume-site`, made for **https://grushor.dpdns.org/cv/**.
This repository holds build output only: edit the source, rebuild, copy `dist/` here.

```bash
cd ~/Projects/career/resume-site
CV_BASE=/cv/ npm run build          # base path lives in vite.config.ts
rsync -a --delete dist/ ~/Projects/career/cv-pages/ --exclude .git
cp public/.nojekyll ~/Projects/career/cv-pages/.nojekyll
cd ~/Projects/career/cv-pages && git add -A && git commit -m "Resume: rebuild" && git push
```

## How the URL works

GitHub Pages serves a project site at `https://<owner>.github.io/<repo>/`, and when the owner's
user site (`Grshor.github.io`) carries a custom domain, project sites move to
`https://<custom-domain>/<repo>/`. So `/cv` is the repository name, nothing more.

Needed once, in order:

1. Private flag off: the repository must be public for Pages on a free account.
2. Settings → Pages → Source: *Deploy from a branch*, branch `main`, folder `/ (root)`.
3. On `Grshor.github.io` → Settings → Pages → Custom domain: `grushor.dpdns.org`;
   tick *Enforce HTTPS* once the certificate is issued.
4. At DigitalPlat DNS: `CNAME  grushor.dpdns.org → grshor.github.io` (TTL default).

`.nojekyll` is here so Pages serves the `assets/` directory as is.
