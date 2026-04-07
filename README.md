# eat-me

## 데이터 수정 가이드

- 카테고리 수정: `category.json`
- 기본 메뉴 수정: `menu.default.json`
- 샘플 메뉴 수정: `menu.sample.json`

## 파일 형식

- `category.json`: key-객체 맵 (`label`, `emoji`, `color`, `tab`)
- `menu.*.json`: 배열 항목 (`name`, `count`, `category`, `fridayOnly`)

## 주의사항

- `menu.*.json`의 `category` 값은 반드시 `category.json`에 존재하는 key를 사용하세요.
- JSON 문법(콤마, 따옴표, 대괄호/중괄호)을 지켜야 화면 로드 에러가 나지 않습니다.

## 사람별 메뉴 적용 방법

- `?person={이름}` 이 있으면 `menu.{이름}.json`을 로드 시도합니다.
- 파일이 없거나 파라미터가 없으면 자동으로 `menu.default.json`을 사용합니다.
- 예시:
  - `https://<id>.github.io/eat-me/` -> `menu.default.json`
  - `https://<id>.github.io/eat-me/?person=sample` -> `menu.sample.json`
- 새 사람 메뉴를 추가하려면 `menu.alice.json` 같은 파일을 만들고 `?person=alice`로 접속하면 됩니다.

## 코드 추가 요청하는 방법

- 전제: `main`(또는 기본 브랜치)에 직접 커밋/푸시하지 않고, 항상 작업 브랜치에서 PR 생성
- 작업 브랜치 생성:
  - `git checkout -b chore/update-menu-profile`
- 변경 파일 확인:
  - `git status`
- 변경 내용 커밋:
  - `git add .`
  - `git commit -m "Update menu profile data and docs"`
- 원격에 브랜치 푸시:
  - `git push -u origin chore/update-menu-profile`
- Pull Request 생성:
  - GitHub 웹에서 Compare 화면으로 PR 생성, 또는
  - CLI 사용 시 `gh pr create --fill`

### PR 체크리스트

- `main`이 아닌 작업 브랜치에서 작업했는지 확인
- 데이터 파일(JSON) 문법 오류 없는지 확인
- README 변경 내용이 실제 동작과 일치하는지 확인
