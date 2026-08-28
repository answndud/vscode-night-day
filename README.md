# Night MJY

A high-contrast VS Code color theme with an electric cyan, Tornado Cash-inspired neon green, and lavender accent palette.

Night MJY includes both a dark theme for focused coding sessions and a clean white light theme for bright environments.

## Themes

### Night (MJY)

- Editor background: `#2B2F45`
- Variables and parameters: bright white
- Strings and keywords: neon green `#94FEBF`
- Functions and methods: cyan `#8BE9FD`
- Types and classes: lavender-blue `#91B4D5`
- Annotations and brackets: lavender `#C4B5FF`

### Day (MJY)

- Editor background: `#FFFFFF`
- Variables and parameters: dark ink for reliable contrast
- Strings and keywords: high-contrast green
- Functions and methods: vivid blue
- Types and classes: indigo
- Annotations and brackets: high-contrast lavender

Both themes include semantic token colors and explicit bracket-pair colors for Java, Python, TypeScript, JavaScript, and other languages.

## Installation

### From the Marketplace

Search for **Night MJY** in the VS Code Extensions view after the extension is published.

### From a VSIX file

1. Download the latest `.vsix` file from the [Releases](../../releases) page.
2. Open VS Code.
3. Open the Command Palette and run **Extensions: Install from VSIX...**.
4. Select the downloaded file.
5. Run **Preferences: Color Theme** and choose `Night (MJY)` or `Day (MJY)`.

You can also install from a terminal:

```sh
code --install-extension night-mjy-0.2.5.vsix
```

## Development

1. Clone this repository and open it in VS Code.
2. Press `F5` to launch an Extension Development Host.
3. Open **Preferences: Color Theme**.
4. Select `Night (MJY)` or `Day (MJY)`.

Theme definitions live in [`themes/`](themes/).

## Packaging

Install the VS Code Extension Manager and create a VSIX package:

```sh
npm install -g @vscode/vsce
vsce package
```

The generated VSIX can be installed locally or uploaded to the Visual Studio Marketplace.

## License

MIT
