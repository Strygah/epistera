# Epistera — shared docs

Password-gated static pages hosted on GitHub Pages.

- `index.html` — Founders First Principles comparison (Alexey, Dima, Evgeny). Client-side AES-encrypted with `staticrypt`. Decrypts in the browser after the visitor enters the shared password.

## Re-encrypting

Edit the source HTML in `_Projects/Epistera/Strategy/Founders_First_Principles_Comparison.html` (Google Drive), then:

```bash
cd ~/Dev/epistera
cp "$HOME/Library/CloudStorage/GoogleDrive-alexey.strygin@gmail.com/My Drive/_Projects/Epistera/Strategy/Founders_First_Principles_Comparison.html" founders-comparison-source.html
npx -y staticrypt founders-comparison-source.html -p "$PASSWORD" --short \
  --template-title "Epistera — Founders First Principles" \
  --template-instructions "Internal document. Enter the password Alexey shared." \
  --template-color-primary "#1d4e89" \
  --template-color-secondary "#fafaf7" \
  -d encrypted
mv encrypted/founders-comparison-source.html index.html
rmdir encrypted
git add index.html && git commit -m "Refresh comparison" && git push
```

The plaintext source file and `.staticrypt.json` are gitignored — never commit them.
