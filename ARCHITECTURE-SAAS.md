# סקיצת ארכיטקטורה טכנית — מוצר SaaS למכירה
## Traffic Diversion Platform for Public Transit Authorities

---

## 1. סקירה כללית

### חזון המוצר
פלטפורמת SaaS לרשויות תחבורה ציבורית בעולם (BSO/MTA/STM וכו'). מאפשרת לכל ארגון:
1. להעלות מסמכי שיבוש (אימייל / Word / PowerPoint)
2. לזהות אוטומטית קווים מושפעים מנתוני GTFS המקומיים
3. לקבל המלצות הסטה הלוקחות בחשבון אילוצי אוטובוס
4. לפרסם הודעות מאושרות ללקוחות / נהגים / אתר ציבורי

### מודל עסקי (לדיון)
- **Tier Starter** ($299/חודש): עד 50 אירועים/חודש, משתמש 1, GTFS אחד
- **Tier Pro** ($999/חודש): עד 500 אירועים, 10 משתמשים, אינטגרציות (Outlook/Slack/SMS)
- **Tier Enterprise** (Custom): unlimited, SSO, on-prem option, SLA

---

## 2. ארכיטקטורה ברמה גבוהה

```
┌─────────────────────────────────────────────────────────────┐
│                     לקוחות (Browsers)                        │
└────────────────────────┬────────────────────────────────────┘
                         │ HTTPS
┌────────────────────────▼────────────────────────────────────┐
│              CDN + WAF (Cloudflare)                          │
└────────────────────────┬────────────────────────────────────┘
                         │
        ┌────────────────┼─────────────────┐
        │                │                 │
┌───────▼──────┐  ┌──────▼───────┐  ┌─────▼──────────┐
│  Marketing   │  │   App SPA    │  │   API Gateway   │
│  (Next.js)   │  │  (Next.js)   │  │  (Express/Fastify)│
│  Vercel      │  │  Vercel      │  │  Railway/Fly     │
└──────────────┘  └──────┬───────┘  └─────┬───────────┘
                         │                 │
                         └────────┬────────┘
                                  │
            ┌─────────────────────┼─────────────────────────┐
            │                     │                          │
    ┌───────▼──────┐    ┌─────────▼────────┐    ┌──────────▼────────┐
    │  Auth        │    │   Core Backend   │    │   Worker Queue    │
    │  Clerk/      │    │   NestJS/        │    │   BullMQ + Redis  │
    │  Supabase    │    │   FastAPI        │    │   (long jobs)     │
    └──────────────┘    └─────┬────────────┘    └──────────┬────────┘
                              │                             │
            ┌─────────────────┼─────────────────────────────┘
            │                 │
    ┌───────▼──────┐  ┌───────▼──────┐  ┌────────────────┐
    │  PostgreSQL  │  │   S3-compat  │  │  External APIs │
    │  (Supabase/  │  │   storage    │  │  - Anthropic   │
    │   Neon)      │  │  (R2/S3)     │  │  - Stripe      │
    │              │  │              │  │  - Mapbox      │
    │  + pgvector  │  │  files,      │  │  - Resend      │
    │  for search  │  │  GTFS feeds  │  │  - GTFS sources│
    └──────────────┘  └──────────────┘  └────────────────┘
```

---

## 3. Stack מומלץ

### Frontend
| רכיב | טכנולוגיה | למה |
|---|---|---|
| Framework | **Next.js 15** (App Router) | SSR לאתר השיווקי, CSR לאפליקציה, RSC לביצועים |
| UI Library | **shadcn/ui + Tailwind** | מהיר, מותאם עיצוב |
| State | **Zustand + TanStack Query** | קל ויעיל לדאטה מ-API |
| Forms | **React Hook Form + Zod** | validation type-safe |
| Internationalization | **next-intl** | רב-שפתיות (אנגלית/עברית/ספרדית מהשלב הראשון) |
| Maps | **Mapbox GL JS** (תשלום) או **MapLibre + Protomaps** (חינם) | חיוני להצגת מסלולים והסטות |
| RTL Support | מובנה ב-Tailwind | חיוני לעברית/ערבית |

### Backend
| רכיב | טכנולוגיה | למה |
|---|---|---|
| Runtime | **Node.js 20 + TypeScript** | אקוסיסטם רחב, type safety |
| Framework | **NestJS** | מבנה ארגוני נקי (modules, DI), מתאים לצוות גדל |
| ORM | **Prisma** | type-safe migrations, נוח עם TypeScript |
| Validation | **Zod** | אחיד עם הפרונטנד |
| Background jobs | **BullMQ** + Redis | עיבוד GTFS feeds (כבדים) ברקע |
| Files | **S3 / Cloudflare R2** | אחסון מסמכים שהועלו, קבצי Word שנוצרו |

### Data
| רכיב | טכנולוגיה |
|---|---|
| Primary DB | **PostgreSQL 16** (Supabase / Neon / RDS) |
| Vector search | **pgvector** (חיפוש סמנטי בהיסטוריית אירועים, RAG על נספחי קווים) |
| Cache | **Redis** (sessions, rate-limiting, queue) |
| Search | **Postgres FTS** בהתחלה, **Meilisearch** בהמשך |

### שירותים מנוהלים
| צורך | שירות | תמחור |
|---|---|---|
| Auth + Org/Roles | **Clerk** | ~$25/חודש בסיס + לפי MAU |
| Payments | **Stripe** | 2.9% + 30¢ לעסקה |
| Email | **Resend** | $20/חודש ל-100K |
| LLM | **Anthropic Claude** | ~$3-15 לאירוע (תלוי במודל) |
| Maps | **Mapbox** | $0.50 / 1K loads |
| Monitoring | **Sentry + PostHog** | $30-50/חודש |
| Hosting (frontend) | **Vercel** | $20/חודש Pro |
| Hosting (API) | **Railway / Fly.io** | $20-100/חודש לפי load |

**עלות תפעול חודשית מינימלית** (5-10 לקוחות): **~$300-500**.
**עלות פר אירוע משתנה** (Claude + Maps): **~$0.30-1.50**.

---

## 4. מודל נתונים (PostgreSQL)

```sql
-- Multi-tenancy via organizations
organizations (id, name, slug, plan, stripe_customer_id, settings_json)
users (id, email, clerk_id, ...)
memberships (user_id, organization_id, role)  -- admin/planner/manager/viewer

-- GTFS configuration per organization
transit_systems (id, org_id, name, gtfs_url, gtfs_realtime_url, last_synced_at)
gtfs_routes (id, transit_system_id, route_short_name, route_long_name, geometry)
gtfs_stops (id, transit_system_id, stop_code, stop_name, lat, lon)
gtfs_route_stops (route_id, stop_id, sequence)

-- Custom appendix per org (their internal data)
line_appendix (id, org_id, line_number, streets[], stations[], notes)

-- Core domain
disruption_events (
  id, org_id, status, created_by, source_type,
  source_files[], extracted_json,
  event_type, severity, location_text, location_geom,
  start_at, end_at,
  affected_routes[], diversion_text, message_text,
  approved_by, approved_at, sent_at
)
event_audit_log (id, event_id, actor, action, payload, ts)

-- Distribution lists
distribution_lists (id, org_id, name, recipients[])

-- Approvals
approval_tokens (id, event_id, token, expires_at, used_at, used_by_email)

-- Billing
subscriptions (id, org_id, stripe_sub_id, plan, status, current_period_end)
usage_events (id, org_id, type, count, period)  -- aggregation for metering
```

---

## 5. זרימה — מקצה לקצה

```
1. UPLOAD
   User → Frontend → POST /api/events/upload
   Backend: שומר קבצים ב-S3, יוצר event record בסטטוס "extracting"
   Backend → BullMQ job: "extract-disruption"

2. EXTRACT (worker)
   Worker: parses files (mammoth/pptx) → calls Claude →
           saves extracted JSON → updates event status "extracted"
   Frontend: polls or subscribes via SSE/WebSocket

3. IDENTIFY ROUTES
   Backend: query gtfs_stops near location_geom (PostGIS) →
            join gtfs_route_stops → return affected routes
   Augment with line_appendix matches

4. RECOMMEND DIVERSION
   Backend → Claude with: event details + selected routes +
                          appendix context + working hours rules
   Result saved, status "diversion-ready"

5. GENERATE MESSAGE
   Backend → Claude → message text
   Backend → docx-templater → Word file → S3
   PDF rendering optional (puppeteer / playwright)

6. APPROVAL
   POST /api/events/:id/send-for-approval
   Creates approval_token, sends email via Resend with magic link:
     https://app.example.com/approve/{token}
   Manager clicks → views in browser → approves/rejects

7. DISTRIBUTION
   On approval: enqueue "send-distribution" job
   Worker sends to: SMTP recipients, optionally Slack webhook,
                    SMS via Twilio, public website API
   All actions logged in event_audit_log

8. METERING
   Each Claude call increments usage_events
   Stripe metered billing reads aggregated usage monthly
```

---

## 6. אבטחה ופרטיות

### חובה לפני go-to-market
- **DPA עם Anthropic** (תקפה לטיפול בנתוני לקוחות)
- **SOC 2 Type I** בשנה הראשונה, **Type II** בשנייה (חיוני למכירה לרשויות ציבוריות)
- **GDPR compliance** (אם מוכרים באירופה): right to delete, data residency
- **Encryption**: at-rest (DB + S3) ו-in-transit (TLS 1.3)
- **Secret management**: AWS Secrets Manager / Doppler
- **Audit log immutable**: PostgreSQL append-only או external (Datadog)
- **PII redaction**: לפני שליחת טקסט ל-LLM להחליף שמות אנשים בטוקנים
- **Rate limiting**: per-org, per-user, per-IP
- **WAF**: Cloudflare מול האפליקציה
- **Vulnerability scanning**: Snyk / Dependabot ב-CI

### ארכיטקטורה Multi-tenant
- **Row-Level Security ב-PostgreSQL**: כל query מסונן אוטומטית לפי `org_id`
- **JWT עם org claim**: לא ניתן לגשת לדאטה של ארגון אחר
- **Separate Stripe customers**: כל ארגון = customer
- **Optional dedicated DB schema** ל-Enterprise (אם דורשים בידוד)

---

## 7. אינטגרציות מהיום הראשון

### חיוני
- **GTFS / GTFS-RT** loader (תומך בכל רשות)
- **Outlook / Microsoft Graph** (לשליחת מיילים בשם המשתמש)
- **Slack webhooks** (התרעות לערוצים)
- **Twilio SMS** (לנהגים בשטח)

### גרסה 2
- **Salesforce / Dynamics** (ניהול קשרי לקוחות לרשויות)
- **PagerDuty** (אירועים קריטיים)
- **Webhooks API** (כל לקוח מתחבר למערכות שלו)
- **GIS systems** (Esri ArcGIS) — קריטי לרשויות גדולות

---

## 8. תכנית שלבית להתקדמות (12 חודשים)

### חודש 1-2: Foundations
- הקמת monorepo (Turborepo)
- Auth + organizations + Stripe boilerplate
- Migration של ה-PoC הנוכחי לארכיטקטורה החדשה
- Landing page + sign-up flow

### חודש 3-4: Core MVP
- העלאת מסמכים → backend + queue
- Claude integration server-side (לא יותר client-side)
- GTFS ingestion pipeline (תומך לפחות ב-2 ערים: NY MTA + ת"א)
- App מלאה לזרימת 6 שלבים

### חודש 5-6: Production-ready
- Audit log, monitoring, error tracking
- SOC 2 readiness assessment
- 2-3 design partners (לקוחות פיילוט בחינם / מוזל)
- Billing + metering live

### חודש 7-9: Sales-ready
- Onboarding flow (self-serve)
- Documentation site (Mintlify)
- Outlook + Slack integrations
- Sales collateral, demo videos
- First paying customers

### חודש 10-12: Scale
- Multi-region deployment
- SSO (SAML) ל-Enterprise
- API public ל-integrations
- Compliance certifications

---

## 9. צוות נדרש

### מינימום ל-MVP
- **Full-stack TypeScript** (1) — Next.js + NestJS
- **DevOps part-time** (0.3) — CI/CD, hosting, monitoring
- **Product / Founder** (1) — מכירות, design partners, ראיונות

### לאחר רווח ראשוני
- **Backend dev** נוסף (GTFS / data engineering)
- **Frontend dev** (UI/UX polish)
- **Customer success** (onboarding ולקוחות ארגוניים)

---

## 10. סיכונים ופתרונות

| סיכון | חומרה | מענה |
|---|---|---|
| תלות ב-Anthropic API (downtime / מחיר) | גבוה | abstraction layer + fallback ל-OpenAI / Bedrock |
| LLM hallucinations בהמלצות הסטה | גבוה | always human-in-the-loop, אזהרות בולטות, מדריך נהלים |
| GTFS feeds לא עדכניים | בינוני | sync יומי + alerts |
| תחרות מספקי תוכנת תחבורה (Trapeze, Optibus) | בינוני | התמקדות ב-LLM-first, מחיר נמוך, onboarding מהיר |
| חוקי IP (אם הקוד "שייך" לארגון) | קריטי | ייעוץ משפטי לפני start |
| GDPR / data residency | בינוני | EU region מהיום הראשון אם מוכרים שם |
| מכירה לרשויות = מחזור מכירה ארוך (12-18 חודש) | גבוה | להתחיל ממפעילי תחבורה פרטיים, לאחר מכן ציבורי |

---

## 11. צעדים מיידיים מומלצים

1. **בירור משפטי** — האם הקוד שלך לחלוטין?
2. **Domain + Brand** — שם, דומיין, לוגו (~$200)
3. **Discovery** — ראיונות עם 5-10 רשויות (חינם) להבין צרכים
4. **Design partner agreement** — לקוח אחד שמתחייב להיות פיילוט תמורת מחיר נמוך לטווח ארוך
5. **Pre-incorporation** — Delaware C-Corp / LLC + bank account + Stripe Atlas (~$500)
6. **Engineering hire** — או שותף טכני, או VA + freelancer ל-MVP

---

**סטטוס מסמך:** סקיצת תכנון. אינו מהווה התחייבות מימוש או ייעוץ משפטי / פיננסי.
