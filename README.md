name: Update README

on:
  schedule:
    - cron: '0 * * * *'
  push:
    branches:
      - main

jobs:
  update-readme:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: '14'
      - run: npm install
      - run: npm run update-readme
      - run: git config --global user.name 'github-actions[bot]'
      - run: git config --global user.email 'github-actions[bot]@users.noreply.github.com'
      - run: git add README.md
      - run: git commit -m 'Update README'
      - run: git push
