---
tags:
  - obsidian
  - PKM
parent: 
type: Permanent Note
deeper: 
against:
---
## Index
[[Obsidian#Why Obsidian]]
[[Obsidian#Obsidian Plugins]]
[[Obsidian#Obsidian Shortcuts]]
[[Obsidian#Basic Markdown]]
[[Obsidian#Advanced Markdown with Obsidian]]
___
### Why Obsidian:
- without distraction or being __online__
- PKM personal **knowledge** management
- your second brain
- Notion is a  management but obsidian is a knowledge management
___
### Obsidian Plugins:
1. Share Note:
	allows you to share obsidian pages to anyone through a link.
2. Fast Text Color:
	allow you to color any text in the file.
3. `Templater`:
	allows you to make templates to use it directly when create note.

___
### Obsidian Shortcuts

| Shortcuts |              Purpose               |
| :-------: | :--------------------------------: |
| ctrl + N  |          open a new note           |
| ctrl + B  |                bold                |
| ctrl + E  | switch between write and read mode |
___
## Markdown with Obsidian:
### Basic Markdown:
#### Headings:
```markdown
# Heading_1
## Heading_2
### Heading_3
#### Heading_4
##### Heading_5
###### Heading_6
```
#### Bold:
```markdown
**Bold Word**
```
#### Italic:
```markdown
*Italic Word*
```
#### Bold and Italic:
```markdown
***bold and italic***
```
#### ~~Strikethrough~~:
	when you make mistake
```markdown
~~This text is crossed out~~
```
#### Word with Special Meaning:
```markdown
`special word`
```
### Tags:
	links between many notes with the same tag
```markdown
#tag
```
#### Word Highlight:
```markdown
==high lighted text==
```
#### Unordered List:
```markdown
- Item 1
- Item 2
  - Sub-item
```
#### Ordered List:
```markdown
1. First item
2. Second item
	1. Sub-item
```
#### Links:
```markdown
[OpenAI](https://www.openai.com)
```
#### Images:
```markdown
![Alt Text](image-url.jpg)
```
#### Blockquote:
```markdown
> This is a quote.
```
#### Code Block:
<pre> ```language Your code here ``` </pre>
#### Horizontal Rule:
```markdown
---
```
#### Tables:
```markdown
| Name     | Age | Country   |
|----------|-----|-----------|
| Tawaky   | 25  | Egypt     |
| John     | 30  | USA       |

```
#### Task Lists:
```markdown
- [x] Write code
- [ ] Test the app
- [ ] Deploy to server
```
#### Footnotes:
- To **cite sources** or references.
- To **explain a term** without breaking the flow.
- To add **comments or side notes** that aren't essential to read immediately.
- To keep your main content **clean and focused**.
you will see all details of this note below.[^note]

[^note]: All other details of the note you can see here
___
### Advanced Markdown with Obsidian:
#### Internal Links:
	This helps you build a **Zettelkasten** or **knowledge graph** by connecting ideas.
```markdown
[[Note Title]]              Links to another note.
[[Note Title#Header]]       Link directly to a header.
[[Note Title^block-id]]     Link to a **block** (more below).
[[Note Title|Custom Text]]
```  
#### Callouts
	Use special blockquotes for visual notes
```markdown
> [!note]
> This is a note callout.
```
More types:
- `[!tip]`, `[!info]`, `[!warning]`, `[!danger]`, `[!quote]`
#### Embed Notes/Sections:
```markdown
![[Note Title]]             Embed an entire note.
![[Note Title#Header]]      Embed just a section.
![[Note Title^block-id]]    Embed a **block** (acts like a quote/reference).

![[image.png]]
![[document.pdf]]
![[audio.mp3]]
```
