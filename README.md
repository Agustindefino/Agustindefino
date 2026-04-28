# ¡Hola a todos! 👋

<p align="left">
  <img src="https://readme-typing-svg.herokuapp.com?font=VT323&size=24&pause=1000&color=61FF00&width=550&lines=Building+things+that+(sometimes)+work;Software+Systems+Student;Turning+logic+into+solutions;Always+learning+new+technologies" />
</p>

Por aqui jogando a criar coisas que (às vezes) funcionam.

Estudante de Desenvolvimento de Sistemas.
### Habilidades e Ferramentas

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)




[![Estatísticas do GitHub](https://github-readme-stats.vercel.app/api?username=Agustindefino&show_icons=true&theme=dark&hide_rank=true)](https://github.com/anuraghazra/github-readme-stats)

[![Linguagens Mais Usadas](https://github-readme-stats.vercel.app/api/top-langs/?username=Agustindefino&layout=compact&theme=dark)](https://github.com/anuraghazra/github-readme-stats)


name: generate animation

on:
  # rodar automaticamente a cada 24 horas
  schedule:
    - cron: "0 */24 * * *" 
  
  # permite rodar manualmente a qualquer momento
  workflow_dispatch:
  
  # roda a cada push na branch main/master
  push:
    branches:
    - master
    - main

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 5
    
    steps:
      # gera o jogo da cobrinha a partir do gráfico de contribuições
      - name: generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark
          
      # envia o conteúdo de dist para a branch output
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
