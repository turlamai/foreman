# AGENTS.md

## Scope

Foreman is the production-rule-system layer of the TurLamAI product
family: declarative pattern matching over working memory with procedural
right-hand sides. It is not an expert-system shell, a planner, or a
business-rules UI.

## Dependency direction

```text
product -> foreman

foreman -X-> product
foreman -X-> any other family library
```

Foreman is a leaf: it depends on nothing beyond base.

## Invariants

- Elements are immutable; memory changes only through right-hand-side
  actions. Matching is read-only.
- Conflict resolution is exactly: recency, then specificity, then
  declaration order. These are semantics, not implementation details.
- modify is remove plus make: a changed fact is a new event with a fresh
  time stamp. No partial-update semantics hides which fact version a match
  used.
- The engine is deterministic given a deterministic assert order; no
  hidden randomness anywhere.
- A stalled program terminates at the cycle cap — bounded and observable,
  never an unbounded hang.
- Public API changes land in the same change as their scribble
  documentation and both READMEs.

## 设计流程（原型先行）

所有 UI 开发与界面改造一律先原型后代码：brief → `design/DESIGN.md`
视觉契约 → HTML 原型 → 按 HIG 基准评审通过才开工；改界面先改原型再改
代码。契约与原型放本仓 `design/`（尚未建立时随首个 UI 切片建立），
实物截图验收后才能作为对外宣传素材。
