# PPKTP 집속 렌즈 선택기

입사 가우시안 빔의 크기(1/e² 반경 또는 직경)와 파장, PPKTP 결정 길이를 넣으면 후보 렌즈마다 다음 값을 계산합니다.

- 집속 허리 반경 w_out (Self의 가우시안 빔 렌즈 공식, 얇은 렌즈)
- 레일리 길이 z_R (공기 중, 결정 안)
- 집속 파라미터 ξ = L/b
- 허리가 결정 중심에 오도록 하는 결정 앞면, 중심, 뒷면 위치
- 결정 면 빔 직경과 개구 투과율

목표 ξ에 가장 가까운 렌즈를 추천하고, 선택한 렌즈의 배치도와 결정 부근 빔 모양을 그려 줍니다.
별도 빌드나 서버 없이 `index.html` 하나로 동작합니다.

## A4 요약 인쇄

추천 배너의 **A4 요약 인쇄** 버튼을 누르면 현재 입력값에 대한 최적 렌즈, 결정 앞면·중심·뒷면 거리, 빔 파라미터, 배치도, 이웃 렌즈 비교표를 A4 한 장으로 정리해 인쇄 창을 엽니다. 인쇄 창에서 대상을 "PDF로 저장"으로 고르면 PDF 파일로도 남길 수 있습니다. 화면이 다크 모드여도 인쇄물은 흰 바탕으로 나옵니다. 브라우저 메뉴의 인쇄(Ctrl/Cmd + P)를 써도 같은 요약이 인쇄됩니다.

## GitHub Pages에 올리기

1. GitHub에서 새 저장소를 만듭니다 (예: `ppktp-lens-selector`). Public이어야 무료 계정에서 Pages를 쓸 수 있습니다.
2. 이 폴더의 파일(`index.html`, `.nojekyll`, `README.md`)을 저장소 최상위에 올립니다.
   - 웹에서: 저장소의 **Add file → Upload files**로 끌어다 놓고 Commit합니다.
     (`.nojekyll`처럼 점으로 시작하는 파일은 운영체제에서 숨김 파일이라 안 보일 수 있습니다. 없어도 동작하지만, 있으면 Jekyll 처리를 건너뛰어 배포가 빨라집니다.)
   - 명령줄에서:
     ```bash
     git init
     git add index.html .nojekyll README.md
     git commit -m "PPKTP 집속 렌즈 선택기"
     git branch -M main
     git remote add origin https://github.com/<사용자명>/ppktp-lens-selector.git
     git push -u origin main
     ```
3. 저장소의 **Settings → Pages**에서 **Source: Deploy from a branch**, **Branch: main / (root)** 를 고르고 Save합니다.
4. 1~2분 뒤 `https://<사용자명>.github.io/ppktp-lens-selector/` 에서 열립니다.

이미 있는 사이트(예: `<사용자명>.github.io` 저장소)에 넣으려면 `index.html`을 하위 폴더(예: `tools/ppktp/index.html`)에 두면 `https://<사용자명>.github.io/tools/ppktp/` 로 열립니다.

## 참고

- 글꼴은 Google Fonts(IBM Plex Sans KR, IBM Plex Mono)를 불러옵니다. 인터넷이 막힌 환경에서는 시스템 글꼴로 대신 표시되며 계산에는 영향이 없습니다.
- 입력값은 브라우저 localStorage에 저장되어 다음에 열 때 그대로 남습니다.
- 자동 굴절률은 KTP n_y Sellmeier 식(Kato & Takaoka, Appl. Opt. 41, 5040, 2002; 유효 범위 0.43–3.54 μm)입니다. 405 nm는 범위 밖 외삽이므로 결정 데이터시트 값이 있으면 직접 입력하세요.
- 거리는 얇은 렌즈의 주평면 기준이며, 결정 면 반사, 열 렌즈, 비대칭 빔은 고려하지 않았습니다.
