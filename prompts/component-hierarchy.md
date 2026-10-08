# Prompt: Turn a frontend codebase into a component explorer

Analyze the actual frontend source and generate a **single interactive HTML document** explaining a relevant component hierarchy. The explorer should answer: *What renders what? Where does data come from? Which parts can change or disappear?*

## Input

- Repository: **[local path or public GitHub URL]**.
- Entry point or feature: **[route, component, page, or user flow]**.
- Desired depth: **[e.g., root to three important leaves]**. Focus on a useful subtree instead of dumping every component.

## Source analysis

1. Pin an exact commit before analyzing. Inspect the entry point, JSX/TSX imports, component definitions, custom hooks, context providers and the relevant calling sites.
2. Identify direct render edges, props, state ownership, context reads, event callbacks, composition slots, portals and conditional branches. Label each relationship based on evidence from the source.
3. Distinguish **source-level component composition** from **runtime DOM hierarchy**. Suspense, portals, tunnels, conditions and higher-order components may make them different.
4. Never claim re-render counts, state propagation or runtime behavior you cannot verify statically. Mark inferences and illustrative flows as such.
5. For every node, provide a permalink to a real file and line at the pinned revision. Ensure the name, edge type and described props are grounded in that source.

## The explorer

- Interactive expand/collapse tree, searchable by component name or source path, with filters for component roles.
- Selecting a node reveals its responsibilities, parent chain, important props, relevant state/context and linked source location.
- Visually distinguish providers, core/editor components, UI components, custom child slots and conditional/portal connections.
- One or two **guided traces**, such as from an app entry to a toolbar or from an event callback to the state owner. Highlight the observed path and clearly label approximations.
- Controls that work without scrolling through a huge SVG; make the hierarchy navigable with keyboard and on a narrow screen.

## Output and checks

- Write `components.html` with all styles, behavior and source-derived data inline. No npm packages, frameworks, CDN requests or runtime network calls.
- Add a provenance note: repository URL, full pinned commit and coverage/limitations of the chosen subtree.
- Validate that node IDs are unique, edges reference existing nodes, there are no cycles, and source file/line links resolve to inspected files.
- Open the page in a browser and test expansion, selection, search, filters, guided traces, responsive layout, light/dark modes and console errors.
- Summarize what is mapped, what is not and anything that could not be statically established.

**Key principle:** An accurate small map is more useful than a misleading complete one.
