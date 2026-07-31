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

## "Generate more" requests
When Eyal pastes the command "צור עוד רעיונות" from the site, add 3 NEW ideas to TODAY's existing day object (ids continue: -4, -5, -6), same rules, then publish the same way.

## "Write full post" requests
When Eyal pastes "כתוב פוסט מלא" with a hook, load the `eyal-post-writer` skill and write the full post (LinkedIn-length default: 100-250 words, strong first line, one idea, ends with a question or crisp takeaway) in the chat. Do not publish it to the site.
