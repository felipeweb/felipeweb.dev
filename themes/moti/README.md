# Moti

Moti theme for [Hugo](https://gohugo.io/) static site generator

For more information read the official [setup guide](https://gohugo.io/getting-started/installing/) of Hugo.

## config.toml

### Nodes

#### [params]

| key | description |
| --- | --- |
| author | Author name |
| keywords | Keywords list |
| avatar | Author picture |
| dateform | Date format ([read more](https://discourse.gohugo.io/t/date-time-format-in-config-toml/5268/2)) |
| lang | Language that the main content will be written |
| footertext | Text at the end of the page (All rights reserved) |
| googleAnalytics | Google Analytics ID |
| about | Author text, show on homepage |

#### [params.social]

| key | description |
| --- | --- |
| linkedin | Account name |
| twitter | Account name |
| github | Account name |
| googleplus | Account name |
| facebook | Account name |

#### [[params.info]]

| key | description |
| --- | --- |
| label | Label |
| value | Valeu |
| link | Hyperlink |

#### [[params.projects]]

| key | description |
| --- | --- |
| name | Project name |
| desc | Project description |
| img | Image path (starting `static/`) |
| link | Hyperlink |

### Example

Show example in [exampleSite](https://github.com/avelino/hugo-theme-sarah/blob/master/exampleSite/config.toml)

```toml
baseURL = "https://felipeweb.dev/"
languageCode = "en-us"
title = "Felipeweb"
theme = "moti"

[permalinks]
fixed = ":title/"
blog  = ":slug"

[params]
author = "Felipeweb"
keywords = ["Golang (Gopher)", "Software Architecture"]
avatar = "img/black-250.png"
dateform = "Jan 2, 2006"
lang = "en"
footertext = "written by felipeweb"
googleAnalytics = "UA-57220118-3"
about = """
I’m a currently a Tech Lead at Nuveo.
"""

[params.social]
linkedin      = "felipewebcloud"
twitter       = "_felipeweb"
github        = "felipeweb"

[[params.info]]
label = "Address"
value = "Brazil, São Paulo, SP"

[[params.projects]]
name = "Vim Bootstrap"
desc = "A generator which provides a simple method of generating a .vimrc configuration for vim"
img = "img/vimbootstrap.png"
link = "https://vim-bootstrap.com/"

[[params.projects]]
name = "Awesome Go"
desc = "A curated list of awesome Go frameworks, libraries and software"
img = "img/awesomego.png"
link = "https://awesome-go.com/"
```

## Contribute

### Build SCSS

```bash
npm install .
gulp build
```
