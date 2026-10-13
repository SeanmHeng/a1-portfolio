--Readme document for Sean Heng, *YOUR_EMAIL@uci.edu*--

A reminder on academic integrity, as described in the syllabus.

In general, the course staff expects that you will look at code and examples from many online resources as part of the assignments, particularly to resolve syntax and understand frameworks. We expect that you'll use other libraries you find, and will even require it in some assignments. These practices are often critical to the work of developers today. The best developers are adept at interpreting the examples they see, customizing them to their specific situation, and citing their sources so they can find them later. We expect you to do the same.

While learning from examples is encouraged, attempting to pass an existing project or example from the web as your own is not allowed. If you ever have a question about what is or is not appropriate, feel free to ask the course staff!

Talking to classmates about class material, assignment requirements, etc. is a great way to verify ideas and get feedback. But this distinctly does *not* permit attempting to pass off someone else’s code as your own. Talking over ideas and approaches is allowed, but the work that you produce and submit must be your own.

1. How many assignment points do you believe you completed (replace the *'s with your numbers)?

10/10
- 1/1 Readme
- 2/2 Basic HTML content
- 1/1 Basic CSS styling
- 1/1 Advanced feature
- 2/2 Responsive layout
- 1/1 Passes validation checks
- 2/2 Embraces spirit of the assignment

2. What (a) basic features, (b) CSS features, and (c) advanced features did you include in your portfolio?

(a) Basic features

Images with alt text: the lantern photo on the home page has a full descriptive alt. The SoCalFurs and LocalFurry screenshots on Home and Projects have descriptive alt text too.
Headings and paragraphs: every page has one <h1> and <h2>/<h3> headings below it, with paragraphs under each.
External links: links to socalfurs.com and localfurry.com open in a new tab (target="_blank" rel="noopener"). The mailto: link and the résumé PDF download are also links.
Multiple pages: four linked pages (Home, Projects, Résumé, Contact), with navigation in the header and footer of each.
Semantic tags: <header>, <nav>, <main>, <section>, <article>, <aside>, <footer>, <dl>, <table> and <form>.
Icons: Google Material Symbols for the menu, arrows, mail, location, link, download and send.

(b) CSS features

Padding and margins: used throughout for spacing and layout.
Colors: a custom autumn palette sampled from the photo, defined once as CSS variables (--night, --rust, --amber, --glow, --lantern, --cream).
Google Fonts: Instrument Serif for headings, DM Sans for body text and JetBrains Mono for labels, each with fallbacks (Times New Roman/Georgia/serif, Helvetica Neue/Arial/sans-serif, Courier New/monospace).

(c) Advanced features

Tables: the Skills table on the Résumé page and the “At a glance” comparison on Projects. Both have a <caption>, <th scope> headers and a horizontal scroll wrapper on phones.
Complex layout: a 12-column CSS grid with asymmetric, alternating columns. There is a sticky header, a sticky project image beside the case-study text, and a two-column résumé with a timeline.
Form: the Contact page has a form with labelled fields, a dropdown, a text area and a submit button.
Nested selectors: descendant and combined selectors scope styles to their context, e.g. .work-item:nth-of-type(even) .work-shot to alternate project rows, .site-nav a[aria-current="page"] for the current page, and .nav-toggle:checked ~ .site-nav to open the mobile menu.
Responsive design: breakpoints at 1024, 820 and 560px, plus a CSS-only mobile menu with no JavaScript.



3. Did you ignore any of the warnings or errors presented by the accessibility checker? If so, why does this not seem like an accessibility concern? If it's useful, you can consolidate your thoughts on multiple warnings/errors if the rationale is similar.

All four pages (index, projects, resume, contact) pass the W3C HTML validator with no errors or warnings, and the W3C CSS validator with no errors. The only warnings left are listed below, with why I kept them.

Fixes made to pass the checks:
- index.html, projects.html and resume.html still linked the old per-page stylesheets (01-base.css, 02-home.css, etc.) after I combined them into styles.css, so those pages were showing unstyled. All four pages now link styles.css.
- The hero label ("Portfolio · Autumn 2026") was hard to read over the brightest lanterns in the photo. I added a soft dark radial gradient behind the hero text and a subtle text-shadow so it stays readable on every part of the photo.
- On phones (360px wide), the email address in the footer and contact sidebar was wider than the screen and caused sideways scrolling. Those list items now use overflow-wrap: anywhere.
- axe flagged "scrollable region must have keyboard access" for the tables on small screens. Each table's scroll wrapper now has tabindex="0", role="region" and aria-labelledby pointing at the table caption, so keyboard users can scroll it and screen readers announce what it is.
- AChecker Known Problem, Check 245 ("Data table with more than one row/column of headers does not use id and headers attributes"): both tables have column headers and row headers, so every header cell now has an id and every cell lists its column and row header in a headers attribute (e.g. headers="glance-role glance-socalfurs"). I kept scope="col"/"row" as well, for screen readers that rely on scope.
- Removed unused CSS rules (old placeholder and pull-quote styles) left over from earlier drafts.
- "Section lacks heading" (index.html, About section): the "About me" label was a <span> inside an <aside>, so the section had no heading of its own. It is now an <h2 class="label"> (it looks the same), and the details list moved from an <aside> to a plain <div>. That list belongs to the About section; it is not a side note.
- "Section lacks heading" (contact.html, form section): added an <h2 id="form-title">Send me a message</h2> that is visually hidden with an .sr-only class. The section uses aria-labelledby to point at it, so screen reader users still get a named landmark. The page design stays the same.
- Moved every inline style="" attribute (padding-top, margin-top) into small modifier classes in styles.css (.section--tight, .btn-row--tight, .table-scroll--flush), so all styling lives in the stylesheet.
- Marked the first <option> of the contact form's Topic <select> as selected, which cleared the HTML_CodeSniffer warning "select element does not have a value available to an accessibility API".

Warnings I kept, and why they are not a problem:
- W3C CSS validator: "Due to their dynamic nature, CSS variables are currently not statically checked" (one warning for each declaration in styles.css that uses a variable). This is a notice, not an error. The validator does not resolve custom properties (var(--night), var(--cream), etc.), so it skips any declaration that uses one. I kept the variables on purpose. They hold the color palette, fonts and spacing in one :root block, so a color change happens in one place and stays the same on every page. Every custom property is defined in :root, and every browser in use today supports them. Swapping them for hard-coded values would only hide the notice and make the CSS harder to maintain.
- Color contrast "needs review" (axe / pa11y on every page, and HTML_CodeSniffer's "text is placed on a background image"): the sections and banner have a soft radial-gradient "lantern glow" behind them. Automated checkers can't calculate contrast over a gradient, so they flag the text for manual review rather than as a failure. I checked it by hand by blending the strongest gradient color (30% #B2651A) over the page background (#110502). The lowest contrast is 5.09:1 (placeholder text), and body text (#D4BC96) is 7.84:1. All of it clears WCAG AA's 4.5:1, so this is not a real contrast problem.
- "If this element contains a navigation section, it is recommended that it be marked up as a list" (index.html hero buttons): that <div class="btn-row"> holds two call-to-action links ("See my projects", "View résumé"). It is not site navigation; the real navigation is the <nav> in the header, which is already a <ul>.
- "If this selection list contains groups of related options, they should be grouped with optgroup" (contact.html Topic select): the list has only three unrelated options, so there is nothing to group.
- The hero text on index.html sits on top of a photo, so checkers also mark it "needs review". After adding the dark gradient and text-shadow above, I checked it by eye at desktop and phone sizes, and all of the hero text is clearly readable.
- html-validate (an extra lint, not one of the required checkers) suggests a <section> instead of <div role="region"> for the table scroll wrappers. I kept the <div>: a <section> without a heading would bring back the W3C "Section lacks heading" warning, and role="region" with an accessible name is the standard pattern for a scrollable table.



4. How long, in hours, did it take you to complete this assignment?
    5


5. What online resources did you consult when completing this assignment? (list specific URLs, describe queries to Generative AI, or use of AI-based code completion)
    Claude (Claude Code by Anthropic), I used it to help design and help with lint checking. Specifically: help laying out the pages and CSS, combining the per-page stylesheets into styles.css, fixing the W3C "Section lacks heading" warnings, running accessibility checks (axe, pa11y) and fixing what they found, and wording parts of this readme.
    Google Fonts: https://fonts.google.com/
    Google Material Symbols: https://fonts.google.com/icons
    MDN Web Docs (CSS grid, custom properties, forms, tables): https://developer.mozilla.org/
    W3C HTML validator: https://validator.w3.org/
    W3C CSS validator: https://jigsaw.w3.org/css-validator/
    AChecker: https://achecker.achecks.ca/
    WAVE: https://wave.webaim.org/


6. What classmates or other individuals did you consult as part of this assignment? What did you discuss?
    N/A


7. Is there anything special we need to know in order to run your code?
    No. Open index.html in a browser; there is no build step and all paths are relative. Fonts and icons load from Google Fonts, so they need an internet connection (the fallback fonts are used otherwise). The contact form uses a mailto: action, so it opens your email app.
