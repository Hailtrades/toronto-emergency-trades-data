# Publishing to HF / Kaggle / data.world / Zenodo (needs Malcolm's accounts)

Blocked: no credentials in the vault (only a Cloudflare card), no Hailtrades mailbox, browser not logged in to GitHub. Accounts need an email verification and CAPTCHA, so they must be created by Malcolm.

## Zenodo (DOI), easiest, ~3 min
1. https://zenodo.org/login -> "Log in with GitHub" as wyllieonchain, authorize.
2. https://zenodo.org/account/settings/github/ -> toggle ON `toronto-emergency-trades-data`.
3. Tell Hermes. It will run `gh release create v2026.11.26` on the repo. Zenodo mints the DOI from `.zenodo.json`. Then add the DOI badge to the README.

## Hugging Face
1. https://huggingface.co/join (or "Sign in with GitHub"), username e.g. `hailtrades`. Verify email.
2. https://huggingface.co/settings/tokens -> new token, role Write. Give it to Hermes (store in vault/secrets, do not paste in chat logs).
3. Hermes runs: `hf upload hailtrades/toronto-emergency-trades data --repo-type dataset` plus `distribution/huggingface-README.md` as README.md.

## Kaggle
1. https://www.kaggle.com/account/login -> register (phone verification may be needed). Username e.g. `hailtrades`.
2. Settings -> API -> Create New Token (kaggle.json). Give it to Hermes.
3. Hermes copies the 3 files + `distribution/kaggle-dataset-metadata.json` (rename dataset-metadata.json, set id, license CC-BY-4.0 via UI if CLI rejects) and runs `kaggle datasets create -p dir`. Verify after upload that Kaggle shows CC BY 4.0.

## data.world
1. https://data.world/join -> create account/org `hailtrades`.
2. Settings -> Advanced -> API token (read/write). Give it to Hermes.
3. Hermes uploads via `dw` CLI or API with the same description and license CC BY 4.0. Or drag the 3 files into "New dataset" and paste the HF card text.

## Logo for dataset pages (after each account exists)
- Hugging Face: card already embeds the logo from GitHub raw; also set the org/user avatar to `assets/logo-512.png`.
- Kaggle: dataset Settings -> cover image: upload `assets/github-social-1280x640.png`; profile avatar `assets/logo-512.png`. (The CLI metadata has no image field.)
- data.world: org avatar `assets/logo-512.png`; dataset cover image `assets/github-social-1280x640.png` (UI only).
- Zenodo: .zenodo.json cannot hold images; skipped.
