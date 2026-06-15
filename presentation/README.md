# Opening deck — Marketplace

A self-contained [Reveal.js](https://revealjs.com/) presentation for the retreat opening and
Marketplace: welcome & agenda, a showcase of each Menu Project and the Arena, an open stage for
participants' own pitches, then team & project finding.

## Run it

It's a static page with Reveal.js vendored under `reveal/` (works offline — no internet
needed at the venue). Open it directly:

```
# just open index.html in a browser, or serve the folder:
python3 -m http.server 8000
# then visit http://localhost:8000/
```

## Presenting

- Arrow keys / space to advance; `Esc` for the slide overview.
- `S` opens the **speaker view** with notes and a timer.
- `?` lists all shortcuts.

Edit the slides in `index.html`. Each `<section>` is a slide; nested `<section>`s stack
vertically. Speaker notes live in `<aside class="notes">`.
