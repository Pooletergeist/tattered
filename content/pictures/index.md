+++
title = "Zola with Images"
date = 2023-10-05
+++

![here](test.png)

tl;dr
1. Markdown image syntax is `![<your description of image>](<path>)`
2. Absolute paths work for pictures in the `static` folder
3. Relative paths work for "co-located assets" 

# Sources: 
> [Zola docs: Content Overview/Asset colocation](https://www.getzola.org/documentation/content/overview/#asset-colocation)
> [Zola forums: figuring it out](https://zola.discourse.group/t/how-to-add-an-image-to-a-blog-post-page/1286)
> [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/)

## Markdown Image Syntax:
Markdown image syntax is `![<alt text>](<path>)`. You should put a description of the image in `<alt text>` for accessability and organization, since: 
1. `<alt text>` is displayed when the image fails to load
2. `<alt text>` is read-aloud to visually impaired readers
3. `<alt text>` is scanned by search engines to classify webpages

---
## Including Images for Posts:
You can include an image in a webpage with 4 steps.

1. Make a directory for the webpage inside the `content` directory. 
2. Put an image file inside your newly made webpage directory.
3. Create a file named `index.md` with the content of the webpage
4. Inside `index.md`, write `![<img description in words>](<img-filename>)` 
    to include the image.

Note that the directory name becomes your webpage link.

### Why it works:
Zola notices the structure of the content directory:
```
.
|
—— content
 |
 some-imgless-post.md 
 |
 —— your-webpage-directory
    |
    —— index.md
    |
    —— your-img.png
```
Whenever Zola sees a directory inside `content` with an `index.md` file, it
preserves that structure. So,`index.md` is always within the same directory as 
`your-img.png`. Since `your-img.png` is in the same directory, it can be 
located by just its name. 

You can use the `img-filename` to include the image because the 
image and webpage share a directory. 

Relative paths work for "co-located assets"
![here](test.png)

```
![here](test.png)
```

## Including Site-Wide images:

Here we use the `static` folder
