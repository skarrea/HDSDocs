# HDS Linux server documentation
This is the documentation for the Linux servers for [Helsedatasenteret at St. Olavs hospital](https://www.stolav.no/avdelinger/sentral-stab/forskningsavdelingen/helsedatasenter/). 
The documentation is based on Markdown and uses the [Zensical static site generator](https://github.com/zensical/zensical) to generate a webpage. The webpage is built and published via GitHub Actions.

## How to edit
If you are not familiar with markdown here is [a quick introduction](extra/markdown.md). Zensical provides a lot of additional functionality, but to keep the documentation portable I've been conservative with regards to the additional features used. Consult the excellent [zensical docmentation](https://zensical.org/docs/get-started). 

### Full functionality
For full functionality set up zensical via pip or uv in your python environment.
For uv this can be done with

```cmd
uv sync
source .venv/bin/activate
```

### For quick edits
Edits can be made on github by connecting the github repository to [vscode.dev](https://vscode.dev/).

### Adding new files
To add a new page or section make sure to add it to the `nav` in the [`zensical.toml`](zensical.toml) configuration file. 