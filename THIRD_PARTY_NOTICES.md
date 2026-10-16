# Third-party notices

This repository's own content is licensed under the [MIT License](LICENSE). It also bundles the third-party skills below. Each keeps its own license and copyright; the root `LICENSE` does not apply to them. Every skill ships twice, once per bundle, with identical content:

- Claude Code: `claude/.claude/skills/<skill>/`
- GitHub Copilot: `copilot/.github/skills/<skill>/`

## Microsoft Azure skills (MIT)

| Skill | Version | Location (both bundles) |
|---|---|---|
| `azure-cloud-migrate` | 1.2.1 | `*/skills/azure-cloud-migrate/` |
| `azure-compliance` | 1.1.1 | `*/skills/azure-compliance/` |
| `azure-cost` | 1.2.2 | `*/skills/azure-cost/` |
| `azure-deploy` | 1.1.2 | `*/skills/azure-deploy/` |
| `azure-resource-visualizer` | 1.1.2 | `*/skills/azure-resource-visualizer/` |

Each `SKILL.md` declares `license: MIT` and `metadata.author: Microsoft` in its frontmatter. These skills ship no separate license file, so the MIT terms are reproduced here:

```
MIT License

Copyright (c) Microsoft

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## drawio-skill (MIT, with Apache-2.0 components)

- **Skill:** `drawio-skill` 1.34.0 by Agents365-ai, <https://github.com/Agents365-ai/drawio-skill>
- **Location:** `claude/.claude/skills/drawio-skill/` and `copilot/.github/skills/drawio-skill/`
- **License:** MIT, Copyright (c) 2026 Agents365-ai. The full text is in [`claude/.claude/skills/drawio-skill/LICENSE`](claude/.claude/skills/drawio-skill/LICENSE) (same file in the Copilot bundle).

The skill contains material from upstream draw.io projects licensed under the **Apache License 2.0** (<https://www.apache.org/licenses/LICENSE-2.0>):

- `data/shape-index.json.gz` is a gzipped copy of the shape search index from [jgraph/drawio-mcp](https://github.com/jgraph/drawio-mcp), generated from the official draw.io / diagrams.net shape libraries. Attribution: [`data/SHAPE-INDEX-NOTICE.md`](claude/.claude/skills/drawio-skill/data/SHAPE-INDEX-NOTICE.md).
- `scripts/shapesearch.py` is based on the jgraph/drawio-mcp shape search, and parts of `references/mermaid-authoring.md` and `references/shapes.md` are condensed from jgraph/drawio-mcp references, as noted in those files.

`data/lobe-icons.json` lists icon names from [lobehub/lobe-icons](https://github.com/lobehub/lobe-icons) (MIT). The icons themselves aren't bundled; diagrams reference them from a CDN.
