# md-to-web

Turn md files to website with [palpatine](https://github.com/batunpc/palpatine) and github workflows

This example workflow (on push event) will convert the "files" folder md/txt files to a website and push it to gh-pages branch what is hosted with github pages https://maurerkrisztian.github.io/md-to-web/

```yml
name: md-to-website

on:
  push:
    branches:
      - main

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    steps:

    # Any prerequisite steps
    - uses: actions/checkout@master
    - run: mkdir -p ./build/dist && ./palpatine -i ./files -o ./build
    # Deploy to local repo
    - name: Deploy
      uses: s0/git-publish-subdir-action@develop
      env:
        REPO: self
        BRANCH: gh-pages
        FOLDER: build/dist/
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
