---
title: "Nav:Breadcrumbs"
parent_tag: ed746608-87f9-448f-bf57-051da132fef7
intro: >
  Breadcrumbs are a common form of site navigation designed to give the user context with hierarchy in mind. Much like the crumbs left by a certain little German boy — they lead from wherever you are, all the way back home.
description: Display breadcrumb-style navigation links to your current page.
parameters:
  -
    name: include_home
    type: 'boolean'
    description: >
      Remove the home page and begin from the first level nav item. Default: `true`.
  -
    name: reverse
    type: 'boolean'
    description: Reverse the order of links.
  -
    name: trim
    type: 'boolean *true*'
    description: >
      Trim the whitespace from each iteration
      of the loop. Default: `true`.
variables:
  -
    name: is_current
    type: boolean
    description: >
      `true` if current page is the URL being viewed. Useful for adding
      active state classes in your HTML.
  -
    name: data/content
    type: mixed
    description: >
      All data and variables are available for each item in the list.
stage: 4
id: 485f1703-fc6f-4d0f-94f2-e84ae625e1b7
---
## Example

Here's an example of what breadcrumbs might look like, as well as a code example in use.

<figure>
    <div class="flex font-mono">
      <div class="mr-4">Home</div>
      <div class="mr-4">&rarr;</div>
      <div class="mr-4">Blog</div>
      <div class="mr-4">&rarr;</div>
      <div class="mr-4 text-pink-hot font-bold">How to Dress Like David Hasselhoff</div>
    </div>
    <figcaption>These crumbs are delicious.</figcaption>
</figure>

```
<ul class="breadcrumbs">
    {{ nav:breadcrumbs }}
    <li{{ if is_current }} class="current"{{ /if }}>
        <a href="{{ url }}">{{ title }}</a>
    </li>
    {{ /nav:breadcrumbs }}
</ul>
```

## How it works

The list of breadcrumbs is derived from the relative URL of the current page (and not, for example,
the current page's list of parents in a navigation or structured collection). Each prefix of the list of
path parts of the page's URL corresponds to a breadcrumb, with `/` prepended unless the `include_home` parameter is `false`. So, the URL of
the page in the above example might be `/blog/how-to-dress-like-david-hasselhoff`; in that case, its
breadcrumbs would be the entries with these URLs: `/`, `/blog`, `/blog/how-to-dress-like-hasselhoff`.
If you want the URL of an entry to correspond to its location in a structured collection, you can use
the `parent_uri` variable in its collection's [route setting](https://statamic.dev/collections#routing).
