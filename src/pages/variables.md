---
layout: ../components/articleComponent.astro
title: Page Title
description: Page Description
car: Hyundai Ioniq5
---
## Comment passer la variable "title"
### Depuis un fichier .astro
```
./pages/index.astro
import Article from '../components/articleComponent.astro'
const title = 'Page Title'
<Article content={{title}}></Article>

./components/articleComponent.astro
import PageLayout from '../layouts/PageLayout.astro'
const { content } = Astro.props
<PageLayout content={content}></PageLayout>

./layouts/PageLayout.astro
import {SITE} from '../config.ts'
const {content} = Astro.props
<title>{content.title} | {SITE.title}</title>
```
### Depuis un fichier .md
```
./pages/about.md
layout: ../components/articleComponent.astro
title: Page Title
```
Le reste est semblable...

### Présentation pour un blog
```
./pages/blog/post1.md
layout: ../../components/blogComponent.astro
title: First blog

./components/blogComponent.astro
import PageLayout from '../layouts/PageLayout.astro'
const data = Astro.fetchContent('../pages/blog/*.md')
const { content } = Astro.props
<PageLayout content={content}>
	<ul>{data.slice(0, 3).map((post) => (
		<li><a href={post.url}>{post.title}</a>: {post.author}</li>
		))}
	</ul>
</PageLayout>

./layouts/PageLayout.astro
import {SITE} from '../config.ts'
const {content} = Astro.props
<title>{content.title} | {SITE.title}</title>
```

### Main navigation with "config.ts"
```
./src/config.ts
export const NAV_ITEMS = {
    home: {
        path: '/',
        title: 'Home'
    },

./layouts/PageLayout.astro
import {NAV_ITEMS} from '../config.ts'
	<ul>{
		Object.keys(NAV_ITEMS).map(navItemKey => <li>
		<a href={NAV_ITEMS[navItemKey].path}>{NAV_ITEMS[navItemKey].title}</a></li>)
	}</ul>
```