# 02 — Architecture, Cost, Data Model, Security

**Project:** VALI-AGENT PRO
**Status:** DRAFT v1 (owner approval pending)
**Batch:** 1 / Milestone 2

**Labels:** [VERIFIED] [ASSUMPTION] [RECOMMENDATION] [UNKNOWN]

> Important: Neeche ki technology list **final nahi** hai. Lock karne se pehle current compatibility aur pricing officially check hogi.

---

## 1. Technical direction (candidate)

| Hissa | Candidate | Status |
|-------|-----------|--------|
| Dashboard (frontend) | React + TypeScript | [RECOMMENDATION] |
| Database + Login | Supabase (PostgreSQL, Auth, RLS) | [RECOMMENDATION] |
| Hosting | Cloudflare Pages / Workers | [UNKNOWN] framework compatibility check baaki |
| Server-side kaam (secrets wala) | Cloudflare Workers ya Supabase Edge Functions | [UNKNOWN] dono compare karenge |
| Approval alerts | Telegram Bot API | [RECOMMENDATION] |
| AI writing/research | Configurable provider (ek provider par lock nahi) | [RECOMMENDATION] |
| Code storage | GitHub repo `valiagentpro/VALIAGENTPRO` | [VERIFIED] repo public hai, abhi sirf README |

**[RECOMMENDATION]** Simple modular app se shuru karo. Microservices nahi.

**[VERIFIED]** Repo **public** hai. Is liye code mein secret daalna aur bhi khatarnak hai. Secrets kabhi repo mein nahi jayenge.

---

## 2. Data model (pehla draft)

- **sites**: id, name, domain, niche, language, audience, tone, rules, timezone, status (active/paused/disconnected)
- **site_connectors**: site_id, type, status (secret yahan **nahi**, server-side secret store mein)
- **topics**: site_id, title, brief, mode (manual/auto), priority, status
- **articles**: site_id, topic_id, current_version, status
- **article_versions**: article_id, version_no, title, slug, meta_description, body, faqs, alt_texts, canonical, created_at
- **sources**: article_version_id, url, note
- **qa_reports**: article_version_id, checks (passed/warning/failed)
- **approvals**: article_version_id, state, decided_by, decided_via (dashboard/telegram), decided_at
- **schedules**: article_version_id, publish_at, status, idempotency_key
- **publish_jobs**: schedule_id, attempts, result, error
- **agents**: name, enabled, scope, last_run, usage
- **audit_logs**: actor, action, target, time
- **settings**: global_stop, monthly_budget_cap

Har site-wala table par `site_id` rahega, taaki data alag rahe (RLS).

---

## 3. Approval state machine

```
draft -> in_qa -> awaiting_approval -> approved -> scheduled -> published
                       |   |  \
                       |   |   -> rejected
                       |    -> revision_requested -> draft
                       -> (article edit hua) -> approval cancel -> awaiting_approval
```

Rules:
- Approval **sirf ek version** par hoti hai. Article badla to approval khatam.
- Dashboard aur Telegram **ek hi `approvals` record** use karenge.
- Double approval / double publish block (database level lock + idempotency key).
- Koi agent approval skip nahi kar sakta.

---

## 4. Security rules
1. Supabase Auth + RLS har table par on.
2. **Service-role key kabhi browser/frontend code mein nahi.** Sirf server-side.
3. Secrets sirf server-side secret store mein. GitHub, ZIP, screenshot, logs, chat mein kabhi nahi.
4. Publishing tokens scoped aur revocable.
5. Rate limits, audit logs, error handling.
6. Alag environments: development / staging / production. [UNKNOWN] free plan par kitne Supabase projects milenge, check baaki.
7. Global emergency stop + per-site pause.
8. Production ya destructive action sirf owner approval ke baad.
9. Backup aur restore plan M13 se pehle test hoga.

---

## 5. Cost (free-first, target ₹0-₹500/month)

| Item | Plan | Cost status |
|------|------|-------------|
| GitHub | Free | [ASSUMPTION] free, abhi verify nahi |
| Supabase | Free tier | [ASSUMPTION] limits hain (storage, projects, pausing). Official page se check karenge. |
| Cloudflare | Free tier | [ASSUMPTION] limits hain. Official page se check karenge. |
| Telegram Bot | Free | [ASSUMPTION] |
| Domain | Abhi nahi chahiye | Kharidne se pehle approval |
| **AI provider API** | Pay-per-use | [UNKNOWN] **sabse bada variable kharcha** |

Mehengai ke baare mein sach:
- Free tiers ki limits hoti hain. Zyada use par plan upgrade ya band hone ka risk hai.
- AI article likhna free nahi hota. Kharcha is par depend karta hai ki kaun sa model, kitne article, kitna research.
- **[RECOMMENDATION]** Pehle chhota test (2-3 articles) karke asli kharcha naapenge, phir monthly cap set karenge. Koi number maine yahan guess nahi kiya.
- Paid plan ya domain kuch bhi bina aapki approval ke nahi hoga.

---

## 6. Risks
- Free tier limits aur auto-pause.
- AI/API cost badhna.
- Publishing platform ka API hai ya nahi: [UNKNOWN]
- Public repo mein galti se secret chala jana: isliye secret scan CI mein.
- Owner phone se kaam karta hai, isliye steps chhote aur mobile-friendly rakhenge.

---

## 7. Approval
- [ ] Owner ne technical direction (candidate) dekhi
- [ ] Owner ne cost aur security rules approve kiye
