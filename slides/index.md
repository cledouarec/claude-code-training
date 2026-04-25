---
theme: dracula
colorSchema: dark
title: Claude Code Workshop
author: Christophe Le Douarec
info: |
  Claude Code workshop for expert developers.
  3-hour hands-on session: theory + practice.
class: text-center
comark: true
transition: slide-left
canvasWidth: 1024
---

<img src="/cover.webp" class="absolute inset-0 w-full h-full object-cover -z-10" />

<div class="inline-block px-2 py-2 rounded-2xl backdrop-blur-[2px] bg-black/50 ring-1 ring-white/10">

# Claude Code Workshop

Mastering agentic AI for developers<br>
[3-hour workshop · Theory + Hands-on]{.text-sm .text-white .opacity-60}

</div>

---
layout: center
---

# Today's plan

| Block          | Content                                              | Duration |
| -------------- | ---------------------------------------------------- | -------- |
| **Theory 1**   | Foundation · Internals · Customization               | 30 min   |
| **Hands-on 1** | Discover context, memory, commands · Build a skill   | 45 min   |
| **Theory 2**   | Subagents · Plugins · Harness & frameworks           | 30 min   |
| **Hands-on 2** | Build a subagent and package it as a plugin          | 45 min   |
| **Wrap-up**    | Q&A, what's next                                     | 30 min   |

---
src: ./pages/01-foundation.md
---

---
src: ./pages/02-under-the-hood.md
---

---
src: ./pages/03-customization.md
---

---
src: ./pages/04-handson-1.md
---

---
src: ./pages/05-theory-2.md
---

---
src: ./pages/06-handson-2.md
---

---
layout: center
class: text-center
---

<script setup>
const baseUrl = import.meta.env.BASE_URL
</script>

# Thanks! 

[Now go ship something with it.]{.text-xl .opacity-80}

<div class="thanks-grid">

<div class="qr-block">
<QRCode
    :width="220"
    :height="220"
    :type="svg"
    data="https://github.com/cledouarec/claude-code-training"
    :dotsOptions="{ type: 'rounded', color: '#bd93f9' }"
    :cornersSquareOptions="{ type: 'extra-rounded', color: '#ffb86c' }"
    :image="baseUrl + 'github-logo.svg'"
    :imageOptions="{ margin: 5 }"
/>

[Slides &amp; resources]{.text-sm .opacity-70}
</div>

<div class="links-block">

### Keep going

- 📚 [Claude Code docs](https://code.claude.com/docs)
- 📚 [Anthropic platform docs](https://platform.claude.com/docs)
- 🎓 [luongnv89/claude-howto](https://github.com/luongnv89/claude-howto)
- 🧩 [skills.sh](https://skills.sh)

### Stay in touch

<!-- **Christophe Le Douarec** [embedded-leadership.com](https://embedded-leadership.com) -->

</div>

</div>

<style scoped>
.thanks-grid {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 3rem;
    align-items: center;
    margin-top: 2.5rem;
    text-align: left;
}
.qr-block { text-align: center; }
.links-block h3 { margin-top: 0.75rem; margin-bottom: 0.5rem; color: #ffb86c; }
.links-block ul { margin: 0 0 1rem 0; }
</style>
