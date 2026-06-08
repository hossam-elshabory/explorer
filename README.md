> [!IMPORTANT]
> This is a fork from the [@quartz-community/explorer](https://github.com/quartz-community/explorer) with extended features. It was ported from an internal explorer component version created for my Quartz 4 site using Gemini 3.5 Flash with a ralph loop.

# @hossam-elshabory/explorer

The Explorer component for Quartz - navigate your digital garden with an interactive file tree.

## Features

- 📁 Interactive folder tree with collapse/expand functionality
- 📱 Mobile-friendly slide-out navigation
- 💾 Persistent state (remembers open/closed folders)
- 🔗 Configurable folder click behavior (link or collapse)
- ⚡ Built-in search and overflow handling
- 🎨 Custom Lucide React icon support directly via frontmatter
- 🔢 Explicit folder and file ordering via frontmatter
- 📂 Custom folder expansion/collapse defaults via frontmatter

## Installation

```bash
npx quartz plugin add github:hossam-elshabory/explorer
```

## Usage

Enable the plugin in your Quartz layout:

```yaml title="quartz.config.yaml"
plugins:
  - source: github:hossam-elshabory/explorer
    enabled: true
    layout:
      position: left
      priority: 50
```

For advanced use cases, you can override properties in TypeScript:

```ts title="quartz.ts (override)"
import * as ExternalPlugin from "./.quartz/plugins";

ExternalPlugin.Explorer({
  title: "Explorer",
  folderDefaultState: "collapsed",
  folderClickBehavior: "link",
  useSavedState: true,
});
```

---

## Frontmatter Configuration (Markdown Notes)

You can customize icons, ordering, and default collapse states directly in the frontmatter of your Markdown files.

### 1. Custom Icons (`icon`)
Assign any valid [Lucide React Icon](https://lucide.dev/icons) name to files or folders:

```yaml
---
title: My note
icon: book-alert
---
```

### 2. Folder Ordering (`folderOrder`)
To specify a custom sort order for a folder, assign `folderOrder` in the folder's representative index file (e.g. `index.md` inside that folder). Folders with lower numbers are sorted first:

```yaml title="content/my-folder/index.md"
---
title: My Folder
folderOrder: 1
icon: folder-heart
---
```

### 3. File/Note Ordering (`noteOrder`)
To specify a custom sort order for individual notes inside a folder, assign a `noteOrder` value. Files with lower numbers are sorted first:

```yaml title="content/my-folder/first-note.md"
---
title: First Note
noteOrder: 1
icon: file-text
---
```

### 4. Custom Folder Collapse Defaults (`collapse` / `collapsed`)
Force individual folders to default to open or closed on startup, overriding the global `folderDefaultState` value. This is specified in the folder's `index.md` file:

```yaml title="content/my-folder/index.md"
---
title: My Folder
collapse: false  # Force this folder to default to expanded (open) on startup
---
```

---

## Configuration Options

```typescript
interface ExplorerOptions {
  /** Title displayed above the explorer */
  title?: string;

  /** Default state for folders: "collapsed" or "open" */
  folderDefaultState: "collapsed" | "open";

  /** Behavior when clicking folders: "collapse" to toggle, "link" to navigate */
  folderClickBehavior: "collapse" | "link";

  /** Whether to persist folder state in localStorage */
  useSavedState: boolean;

  /** Custom sort function for entries */
  sortFn?: (a: FileTrieNode, b: FileTrieNode) => number;

  /** Custom filter function for entries */
  filterFn?: (node: FileTrieNode) => boolean;

  /** Custom map function for transforming entries */
  mapFn?: (node: FileTrieNode) => void;

  /** Order in which to apply filter, map, and sort */
  order?: Array<"filter" | "map" | "sort">;
}
```

## Default Behavior

By default, the Explorer:

- Shows folders in a collapsed state
- Opens folders when clicked (navigates to index page)
- Saves folder states between sessions
- Excludes the "tags" folder from the tree
- Sorts folders first, then files alphabetically

## Development

This is a first-party Quartz community plugin. It serves as both:

1. A production-ready Explorer component
2. A reference implementation for building Quartz community plugins

## Documentation

See the [Quartz documentation](https://quartz.jzhao.xyz/features/explorer) for more information.

## License

MIT
