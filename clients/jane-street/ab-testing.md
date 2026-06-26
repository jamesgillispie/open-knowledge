---
type: note
title: AB Testing
description: Jane Street notes on Payload CMS AB testing, AI embeddings, audit logs, and publication workflow plugin setup.
tags:
  - client
  - jane-street
  - area17
---
# AB Testing

AB Testing Plugin Setup Complete

Installed

- @payloadcms/plugin-ab-testing@0.0.2

Files Created

1. middleware.ts - Next.js middleware that reads the AB manifest and uses the built-in abMiddleware to randomly assign visitors to variants and rewrite URLs via cookies
2. src/app/(frontend)/[slug]/page.tsx - Dynamic page route for the pages collection (exports PageTemplate for reuse by variants)
3. src/app/(frontend)/[slug]/variants/[id]/page.tsx - Variant page route that fetches the variant document by ID and renders it using the same PageTemplate

Files Modified

4. src/payload.config.ts - Added the abTesting plugin with payloadGlobalConfig storage adapter, configured for the pages collection with path generation (/home maps to /, all others use /{slug})
5. src/collections/Pages.ts - Reverted to original (the plugin auto-adds _variantOf and _variants fields)
6. src/payload-types.ts - Regenerated (now includes _variantOf field on Page type)
7. src/app/(payload)/admin/importMap.js - Regenerated (includes the plugin's VariantsCell and VariantsField components)

How it works

- The plugin adds _variantOf (relationship) and _variants (UI field) to the pages collection automatically
- Variants are created as documents in the same pages collection, linked via _variantOf to their parent
- Variants are hidden from the admin list view (only parents show)
- The manifest global (abManifest) maps page paths to their variant rewrites
- Middleware randomly assigns visitors to a variant or the original, persisted via cookies

Note

There's a pre-existing type error with the @ai-sdk/openai compatibility property that surfaced after the lockfile update. This is unrelated to the AB testing changes.

---

Done. Here's a summary of what was set up:

Installed: @payloadcms/plugin-ai-embeddings@1.0.0

Configuration:
- Embedding model: text-embedding-3-large (3072 dimensions) via OpenAI
- Similarity search: similaritySearchAdapterLocal() (local MongoDB, not Atlas)
- Admin search: Enabled, pointing to the auto-generated content-embeddings collection
- Collections indexed: pages, blog-posts, events, jobs
    - Each extracts title + relevant text/rich text content fields

Before running, you'll need:
1. OPENAI_API_KEY in your .env (not currently present)
2. The similarity search endpoint will be available at: http://janestreet-demo.local:3000/api/content-embeddings/similarity-search?text="your query"

---

Config changes (src/payload.config.ts):
- Added import { auditLogs } from '@payloadcms/plugin-audit-logs'
- Added auditLogs() to the plugins array (using default options — logs all collections/globals)

Still needed from you:
- Set the PAYLOAD_NPM_KEY env var so the private package can be installed
- Run pnpm add @payloadcms/plugin-audit-logs@3.76.1
- Run pnpm generate:types and pnpm generate:importmap after install

Do you have the npm key available, or would you like me to try a different approach?

---

The plugin is fully installed and configured. Here's a summary of everything that's already in place:

Package: @payloadcms/plugin-publication-workflows@^1.3.5 is installed in node_modules

.npmrc: Configured with //registry.npmjs.org/:_authToken=${PAYLOAD_NPM_KEY}

.env: Has PAYLOAD_PLUGIN_KEY=npm_WdOXcrUg4wZ9Ga... (the token)

Config (src/payload.config.ts):
- Plugin imported and added to plugins array (line 103-108)
- Applied to pages collection with reviewWorkflow

Workflow (src/workflows/index.ts):
- 3-step review workflow: Business Review → Accuracy Review → Final Review
- Each step has admin-only read access on its review collection

Users (src/collections/Users.ts):
- Has roles field with editor and admin options (default: editor)

Pages (src/collections/Pages.ts):
- versions: { drafts: true } enabled
- Access control uses changeDraftsOnly for create/update, isAdmin for delete
- Public read filtered to _status: 'published'

Access helpers (src/access/):
- isAdmin.ts — checks user.roles.includes('admin')
- isEditor.ts — checks user.roles.includes('editor')
- changeDraftsOnly.ts — admins can do anything, editors can only publish if workflow is complete
- workflowIsReady.ts — queries the workflows collection to check if all steps are complete

Everything is wired up. You should be able to run pnpm dev and see the publication workflow sidebar on Pages documents. Want me to start the dev server to verify it's working?
