# djLint Config

My djLint config for djLint 1.42+.

Install djLint using Homebrew: `brew install djlint`

Clone this repository to `~/.config/djlint`

For formatting in VSCode, `jkillian.custom-local-formatters` extension is recommended. Use a wrapper shell script to enable custom config in djLint:

```json
"customLocalFormatters.formatters": [
  {
    "command": "\"$HOME/.local/bin/djlint-vscode-format\"",
    "languages": [
      "volt"
    ]
  }
]
```

Create a wrapper shell script

```zsh
mkdir -p "$HOME/.local/bin"

cat > "$HOME/.local/bin/djlint-vscode-format" <<'SH'
#!/usr/bin/env bash
set -euo pipefail

# read from stdin and write formatted Volt to stdout
/opt/homebrew/bin/djlint \
    --configuration "$HOME/.config/djlint/djlint.toml" \
    --reformat - \
    | sed -E 's/<([A-Za-z][A-Za-z0-9:-]*) +>/<\1>/g'
SH

chmod +x "$HOME/.local/bin/djlint-vscode-format"
```

For more information see:

- [djLint](https://djlint.com/)
- [VSCode marketplace for Custom Local Formatters](https://marketplace.visualstudio.com/items?itemName=jkillian.custom-local-formatters)
