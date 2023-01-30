---
title: "LaTeX for KDP"
summary: LaTeX tips for Kindle Direct Publishing
date: 2022-08-19
series: ["Publishing"]
tags: ["LaTeX", "KDP", "Self-publishing"]
author: "Pantelis Sopasakis"
---

In brief, for 580-page book, here is my `geometry`

```latex
\usepackage[paperwidth=6in,
            paperheight=9in,
            includefoot, 
            footskip=0.2in,
            top=0.67in,
            bottom=0.45in,
            inner=0.77in,
            outer=0.55in,
            bindingoffset=0.2in,
            marginparwidth=1.1cm,
            marginparsep=2mm,
            % showcrop, showframe,
            ]{geometry}
```

Of course, you may want to configure this. It is important not to be sparing with the size of the gutter, especially if your book has more than 200 pages, otherwise you will make your readers' life difficult. 