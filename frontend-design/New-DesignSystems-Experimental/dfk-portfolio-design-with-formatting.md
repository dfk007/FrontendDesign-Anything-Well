name: DFK Portfolio Design System

description: >
  A bold, high-contrast, and professional frontend design system for Daud Farzand's portfolio.
  Built around a deep black background, a striking red accent color (#f8333c), and a typography stack
  featuring Lora for headings and Roboto Slab for subtitles. The design emphasizes clarity,
  responsiveness, and a clean grid-based layout with a mobile-first approach. Ideal for
  professional portfolios, developer profiles, and personal websites that require a
  modern, tech-savvy aesthetic with a touch of elegance.

DFK Portfolio — Design System

Concept & Aesthetic Direction

The DFK Portfolio Design System embodies a professional, high-contrast, and tech-focused aesthetic. It draws inspiration from modern developer portfolios and sys-admin profiles, emphasizing clarity, responsiveness, and a clean grid-based layout. The design is mobile-first, ensuring seamless usability across all devices.

Core Principles





High Contrast: Deep black backgrounds with white and red accents for maximum readability and visual impact.



Minimalist Elegance: Clean lines, ample whitespace, and a focus on content over decoration.



Tech-Savvy: A design that resonates with developers, sys-admins, and DevOps engineers.



Responsive: Adapts fluidly to all screen sizes, from mobile to desktop.



Color Palette







Token



Value



Usage





--clr-light



#fff



Primary text color on dark backgrounds, default background color for light mode.





--clr-dark



#303030



Primary text color on light backgrounds, default background color for dark mode sections.





--clr-accent



#f8333c



Accent color for buttons, subtitles, focus states, and interactive elements.





Dark Mode BG



#111



Background color for the footer and dark mode.

Usage Guidelines





--clr-accent: Use sparingly for CTA buttons, subtitles, and interactive elements to maintain visual hierarchy.



--clr-light/--clr-dark: Use for text and backgrounds to ensure readability and contrast.



Typography

Font Families







Token



Value



Usage





--ff-primary



'Lora', serif



Headings (h1, h2, h3)





--ff-secondary



'Roboto Slab', serif



Subtitles and accent text

Font Weights







Token



Value



Usage





--fw-reg



400



Regular text, headings





--fw-bold



700



Bold text, emphasis

Font Sizes







Token



Mobile Value



Desktop Value (>= 800px)



Usage





--fs-h1



3rem



4.5rem



Primary headings (h1)





--fs-h2



2.25rem



3.75rem



Secondary headings (h2)





--fs-h3



1.25rem



1.5rem



Tertiary headings (h3)





--fs-body



1rem



1.125rem



Body text

Line Height & Spacing





Body: line-height: 1.6 for comfortable readability.



Headings: line-height: 1 for tight, impactful typography.



Layout & Spacing

Grid & Flexbox





Mobile-First: Layouts are designed for mobile and scaled up using min-width media queries.



Grid Areas: Used for complex layouts (e.g., intro and about sections) to align images and text.



Flexbox: Used for navigation, services, and portfolio grids to ensure flexible, responsive alignment.

Section Padding





Default: padding: 5em 2em for all sections to ensure consistent spacing.

Max Widths





Content: max-width: 1000px for centered content (e.g., services, about sections).



Portfolio Grid: repeat(auto-fit, minmax(300px, 1fr)) for responsive portfolio items.



Components

1. Header & Navigation





Logo: Positioned on the left, links to the home section.



Navigation Toggle: Hamburger menu (3 horizontal lines) for mobile, transforms into an overlay menu.



Navigation Overlay: 





Background: --clr-dark (#303030).



Text: --clr-light (#fff).



Links: Hover color changes to --clr-accent (#f8333c).



Animation: Smooth slide-in from the right (transform: translateX(100%) to translateX(0)).



Hamburger Animation: Rotates 225 degrees on open, with top/bottom bars animating to form an 'X'.

2. Buttons





Primary Button (.btn):





Background: --clr-accent (#f8333c).



Text: --clr-dark (#303030), uppercase, letter-spacing: 2px.



Padding: .5em 2.5em.



Hover: Scales to 1.1 with a smooth transition.



Focus: 3px solid --clr-accent outline with 3px offset.

3. Sections

Intro Section





Layout: 





Mobile: Stacked (image above title/subtitle).



Desktop (>= 600px): Grid layout with image on the left and title/subtitle on the right.



Image: 





box-shadow: var(--bs) (double shadow for depth).



min-width: 250px on desktop.



Subtitle: 





Background: --clr-accent (#f8333c).



Padding: .25em 1em.



Font: --ff-secondary (Roboto Slab).



Positioned to overlap the image slightly on desktop (left: -1.5em).

Services Section





Background: 





Color: --clr-dark (#303030).



Image: url(../img/services-bg.jpg) with cover sizing.



Text color: --clr-light (#fff).



Title: 





Color: --clr-accent (#f8333c).



Underline: 1px light line (opacity: 0.25) below the title.



Services Grid: 





Mobile: Stacked.



Desktop (>= 800px): Flexbox with max-width: 1000px, centered.



Spacing: margin-left: 2em between services.

About Section





Layout: 





Mobile: Stacked.



Desktop (>= 600px): Grid with title/subtitle on the left and image on the right.



Image: 





box-shadow: var(--bs).



Positioned to overlap text slightly (z-index: 2).



Subtitle: 





Background: --clr-accent (#f8333c).



Padding: .25em 1em.



Font: --ff-secondary (Roboto Slab).



Positioned to span full width with left/right padding.

Work Section





Background: --clr-dark (#303030).



Text: --clr-light (#fff).



Title: Color: --clr-accent (#f8333c).



Portfolio Grid: 





display: grid with repeat(auto-fit, minmax(300px, 1fr)).



Items: Background --clr-accent (#f8333c), overflow hidden.



Images: 





Transition: transform 750ms cubic-bezier(.5, 0, .5, 1), opacity 250ms linear.



Hover: transform: scale(1.2), opacity: 0.5.

Footer





Background: #111 (darker than --clr-dark).



Text: --clr-accent (#f8333c).



Padding: 2.5em 0.



Font Size: --fs-h3 (1.25rem mobile, 1.5rem desktop).



Social Links: 





Flexbox layout, centered.



Hover: opacity: 0.7.

4. Dark Mode Toggle





Position: Fixed at top: 0.5rem, right: 0.5rem.



Dark Mode Class: 





color: white, background-color: black for the entire page.



UX Patterns

Interactions





Hover States: 





Buttons: Scale up by 10%.



Portfolio images: Scale up by 20% and fade to 50% opacity.



Navigation links: Change color to --clr-accent (#f8333c).



Social/footer links: Fade to 70% opacity.



Focus States: 





All interactive elements: 3px solid --clr-accent outline with 3px offset.



Portfolio items: z-index: 2 to bring to front.

Animations





Transitions: 





Navigation overlay: 250ms cubic-bezier(.5, 0, .5, 1).



Button hover: 200ms ease-in-out.



Portfolio images: 750ms cubic-bezier(.5, 0, .5, 1) for transform, 250ms linear for opacity.



Hamburger Menu: 





Rotates 225 degrees (0.625turn) on open.



Top bar: Rotates 90 degrees and translates left by 6px.



Bottom bar: Fades out (opacity: 0).



Responsive Design

Breakpoints







Breakpoint



Media Query



Changes





Mobile



Default



Stacked layouts, smaller font sizes, hamburger navigation.





Tablet



min-width: 600px



Grid layouts for intro/about sections, larger images.





Desktop



min-width: 800px



Larger font sizes, multi-column layouts for services/portfolio, max-width constraints.

Layout Adjustments





Intro Section: 





Mobile: Stacked.



Tablet+: Grid with image and text side-by-side.



Services Section: 





Mobile: Stacked.



Desktop: Flexbox with horizontal spacing.



About Section: 





Mobile: Stacked.



Tablet+: Grid with text and image side-by-side.



Accessibility

Color Contrast





Light Mode: 





Text (--clr-dark #303030) on light background (--clr-light #fff) meets WCAG AA standards.



Accent (--clr-accent #f8333c) on light/dark backgrounds provides sufficient contrast.



Dark Mode: 





Text (--clr-light #fff) on dark background (#111 or --clr-dark #303030) meets WCAG AA standards.

Focus Indicators





All interactive elements have a 3px solid --clr-accent outline with a 3px offset for visibility.

Keyboard Navigation





Navigation, buttons, and portfolio items are fully keyboard-accessible with visible focus states.



Implementation Notes

HTML Structure





Semantic HTML: Use <header>, <section>, <nav>, <footer> for accessibility and SEO.



ARIA Labels: Include aria-label for interactive elements (e.g., navigation toggle).



Meta Tags: 





Viewport: width=device-width, initial-scale=1.0.



Normalize.css: Reset default styles for cross-browser consistency.

CSS





Custom Properties: All colors, fonts, and sizes are defined as CSS variables for easy theming.



Box Sizing: box-sizing: border-box for all elements to include padding/border in width/height.



External Libraries:





Normalize.css: CSS reset.



Font Awesome: Icons.



Google Fonts: Typography.

JavaScript





Dark Mode Toggle: Custom element <dark-mode-toggle> for switching between light/dark modes.



Mobile Navigation: JavaScript required to toggle the nav-open class on the <body> for navigation overlay.



Example Code Snippets

CSS Variables

:root {
    --ff-primary: 'Lora', serif;
    --ff-secondary: 'Roboto Slab', serif;
    --fw-reg: 400;
    --fw-bold: 700;
    --clr-light: #fff;
    --clr-dark: #303030;
    --clr-accent: #f8333c;
    --fs-h1: 3rem;
    --fs-h2: 2.25rem;
    --fs-h3: 1.25rem;
    --fs-body: 1rem;
    --bs: 0.25em 0.25em 0.75em rgba(0,0,0,.25),
          0.125em 0.125em 0.25em rgba(0,0,0,.15);
}

Button Style

.btn {
    display: inline-block;
    padding: .5em 2.5em;
    background: var(--clr-accent);
    color: var(--clr-dark);
    text-decoration: none;
    cursor: pointer;
    font-size: .8rem;
    text-transform: uppercase;
    letter-spacing: 2px;
    font-weight: var(--fw-bold);
    transition: transform 200ms ease-in-out;
}

.btn:hover {
    transform: scale(1.1);
}

Navigation Overlay

.nav {
    position: fixed;
    background: var(--clr-dark);
    color: var(--clr-light);
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 100;
    transform: translateX(100%);
    transition: transform 250ms cubic-bezier(.5, 0, .5, 1);
}

.nav-open .nav {
    transform: translateX(0);
}



Usage Instructions for AI

To replicate this design system in an unrelated HTML file:





Setup:





Include the CSS variables (:root) at the top of your stylesheet.



Link the required fonts (Lora, Roboto Slab) from Google Fonts.



Add Normalize.css and Font Awesome for consistency.



Structure:





Use semantic HTML5 elements (<header>, <section>, <footer>).



Organize content into sections with padding: 5em 2em.



Styling:





Apply the typography, color, and spacing rules as defined above.



Use flexbox/grid for layouts, following the responsive breakpoints.



Components:





Recreate the header, navigation, buttons, and sections as described.



Ensure hover/focus states match the specified animations and colors.



Responsiveness:





Use media queries at 600px and 800px to adjust layouts and font sizes.



Dark Mode:





Add a toggle mechanism (e.g., <dark-mode-toggle>) to switch between light/dark modes.



Apply the .dark class to the <body> for dark mode styles.



Testing:





Verify color contrast meets WCAG standards.



Test keyboard navigation and focus states.



Ensure all animations are smooth and performant.



Inspiration & References





Aesthetic: Professional portfolios, developer profiles, sys-admin dashboards.



Technologies: HTML5, CSS3 (Flexbox, Grid, Custom Properties), JavaScript (for interactivity).



Libraries: Normalize.css, Font Awesome, Google Fonts.



This design system is tailored for Daud Farzand's portfolio but can be adapted for any professional or technical portfolio website.
