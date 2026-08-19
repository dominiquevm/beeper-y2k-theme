# Release v0.2.1

Summary
- Stop media results from ballooning and overflowing the search palette.
- Make search thumbnails fill their square instead of letterboxing inside it.

Changelog
- fix(search): stop media results from blowing up the search palette (b5a8083)

Notes
Beeper sizes the media grid in the search palette with `repeat(5, minmax(auto, 1fr))`.
The `auto` minimum means a single result whose title is a long unbreakable URL grows every
column to that min-content width. Combined with `aspect-ratio: 1/1` and no overflow clamp on
the tile, the thumbnails balloon and paint over the rest of the popup. Measured against
Beeper's own stylesheet, one such result took the grid from 5x186px to 5x369px with 899px of
horizontal overflow.

The tracks now get a fixed minimum through `auto-fill`, so no single result can resize the
others, and the tile itself is clamped. Thumbnail size is controlled by the
`--msn-search-media-size` variable at the top of the file; raise it for bigger tiles.

Beeper also stretches `.enhanced-img` to the tile but not the wrapper inside it, so images
letterboxed within the square rather than filling it. That wrapper is now stretched too, which
lets `object-fit: cover` do its job.

Upgrading from v0.2.0 requires no action for `@import` installs; copy `custom.css` again for
manual installs.
