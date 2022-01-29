# component-leipzig

A WebComponent for rendering Leipzig Interlinear Gloss.

## Usage

Just import the module(browser only), the WebComponent will be automatically added to your component registry.

```js
import '@yixuan-wang/component-leipzig';
```

The HTML tag of this component is `<leipzig-gloss />`.

## Reference

```html
<leipzig-gloss def="#.:#" lang="en,ru,en,en" data="
Russian
My s Marko poexa-l-i avtobus-om v Peredelkino. 
1PL COM Marko go-PST-PL bus-INS ALL Peredelkino
'Marko and I went to Perdelkino by bus.'
" />
```

Put your gloss contents inside the `data` prop, and separate lines by `\n`.

The `def` prop marks the type definition of each non-blank lines, where

- `#` means annotation that stretch across the whole line **without word-to-word alignment**. This could be used as caption or translation.
- `.` means object language materials. This line will be *word-to-word aligned*.
- `.` means gloss. This line will be *word-to-word aligned*. `-.=_;:\>~[]()<>` are considered lexicon separators, and lexicons that contain only capital Latin letters(an optional numeral at start is allowed) will be considered as **labels** and turned into small cap variants. For 4th gender labels like `G4`(Rule 7, Example 23), use `4G` instead.

**Notice that Leipzig Glossing Rule 2A is not supported**. For such prosodic or phonological words separator in object language, use en-space(`U+2002`, ` `) with hyphen instead.

The default value of `def` prop is `.:#`.

The optional `lang` prop can be used to assign `lang` attributes to each line. Separate [BCP-47](https://www.ietf.org/rfc/bcp/bcp47.txt) tags assigned to each line by comma `,`.

## External Materials

See [Leipzig Glossing Rules](https://www.eva.mpg.de/lingua/pdf/Glossing-Rules.pdf) for detailed rules and syntax of glossing. Check [BCP-47 Language Subtag Lookup](https://r12a.github.io/app-subtags/) for  BCP-47 tags.

This package is built with [Svelte](https://svelte.dev/).
