---
name: ontoly-software-graph
description: "Use Ontoly to build and query a deterministic Software Graph before manually searching a TypeScript repository. Use when asked about architecture, dependencies, routes, services, modules, configuration, request traces, impact analysis, or codebase onboarding."
metadata:
  version: "1.0.0"
  author: "0xsarwagya"
  tags: ["code-analysis", "software-graph", "typescript"]
license: MIT
---

# Ontoly Software Graph

Use this skill when a user asks codebase-understanding questions that should be answered from Ontoly's deterministic Software Graph.

## Steps

1. Verify whether an Ontoly graph already exists.
2. If no graph exists or it is stale, run:

```bash
ontoly build .
```

3. Check graph diagnostics, trust, graph hash, and detected frameworks.
4. Use Ontoly CLI or MCP capabilities before searching files directly.
5. Answer with concrete graph evidence: node IDs, edge types, source locations, diagnostics, route paths, package names, and confidence.
6. Inspect source files only when Ontoly cannot answer or reports low confidence.

## Useful commands

```bash
ontoly build .
ontoly inspect
ontoly graph
ontoly trace
ontoly mcp
```

## Notes

- Do not invent relationships that are not present in the graph.
- Separate measured graph facts from inferred observations.
- If the graph is missing evidence, explain what query or validation step should run next.
