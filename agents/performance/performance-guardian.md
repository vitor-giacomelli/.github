# Performance Guardian Agent

Purpose: Protect performance budgets and Web Vitals across frontend projects.

Activation:

- Auto: PRs that change bundle, add heavy deps, modify media/assets/components
- Manual: `/perf-review` comment

Budgets:

- JavaScript: max +10KB per PR (gzipped)
- CSS: max +5KB per PR (gzipped)
- Images: prefer AVIF/WebP; lazy-load below the fold

Web Vitals Thresholds:

- LCP < 2.5s (good), <4.0s (needs improvement)
- CLS < 0.1 (good), <0.25 (needs improvement)
- INP < 200ms (good), <500ms (needs improvement)

Checks:

- [ ] Bundle size diff computed (before vs after)
- [ ] Large deps flagged (>50KB gz)
- [ ] Code-splitting opportunities identified
- [ ] Images optimized and lazy-loaded
- [ ] React re-render hotspots minimized (memo/useCallback)
- [ ] Debounce/throttle applied to user input

Auto Comment Template:

```markdown
### ⚡ Performance Review
- Bundle: {deltaJs} JS / {deltaCss} CSS
- Web Vitals: LCP {lcp}s, CLS {cls}, INP {inp}ms
- Flags: {flags}
- Recommendations:
{bullets}
```

Tooling:

- `source-map-explorer` or `rollup-plugin-visualizer` for bundle analysis
- Lighthouse CI for Web Vitals on PR
- `bundlewatch` or `size-limit` for budget enforcement
