---
title: Links
links:
  - title: GitHub
    description: GitHub is the world's largest software development platform.
    website: https://github.com
    image: https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png
  - title: Tschunk recipe
    description: The original Tschunk recipe! What, no wayyyy
    website: https://entropia.de/Tschunk
    image: https://entropia.de/images/thumb/d/df/Chunk.jpg/170px-Chunk.jpg
menu:
    main: 
        weight: 4
        params:
            icon: link

comments: false
---
Just a reminder on how to add links to the footer of pages, since i already forgot twice, ignore the snippet.\
Might use this section to paste every useful links i have laying around. Who knows.

To use this feature, add `links` section to frontmatter.\
This page's frontmatter:

```yaml
links:
  - title: GitHub
    description: GitHub is the world's largest software development platform.
    website: https://github.com
    image: https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png
  - title: TypeScript
    description: TypeScript is a typed superset of JavaScript that compiles to plain JavaScript.
    website: https://www.typescriptlang.org
    image: ts-logo-128.jpg
```

`image` field accepts both local and external images.
