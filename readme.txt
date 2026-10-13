--Readme document for *YOUR NAME*, *YOUR_EMAIL@uci.edu*--

A reminder on academic integrity, as described in the syllabus.

In general, the course staff expects that you will look at code and examples from many online resources as part of the assignments, particularly to resolve syntax and understand frameworks. We expect that you'll use other libraries you find, and will even require it in some assignments. These practices are often critical to the work of developers today. The best developers are adept at interpreting the examples they see, customizing them to their specific situation, and citing their sources so they can find them later. We expect you to do the same.

While learning from examples is encouraged, attempting to pass an existing project or example from the web as your own is not allowed. If you ever have a question about what is or is not appropriate, feel free to ask the course staff!

Talking to classmates about class material, assignment requirements, etc. is a great way to verify ideas and get feedback. But this distinctly does *not* permit attempting to pass off someone else’s code as your own. Talking over ideas and approaches is allowed, but the work that you produce and submit must be your own.

1. How many assignment points do you believe you completed (replace the *'s with your numbers)?

*/10
- */1 Readme
- */2 Basic HTML content
- */1 Basic CSS styling
- */1 Advanced feature
- */2 Responsive layout
- */1 Passes validation checks
- */2 Embraces spirit of the assignment

2. What (a) basic features, (b) CSS features, and (c) advanced features did you include in your portfolio?

(a) Basic features



(b) CSS features



(c) Advanced features




3. Did you ignore any of the warnings or errors presented by the accessibility checker? If so, why does this not seem like an accessibility concern? If it's useful, you can consolidate your thoughts on multiple warnings/errors if the rationale is similar.

All four pages (index, projects, resume, contact) pass the W3C HTML validator with no errors or warnings, and the W3C CSS validator with no errors. The only warnings left are listed below, with why I kept them.

Fixes made to pass the checks:
- "Section lacks heading" (index.html, About section): the "About me" label was a <span> inside an <aside>, so the section had no heading of its own. It is now an <h2 class="label"> (it looks the same), and the details list moved from an <aside> to a plain <div>. That list belongs to the About section; it is not a side note.
- "Section lacks heading" (contact.html, form section): added an <h2 id="form-title">Send me a message</h2> that is visually hidden with an .sr-only class. The section uses aria-labelledby to point at it, so screen reader users still get a named landmark. The page design stays the same.
- Moved every inline style="" attribute (padding-top, margin-top) into small modifier classes in styles.css (.section--tight, .btn-row--tight, .table-scroll--flush), so all styling lives in the stylesheet.
- Marked the first <option> of the contact form's Topic <select> as selected, which cleared the HTML_CodeSniffer warning "select element does not have a value available to an accessibility API".

Warnings I kept, and why they are not a problem:
- W3C CSS validator: "Due to their dynamic nature, CSS variables are currently not statically checked" (27 warnings in styles.css). This is a notice, not an error. The validator does not resolve custom properties (var(--night), var(--cream), etc.), so it skips any declaration that uses one. I kept the variables on purpose. They hold the color palette, fonts and spacing in one :root block, so a color change happens in one place and stays the same on every page. Every custom property is defined in :root, and every browser in use today supports them. Swapping them for hard-coded values would only hide the notice and make the CSS harder to maintain.
- Color contrast "needs review" (axe / pa11y on contact.html, and HTML_CodeSniffer's "text is placed on a background image"): the sections and banner have a soft radial-gradient "lantern glow" behind them. Automated checkers can't calculate contrast over a gradient, so they flag the text for manual review rather than as a failure. I checked it by hand by blending the strongest gradient color (30% #B2651A) over the page background (#110502). The lowest contrast is 5.09:1 (placeholder text), and body text (#D4BC96) is 7.84:1. All of it clears WCAG AA's 4.5:1, so this is not a real contrast problem.
- "If this element contains a navigation section, it is recommended that it be marked up as a list" (index.html hero buttons): that <div class="btn-row"> holds two call-to-action links ("See my projects", "View résumé"). It is not site navigation; the real navigation is the <nav> in the header, which is already a <ul>.
- "If this selection list contains groups of related options, they should be grouped with optgroup" (contact.html Topic select): the list has only three unrelated options, so there is nothing to group.



4. How long, in hours, did it take you to complete this assignment?



5. What online resources did you consult when completing this assignment? (list specific URLs, describe queries to Generative AI, or use of AI-based code completion)



6. What classmates or other individuals did you consult as part of this assignment? What did you discuss?



7. Is there anything special we need to know in order to run your code?

