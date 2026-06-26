---
type: note
title: Infrastructure & Hosting
description: Jane Street project notes on infrastructure, hosting, deployment model, database, and stack decisions from Luis.
tags:
  - client
  - jane-street
  - area17
---
# Infrastructure & Hosting

**Infrastructure & Hosting** Luis is provisioning to AREA 17's European server (not Digital Ocean droplets). For the Jane Street demo, it's hosted there to avoid data concerns. Production deployment will eventually run on Jane Street's internal infrastructure.

**Deployment Model** Jane Street uses Mercurial internally, but you're building with Git. Luis's solution: tag releases in Git, pipeline packages everything into a zip file, and Jane Street unpacks and deploys via script. This is the same pattern they used for BCA. No direct Git access to their infrastructure needed.

**Database Decision** Postgres, not MongoDB. Luis flagged MongoDB licensing issues (becomes commercial at scale) and deployment complexity. Postgres is open source under OSI, which fits Jane Street's security posture better.

**Technology Stack** Next.js, Payload CMS, TypeScript, Tailwind, Postgres. This is locked in—no flexibility here.

**CI/CD** You can run builds locally for demos. The pipeline handles release packaging automatically. When ready for production, you send Jane Street a tarball snapshot of the code that they build themselves on their infrastructure.

**Mercurial vs Git Flexibility** Luis pushed back on Jane Street expecting you to adopt their entire workflow. His stance: Git is standard everywhere (npm, registries, etc.), so Jane Street needs to handle conversion or accept the tarball approach. He's dealt with Mercurial before but made clear there's a limit to how much tooling you reshape for a client.

**What You Need to Know** If infrastructure questions come up with Jane Street, Luis is the only person on the AREA 17 side who can handle Mercurial conversion or unusual deployment scenarios. You can pull him in as needed.
