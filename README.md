name: Generate Snake Animation

on:
  schedule:
    - cron: "0 */12 * * *"
  workflow_dispatch:

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - uses: actions/checkout@v3

      - uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg?palette=github-light&color_snake=000000&color_dots=#cccccc,#aaaaaa,#888888,#555555,#ffffff
            dist/github-snake-dark.svg?palette=github-dark&color_snake=ffffff&color_dots=#1a1a1a,#333333,#555555,#888888,#ffffff

      - uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
