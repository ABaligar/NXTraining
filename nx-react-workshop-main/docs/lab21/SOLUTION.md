##### GitHub CD setup

```
name: Deploy Website

on:
  push:
    branches:
      - master

env:
  SURGE_DOMAIN: ${{ secrets.SURGE_DOMAIN }}
  SURGE_TOKEN: ${{ secrets.SURGE_TOKEN }}
  HEROKU_API_KEY: ${{ secrets.HEROKU_API_KEY }}
  NX_API_URL: https://<your-heroku-app>.herokuapp.com

jobs:
  build:
    runs-on: ubuntu-latest
    name: Deploying apps
    steps:
      - uses: actions/checkout@v2.3.4
      - uses: bahmutov/npm-install@v1.4.5
      - run: npm run nx build store -- --configuration=production
      - run: npm run nx build api -- --configuration=production
      - run: npm run nx deploy store
      - run: npm run nx deploy api
```
