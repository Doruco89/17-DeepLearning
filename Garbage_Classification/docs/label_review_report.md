# 라벨 오류 검토 보고서

`garbage_classification/` 데이터셋에서 모델(EfficientNetV2-S unfreeze) 기반 진단으로 찾고, **사람이 직접 육안으로 전수 확인한** 라벨 오류 의심 사례 정리. 공유·논의용 문서.

이 문서는 실제 이미지 파일을 옮기지 않는다 — 어떤 파일을 정정 대상으로 볼지, 어떤 건 애매한지를 정리한 검토 기록이다.

## 방법

1. **held-out 검사**: val+test(학습에 안 쓰인 4,655장) 전체에서, 최종 모델이 확신도(softmax 확률) 0.9 이상으로 **틀리게** 예측한 사례를 전수 확인 (59건).
2. **train 검사(2-fold out-of-fold)**: train(10,838장)은 모델이 암기했을 수 있어, train을 절반씩 나눠 서로 반대쪽 fold로 학습한 두 모델로 교차 평가해 "안 본 상태"의 정직한 예측을 얻은 뒤 확신도 0.9 이상 오분류를 전수 확인 (145건).
3. 1차로 모델 예측과 이미지를 대조해 자동 분류(A/B/C/D) → **2차로 사람이 이미지 204건을 전부 육안 재검토**해 최종 확정(아래 내용에 반영됨).

---

## A. 확실한 라벨 오류 — `clothes ↔ shoes` (총 44건, `shoes` 폴더로 이동 권장)

사진 내용이 명백히 신발(운동화/샌들/부츠/로퍼/구두/슬리퍼)인데 `clothes` 폴더에 들어있던 파일들.

### A-1. held-out 검사에서 발견 — 19건

**`clothes/` → `shoes/`로 이동 (18건)**

```
clothes3062.jpg
clothes3330.jpg
clothes5002.jpg
clothes2197.jpg
clothes4465.jpg
clothes1229.jpg
clothes2272.jpg
clothes791.jpg
clothes4836.jpg
clothes5277.jpg
clothes5181.jpg
clothes3623.jpg
clothes3807.jpg
clothes451.jpg
clothes2162.jpg
clothes4329.jpg
clothes255.jpg
clothes559.jpg
```

**`shoes/` → `clothes/`로 이동 (1건, 반바지 사진)**

```
shoes1826.jpg
```

> `clothes2073.jpg`는 육안 재검토 결과 **모자 사진, `clothes` 라벨이 맞음** — 오류 아님, 목록에서 제외.

### A-2. train(OOF) 검사에서 발견 — 25건

**`clothes/` → `shoes/`로 이동 (25건)**

```
clothes2185.jpg
clothes4319.jpg
clothes4611.jpg
clothes5201.jpg
clothes2556.jpg
clothes1015.jpg
clothes82.jpg
clothes3374.jpg
clothes4466.jpg
clothes4635.jpg
clothes2334.jpg
clothes2654.jpg
clothes4150.jpg
clothes1312.jpg
clothes4293.jpg
clothes2733.jpg
clothes53.jpg
clothes3206.jpg
clothes5045.jpg
clothes1444.jpg
clothes4495.jpg
clothes4469.jpg
clothes3895.jpg
clothes1582.jpg
clothes3545.jpg
```

(`clothes3545.jpg`는 모델이 "metal"로 예측했지만 육안으로 명백한 고무장화 사진이라 포함함)

> `clothes526.jpg`는 육안 재검토 결과 **뭔지 알아보기 어려움** — C(애매한 경계)로 이동.
> `clothes1150.jpg`는 육안 재검토 결과 **상의(옷) 사진, `clothes` 라벨이 맞음** — 오류 아님, 목록에서 제외.

---

## B. 추가 확인된 라벨 오류 (사람이 확정, 2건)

육안 재검토로 **오류가 맞다고 확정된** 재질/색상 클래스 사례. (`plastic351.jpg`는 재검토 결과 라벨이 맞아 목록에서 제외)

```
white-glass704.jpg   (라벨:white-glass → green-glass가 맞음, green-glass로 정정 필요)
paper9.jpg           (라벨:paper → 비닐봉투(plastic)가 맞음, plastic으로 정정 필요)
```

---

## C. 애매해서 보류 — 팀 논의 필요 (자동 정정 안 함, 3건)

사람이 봐도 판단이 갈리는 경계 사례.

```
white-glass58.jpg   (여러 병이 섞여있어 판단 애매)
shoes379.jpg        (하이힐 모양 유리 장식품 — 진짜 애매함)
clothes526.jpg      (사진 내용을 알아보기 어려움 — 애매)
```

---

## D. 사진이 아닌 이미지 (라벨 문제가 아니라 데이터 품질 문제) — 6건, 보류

실제 촬영 사진이 아니라 일러스트/스케치/목업 템플릿이 섞여 있음. 어떻게 처리할지 아직 결정 못 함 — 일단 그대로 둠.

```
trash223.jpg       (마스크 클립아트 일러스트, 라벨:trash)
plastic605.jpg     (플라스틱 병 연필 스케치, 라벨:plastic)
white-glass112.jpg (깨진 유리 클립아트, 라벨:white-glass)
metal502.jpg       ("Circular Canned Food Packaging Mockup Template" 워터마크가 찍힌 디자인 목업, 라벨:metal)
green-glass372.jpg (병 목업 템플릿 이미지, 라벨:green-glass)
shoes1878.jpg      (부츠를 스타일라이즈(렌더링)한 이미지 — 라벨 자체는 맞지만 실제 사진은 아님)
```

---

## 요약

| 구분                          | 건수 | 처리 방향                         |
| ----------------------------- | ---- | --------------------------------- |
| A. clothes↔shoes 명백한 오류 | 44   | `shoes`로 이동 (18+1+25)        |
| B. 추가 확인된 오류           | 2    | 각각 green-glass/plastic으로 정정 |
| C. 애매한 경계 사례           | 3    | 보류, 팀 논의 후 결정             |
| D. 비사진 이미지              | 6    | 보류, 처리 방법 미정              |

(오탐으로 확인된 사례는 조치가 필요 없어 이 문서에서 제외함)

**검사 범위**: held-out(val+test) 확신도 0.9 이상 59건 + train(OOF) 확신도 0.9 이상 145건 = 총 204건 자동 후보 추출 → 사람이 전수 육안 재검토로 최종 확정.

> **검토 건수 정정 (2026-09-07)**
> 초기 작성본에는 "held-out 87건(확신도 0.7까지 확장) + 145건 = 232건"으로 적혀 있었으나,
> `appendix/A2_label_error_detection.ipynb`의 `CONF_THRESHOLD`가 5-1과 5-2 모두 **0.9 고정**이고
> 저장된 실행 출력도 held-out 59건으로 찍혀 있어 재현 근거가 없었다.
> 임계값을 0.7까지 낮춘 코드나 실행 기록은 노트북 어디에도 존재하지 않으므로 **59건 / 204건으로 정정**한다.
> 정정 근거는 `label_error_detection_method.md`의 "검토 건수 (정정 기록)" 절 참고.

**검사 방법 상세**: `appendix/A2_label_error_detection.ipynb` 5-1(held-out), 5-2(train OOF) 섹션 /
`appendix/A1_duplicate_detection.ipynb` 4장(육안 재확인) 참고.
**작성일**: 2026-09-05 (사람 육안 재검토 반영) / 2026-09-07 (검토 건수 정정)
