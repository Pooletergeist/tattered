+++
title = "Zola with links" # url defaults to file title not post title
date = 2023-12-01

draft = false # won't render unless --drafts passed
insert_anchor_links = true # link local with [text](@/<pathfromcontent.md#heading>)

[taxonomies]
categories = ["blog-building"]
tags = ["zola"]
+++

hello, world!

## Links to pages on other websites
This link: ([to Cameron's World](https://www.cameronsworld.net/)) is produced by,
```
[to Cameron's World](https://www.cameronsworld.net/)
```

## Links to other pages on your site
This link to a page on my site ([to first post](@/first.md)) is produced by,
```
[to first post](@/first.md)
```

The start of the path `@/` searches from the `content` directory. So this link
works because my `first.md` file is directly inside my `content` directory.

## Links within page
If you want to link to headings (text prefaced by `#`) on your page, you need
to set the frontmatter variable `insert_anchor_links = true` up at the top of
your post, in between the `+++` lines. I set mine right underneath the
`date=` line. So, the top of this file, `links.md`, looks like:
```
+++
title = "Zola with links" 
date = 2023-12-01

insert_anchor_links = true # the key line 
+++
``` 

This link to the first heading on this page ([top heading](@/links.md#links-to-pages-on-other-websites)) is produced by, 
```
[top heading](@/links.md#links-to-other-pages-on-other-websites)
```

Generically, you might write this as
```
[<text>](@/<pathfromcontent.md#heading>)
```

---

To link to a post that lives within a subdirectory, write path `@/subdirectory/name.md`. For instance, I have a post (titled `index.md` by necessity) inside a subdirectory `picture-post`
```
.
|
+ -- content
    |
    + -- picture-post
        | 
        | -- index.md
```

To link that post, I write `[link to picture post](@/picture-post/index.md)`
which produces: [link to picture post](@/picture-post/index.md)

If I want to write a link to a heading in that post, 
[link to subheading](@/picture-post/index.md#what-if-i-want-to-re-use-the-same-image-on-multiple-pages)
is produced via
```
[link to subheading](@/picture-post/index.md#what-if-i-want-to-re-use-the-same-image-on-multiple-pages)

```
Note the lack of punctuation in the link path, despite the heading ending with a
questionmark. Also note that everything, including `I`, gets lowercased.




