# eat-me

오늘 점심 랜덤 뽑기 앱.

---

## 브라우저에서 바로 편집하기 (권장)

별도 도구 없이 앱 UI에서 직접 메뉴를 편집할 수 있습니다.

### 세트 전환

- 상단 **SET** 드롭다운으로 메뉴 세트를 전환합니다.
- URL: `?set=<key>` (예: `?set=jychang`)

### 새 세트 만들기

1. **SET** 드롭다운 하단 **+ 새 세트 추가** 클릭
2. set key(영문/숫자/._-)와 표시명 입력
3. 템플릿 선택: 빈 세트 또는 기존 세트 복사
4. **새 세트 만들고 편집 시작** 클릭

> 기본 세트(`menu.default.json`)는 읽기 전용입니다. 개인 세트를 만들어 사용하세요.

### 메뉴 편집

1. **SET** 드롭다운 → 해당 세트의 **수정** 버튼 클릭
2. **+ 메뉴 추가** 또는 각 항목의 **수정 / 삭제** 버튼으로 편집
3. 편집 완료 후 **필요 파일 원클릭 다운로드**
4. 다운로드한 파일을 GitHub `eat-me/` 폴더에 업로드(교체)하면 반영됩니다.

---

## 파일 형식

| 파일 | 역할 |
|---|---|
| `category.json` | 카테고리 정의 |
| `menu.default.json` | 기본 메뉴 (읽기 전용) |
| `menu.<set>.json` | 세트별 메뉴 (예: `menu.jychang.json`) |
| `sets.json` | SET 드롭다운 목록 |
| `ui-config.json` | 파티 모드 색상·이모지 |
| `release-notes.json` | 릴리즈 노트 |

### category.json 구조

```json
{
  "key": { "label": "표시명", "emoji": "🥢", "color": "#hex", "tab": true }
}
```

- `tab: true` — 카테고리 필터 탭에 표시
- `tab: false` — 태그 전용 (탭 미표시, 예: `nocoupon`)

### 카테고리 목록

| key | 이름 | 용도 |
|---|---|---|
| `korean` | 한식 | 한식 전반 |
| `chinese` | 중식 | 중식 전반 |
| `japanese` | 일식 | 라멘·돈까스·스시 등 |
| `western` | 양식 | 파스타·피자·스테이크·샌드위치 등 |
| `bunsik` | 분식 | 김밥·떡볶이·순대 등 분식점 |
| `light` | 라이트 | 샐러드·포케·저칼로리 |
| `soup` | 국물 | 탕·국·찌개 (국적 무관) |
| `noodle` | 면 | 국수·우동·파스타·라멘 (국적 무관) |
| `other` | 기타 | 편의점·기타 |
| `friday` | 금요일 전용 | 금요일 모드에서만 출현 |
| `nocoupon` | 식권대장 안됨 | 태그 전용 |

카테고리는 복수 선택 가능합니다 (예: `["korean", "soup"]`).

### menu.\*.json 구조

```json
[
  {
    "name": "식당",
    "count": 3,
    "category": ["korean", "soup", "noodle"],
    "fridayOnly": false
  }
]
```

- `count`: 뽑기 가중치 (클수록 자주 출현)
- `fridayOnly`: `true`면 금요일 모드에서만 출현

---

## GitHub 반영 방법

```bash
git checkout -b chore/update-menu
git add .
git commit -m "Update menu data"
git push -u origin chore/update-menu
gh pr create --fill
```

### PR 체크리스트

- `main`이 아닌 작업 브랜치에서 작업했는지 확인
- JSON 문법 오류 없는지 확인 (`category` 값이 `category.json`에 존재하는 key인지 포함)
