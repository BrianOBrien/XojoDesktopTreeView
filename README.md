# XojoDesktopTreeView

A cross-platform TreeView implemented using `DesktopListBox` (Xojo Desktop 2025+).
Works on Windows and Linux (including Raspberry Pi), with dark/light mode support via `ColorGroup`s.

## Features

- Tree model + view separation (`TreeNode` + `DesktopTreeView`)
- Expand/collapse with disclosure glyphs
- Selection event returns a stable `Path` string
- Dark/light styling using `ColorGroup` properties (no platform-specific SystemColors)
- Handles deep nesting and large node counts (stress tested with generated data)

## Components

### `TreeNode` (model)
- `Name As String`
- `Value As String`
- `Path As String`
- `Children() As TreeNode`

### `TreeNodeFactory` (builder)
- `FromJSON(jsonText As String, rootName As String = "root") As TreeNode`
- `FromDictionary(d As Dictionary, rootName As String = "root") As TreeNode`
- `FromVariant(name As String, v As Variant, parentPath As String) As TreeNode`

### `DesktopTreeView` (DesktopContainer)
Wraps a `DesktopListBox` and renders a tree using:
- `PaintCellBackground`
- `PaintCellText`
- `MouseDown`
- `SelectionChanged`

## Setup / Usage

1) Drop `DesktopTreeView` onto a Window.
2) Configure these `ColorGroup` properties on the container (Light/Dark values):
- `TreeTextColor`
- `TreeSelectedTextColor`
- `TreeRowEvenColor`
- `TreeRowOddColor`
- `TreeSelectedRowColor`

3) Load data:

```xojo
Var root As New Dictionary
root.Value("Hello") = "World"
DesktopTreeView1.LoadFromDictionary(root, "Root")

Var json As String = "{""a"":1,""b"":[2,3]}"
DesktopTreeView1.LoadFromJSON(json, "Root")

