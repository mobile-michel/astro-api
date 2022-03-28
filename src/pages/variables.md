---
layout: ../layouts/PageLayout.astro
title: Page Title
description: Page Description
car: Hyundai Ioniq5
---
## Comment passer des variables
### Depuis un fichier .astro
```
./pages/index.astro
import PageLayout from '../layouts/PageLayout.astro'
const title = 'Page Title'
<PageLayout content={{title}}></PageLayout>

./layouts/PageLayout.astro
const {content} = Astro.props
<title>{content.title}</title>
```
### Depuis un fichier .md
```
./pages/about.md
layout: ../layouts/PageLayout.astro
title: Page Title

./layouts/PageLayout.astro
const {content} = Astro.props
<title>{content.title}</title>
```
### Fichiers .md + Head.astro
```
./pages/about.md
layout: ../layouts/PageLayout.astro
title: Page Title

./layouts/PageLayout.astro
import Head from '../components/Head.astro'
const { content } = Astro.props
<Head content={content} />

./components/Head.astro
const {content} = Astro.props
<title>{content.title}</title>
```

### Fichiers .astro + config.ts
```
./src/config.ts
export const SITE = {
    name: 'Company Name'
}

./pages/index.astro
import {SITE} from '../config.ts'
<p>Name: {SITE.name}</p>
```