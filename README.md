# 🦁 내 책상 위의 사파리 동물원 (Safari Zoo MR)

스마트폰 카메라 화면에서 육지동물과 바다동물의 3D 모델을 체험하는 웹 콘텐츠입니다. **기본 버전은 카메라 합성형 3D 체험이며, 실제 바닥/책상 평면 인식이나 월드 앵커 기능은 제공하지 않습니다.**

## 저장소

- 저장소 이름: `safari-zoo-mr`
- GitHub Pages 주소: `https://imm-content.github.io/safari-zoo-mr/`
- 공개 저장소(Public)로 만들고 Settings → Pages → Deploy from a branch → `main` / `(root)` → Save

- GitHub 저장소: https://github.com/imm-content/safari-zoo-mr

## 파일 구조

```text
safari-zoo-mr/
├── index.html
├── README.md
├── models/
│   ├── bear.glb
│   ├── rhino.glb
│   ├── sparrow.glb
│   ├── sperm-whale.glb
│   ├── turtle.glb
│   ├── rabbit.glb
│   └── white-rhino.glb
├── images/
│   ├── safari-background.png
│   ├── forest-background.png
│   └── ocean-background.png
└── sounds/
    ├── forest.mp3
    └── ocean.mp3
```

**중요:** 첨부된 `forest(1).mp3` 및 `ocean(1).mp3` 파일은 GitHub에 업로드하기 전에 각각 `forest.mp3`, `ocean.mp3`로 이름을 바꿔 주세요.

## 사용 방법

1. 페이지를 열면 사파리 배경과 7종의 3D 동물이 표시됩니다.
2. **카메라 켜기**를 누르고 카메라 접근 권한을 허용합니다.
3. **육지관**을 선택한 뒤 곰, 새, 코뿔소, 모두 중 하나를 누릅니다.
4. **바다관**을 선택한 뒤 고래, 거북이, 모두 중 하나를 누릅니다.
5. 체험관을 전환하면 배경 이미지와 반복 환경음도 전환됩니다.
6. **처음으로** 버튼을 누르면 카메라를 종료하고 시작 화면으로 돌아갑니다.

## 사용한 애니메이션

실제 업로드된 GLB를 확인했습니다.

| 모델 | 애니메이션 |
|---|---|
| bear.glb | `Armature|run` 포함, 여러 달리기/걷기 동작 |
| rhino.glb | `Animation` |
| sparrow.glb | `AA_Sparrow_Fly` 포함 |
| sperm-whale.glb | `ArmatureAction` 2개 |
| turtle.glb | `Swim Cycle` |
| rabbit.glb | 없음 (정지 모델) |
| white-rhino.glb | `Action` |

> 실제 애니메이션의 방향, 모델별 회전 및 크기는 스마트폰 실행 후 보정이 필요할 수 있습니다.

## 기술 구성

- Three.js 0.160.1 (CDN, 네트워크 필요)
- GLTFLoader / SkeletonUtils / AnimationMixer
- MediaDevices `getUserMedia` 후면 카메라
- HTML5 Audio, CSS 배경 합성
- GitHub Pages 정적 호스팅

## 유의사항

- 카메라 접근은 HTTPS 환경과 사용자의 권한 허용이 필요합니다.
- 일부 모바일 브라우저는 성능이나 권한 제한으로 정상 작동하지 않을 수 있습니다.
- 이미지 배경은 카메라 화면 위에 반투명하게 합성됩니다. **실제 책상에 숲/해저가 기하학적으로 투영되거나 물체 뒤에 가려지는 AR은 아닙니다.**
- GLB 총용량이 크므로 첫 로딩에는 시간이 걸릴 수 있습니다.
- Sketchfab에서 내려받은 모델은 **각 모델의 원본 라이선스 및 저작자 표시 조건을 확인**하여 이 문서에 출처를 추가해 주세요.

## 제작 목적

스마트폰과 3D 동물 모델을 활용하여 자연·생태 교육에 적용 가능한 실감형 콘텐츠를 실습합니다.

## 2026.11.26 카메라 호환성 개선

- 기존 후면 카메라 호출을 우선 시도합니다. 실패하면 다른 후면카메라를 찾고 있다는 안내를 표시하고 개별 카메라를 자동 탐색합니다.
- 개별 후보는 기본 조건과 저해상도 조건으로 시도하며, 특정 기종이나 카메라 번호를 고정하지 않습니다. 실제 후면 방향이 확인된 영상만 사용합니다.
- 전체 카메라 초기화 대기시간은 60초로 제한합니다. 늦게 반환된 영상 스트림도 해제합니다. 운영체제의 카메라 요청 자체를 즉시 취소할 수는 없습니다.
- 권한 거부와 실행 실패를 구분하여 안내하며, 실패 시 카메라 켜기 버튼으로 다시 시도할 수 있습니다. 필요하면 브라우저 재접속 및 스마트폰 재부팅을 안내합니다.
- 처음으로 및 페이지 이탈 시 카메라 자원을 해제합니다.
- 기존 동물 모델, 배치, 애니메이션, 환경음 및 터치 조작은 유지합니다.

### 검증 방법

Galaxy A36 5G, Wide5, Z Flip5에서 기존 QR 또는 배포 주소로 접속하여 카메라 켜기 → 육지관/바다관 → 처음으로를 3회 반복합니다. 동물 표시, 회전·확대 및 환경음도 확인합니다. 실제 기기 검증은 배포 후 수행해야 합니다.
