# 01 — Product Blueprint aur MVP Scope

**Project:** VALI-AGENT PRO
**Status:** DRAFT v1 (owner approval pending)
**Batch:** 1 / Milestone 1

## Labels (har baat par)
- **[VERIFIED]** = actually check kiya gaya
- **[ASSUMPTION]** = maan ke chal rahe hain, check baaki
- **[RECOMMENDATION]** = meri salah
- **[UNKNOWN]** = abhi pata nahi

---

## 1. Product kya hai
VALI-AGENT PRO ek **blog content operations platform** hai. Ye connected blog websites ka poora content kaam sambhalega:

Topic -> Research -> SEO brief -> Outline -> Draft -> Images -> Fact check -> QA -> **Owner approval** -> Schedule -> Publish -> Analytics

## 2. Ye kya NAHI hai
- Ye website builder nahi hai. Websites banana baad mein alag project **BLOG WEBSITE FACTORY** se hoga.
- Ye bina approval ke kuch publish nahi karega. **Kabhi nahi.**
- Ye traffic ya kamai ki guarantee nahi deta.

## 3. Owner aur working rules
- Owner Android phone se kaam karta hai, beginner hai. [VERIFIED: prompt se]
- Ek step, phir DONE, phir agla step.
- Koi secret (password, API key, token) chat ya GitHub mein nahi jayega.
- Koi paid cheez bina approval ke nahi.

---

## 4. MVP scope

### MVP-1 (pehle banega) — "Approved article tak"
| # | Feature | Detail |
|---|---------|--------|
| 1 | Owner login | Sirf owner (single user). Supabase Auth. |
| 2 | Website manager | 1-2 websites add karo: naam, domain, niche, language, audience, tone, rules, timezone. Pause/resume. |
| 3 | Manual topic mode | Owner topic ya brief deta hai. |
| 4 | Article pipeline (basic) | Brief -> outline -> draft -> SEO fields (title, slug, meta, headings, FAQ, alt text). |
| 5 | QA checklist | Passed / warning / failed dikhega. "QA pass = sab facts sahi" nahi hota, ye bhi likha rahega. |
| 6 | Dashboard approval | Approve / reject / revision / return to draft. Approval ek specific **version** par lagta hai. |
| 7 | Export | Approved article copy/download. Auto-publish nahi. |
| 8 | Audit log + emergency stop | Har action ka record. Ek global stop button. |

### MVP-2 (uske baad)
- Telegram approval (dashboard ke saath **ek hi approval record**, double approval nahi).
- Publishing connector (pehle platform verify hoga, phir banega).
- Scheduling, retries, duplicate prevention.

### Baad mein (MVP ke bahar)
- Autonomous topic discovery aur monthly calendar
- Fact-check agent, internal linking agent
- Search Console / GA4 analytics, affiliate, ads readiness
- Content refresh agent, budget dashboard

**[RECOMMENDATION]** Publishing connector MVP-1 mein na rakho. Pehle approval aur quality pipeline solid karo. Connector ka design is par depend karta hai ki blog kis platform par hai (**[UNKNOWN]** abhi).

---

## 5. Milestones aur acceptance criteria

| M | Milestone | Done tab maanenge jab |
|---|-----------|----------------------|
| M1 | Blueprint + MVP scope | Ye doc owner approve kare |
| M2 | Architecture, cost, data model, security | Doc 02 approve ho |
| M3 | Repo foundation + CI checks | Repo mein structure ho, build/lint check chale, koi secret na ho |
| M4 | Auth + DB + RLS + dashboard shell | Owner login kare; bina login data na dikhe |
| M5 | Website manager | Site add/pause/resume ho; ek site ka data dusre mein na dikhe |
| M6 | Topic input + content calendar | Manual topic se brief bane |
| M7 | Writer + editor + source tracking | Draft ke saath sources save hon |
| M8 | QA / fact-check pipeline | Passed/warning/failed report bane |
| M9 | Dashboard approval | Version-based approve/reject kaam kare |
| M10 | Telegram approval | Dono jagah ek hi state; double approval block |
| M11 | Publishing connector + scheduling | Verified platform par draft-first publish, retry, duplicate-proof |
| M12 | Analytics foundations | Sirf real data integration se numbers |
| M13 | Automation, budget limits, backup | Monthly AI cost cap, backup/restore test |
| M14 | Testing + production readiness | Mobile test, security check, owner approval |

Har milestone se pehle scope aur acceptance criteria dobara dikhaaunga.

---

## 6. Owner se abhi baaki sawal (ek-ek karke baad mein puchunga)
1. Pehli website ka niche aur language kya hai?
2. Blog kis platform par hai ya banega (WordPress / custom / Blogger / kuch aur)?
3. Shuru mein kitni websites?

---

## 7. Approval
- [ ] Owner ne MVP-1 scope approve kiya
- [ ] Owner ne milestone list approve ki
