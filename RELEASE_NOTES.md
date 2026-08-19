# Release v0.2.0

Summary
- Restore compatibility with Beeper Desktop v4.3.34.
- Place the merged-contact chat switcher on the contact's avatar instead of the self-portrait slot.
- Stop the thread list hover frame from running underneath Beeper's row divider.
- Give pinned chats the same MSN selection treatment, including a white title.
- Keep mentions readable inside the pale MSN message bubbles.
- Pin the text caret colour so it stays visible (reported invisible on Windows).
- Re-pin the surface tokens that Beeper's "Rich" and "Monochrome" base themes override on `<body>`, without touching your accent colour.

Changelog
- fix(compat): support Beeper v4.3.34 UI changes
- docs: note v4.3.34 compatibility and base-theme independence

Notes
Beeper 4.3 renders the merged-chat switcher through the same `AccountAvatar-module__container`
class as your own avatar, which is why the theme used to blow it up into the self-portrait slot.
All selectors added in this release are additive, so the theme keeps working on the v4.2 class
names as well.

Beeper's own "Rich" and "Monochrome" base themes redefine core tokens on `<body>`, which outranks
`:root`. That made the theme look different depending on which base theme an install happened to
use — most visibly the left pane background and the message surfaces. Those tokens are now re-pinned.
The accent tokens are deliberately left alone, so the green accent colour recommended in the README
keeps working.
