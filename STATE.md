# STATE — flujo-landing

## 2026-08-31 — 9 staged brand-asset changes, uncommitted

Live site repo (`origin`: `matiasarielcohen/flujo-landing`, branch `main`).
Last commit `4822b13` on 2026-08-07.

HEAD equals the **local** `origin/main` ref (0 ahead, 0 behind) — but there is no
`FETCH_HEAD`, so that ref dates from the clone and has never been refreshed. Whether the
GitHub remote has moved since is **unknown without a `git fetch`**; don't assume it hasn't.

**There are 9 files staged but never committed** (0 unstaged, 0 untracked): the `@4x`
brand assets were swapped from PNG to JPG and the three logo SVGs edited.

```
3 A  brand_assets/*@4x.jpg          (added)
3 D  brand_assets/*@4x.png          (deleted)
3 M  brand_assets/*.svg             (modified)
```

- **Next:** decide whether that swap is intended, then commit and push it — or reset it.
  It has been sitting in the index since before 2026-08-31 and is the only pending work here.
- **Open question:** was the PNG→JPG change deliberate? JPG has no transparency, which
  usually matters for a logo. Confirm before committing.
- Deploys on Vercel with `cleanUrls` (URLs have no `.html`), per commit `40834a7`.
