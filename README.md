See my portfolio at [tmpegues.github.io](https://tmpegues.github.io)

Original theme: [PortfolYou](https://github.com/yousinix/portfolYOU)

I have made a few modifications to the theme:
1. Added a video element that doesn't have to reference youtube ([./_includes/elements/video.html](./_includes/elements/video.html))
2. Added a external link element to open external links in a new tab ([./_includes/elements/ext_link.html](./_includes/elements/ext_link.html))
3. Default theme is dark ([./assets/js/theme.js](./assets/js/theme.js), line 23)
4. Project cards (shown on project index page) match blog post card style to enable different fill and border colors ([./_includes/projects/project-card.html](./_includes/projects/project-card.html))
5. Removed footer theme link. It's easily found without the link on every page. ([./_includes/footer.html](./_includes/footer.html))
6. Added navbar link to this repo.([./_includes/navbar.html](./_includes/navbar.html), line 58)
7. Modified carousel element. In default theme, it looks like you can only have one image carousel per page. If you do more than one, the buttons on all of them only shift the image on the first one. By providing a name, you can have multiple image carousels on one page. ([./_includes/carousel.html](./_includes/elements/carousel.html))