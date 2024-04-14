+++
title = "Zola with images"
date = 2023-10-05

insert_anchor_links = true
+++

![cute racoon peeking out of tree](test.png)

tl;dr
1. Markdown image syntax is `![<your description of image>](<path>)`
2. Absolute paths work for pictures in the `static` folder:
    - locate `static/<subfolder>/<imgname.png>` by the path 
    `/<subfolder>/<imgname.png>` 
3. Relative paths work for "co-located assets," e.g.`<imgname.png>`

## Sources: 
- [Zola docs: Content Overview/Asset colocation](https://www.getzola.org/documentation/content/overview/#asset-colocation)
- [Zola forums: figuring it out](https://zola.discourse.group/t/how-to-add-an-image-to-a-blog-post-page/1286)
- [Core Markdown (Commonmark)](https://commonmark.org/help/)[^1]
- [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/)


## What is Markdown image syntax?
Markdown image syntax is `![<alt text>](<path>)`. You should put a description of the image in `<alt text>` for accessability and organization, since: 
1. `<alt text>` is displayed when the image fails to load
2. `<alt text>` is read-aloud to visually impaired readers
3. `<alt text>` is scanned by search engines to classify webpages

---
## How do I include images for posts?
You can include an image in a webpage with 4 steps.

1. Make a directory for the webpage inside the `content` directory. 
2. Put an image file inside your newly made webpage directory.
3. Create a file named `index.md` with the content of the webpage
4. Inside `index.md`, write `![<img description in words>](<img-filename>)` 
    to include the image.

You can use the `img-filename` to include the image because the 
image and webpage share a directory. 
Note that the directory name becomes your webpage link.

### Why does this work?
Zola notices the structure of the content directory:
```
.
|
+-- content
     |
     |--some-imgless-post.md 
     |
     +-- directory-for-the-page-with-images
        |
        |— index.md
        |
        |— your-img.png
```
Whenever Zola sees a directory inside `content` with an `index.md` file, it
preserves that structure. So,`index.md` is always within the same directory as 
`your-img.png`. Since `your-img.png` is in the same directory, it can be 
located by just its name. 


![happycow](happycow.jpeg)

```
![happycow](happycow.jpeg)
```

## What if I want to re-use the same image on multiple pages?

Here we use the `static` folder to bring-in photos that we'll use 
multiple times across the site. Using the `static` folder ensures that the file 
is only copied once but can be used at multiple places! Handy for icons and the
like.

```
.
|
+--static
    |
    +--<img-directory> 
        |
        +--<re-used-img.png>
```
With ^ the above directory structure, `<re-used-img.png>` can be included in any
webpage with the markdown syntax:
```
![<verbal-description>](/img-directory/re-used-img.png)
```
So, now that we're stylish:
![stylishlion](/images/stylelion.jpg)
```
![stylishlion](/images/stylelion.jpg)
```

[^1]: Footnotes aren't guarenteed to be supported by [commonmark](@/picture-post/index.md#sources),
but might be, depending on theme.

[linktosubheading](@/picture-post/index.md#sources)

