# 데이터 정제 검토 요약

`garbage_classification/` 데이터셋에서 발견한 중복·라벨 오류·비사진 이미지 정리.

## 1. 중복 이미지

### 1-1. 완전 동일 중복 - 같은 클래스 (16장, 삭제 대상)

- `clothes5234.jpg` — `clothes2051.jpg`와 완전 동일 파일, 삭제
- `green-glass530.jpg` — `green-glass231.jpg`와 완전 동일 파일, 삭제
- `green-glass555.jpg` — `green-glass285.jpg`와 완전 동일 파일, 삭제
- `green-glass443.jpg` — `green-glass292.jpg`와 완전 동일 파일, 삭제
- `green-glass554.jpg` — `green-glass336.jpg`와 완전 동일 파일, 삭제
- `green-glass461.jpg` — `green-glass349.jpg`와 완전 동일 파일, 삭제
- `green-glass459.jpg` — `green-glass388.jpg`와 완전 동일 파일, 삭제
- `green-glass564.jpg` — `green-glass403.jpg`와 완전 동일 파일, 삭제
- `green-glass517.jpg` — `green-glass413.jpg`와 완전 동일 파일, 삭제
- `green-glass563.jpg` — `green-glass413.jpg`와 완전 동일 파일, 삭제
- `green-glass482.jpg` — `green-glass422.jpg`와 완전 동일 파일, 삭제
- `green-glass561.jpg` — `green-glass424.jpg`와 완전 동일 파일, 삭제
- `green-glass565.jpg` — `green-glass449.jpg`와 완전 동일 파일, 삭제
- `green-glass544.jpg` — `green-glass471.jpg`와 완전 동일 파일, 삭제
- `green-glass492.jpg` — `green-glass476.jpg`와 완전 동일 파일, 삭제
- `green-glass592.jpg` — `green-glass583.jpg`와 완전 동일 파일, 삭제

### 1-2. 완전 동일 중복 - 클래스가 다름 (6장, 라벨 신뢰 불가로 둘 다 제외)

- `metal459.jpg` / `white-glass412.jpg` — 서로 완전 동일한데 라벨이 다름(metal vs white-glass), 둘 다 제외
- `plastic159.jpg` / `white-glass129.jpg` — 서로 완전 동일한데 라벨이 다름(plastic vs white-glass), 둘 다 제외
- `plastic556.jpg` / `white-glass761.jpg` — 서로 완전 동일한데 라벨이 다름(plastic vs white-glass), 둘 다 제외

### 1-3. 근접 중복 (42그룹, 파일 삭제 없이 같은 data split에만 배치)

- `battery268.jpg`, `battery343.jpg`
- `battery63.jpg`, `battery833.jpg`
- `battery759.jpg`, `battery945.jpg`
- `biological401.jpg`, `biological709.jpg`
- `biological402.jpg`, `biological781.jpg`
- `biological410.jpg`, `biological865.jpg`
- `brown-glass19.jpg`, `brown-glass439.jpg`
- `clothes2051.jpg`, `clothes5234.jpg`
- `clothes5095.jpg`, `clothes536.jpg`
- `green-glass190.jpg`, `green-glass46.jpg`
- `green-glass2.jpg`, `green-glass292.jpg`, `green-glass443.jpg`
- `green-glass228.jpg`, `green-glass433.jpg`
- `green-glass231.jpg`, `green-glass530.jpg`
- `green-glass285.jpg`, `green-glass555.jpg`
- `green-glass336.jpg`, `green-glass554.jpg`
- `green-glass349.jpg`, `green-glass461.jpg`
- `green-glass388.jpg`, `green-glass459.jpg`
- `green-glass403.jpg`, `green-glass564.jpg`
- `green-glass413.jpg`, `green-glass517.jpg`, `green-glass563.jpg`
- `green-glass422.jpg`, `green-glass482.jpg`
- `green-glass424.jpg`, `green-glass561.jpg`
- `green-glass449.jpg`, `green-glass565.jpg`
- `green-glass451.jpg`, `green-glass488.jpg`
- `green-glass471.jpg`, `green-glass544.jpg`
- `green-glass476.jpg`, `green-glass492.jpg`
- `green-glass583.jpg`, `green-glass592.jpg`
- `metal459.jpg`, `white-glass412.jpg`
- `metal590.jpg`, `metal745.jpg`
- `plastic159.jpg`, `white-glass129.jpg`
- `plastic467.jpg`, `plastic506.jpg`
- `plastic556.jpg`, `white-glass761.jpg`
- `shoes1049.jpg`, `shoes1390.jpg`
- `shoes1065.jpg`, `shoes1482.jpg`, `shoes651.jpg`
- `shoes1095.jpg`, `shoes777.jpg`
- `shoes1128.jpg`, `shoes615.jpg`
- `shoes1227.jpg`, `shoes1368.jpg`
- `shoes29.jpg`, `shoes621.jpg`
- `trash238.jpg`, `trash301.jpg`
- `trash254.jpg`, `trash559.jpg`
- `trash683.jpg`, `trash688.jpg`
- `white-glass300.jpg`, `white-glass472.jpg`
- `white-glass674.jpg`, `white-glass688.jpg`

---

## 2. 라벨 오류 (정정 대상)

### 2-1. `clothes` → `shoes` 이동 필요 (43장, 신발 사진이 clothes 폴더에 있음)

- `clothes3062.jpg`
- `clothes3330.jpg`
- `clothes5002.jpg`
- `clothes2197.jpg`
- `clothes4465.jpg`
- `clothes1229.jpg`
- `clothes2272.jpg`
- `clothes791.jpg`
- `clothes4836.jpg`
- `clothes5277.jpg`
- `clothes5181.jpg`
- `clothes3623.jpg`
- `clothes3807.jpg`
- `clothes451.jpg`
- `clothes2162.jpg`
- `clothes4329.jpg`
- `clothes255.jpg`
- `clothes559.jpg`
- `clothes2185.jpg`
- `clothes4319.jpg`
- `clothes4611.jpg`
- `clothes5201.jpg`
- `clothes2556.jpg`
- `clothes1015.jpg`
- `clothes82.jpg`
- `clothes3374.jpg`
- `clothes4466.jpg`
- `clothes4635.jpg`
- `clothes2334.jpg`
- `clothes2654.jpg`
- `clothes4150.jpg`
- `clothes1312.jpg`
- `clothes4293.jpg`
- `clothes2733.jpg`
- `clothes53.jpg`
- `clothes3206.jpg`
- `clothes5045.jpg`
- `clothes1444.jpg`
- `clothes4495.jpg`
- `clothes4469.jpg`
- `clothes3895.jpg`
- `clothes1582.jpg`
- `clothes3545.jpg`

### 2-2. `shoes` → `clothes` 이동 필요 (1장)

- `shoes1826.jpg` — 반바지 사진

### 2-3. 기타 정정 필요(2장)

- `white-glass704.jpg` → `green-glass`로 정정 (사진은 짙은 녹색)
- `paper9.jpg` → `plastic`으로 정정 (비닐봉투 사진)

---

## 3. 애매한 경계 (보류, 3장)

- `white-glass58.jpg` — 여러 병이 섞여있어 판단 애매
- `shoes379.jpg` — 하이힐 모양 유리 장식품, 재질 기준 애매
- `clothes526.jpg` — 사진 내용 식별 어려움

---

## 4. 비사진 파일 (처리 보류, 6장)

- `trash223.jpg` — 마스크 클립아트 일러스트
- `plastic605.jpg` — 플라스틱 병 연필 스케치
- `white-glass112.jpg` — 깨진 유리 클립아트
- `metal502.jpg` — 캔 목업 템플릿(워터마크 있음)
- `green-glass372.jpg` — 병 목업 템플릿(워터마크 있음)
- `shoes1878.jpg` — 스타일라이즈된 부츠 렌더링(라벨 자체는 맞음)
