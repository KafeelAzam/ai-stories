# Social Stories — Vercel Deploy

## Structure
- `index.html` — the app (static, served as-is)
- `api/generate-story.js` — serverless function that securely calls the Anthropic API using a server-side key

## Steps to deploy

1. **Anthropic API key banayen**
   - https://console.anthropic.com par jayen → API Keys → Create Key
   - Key copy kar lein (sk-ant-... se shuru hogi)

2. **Is folder ko GitHub par push karen** (ya seedha Vercel CLI se deploy karen)
   ```bash
   git init
   git add .
   git commit -m "social stories app"
   git remote add origin <your-repo-url>
   git push -u origin main
   ```

3. **Vercel par import karen**
   - https://vercel.com/new → apna GitHub repo select karen → Import
   - Framework preset: "Other" (koi build step nahi chahiye)

4. **Environment Variable add karen** (zaroori step, warna API kaam nahi karegi)
   - Vercel project → Settings → Environment Variables
   - Add: `ANTHROPIC_API_KEY` = `<apki asli key>`
   - Production, Preview, Development teeno mein add karen
   - Deploy/Redeploy karen taake variable load ho jaye

5. **Deploy** — Vercel apne aap `index.html` ko static serve karega aur `api/generate-story.js` ko `/api/generate-story` route pe serverless function ke tor par run karega.

## Local testing (optional)
```bash
npm i -g vercel
vercel dev
```
Isse localhost pe dono (static file + API route) ek sath chalte hain.

## Note on cost
Har "Create Story" click ek Anthropic API call karta hai jo aapki key se billed hoti hai. Agar public site hai to rate-limiting (e.g. per-IP) add karna consider karen taake koi abuse na kar sake.
