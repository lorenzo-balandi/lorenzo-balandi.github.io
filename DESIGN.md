# Design choices

- **Only two lines of content:** the name is the main heading, followed by “work in progress”. No navigation, images, icons, buttons, or extra sections are displayed.
- **Centered composition:** the text sits in the center of the viewport with generous empty space to keep attention on the name.
- **Quiet colors:** an off-white background (`#f7f7f2`), dark green heading (`#202e28`), and muted gray-green status text (`#626b63`) retain the original palette in a simpler form.
- **Clear typography:** a large, regular-weight name and a smaller status line create a straightforward hierarchy. System fonts load without external font services.
- **Responsive and accessible:** the heading scales with the screen, padding protects the edges, and semantic HTML identifies the heading and main content. There is no animation.
- **Simple implementation:** plain HTML and CSS make the site easy to edit and compatible with static hosting such as GitHub Pages or GitLab Pages.
