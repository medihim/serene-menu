# SERENE Treatment Funnel

세린의원 시술메뉴를 홈페이지 퍼널형 위젯으로 운영하기 위한 저장소입니다.

## 1. 목적

기존 시술 가격표를 단순 노출하지 않고 다음 흐름으로 전환합니다.

`고민 탐색 → 시술 메뉴 → 일반가/첫방문가 → 월간 EVENT → LINE 상담 → Bridge → CRM`

현재 버전은 **한글 내부 검수/운영용 브랜드 버전 v1.1**입니다.

## 2. 폴더 구조

```text
serene-treatment-funnel/
├─ README.md
├─ CHANGELOG.md
├─ .gitignore
├─ dist/
│  └─ serene_ko_treatment_funnel_widget_brand_v1.1.html
├─ data/
│  └─ serene_ko_treatment_funnel_data_v1.1.json
├─ docs/
│  ├─ IMWEB_DEPLOY.md
│  └─ RELEASE_CHECKLIST.md
└─ preview/
   └─ index.html
```

## 3. 주요 파일

### `dist/serene_ko_treatment_funnel_widget_brand_v1.1.html`
아임웹 **코드 위젯에 그대로 붙여넣는 단일 배포 파일**입니다.

별도로 `<html>`, `<head>`, `<body>`를 추가하지 않습니다.

### `preview/index.html`
브라우저에서 독립적으로 열어 디자인을 검수하는 파일입니다.

### `data/serene_ko_treatment_funnel_data_v1.1.json`
현재 시술/가격/월간 이벤트/Bridge 설정을 추적하기 위한 데이터 스냅샷입니다.

현재 `dist` 파일은 배포 편의를 위해 데이터를 내부에 포함한 단일 HTML입니다.
따라서 데이터 변경 후에는 `dist` 파일도 함께 갱신해야 합니다.

## 4. 세린 브랜드 기준

현재 반영된 핵심 컬러:

- Deep Green: `#446A5B`
- Serene Green: `#598865`
- Soft Green: `#8BA991`
- Mist Green: `#E5ECE4`
- Warm Beige: `#DACEB8`
- Ivory: `#E3DAC8`

톤앤매너:

- 가격보다 상담과 피부 고민을 먼저 제시
- 과도한 할인몰/커머스 UI 지양
- 넓은 여백과 얇은 라인 중심
- 의료적 신뢰감 + 차분한 프리미엄
- 강한 예약 압박보다 상담 중심 CTA

## 5. 로컬 미리보기

가장 간단한 방법:

```bash
cd preview
python -m http.server 8080
```

브라우저:

```text
http://localhost:8080
```

또는 `preview/index.html`을 직접 열어도 됩니다.

## 6. 아임웹 배포

상세 절차는 [`docs/IMWEB_DEPLOY.md`](docs/IMWEB_DEPLOY.md)를 참고합니다.

요약:

1. `/106` 테스트용 복제
2. 코드 위젯 12컬럼 삽입
3. `dist/*.html` 전체 복사
4. 코드 위젯에 붙여넣기
5. PC/Mobile Preview 검수
6. LINE Bridge 파라미터 검수
7. GTM 이벤트 검수
8. 가격/조건 승인
9. 원본 `/106` 반영
10. 게시

## 7. GTM 이벤트

현재 위젯에서 다음 이벤트를 `dataLayer`에 전송합니다.

- `menu_funnel_view`
- `menu_category_click`
- `menu_concern_click`
- `menu_expand`
- `menu_line_click`

## 8. LINE Bridge

기본 Bridge:

```text
https://medihim-bo.vercel.app/bridge
```

주요 전달값:

- `hospital=SERN`
- `oa=@serene.clinic`
- `menu_code`
- `event_code`
- `offer_type`
- `source_page=jp_treatment_funnel`
- UTM / fbclid / gclid / session 등

## 9. 운영 원칙

다음 조건이 확정되지 않은 가격은 할인율을 자동 계산하지 않습니다.

- 동일 제품
- 동일 규격/용량
- 동일 샷 수
- 동일 팁
- 동일 부위
- 동일 횟수
- 동일 부가관리

월간 EVENT는 일반/첫방문가와 별도 조건으로 관리합니다.

## 10. 버전

현재: `v1.1-brand-ko`

- 한글 내부 검수용
- 세린 룩앤필 반영
- 아임웹 코드 위젯 배포 가능
