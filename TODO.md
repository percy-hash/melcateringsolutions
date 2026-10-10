# TODO

## Fix page starting/scroll jumping to last section/slide — DONE
- [x] Inspect current slider logic (hash/:target) and autoplay behavior
- [x] Update `Index.html` slider markup/scripts to remove `location.hash` usage during autoplay
- [x] Update `style.css` to use class-based slider position instead of `:target`
- [x] Ensure default visible slide is Slide 1 on page load
- [x] Verify no jump to last section occurs when loading the page

The slider already used class-based positioning (`.CSSgal.is-slide-N`), not `:target`,
and autoplay never touched `location.hash`. The real bug was that the prev/next
arrows and bullet dots were plain `<a href="#s1">` anchors left over from the old
`:target` implementation — clicking them changed `location.hash` and triggered the
browser's native anchor scroll (jumping to the empty `<s id="s1">` markers) without
ever advancing the slide, since no code listened for those clicks. Fixed by adding a
click handler that calls `preventDefault()` and drives `setSlide()` directly.

