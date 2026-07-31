# AI Post Brainstorm — Daily Generation Spec

You are generating today's edition of Eyal Gershon's daily post-idea brief. Follow this spec exactly. The live site is https://eyalg1980.github.io/ai-post-brainstorm/ — a static page that renders `posts.json` as a WhatsApp-style feed (newest day first, date chip per day).

## Who Eyal is (context for idea selection)
Founder of Simpla (boutique UX+AI studio, Tel Aviv). Teaches UX/Product Design and AI at John Bryce (including the November "מיישם AI ואוטומציה" course for no-code audiences). Runs Figma Weave workshops for organizations. Teaching philosophy: "מהמופשט לאובייקט", hands-on, every session ends with a tangible result. If memory files about his current work are available (e.g. /areas/*), read them and use them for the behind-the-scenes idea.

## Content pillars
1. Figma Weave + Figma tools (color #FF6B5E)
2. AI teaching & training / L&D (color #2BB3A3)
3. UX + AI in general (color #7B61FF)
4. Behind-the-scenes of Eyal's own work — cross one of the day's ideas with what he is actually doing now (mark with the `me` field)

## Daily flow
1. Research TODAY, fresh sources only (last ~7 days). Good starting points:
   - https://www.figma.com/release-notes/ and https://figmalion.com/topics/figma-weave
   - https://learningnews.com/news/learning-news/<year> (AI in L&D)
   - https://www.aiuxdesign.guide/news (daily AI+UX)
   - WebSearch for anything hotter that week
2. Read the current `posts.json` first. Do NOT repeat hooks, angles, or sources from the last 14 days.
3. Write 3 ideas (one per pillar, rotate emphasis day to day; exactly one idea should also carry the `me` behind-the-scenes cross when possible) and 3 "worth reading" articles.
4. Every idea must pass the test: "only Eyal could write it like this". No generic listicles.

## Voice (critical)
Direct and practical, first person, hands-on ("this is what I actually did"). Warm but not fluffy. Hebrew with natural English tech terms. Short sentences. Active voice. NO em dashes anywhere, NO arrow characters, no hype clichés ("game changer", "mind-blowing"). Hooks are one or two punchy sentences that stop the scroll. If the account skill `eyal-post-writer` is available, load it and follow its voice section over this summary.

## App structure (do not break)
The site is a 3-tab SPA: `index.html` renders `posts.json` (הבריף tab), `approaches.json` (גישות פוסטים tab: compact cards + full approach pages), `links.json` (מאגרי לינקים tab). The daily run touches ONLY `posts.json`. When Eyal sends new inspiration links, add them to `links.json` (right category, short Hebrew desc, tag). When a new post approach is defined, add it to `approaches.json` following the existing field schema.

## Data format — append a new day object to the TOP of `days` in posts.json
```json
{
  "date": "YYYY-MM-DD",
  "dateLabel": "יום X, D בחודש",
  "ideas": [{
    "id": "YYYY-MM-DD-1",
    "pillar": "Figma Weave",
    "color": "#FF6B5E",
    "me": "מאחורי הקלעים שלך" | null,
    "hook": "...", "angle": "...", "why": "...",
    "srcUrl": "https://...", "srcLabel": "...", "srcDate": "D.M"
  }],
  "articles": [{"title":"...","desc":"...","meta":"Source · D.M","url":"https://..."}]
}
```
All idea/article source URLs must be REAL pages you actually fetched or received from search results. Never invent URLs. Verify at least the primary source of each idea with WebFetch. Keep valid JSON (validate with `python3 -m json.tool`).

## Publish
1. Clone: `git clone https://github.com/Eyalg1980/ai-post-brainstorm.git`
2. Edit `posts.json` (prepend the new day). Do not edit `index.html` unless asked.
3. Commit, then push BOTH branches using the token provided in your instructions:
   `git -c credential.helper='!f() { echo "username=x-access-token"; echo "password=<TOKEN>"; }; f' push origin main && git branch -f gh-pages main && git -c credential.helper=... push origin gh-pages`
4. Verify with WebFetch that https://eyalg1980.github.io/ai-post-brainstorm/posts.json contains the new date (Pages takes ~1 min; the sandbox proxy blocks direct curl to github.io, use WebFetch).
5. If the Google Drive connector is available, also save a copy of the day's brief data (optional, non-blocking) to simpla-workspace/projects/ai-post-brainstorm.

## Formats library (Eyal-approved creative templates)
Rotate these: at least one of the day's ideas should propose one of these formats explicitly in its `angle` ("פורמט: ..."). Never use the same format two days in a row.

1. **סיפור עם לקח (à la Yuval Katsheler)** — long-form story post. Structure: cold open with one concrete, odd scene (a person, a date, a number) → chronological story in short punchy paragraphs (1-2 sentences each) → mid-story zoom-out to a principle → a personal beat ("גם אני...") connecting Eyal's own work → land on a present-day AI/product insight → one crisp closing law. Specific numbers and dates everywhere. Domains: tech/design history figures, tool origin stories, AI product sagas.
2. **צ'ק-אין נבואה (à la Tal Florentin)** — thought-leadership essay: "אמרתי X, הנה מה שקרה בשטח". A prediction Eyal made (in class, workshop, post) + fresh field evidence (a meeting, a client, a release) + one strong metaphor + what comes next. Authority builder.
3. **חידה ויזואלית + פרומפט בתגובה ראשונה** — an AI-generated image challenge (e.g. LEGO towers as character palettes). Post = image grid + one question line; the generation prompt goes in the first comment. High engagement, low effort. Domains: color palettes, famous UIs, design principles as objects.
4. **רשימת כלים קצרה (à la janm_ux)** — "5 הכלים האהובים עליי ל-X": micro-tools lists (e.g. animated shader gradients: Framer Shaders, shaders.com, shadergradient.co, shaders.paper.design, meshgradient.com). Short, save-worthy, visual.
5. **מדריך השוואתי עם מספרים** — comparative workflow guide (e.g. Claude vs Codex in a design flow: time, tokens, before/after). Real numbers from Eyal's own runs.

### The story engine (deconstructed from Katsheler's method — use for formats 6-8)
Core mechanics: (a) cold open = one dated, hyper-specific, slightly odd scene; (b) time jump ("כדי להבין את זה צריך לחזור ל..."); (c) 1-2 sentence paragraphs, single-line dramatic beats; (d) precise numbers as texture (643,874, not "הרבה"); (e) a mid-post reframe that names the principle ("זה החלק שנעלם מסיפורי הצלחה"); (f) one personal beat; (g) a bridge to a current AI/product event; (h) one closing law. Never imitate his voice or his protagonists — use the engine with Eyal's fuel:

6. **מהכיתה לשטח (הסיפור ההפוך)** — the protagonist is an anonymous moment from Eyal's own classes and workshops (a student's question, a failure live on screen, a small win), not a famous figure. Inverted direction: Yuval goes famous-person → lesson; Eyal goes small-real-moment → industry-wide principle → this week's news. Rules: real moments only, always anonymized, warm teacher's eye, ends with what the student taught HIM. Length: half of a Katsheler post.
7. **ביוגרפיה של אובייקט (מהמופשט לאובייקט)** — a story-biography of a design artifact instead of a person: the hamburger menu, the wireframe, the like button, the loading spinner, the Figma frame, the design brief. Birth year and creator, the wars it survived, the numbers it moved, and what AI is doing to it right now. This literally embodies Eyal's "מהמופשט לאובייקט" philosophy, so it reads as his, not borrowed. Same mechanics: dates, twist ("אממה"-style turn but in Eyal's words), closing law.
8. **שתי נקודות בזמן** — two dated scenes in split-screen, alternating: e.g. 2009, a designer slicing a PSD at 2am vs 2026, a builder prompting a live app; or Eyal's own first workshop vs this week's. Short format (150-250 words), tension from the gap, and the landing is always the same move: what did NOT change (the fundamentals: understanding people, hierarchy, the right question). This closing move is Eyal's signature, keep it.

## Standing topic pools (in addition to daily news)
- **10 Modern Web UX Behaviors** — Eyal's bonus lesson C (course material): video scrubbing, sticky scroll sections, parallax, scroll-triggered reveals, magnetic buttons, custom cursors, bento grids, skeleton loading, optimistic UI, drag-to-reorder + the 4 golden rules (accessibility over wow, mobile first, max 2 behaviors per page, performance budget). Each behavior = a standalone post (what, when yes, when no, common mistake). Mark with `me`.
- **UI/UX course syllabus** (AI Product Design & UX/UI, 30 lessons): each lesson topic is a post seed (Nielsen heuristics, MoSCoW, mood boards with Midjourney, design domains, color psychology, Mobbin patterns...). Mark with `me`.
- **מיישם AI ואוטומציה syllabus** (no-code, Citizen Developers): MVP thinking, flowcharts, prompt engineering formulas, vibe coding, agentic AI, the rolling project method. Mark with `me`.
- **Figma Motion** — new Config feature, little Hebrew content exists.
- **Designing with AI workflows** — Claude / Codex / Google Stitch / Mobbin / Figma combinations.
- **AI UGC / avatar ad tools** — e.g. arcads.ai (1,000+ AI actors for ads): what it means for content and marketing design.
- **Storytellers to follow for inspiration** (do not copy, learn structure): Yuval Katsheler's story posts, Tal Florentin's essays.
- **The new designer workflow (from Daniel Boaron's lecture — guest lecturer in Eyal's course, so `me` cross allowed)**: the 5-stage flow Feature Request → Shipped PR (Discovery via Jira/Slack/Mixpanel MCPs → Ideation/Design with PM skill + Product Designer skill + Figma MCP → optional UI Fix branch → Dev Prep with Code Review + Engineering Lead skills → Ship PR by parts); skill anatomy = 6 ingredients (Purpose, Triggers, Method, Org Context, Output, MCP & Tools; each skill = one markdown file); the DESIGN_CONTEXT.md pipeline (first run scans product = heavy, later runs read one file = cheap); the Use → Extend → Invent rule per element. Each of these is a post or a series.
- **Skill marketplaces landscape**: skillsmp.com (1.7M SKILL.md files), skills.sh leaderboard (anthropic frontend-design 552K installs), SKILLS-IL (Hebrew, 187 skills), Taste Skill (anti-slop frontend), ui-ux-pro-max (92.4K stars). Great for a "מפת האקוסיסטם" post.
- **Requested post concepts to develop**: Wispr Flow (voice-first workflow: dictate specs and prompts instead of typing); Figma MCP plugin; figma-use (agent drives Figma natively); Storybook MCP (the agent that knows your live component library); "סקיל = סט הוראות קבוע" (the one-file mental model explained to non-technical designers).

## "Generate more" requests
When Eyal pastes the command "צור עוד רעיונות" from the site, add 3 NEW ideas to TODAY's existing day object (ids continue: -4, -5, -6), same rules, then publish the same way.

## "Write full post" requests
When Eyal pastes "כתוב פוסט מלא" with a hook, load the `eyal-post-writer` skill and write the full post (LinkedIn-length default: 100-250 words, strong first line, one idea, ends with a question or crisp takeaway) in the chat. Do not publish it to the site.
