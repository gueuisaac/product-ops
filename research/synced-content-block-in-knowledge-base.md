# Synced Content Block in Knowledge Base: PRD Research Baseline

*Generated: 2026-02-05*

## Summary

A synced content block is a standalone, reusable unit of content (paragraph, disclaimer, pricing table, warning banner, etc.) that can be created once and embedded across multiple knowledge base articles. When edited in one place, all articles containing that block update automatically. This feature eliminates the tedious and error-prone process of manually updating the same information across dozens of articles, which is critical for teams managing compliance notices, pricing info, and feature availability notes at scale.

---

## Competitive Analysis

### Zendesk — "Content Blocks"

- **Feature name:** Content Blocks
- **How it works:** Content Blocks are standalone, reusable units of content that exist independently from any article. Authors create a content block (from scratch via the "Add" menu, or by selecting existing text within an article and converting it), then insert that block into one or many articles. The block appears inline within the article but is visually distinguished in the editor. When anyone edits the content block, all articles containing it are automatically updated in the published help center without changing the article's publication status.
- **Key capabilities:**
  - Create from existing text or standalone from admin menu
  - Rich content support: bold, italics, lists, tables, headings, links, images, videos, HTML blocks
  - Automatic sync: editing a content block propagates to all articles immediately
  - Content block list/dashboard: admins see all blocks, last edited date, article count
  - Usage tracking sidebar: every article a block appears in, with article status
  - Unlink (converts to regular inline text, breaking sync) vs. Remove (deletes from article, keeps in others)
  - Permissions: admin toggle for "Allow agents to update content blocks"
  - Multilingual support: content blocks can be translated, though each translation is a separate block
  - API support: read works (blocks inlined as text), write creates inconsistent state
- **Limitations:**
  - Enterprise-only (Suite Enterprise or Enterprise Plus with Guide Enterprise)
  - Translated blocks are separate objects, not linked translations
  - API write creates divergent state between published article and editor
  - Cannot insert content blocks inside bulleted/numbered lists
  - Must remove block from all articles before deleting it
- **Pricing tier:** Suite Enterprise ($169-209/agent/month billed annually)
- **Sources:**
  - [Reusing content with content blocks](https://support.zendesk.com/hc/en-us/articles/4408829589274-Reusing-content-with-content-blocks)
  - [Creating and inserting reusable information with content blocks](https://support.zendesk.com/hc/en-us/articles/4408832857754-Creating-and-inserting-reusable-information-with-content-blocks)
  - [Managing content blocks in articles](https://support.zendesk.com/hc/en-us/articles/4408829568282-Managing-content-blocks-in-articles)
  - [Allowing agents to update content blocks](https://support.zendesk.com/hc/en-us/articles/4823057157146-Allowing-agents-to-update-content-blocks)
  - [Removing content blocks from articles](https://support.zendesk.com/hc/en-us/articles/5519936040986-Removing-content-blocks-from-articles-and-your-help-center)
  - [Using content blocks in translated articles](https://support.zendesk.com/hc/en-us/articles/4486473049370-Using-content-blocks-in-translated-articles)
  - [Help Center API limitations with content blocks](https://developer.zendesk.com/documentation/help_center/help-center-api/content-blocks-limitations/)

### Salesforce Knowledge — No Direct Equivalent

- **Feature name:** No native synced content block feature
- **How it works:** Salesforce Knowledge does not have synced/reusable content blocks for knowledge articles. The closest capabilities are:
  - **Quick Text**: Short reusable text snippets for case comments, emails, and chats. Supported in Lightning Article Editor as of Winter '24, but insert-and-forget — no ongoing sync.
  - **Article Templates (Record Types)**: Custom field layouts for different article types (FAQ, How-To), but controls structure, not shared content.
  - **Article Personalization**: Dynamic Forms for Knowledge allows conditional field visibility, but this is about showing/hiding fields, not sharing content.
- **Key capabilities (Quick Text):**
  - Insert pre-written text snippets into the article editor
  - Useful for common phrases, disclaimers, boilerplate
  - Once inserted, text becomes static — updating Quick Text does not update articles
- **Limitations:**
  - No true synced/reusable content block
  - No dashboard to track where a snippet has been used
  - No way to bulk-update a phrase across all articles
- **Pricing tier:** Salesforce Knowledge included in Service Cloud Enterprise ($165/user/month) and above. Quick Text available at that tier. Synced content blocks do not exist at any tier.
- **Sources:**
  - [Rich Text Fields in Knowledge Articles](https://help.salesforce.com/s/articleView?id=service.knowledge_rich_text_considerations.htm&language=en_US&type=5)
  - [The Ultimate Guide to Salesforce Knowledge](https://www.salesforceben.com/introduction-salesforce-knowledge/)
  - [Lightning Article Editor & Article Personalization](https://advancedcommunities.com/blog/lightning-article-editor-article-personalization-biggest-salesforce-knowledge-update/)

### Intercom — "Snippets" (AI-only, not article-level synced blocks)

- **Feature name:** Snippets
- **How it works:** Snippets are standalone knowledge entries designed primarily as a content source for Fin AI Agent and Copilot, **not** as embeddable/synced blocks within help center articles. Community members have explicitly requested "reusable blocks similar to Notion synced blocks" for the Help Center, but this remains a feature request as of early 2026.
- **Key capabilities:**
  - Standalone knowledge entries with title and body (text with basic formatting)
  - AI-first: designed as training data for Fin AI, not for article-level content reuse
  - Audience targeting via filters
  - Folder organization alongside articles
  - Private content: store info for Fin to reference without public visibility
  - Quick creation from conversation insights
- **Limitations:**
  - No synced content blocks in help center articles
  - Snippets are text-only (no images, tables, video)
  - Not a substitute for Zendesk-style content blocks
  - Community feature request exists but is unfulfilled
- **Pricing tier:** Snippets available on all plans: Essential ($29/seat/mo), Advanced ($85/seat/mo), Expert ($132/seat/mo). But synced content blocks in articles do not exist at any tier.
- **Sources:**
  - [Create and manage snippets](https://www.intercom.com/help/en/articles/8074407-create-and-manage-snippets)
  - [Overview of content types and when to use them](https://www.intercom.com/help/en/articles/9357928-overview-of-content-types-and-when-to-use-them)
  - [Introducing Snippets for Fin](https://www.intercom.com/changes/en/24270-introducing-snippets-a-new-text-content-source-for-fin)
  - [Centralized media library request](https://community.intercom.com/knowledge-6/centralized-media-library-for-reusable-assets-in-help-center-10465)

### HubSpot — No Native Synced Content Blocks

- **Feature name:** No equivalent for knowledge base articles
- **How it works:** HubSpot has Snippets (for conversations/emails, max 2,500 chars) and Global Content (for CMS templates — headers, footers, sidebars), but neither works inside knowledge base article bodies. There is an active, upvoted community request for this.
- **Key capabilities (adjacent features):**
  - **Snippets** (conversations): Max 2,500 chars, insert into emails/chats/notes. Not available in KB articles.
  - **Global Content** (CMS): Repeat headers/footers/sidebars across website templates. Does not apply to KB articles.
  - **Smart Content**: Audience targeting on website pages, not content reuse/syncing.
- **Limitations:**
  - No synced content blocks in knowledge base articles at any tier
  - Snippets limited to 2,500 characters and cannot be used in KB
  - Global Content applies to CMS templates only
- **Pricing tier:** Knowledge Base available on Service Hub Professional ($90-100/seat/month) and above. Synced content blocks do not exist at any tier.
- **Sources:**
  - [Create and use snippets](https://knowledge.hubspot.com/conversations/use-snippets)
  - [Be Able to Use Snippets in the Knowledge Base (community request)](https://community.hubspot.com/t5/HubSpot-Ideas/Be-Able-to-Use-Snippets-in-the-Knowledge-Base/idi-p/654229)
  - [Use global content across multiple templates](https://knowledge.hubspot.com/design-manager/use-global-content-across-multiple-templates)

### Common Patterns

| Capability | Zendesk | Salesforce | Intercom | HubSpot |
|---|---|---|---|---|
| Synced content blocks in articles | ✅ | ❌ | ❌ | ❌ |
| Edit once, update everywhere | ✅ | ❌ | ❌ | ❌ |
| Rich content (images, tables, video) | ✅ | N/A | ❌ (text-only snippets) | N/A |
| Usage tracking dashboard | ✅ | ❌ | ❌ | ❌ |
| Unlink/detach option | ✅ | N/A | N/A | N/A |
| Role-based permissions for blocks | ✅ | N/A | N/A | N/A |
| Multilingual synced blocks | ⚠️ Partial (separate translated blocks) | ❌ | ❌ | ❌ |
| API support for content blocks | ⚠️ Partial (read OK, write issues) | N/A | N/A | N/A |
| AI-first content snippets | ❌ | ❌ | ✅ | ❌ |
| Reusable text snippets (non-synced) | N/A | ✅ Quick Text | ✅ Snippets | ✅ Snippets (not in KB) |

### Notable adjacent tools with synced blocks
- **Notion** — Synced Blocks: any block can be synced across pages, edits propagate instantly. Gold standard UX.
- **Confluence** — Include/Excerpt macros: embed content from one page into another. Mature but macro-based, less modern UX.

---

## Current Pylon Implementation

### Data Model

| Table/Struct | Purpose | Reference |
|---|---|---|
| `Article` | Core article entity with title, slug, visibility settings, versioning | `backend/go/src/pylon/models/knowledgebase.go:14-40` |
| `ArticleVersion` | Version history with ContentHTML + ContentJSON (ProseMirror) | `backend/go/src/pylon/models/knowledgebase.go:87-107` |
| `Collection` | Hierarchical article grouping with nested collections | `backend/go/src/pylon/models/knowledgebase.go:109-127` |
| `KnowledgeBase` | Top-level KB entity with metadata, config, layout | `backend/go/src/pylon/models/knowledgebase.go:137-150` |
| `ArticleTemplate` | Reusable article templates (static, not synced) | `backend/go/src/pylon/models/knowledgebase.go:166-176` |
| `ArticleTranslation` | Translation state per language with auto-update and staleness tracking | `backend/go/src/pylon/models/knowledgebase.go:178-232` |
| `ArticleTranslationVersion` | Translated content with original language diff tracking | `backend/go/src/pylon/models/knowledgebase.go:178-232` |
| `ArticleSuggestion` | AI-generated suggestions for new articles or updates | `backend/go/src/pylon/models/knowledgebase.go:251-271` |

### Content Architecture
- **ProseMirror JSON** stored as `ContentJSON` for editing
- **Sanitized HTML** stored as `ContentHTML` for rendering/publishing
- 30+ block types in the rich text editor: accordion, callout, code-block, table, image, video, file, embed, math, etc.
- Full version history per article (draft vs. published versions)
- Hierarchical organization: KnowledgeBase → Collection (nestable) → Article

### Current Capabilities (related to content reuse)
- **Article Templates**: Static templates for article creation — not synced, one-time scaffold only
- **Multilingual syncing**: Translations track staleness when original article changes, with auto-update flag
- **AI article suggestions**: AI-generated content suggestions based on issues/topics
- **Duplicate content detection**: Vector search-based duplicate source detection
- **Rich text editor**: ProseMirror-based editor with 30+ block types, collaborative editing support

### What Does NOT Exist
- No `ContentBlock`, `SyncedBlock`, `ReusableContent`, or similar model/table
- No mechanism to embed a shared content fragment across multiple articles with sync
- No content block dashboard or usage tracking
- No unlink/detach workflow
- No API for managing reusable content blocks

### Key Files

| File | Purpose |
|---|---|
| `backend/go/src/pylon/models/knowledgebase.go` | Core KB data models (Article, ArticleVersion, Collection, KnowledgeBase, ArticleTemplate, translations) |
| `backend/go/src/pylon/models/knowledge.go` | Knowledge associations, training data, external sites |
| `backend/go/src/pylon/models/knowledgebase_comments.go` | Article discussion threads and comments |
| `backend/go/src/pylon/knowledgebase/accessor.go` | Main KB business logic — CRUD, versioning, publishing, search, bulk ops (5000+ LOC) |
| `backend/go/src/pylon/knowledgebase/knowledgebasetypes/knowledgebasetypes.go` | Type definitions: Visibility, AIAgentAccess, ProseMirrorDoc/Node, ArticleSettings |
| `backend/go/src/pylon/graphql/graph/schema.knowledgebase.graphqls` | GraphQL schema: queries, mutations, types for KB |
| `backend/go/src/pylon/graphql/graph/schema.knowledge.resolvers.go` | GraphQL resolvers |
| `frontend/src/pages/app/knowledge-base/` | KB management UI (article pages, collections, templates, settings, metrics) |
| `frontend/src/common/components/document-rte/` | ProseMirror-based rich text editor with 30+ extensions |
| `frontend/src/pages/public-kb/` | Customer-facing public knowledge base portal |
| `backend/go/src/pylon/features/featureflags/flags.go` | Feature flags (MultiKB, multilingual, AI agent KB access, etc.) |

### Feature Flags (KB-related)

| Flag | Purpose |
|---|---|
| `FeatureMultiKnowledgeBase` | Multiple knowledge bases per org (Enterprise) |
| `FeatureArticleTranslation` | Multilingual article support |
| `FeatureUnlimitedKBCopilot` | Unlimited KB AI Copilot usage |
| `multilingual-kb` (LaunchDarkly) | Multilingual KB features |
| `ai-agent-granular-kb-access` (LaunchDarkly) | Per-article/collection AI agent access control |
| `ai-synthesized-public-kb-response` (LaunchDarkly) | AI-synthesized responses on public KB |

---

## Gap Analysis

| Feature | Competitors | Pylon | Gap |
|---|---|---|---|
| Synced content blocks in articles | ✅ Zendesk (mature) | ❌ Not built | **Critical gap vs. Zendesk** — this is Zendesk's key KB differentiator |
| Reusable article templates | ✅ All have some form | ✅ ArticleTemplate model exists | No gap — but templates are static, not synced |
| Rich text editor with 30+ block types | ✅ Zendesk, Intercom | ✅ ProseMirror with 30+ extensions | No gap — strong foundation to build synced blocks on |
| Content block dashboard / usage tracking | ✅ Zendesk | ❌ Not built | Gap — needed for managing blocks at scale |
| Unlink/detach workflow | ✅ Zendesk | ❌ Not built | Gap — important for author flexibility |
| Multilingual synced blocks | ⚠️ Zendesk (partial — separate translated blocks) | ❌ Not built | **Opportunity** — Pylon could do this better by linking translated blocks to their source |
| API support for content blocks | ⚠️ Zendesk (read OK, write broken) | ❌ Not built | **Opportunity** — Pylon could ship with full API support from day one |
| AI-first content snippets for agents | ✅ Intercom (Snippets for Fin) | ❌ Not built (training data is closest) | **Opportunity** — synced blocks could double as AI agent knowledge sources |
| Version history for articles | ✅ All | ✅ ArticleVersion model | No gap |
| Multilingual article translation | ✅ Zendesk, Salesforce | ✅ ArticleTranslation with auto-update + staleness | No gap — strong existing implementation |
| Content block nesting in lists | ❌ Zendesk cannot do this | N/A | **Opportunity** — could differentiate by supporting this |
| Content block permissions | ✅ Zendesk (admin toggle for agents) | ❌ Not built | Gap — needed for team governance |

### Opportunities

1. **Only Zendesk has this — and it's Enterprise-only.** Building synced content blocks would match Zendesk's #1 KB differentiator and leapfrog Salesforce, Intercom, and HubSpot (none of whom have it).
2. **Zendesk's multilingual content blocks are weak** — translated blocks are separate, unlinked objects. Pylon's existing translation infrastructure (auto-update, staleness tracking) could enable linked multilingual synced blocks that automatically flag translations as stale when the source block changes.
3. **Zendesk's API support for content blocks is broken** — writing articles with content blocks via API creates inconsistent state. Pylon could ship with full GraphQL API support for content blocks from day one.
4. **AI + synced blocks** — Synced content blocks could double as knowledge sources for AI agents (similar to Intercom's Snippets concept), creating a unified content reuse system for both human readers and AI.
5. **ProseMirror foundation is ideal** — The existing ProseMirror-based editor with 30+ block types provides a natural extension point. A synced block could be implemented as a new ProseMirror node type that references a shared content entity.
6. **Content block nesting** — Zendesk cannot embed content blocks inside lists. Supporting this would be a concrete differentiator.
7. **Pricing differentiation** — Zendesk locks this behind Enterprise ($169-209/agent/mo). Offering it on a lower tier would be compelling for Zendesk migrations.

### Common Use Cases (from competitor research)

1. Legal disclaimers and compliance notices across many articles
2. Pricing and plan information tables
3. Warning/caution banners (data loss, irreversible actions)
4. Contact information and support hours
5. Product prerequisites or system requirements
6. Feature availability notes ("Available on: Pro, Enterprise")
7. Regulatory/security boilerplate (GDPR, SOC 2)

---

## Customer Feedback

*To be filled in from Pylon conversations — search for "content block", "reusable content", "synced", "update across articles", "disclaimer" related tickets.*

---

## Next Steps

- [ ] Gather customer feedback from Pylon conversations (search for content reuse pain points)
- [ ] Validate gaps with internal stakeholders
- [ ] Design data model: new `ContentBlock` entity with version history, linked to articles via ProseMirror node reference
- [ ] Decide on multilingual strategy: linked translated blocks vs. Zendesk's separate-block approach
- [ ] Decide on AI integration: should synced blocks be available as AI agent knowledge sources?
- [ ] Decide on pricing tier: which Pylon plans get access?
- [ ] Draft PRD with requirements
