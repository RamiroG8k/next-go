# next-go

> **Legacy — documentation only.** The source was removed from `master` on 2026-11-13 and is
> preserved at tag [`legacy-2026-11`](https://github.com/RamiroG8k/next-go/tree/legacy-2026-11).
>
> This was the template every 2024 project was scaffolded from (`geb`, `prueba`, `3DM`,
> `pedro-tattooer`, `animoving`). Docs-only means it can no longer be cloned as a starter —
> see the rebuild notes for how to recreate it.

## What it was

A Next.js App Router boilerplate with three opinions baked in:

1. **Typed environment variables** — Zod schemas split into `serverSchema` and `clientSchema`,
   validated at build/start, exported as one `env` object.
2. **`cn()`** — `twMerge(clsx(...))`, the shadcn-style class merger.
3. **The boring scaffolding** — `src/app/layout.tsx`, `fonts.ts` (next/font), `sitemap.ts`,
   `types/`, `declarations.d.ts`, ESLint, Tailwind, `bun.lockb`.

Built 2024-08 (10 commits), public.

## The env pattern (the reason this repo existed)

```
src/env/schema.mjs   # zod: serverSchema + clientSchema
src/env/client.mjs   # NEXT_PUBLIC_* → parsed client env
src/env/server.mjs   # server-only vars
src/env/format.mjs   # error formatting
src/env/index.mjs    # merges into `env`
```

Any module imports `env` from `~/env` and gets validated values. Missing or malformed vars fail
fast with a readable error instead of `undefined` at runtime.

## What worked, worth reusing

- The split between client and server schemas — `NEXT_PUBLIC_*` validated separately stops secrets
  leaking into the bundle.
- `cn()` as the single class-merging helper.
- `next/font` loaded once in `fonts.ts` and re-exported.

## Why it stopped

Next.js absorbed most of it (`next/font`, typed env via `@t3-oss/env-nextjs`), Tailwind moved to v4
with a CSS-first config, and the boilerplate stopped paying rent.

## Rebuild notes

See [docs/refactor-brief.md](docs/refactor-brief.md).

## Recover the code

```bash
git clone https://github.com/RamiroG8k/next-go && cd next-go
git checkout legacy-2026-11
bun install && bun dev
```
