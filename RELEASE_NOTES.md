# Release v0.2.2

Summary
- Keep the theme identical in light and dark mode. The chat info panel, dialogs, and
  settings no longer turn black when the operating system switches to dark mode.

Changelog
- fix(dark-mode): pin Beeper's dark-mode tokens to their light values (ad87a8a)

Notes
MSN Messenger never had a dark mode, so the theme is meant to look the same either way. It
already pinned `color-scheme` and Beeper's older `--color-*` tokens to light, but Beeper's
newer `--appearance-*` design tokens switch to dark through
`:root:not([data-theme=light])` inside a `prefers-color-scheme: dark` query. That selector
outranks the plain `:root` the theme used, so those tokens slipped through. Anything built
on them, most visibly the chat info panel on the right, rendered black with dark text on
top.

Every token Beeper changes in dark mode is now pinned to Beeper's own light value, on
selectors that match its specificity: 99 `--appearance-*` tokens plus 36 older tokens the
theme's palette did not cover yet (status colours, secondary buttons, selects, the emoji
picker). The Rich and Monochrome base themes get their light accent gradient back, and the
few colours Beeper hard-codes for dark mode (add-account flow, onboarding steps, network
badges, confirmation prompts) are reset as well. The accent colour picked in
Settings > Appearance keeps working.

The token list was derived from the Beeper v4.3.176 stylesheet and checked against it for
coverage. Nothing changes in light mode.

Upgrading from v0.2.1 requires no action for `@import` installs; copy `custom.css` again for
manual installs.
