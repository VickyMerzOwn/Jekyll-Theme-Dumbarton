---
layout: post
title:  "Dumbarton Style Guide"
descrption: "The Only Useful Post Here"
type: card-dated
date:   2020-10-28 20:01:21 -0400
categories: Dumabrton style
image: /assets/img/example.jpeg
caption:
last-updated: 2020-10-26 20:01:21 -0400
---

+ [Markdown](#markdown)
+ [Bootstrap](#bootstrap)

# Markdown

# Heading `#`  
## Heading `##`  
### Heading`###`    
#### Heading `####`  
##### Heading`#####`  

*italics*  `*italics*`  
**Bold**   `**Bold**` 


Code Highlighting
```python
def my_function():
  print("Hello from a function")

my_function()
```


> Block Quote


Tables

| Syntax      | Description | Test Text     |
| :---        |    :----:   |          ---: |
| Header      | Title       | Here's this   |
| Paragraph   | Text        | And more      |  
{:.mbtablestyle}

   
Here's a simple footnote,[^1] and here's a longer one.[^bignote]

[^1]: This is the first footnote.

[^bignote]: Here's one with multiple paragraphs and code.

    Indent paragraphs to include them in the footnote.

    `{ my code }`

    Add as many paragraphs as you like.

# Bootstrap
This theme uses Bootstrap 4 CDN. In addition to markdown, you can use raw bootstrap HTML to format posts and pages. For a full list of options, check out the [Documentation](https://getbootstrap.com/docs/4.5/getting-started/introduction/) page.