# Refactor brief — next-go

## If rebuilt today

- **Next 15 + React 19**, App Router only.
- **Env**: replace the hand-rolled `src/env/*.mjs` with `@t3-oss/env-nextjs` +
  `experimental__runtimeEnv`. It does exactly the same split (server/client schemas, fail-fast) with
  less code. If staying hand-rolled, convert `format.mjs` to TypeScript.
- **Tailwind v4**: no `tailwind.config.ts`; tokens move into `@theme` in CSS. The `cn()` helper
  stays (`clsx` + `tailwind-merge`).
- **Fonts**: `next/font` with a local `fonts.ts` is still the right pattern — keep it.
- **Package manager**: Bun is fine; commit `bun.lock` (text), not `bun.lockb`.
- **Delete**: `declarations.d.ts` (covered by TS 5), `.eslintrc.json` (flat config now).

## If you want a cloneable starter again

Two options:
1. Recreate it from the tag: `git checkout legacy-2026-11 -- .` on a fresh branch, then upgrade in
   place.
2. Start from `create-next-app` and port only `src/env/*` and `src/lib/index.ts` — everything else
   is stock.

Option 2 is cheaper; the env pattern is the only original idea.

## Recover the code

```bash
git clone https://github.com/RamiroG8k/next-go && cd next-go
git checkout legacy-2026-11
```
