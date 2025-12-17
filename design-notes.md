DESIGN & ACCESSIBILITY NOTES

Overall goal --> build a small, friendly contact card that:
    -looks playful & intentional
    -works with mouse, keyboard, and screen reader
    -respects reduced motion preferences
    -avoids </br> and tabindex abuse

LAYOUT DECISIONS

Body Centering

body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}

-flexbox centers the card both vertically and horizontally
-min-height instead of height prevents clipping on small screens
-default body margin removed to avoid "almost centered" bugs

Card Sizing

.card {
  width: 350px;
  padding: 72px 24px;
}

-fixed width for visual consistency
-no fixed height to avoid centering issues and overflow
-vertical padding creates breathing room instead of fake spacing with </br>

TYPOGRAPHY

Name Styling
-pixel font chosen for personality
-"-webkit-text-stroke" used to match Figma outline
-color + outline chosen to maintain contrast against orange background
-fallbacks intentionally minimal, acceptable for modern browsers

Contact Pills
Why "inline-flex":

.contact {
  display: inline-flex;
  align-items: center;
}

-allows icon + text alignment
-pill sizes to its content (no full-width buttons)
-multiple pills can sit inline if desired

Verticle Stacking

.contact-list {
  display: flex;
  flex-direction: column;
  gap: 2px;
  align-items: center;
}

-layout handled in CSS, not HTML
-avoids </br> for spacing
-easier to adjust spacing later

HOVER VS FOCUS

Hover (Mouse Users)
-subtle scale + soft shadow
-indicates interactivity, not location

Focus (Keyboard Users)
-stronger than hover
-visible even with reduced motion
-indicates current position, not just interactivity

KEYBOARD ACCESSIBILITY
-no "tabindex" added manually
-only real interactive elements receive focus (<a>)
-focus stays on links, not container elements
-pill reacts visually using ":has(a:focus-visible)"
-avoids double tab stops & screen reader confusion

REDUCED MOTION

@media (prefers-reduced-motion: reduce) {
  .contact {
    transition: none;
  }
  .contact:hover,
  .contact:has(a:focus-visible) {
    transform: none;
  }
}

-motion (scale/animation) removed
-focus visibility retained
-calm UI without loss of usability

SCREEN READER DECISIONS

Decorative Images

<img alt="">

-empty alt hides images from screen readers
-avoids redundant narration
-used for avatar, flower graphic, email icon

Link Clarity

<span class="visually-hidden">Email Viktoria Rad:</span>

-adds context when links are read aloud
-no visual change
-avoids ARIA where semantic HTML is sufficient
-links make sense when heard out of context

VISUALLY HIDDEN UTILITY

.visually-hidden { … }

-invisible to sighter users
-readable by assistive tech
-preferred over "aria-label" for inline context

THINGS INTENTIONALLY AVOIDED
-</br> for layout
-fixed heights
-"tabindex" hacks
-removing focus outlines without replacement
-color-only focus indicators
-overusing ARIA where HTML already works


