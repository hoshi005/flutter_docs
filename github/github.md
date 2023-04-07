# Github 便利情報

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Github 便利情報](#github-便利情報)
  - [Auto Assign](#auto-assign)
  - [PRテンプレート](#prテンプレート)
  - [renovate](#renovate)
  - [Labeler](#labeler)

<!-- /code_chunk_output -->


## Auto Assign

- https://probot.github.io/apps/auto-assign/
- Githubに追加、リポジトリに追加
- .github/auto_assign.yml に設定を記述
- 自分はレビュワーにできないらしい！！

## PRテンプレート

- .github/PULL_REQUEST_TEMPLATE.md に記述
- なぜ大文字になっているのかは不明w

## renovate

- https://github.com/apps/renovate
- 依存パッケージのアップデートを自動でやってくれる
- Githubに追加、リポジトリに追加

## Labeler

- PRに対して、ラベルを自動付与してくれる
- `.github/workflows/labeler.yml`

```yml
name: "Pull Request Labeler"
on:
  - pull_request_target

jobs:
  triage:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/labeler@v4
      with:
        repo-token: "${{ secrets.GITHUB_TOKEN }}"
        sync-labels: true
```

- `.github/labeler.yml`

```yml
document:
- '*'
```