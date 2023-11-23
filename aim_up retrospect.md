package manager : npm

- index.js : `<App>`컴포넌트를 render
- App.js : Start 전인지 후인지 감시 (`onStartButtonClicked`를 넘김) 하고, 상태에 맞는 컴포넌트 리턴
	- 근데 왜 `setIsStarted`자체를 넘기지 않았지??
	- 또는 그냥 람다식으로 넘겨도 됐을 듯
- BeforeGameStart.js : 그냥 시작화면. 버튼 누르면 state변경
	- 여기다 추가할만한거 : ?
		- 몇 초 플레이할건지?
		- 난이도??
- AfterGameStart.js : 시간을 잰다, Game컴포넌트 호출 
	- (`setTimeout` : 이거 머라더라?비동기 어쩌구..라서 좀 손봐야하나 싶기도 하고)
- Game.js
	- `getRandom` : 랜덤으로 난수 생성, 리턴
	- `newPosition` : `getRandom` 두 개 불러서 랜덤한 위치좌표 생성
	- `isInTarget` : 타겟을 클릭했는지 확인 : 
		- 먼저 헤드(동그라미)로의 거리를 재고, 좌표가 내부인지 확인
		- 헤드 아니면 몸통 히트인지 확인 (몸통은 직사각형으로 간주)
	- `drawBody` : 어깨부분 둥글게 그린다
	- `drawEyes` : 눈 그려줌ㅋㅋ
	- `drawCross` : 현재 마우스 위치에 크로스헤어 추가
	- `Game` : 
		- `useEffect`로 `setInterval`감싸서 시간 재는데 잘 안나옴


***package.json에서 `"hompage":"./"` 추가해서 상대경로 추가함***
```yaml
# Simple workflow for deploying static content to GitHub Pages
name: Deploy aim.io

on:
  # Runs on pushes targeting the default branch
  push:
    branches: ["master"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Single deploy job since we're just deploying
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Install Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - name: Install dependencies and build
        run: |
          npm install
          npm run build
      - name: Setup Pages
        uses: actions/configure-pages@v3
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          # only build folder
          path: './build'
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2

```
env.CI 해결 https://velog.io/@zemma0618/GitHub-Actions-Treating-warnings-as-errors-because-process.env.CI-true-%EC%97%90%EB%9F%AC


![](https://i.imgur.com/xK4OMVY.png)
