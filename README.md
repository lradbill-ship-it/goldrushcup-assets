# goldrushcup-assets

Public static assets for [goldrushcup.com](https://goldrushcup.com).

This repository exists for one reason: to serve `super-custom.css` from a CDN
instead of embedding it in the site's HTML.

The site is a Notion source with a [Super.so](https://super.so) skin. Super
injects custom CSS as an inline `<style>` tag, which meant the stylesheet was
re-downloaded on every page navigation (the HTML is served
`cache-control: max-age=0, must-revalidate`) and, because Next.js also embeds it
twice more in its hydration payload, accounted for roughly **half of every
550 KB page**.

Served via jsDelivr from a version tag, so the URL is immutable and cached for
a year:

```
https://cdn.jsdelivr.net/gh/lradbill-ship-it/goldrushcup-assets@v1/super-custom.css
```

## Updating

Bump the tag; never move an existing one. A tagged jsDelivr URL is cached
`immutable, max-age=31536000`, so an in-place change to an existing tag will not
propagate.

```bash
git commit -am "css: <what changed>"
git tag v2 && git push origin master --tags
```

Then update the `<link>` in the site's Super head snippet to the new tag.

The canonical source for this file lives in the private `gold-rush-cup`
repository, alongside its documentation (`docs/CSS_NOTES.md`). This repo is a
publishing target, not the place to edit.
