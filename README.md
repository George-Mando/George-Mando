<!-- XENCLIPSE HIVE CONTROL PANEL — George Mando -->

<div align="center">

![header](svgs/header.svg)

</div>

---

<div align="center">

![bio](svgs/bio-panel.svg)

</div>

---

<div align="center">

![projects](svgs/projects-panel.svg)

</div>

---

<div align="center">

![tech](svgs/tech-panel.svg)

</div>

---

<!-- LIVE STATS — rendered via github-readme-stats (GitHub-hosted) -->
<div align="center">

<img height="175em" src="https://github-readme-stats.vercel.app/api?username=George-Mando&show_icons=true&theme=merko&include_all_commits=true&count_private=true&hide_border=true&bg_color=000800&title_color=00ff9c&icon_color=00ff9c&text_color=55cc88&border_color=00ff9c&custom_title=TELEMETRY+READOUT"/>
&nbsp;
<img height="175em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=George-Mando&layout=compact&langs_count=8&theme=merko&hide_border=true&bg_color=000800&title_color=00ff9c&text_color=55cc88&custom_title=LANG+MATRIX"/>

</div>

<div align="center">

![Streak](https://streak-stats.demolab.com?user=George-Mando&theme=merko&hide_border=true&background=000800&ring=00FF9C&fire=FF6B35&currStreakLabel=00FF9C&sideLabels=00FF9C&dates=448844&strokeWidth=0.8)

</div>

<div align="center">

[![Activity Graph](https://github-readme-activity-graph.vercel.app/graph?username=George-Mando&theme=react-dark&bg_color=000800&color=00ff9c&line=00ff9c&point=ff6b35&area=true&hide_border=true&area_color=001a06)](https://github.com/ashutosh00710/github-readme-activity-graph)

</div>

---

<!-- HIVE NEURAL ACTIVITY (snake — activate via Actions) -->
<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/George-Mando/George-Mando/output/github-contribution-grid-snake-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/George-Mando/George-Mando/output/github-contribution-grid-snake.svg">
  <img alt="hive neural activity" src="https://raw.githubusercontent.com/George-Mando/George-Mando/output/github-contribution-grid-snake-dark.svg"/>
</picture>

</div>

---

<!-- TROPHIES -->
<div align="center">

[![trophy](https://github-profile-trophy.vercel.app/?username=George-Mando&theme=matrix&no-frame=true&no-bg=true&margin-w=8&row=1&title=Stars,Commits,Repositories,PullRequest,Issues,Reviews)](https://github.com/ryo-ma/github-profile-trophy)

</div>

---

<div align="center">

![footer](svgs/footer-panel.svg)

<br/>

![Visitor Count](https://komarev.com/ghpvc/?username=George-Mando&color=00ff9c&style=for-the-badge&label=UNITS+DETECTED)

</div>

---

<!--
═══════════════════════════════════════════════════════════
  SETUP — DELETE AFTER READING
═══════════════════════════════════════════════════════════

  1. Create repo named exactly: George-Mando (public)
  2. Place this README.md at the ROOT
  3. Place all files from svgs/ folder into a svgs/ folder
     in the same repo — they must be in the same repo as
     the README or the images won't load on GitHub.

  4. ACTIVATE SNAKE:
     → Actions → New workflow → paste below as snake.yml

name: Generate Snake
on:
  schedule: [{ cron: "0 */12 * * *" }]
  workflow_dispatch:
  push: { branches: ["main"] }
jobs:
  generate:
    permissions: { contents: write }
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
      - uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

     → Run it manually once from Actions tab.

  5. Everything else is automatic.
═══════════════════════════════════════════════════════════
-->
