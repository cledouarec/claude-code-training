# Claude Code Workshop

A 3-hour hands-on workshop for expert developers on getting the most out of **Claude Code**.

## Workshop schedule (3h)

| Time        | Block                                                                | Format   |
| ----------- | -------------------------------------------------------------------- | -------- |
| 0:00 – 0:30 | **Theory 1**: Foundation · Internals · Customization                 | Theory   |
| 0:30 – 1:15 | **Hands-on 1**: Discover context, memory, commands · Build a skill   | Practice |
| 1:15 – 1:45 | **Theory 2**: Subagents · Plugins · Harness & frameworks             | Theory   |
| 1:45 – 2:30 | **Hands-on 2**: Build a subagent and package it as a plugin          | Practice |
| 2:30 – 3:00 | **Wrap-up**: Demo, Q&A, what's next                                  | —        |

Audience: expert developers, all with Claude Code already installed locally.

## Slides

Built with [Slidev](https://sli.dev/). Markdown sources in [slides/](slides/).

```bash
npm install
npm run dev      # opens http://localhost:3030
npm run build    # static SPA in dist/
npm run export   # PDF export (requires playwright-chromium)
```

Slide structure:

```
slides/
├── index.md                  # entry point (headmatter + imports)
├── pages/
│   ├── 01-foundation.md      # Theory 1 · Foundation
│   ├── 02-under-the-hood.md  # Theory 1 · Internals
│   ├── 03-customization.md   # Theory 1 · Customization
│   ├── 04-handson-1.md       # Hands-on 1 · Discovery + build a skill
│   ├── 05-theory-2.md        # Theory 2 · Subagents + plugins + harness/frameworks
│   └── 06-handson-2.md       # Hands-on 2 · Build a subagent + package as a plugin
└── public/                   # Diagrams and pictures
```

## Exercises

See [exercises/](exercises/) for hands-on instructions.

## References used

- [Claude Code docs](https://code.claude.com/docs)
- [Anthropic platform docs](https://platform.claude.com/docs)
- [luongnv89/claude-howto](https://github.com/luongnv89/claude-howto)
- [skills.sh](https://skills.sh)
