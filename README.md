# unlighthouse

This repo will run a workflow periodically to check the performance of multiple sites and generate a report using [unlighthouse](https://unlighthouse.dev). This report will be then deployed to a static site hosted on Netlify.

## [Github Actions & Netlify Example](https://unlighthouse.dev/integrations/ci#github-actions-netlify-example)

This example is for Github Actions and deploys a static client build to Netlify.

```yml
name: Assertions and static report

on:
  workflow_dispatch:

jobs:
  demo:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0

      - name: Install Dependencies
        run: npm install -g @unlighthouse/cli puppeteer netlify-cli

      - name: Unlighthouse assertions and client
        run: unlighthouse-ci --site <your-site> --budget 75 --build-static

      - name: Deploy
        run: netlify deploy --dir=.unlighthouse --prod --message="New Release Deploy from GitHub Actions"
        env:
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}
```

### Additional steps:

1. Create a project in NETLIFY
2. Create a Personal Access Toke in NETLIFY
3. Add the NETLIFY_SITE_ID & NETLIFY_AUTH_TOKEN to the repo secrets.
