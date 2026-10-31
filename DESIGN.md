# Design choices

- **Reference and palette:** a restrained academic layout inspired by https://sarmadmehrdad.github.io/, using white space, dark text, blue links, and simple system typography.
- **Home:** Lorenzo Balandi’s portrait sits beside the supplied introduction. Only the supplied LinkedIn, GitHub, and YouTube links are displayed. The video remains in `assets` for future editing and is not loaded on the page.
- **CV:** two sections present research and work experience, and education. Dates, role titles, institutions, and concise descriptions form a vertical timeline; additional training follows the degrees. Content is based on the supplied October 2026 CV, including expected PhD completion in December 2026.
- **Institution markers:** neutral initials in circles provide visual anchors without reproducing official logos. Public brand guidance does not establish permission for this personal-site use. These are ordinary text badges, not modified institutional logos.
- **PhD Thesis:** the supplied abstract is presented as readable paragraphs under “Thesis Abstract”, without a materials section or status placeholder.
- **Personal projects:** only the page heading and “work in progress” remain.
- **Responsive and accessible:** timelines compress on phones, navigation can wrap, the active page has an underline, and semantic headings, image alt text, a skip link, and visible keyboard focus styles support navigation.
- **Static implementation:** HTML and shared CSS need no build step or external scripts. Text-file content is copied into HTML so the pages also work when opened directly from the filesystem.

- **Copyright footer:** a small, muted notice appears after the content on every page, distinguishing MIT-licensed website code from personal content with all rights reserved. The MIT label links to `LICENSE`; the scope is also explained in the README.
