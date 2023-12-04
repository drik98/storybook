---
title: 'Markdown'
---

The `Markdown` block allows you to import and include plain markdown in your MDX files.

![Screenshot of Markdown block](./doc-block-markdown.png)

When importing markdown files, it’s important to use the `?raw` suffix on the import path to ensure the content is imported as-is, and isn’t being evaluated:

````md
<!-- README.md -->

# Button

Primary UI component for user interaction

```js
import { Button } from '@storybook/design-system';
```
````

```md
// DON'T do this, will error
import ReadMe from './README.md';
// DO this, will work
import ReadMe from './README.md?raw';

import { Markdown } from '@storybook/blocks';

# A header

<Markdown>{ReadMe}</Markdown>
```

## Markdown

```js
import { Markdown } from '@storybook/blocks';
```

`Markdown` is configured with the following props:

### `children`

Type: `string`

Provides the markdown-formatted string to parse and display.

### `options`

Specifies the options passed to the underlying [`markdown-to-jsx` library](https://github.com/probablyup/markdown-to-jsx/blob/main/README.md).

## Why not import markdown directly?

From a purely technical standpoint, we could include the imported markdown directly in the MDX file like this:

```md
{/_ THIS WON'T WORK, THIS IS TO DEMONSTRATE AN ERROR _/}

import ReadMe from './README.md';

# A header

{ReadMe}
```

However, there are small syntactical differences between plain markdown and MDX2. MDX2 is more strict and will interpret certain content as JSX expressions. Here’s an example of a perfectly valid markdown file, that would break if it was handled directly by MDX2:

```md
# A header

{ this is valid in a plain markdown file, but MDX2 will try to evaluate this as an expression }

<This is also valid, but MDX2 thinks this is a JSX component />
```

Furthermore, MDX2 wraps all strings on newlines in `p` tags or similar, meaning that content would render differently between a plain `.md` file and an `.mdx` file.

```md
# A header

<div>
  Some text
</div>

The example above will remain as-is in plain markdown, but MDX2 will compile it to:

# A header

<div>
  <p>Some text</p>
</div>
```