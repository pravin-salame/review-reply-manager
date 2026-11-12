# Review Reply Manager

Paste Google reviews, get a draft reply for each one, and a flag on the reviews that need a human.
Runs on Cloudflare Workers (free plan) and the Google Gemini API (free tier).

## Structure

- `public/index.html`: home page (edit the email address and price in this file)
- `public/app/index.html`: the tool
- `src/index.js`: the API at `/api/reply`
- `wrangler.jsonc`: Cloudflare settings (project name, model ID)

## Run it on your computer

Install Node.js (version 20 or newer), then in this folder:

    npm install
    cp .dev.vars.example .dev.vars     # then edit .dev.vars and add your Gemini key
    npm run dev

Open the address it prints (usually http://localhost:8787).

## Deploy for free

    npm install
    npx wrangler login                 # opens your browser; sign in to your free Cloudflare account
    npx wrangler secret put GEMINI_API_KEY
    npx wrangler secret put ACCESS_CODE
    npm run deploy

Wrangler prints your live address (for example `https://review-replies.your-name.workers.dev`).
The home page is at that address and the tool is at `/app`.

To update later, change the files and run `npm run deploy` again.

## Before you share it

1. In `public/index.html`, replace `you@example.com` (two places) and `[price]`.
2. In `wrangler.jsonc`, set `GEMINI_MODEL` to a model ID that Google AI Studio lists with a free tier.
3. Give customers the `/app` link and your access code.

## Notes

- Use it for public reviews only. Google's free tier may use submitted content to improve its products.
- Replies are drafts. Customers should read and edit each one before posting.
- Free-plan limits (checked November 2026): Workers allows 100,000 requests a day; Gemini free-tier limits are shown in your AI Studio console.
