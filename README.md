PIVX Documentation
=====================================

The PIVX Documentation website is synchronised to the main branch of a github repository.  

https://github.com/PIVX-Project/PIVX-Doc-Website-Content

Any pull request merged into the main branch of this repository will be deployed automatically to the https://docs.pivx.org website.  


### Contribution Process  

* All PIVX users & community members are welcome to raise any document suggestions, questions or issues on the [PIVX Discord](https://discord.PIVX.org).
* Contributions are also accepted in the form of **Issues** or **Pull Requests** on the above repository.
* Pull requests will be merged into the main branch after they have been reviewed.

### Documentation Sctructure  

All documents are based on YAML frontmatter and GFM (GitHub Flavored Markdown Specification).  A few enhanced markdown features are also provided in addition to some custom shortcodes which are powered by the [Grav CMS](https://getgrav.org).   

* [Learn about GFM](https://github.github.com/gfm/)  
* [Learn about Grav Markdown](https://learn.getgrav.org/17/content/markdown)  
* [YAML Specs](https://github.com/yaml/yaml-spec)
* [YAML Wikipedia](https://en.wikipedia.org/wiki/YAML)

Every document must have it's own folder/directory. The folder name must be in the format of `xx.my-folder-name` where `xx` is a numeric position.  The folder name becomes the pages slug/url and must be lower case with no spaces, underscores or other characters. The only character exception allowed is the use of dashes (`-`).  Using a dash (`-`) to simulate a space is highly recomended for URL readability and search engine indexing.  

Documents must be named `article.md` and placed into the document folder. Supporting images and files can also be placed into the same folder.

### Tips and Tricks

On any https://docs.pivx.org documentation page, click the **git** icon to view the page on github

![docs-git-link](docs-git-link.png?classes=center,img-fluid,rounded "docs-git-link")  

Then click the "Raw" button

![git-raw](git-raw.png?classes=center,img-fluid,rounded "git-raw")  

This reveals the pages YAML and Markdown code:

![git-markdown](git-markdown.png?classes=center,img-fluid,rounded "git-markdown")  

YAML frontmatter is always placed at the top of the document. The only required YAML frontmatter is as follows:  

```yaml
---
title: 'This is My Page's Title'
taxonomy:
    category:
        - 'Getting Started, etc'
---
```