# 아임웹 배포 가이드

## 1. 배포 대상

- 사이트: 세린의원 홈페이지
- 대상 페이지: 일본 이벤트 `/106`
- 방식: 아임웹 코드 위젯
- 배포 파일: `dist/serene_ko_treatment_funnel_widget_brand_v1.1.html`

현재 한글 버전은 내부 검수용입니다.
실제 일본 페이지 공개 전에는 동일 디자인 시스템을 적용한 일본어 최종본으로 교체합니다.

## 2. 테스트 페이지 생성

원본 `/106`에 바로 반영하지 않습니다.

1. 아임웹 디자인 모드 진입
2. `/106` 복제
3. 테스트 URL 생성
4. 메뉴 숨김
5. 검색엔진 노출 차단

권장 테스트 URL:

```text
/treatment-menu-test
```

## 3. 코드 위젯 삽입

권장 위치:

```text
월간 EVENT 대표 배너
↓
신규 Treatment Menu Funnel
↓
기존 월간 EVENT 상세 콘텐츠
↓
안내사항
↓
Footer
```

아임웹:

```text
위젯 추가
→ 코드 위젯
→ 12컬럼 전체 폭
→ 코드 설정
→ dist HTML 전체 붙여넣기
```

## 4. Width

아임웹 바깥 위젯은 12컬럼 전체 폭으로 둡니다.

내부 HTML에서 이미 다음처럼 콘텐츠 폭을 제어합니다.

```css
.stf-wrap {
  max-width: 1160px;
  margin: 0 auto;
}
```

아임웹에서 별도로 8~10컬럼으로 줄이지 않습니다.

## 5. Preview 검수

디자인 모드보다 반드시 실제 미리보기에서 확인합니다.

PC:
- Hero 높이
- 좌우 정렬
- 2열 카드
- 이벤트 카드 균형

Mobile:
- 375px
- 390px
- 430px

검수:
- 가로 스크롤 없음
- 텍스트 잘림 없음
- 메뉴 카드 1열
- 카테고리 가로 스크롤
- LINE CTA 정상
- Sticky 영역과 GNB 충돌 없음

## 6. LINE Bridge 검수

개별 시술 클릭 시 URL에 다음 값이 있는지 확인합니다.

```text
hospital
oa
menu_code 또는 event_code
offer_type
source_page
```

광고 유입 시 아래 값도 유지되는지 확인합니다.

```text
utm_source
utm_medium
utm_campaign
utm_content
utm_term
fbclid
gclid
session
```

## 7. GTM 검수

GTM Preview에서 다음 이벤트를 확인합니다.

```text
menu_funnel_view
menu_category_click
menu_concern_click
menu_expand
menu_line_click
```

특히 LINE 클릭:

```text
event = menu_line_click
menu_code = ...
category = ...
```

## 8. 공개 전 승인

필수 확인:

- 일반가
- 첫방문가
- 월간 EVENT 가격
- 이벤트 적용 기간
- 중복 적용 여부
- 예약일/내원일 기준
- VAT
- 상담비
- 마취/팁/관리 추가비용
- 시술 규격
- 증례 외부사용 동의범위

## 9. 실배포

검수 완료 후:

1. 일본어 브랜드 버전으로 교체
2. 원본 `/106` 코드 위젯 반영
3. GTM Preview
4. Bridge E2E 테스트
5. 게시
6. 실모바일 재검수
