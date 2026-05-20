# 🎯 유튜브 콘텐츠 풀 오토메이션 마스터 워크플로우 V3.5
## 시간의발굴자 v3.2 흡수 — 패널수 가변 + 행동 구체화 + 볼륨 강제 + Voice Performance

**버전:** V3.5
**업데이트:** 2026.05.18
**적용 범위:** 모든 유튜브 채널 카테고리 (롱폼 + 쇼츠)
**기준:** V3.0 + 시간의발굴자 v3.2 (hamong-tv-v2.8) 통합
**핵심 변경:** I2V 룰 12개 정밀화 + 씬 패키지 출력 포맷 완전 표준 + 실패 패턴 6가지 자동 차단

---

## 📋 V3.0 → V3.5 핵심 변경 사항

| 영역 | V3.0 (이전) | V3.5 (보완) |
|---|---|---|
| 패널 수 | 무조건 3패널 (씬당 2~3패널 표준) | **나레이션 글자수 기준 동적 결정**: 60자+ = 2패널, 50~59자 = 3패널 |
| 행동 지시 | 추상적 ("hand stops mid-air") | **구체적**: 어느 손/발 / 방향 / 속도 / 얼굴 세부 (눈썹/입술/턱/시선) |
| 볼륨 명시 | 누락 | **"speak loudly and clearly" 필수 문구** |
| Voice Performance | 톤 1줄만 ("brisk pace") | **문장별 4요소**: Tempo / Tone / Emphasis / End direction |
| SPATIAL DESIGN | 텍스트 블록만 | **시각 평면도 인셋** + 📷 카메라 위치 마커 + 패널별 BG 매핑 |
| 연속성 명시 | 누락 | **4항목 강제**: SPACE / CHARACTER / PROP / TIME CONTINUITY |
| 실패 패턴 차단 | 없음 | **PART 36 6가지 패턴 자동 검수** |
| 자동 검수 | 22항목 | **30항목** (V3.5 신규 8항목 추가) |

---

# 🚦 PHASE 0 — 프로젝트 컨텍스트 자동 파악 (V3.5 보강)

```
1. 메모리 확인 (V3.5 신규 메모리 7개 추가)
   tool: memory_user_edits view
   V3.5 신규 메모리:
   - 패널 수 결정 룰 (60자/50자 기준)        ← v3.2
   - 행동 지시 구체화 룰                       ← v3.2
   - 볼륨 강제 룰 (speak loudly clearly)       ← v3.2
   - Voice Performance 문장별 룰              ← v3.2
   - SPATIAL DESIGN 평면도 시각 인셋 룰         ← v3.2
   - 연속성 4항목 명시 룰                      ← v3.2
   - I2V 실패 패턴 6가지 (자동 차단)            ← v3.2

2. 지식파일 검색 (V3.5 추가 검색어)
   - "패널 수 결정"                            ← V3.5
   - "행동 지시 구체화"                        ← V3.5
   - "Voice Performance 문장별"                ← V3.5
   - "연속성 4항목"                            ← V3.5
   - "I2V 실패 패턴"                           ← V3.5
   - (기존 V3.0 검색어 모두 유지)

3. 채널 정체성 + V3.5 신규 자동 인식
   - 채널/카테고리/타겟
   - 포맷 (롱폼/쇼츠)
   - 글자수별 패널 수 자동 매핑 (NEW V3.5)
   - TTS 4요소 + Voice Performance 문장별 디폴트 (NEW V3.5)
   - I2V 엔진 + 실패 패턴 차단 룰 (NEW V3.5)
```

---

# 🧭 PHASE 1~3 — 트렌드 + 후보 + 사료 (V3.0 유지)

V3.0 PHASE 1~3 그대로 유지. 변경 없음.
- PHASE 1: 트렌드 5개 키워드
- PHASE 2: 후보 12개 → 95점 이상 1개 선정
- PHASE 3: 사료 5~6개 교차 + 충격 디테일 5개+

---

# ✍️ PHASE 4 — 대본 작성 (V3.0 유지 + 글자수 룰 명시)

V3.0 PHASE 4 그대로 유지. 변경 없음.
- 30초 폭발 + 반전 2개
- 글자수 60~80자 강제 (Python len() 검증)
- AI Slop 5단 차단 (빙산/비선형/자기의심/1인칭/킬러라인)

**V3.5 추가 인식:**
- 대본 작성 시 각 씬 글자수가 패널 수 결정의 기준이 됨
- 60자 이상 씬은 자동으로 2패널 할당 예정
- 50~59자 씬은 3패널 할당 예정 (감정 전환 필요시)
- 49자 이하는 침묵/CUT 씬 후보

---

# 🎨 PHASE 5 — 비주얼 프롬프트 생성 (V3.5 완전 재정립)

## 5-A. 패널 수 결정 룰 (NEW V3.5) ⭐

```
[V3.5 절대 룰 — v3.2 룰 12 흡수]

나레이션 글자수에 따라 패널 수 자동 결정:

┌──────────────────┬─────────┬──────────────┐
│ 나레이션 글자수    │ 패널 수  │ Shot당 시간   │
├──────────────────┼─────────┼──────────────┤
│ 60자 이상         │ 2패널    │ 5.0초         │
│ 50~59자 + 감정전환 │ 3패널    │ 3.3초         │
│ 49자 이하          │ 침묵/CUT │ 10초 단일     │
└──────────────────┴─────────┴──────────────┘

⛔ 무조건 3패널 = 위반
⛔ SPLIT 화면 구성 = 금지 (Grok 구현 불가)
   불가피 시 씬 분리 (씬 N-A / 씬 N-B)
```

## 5-B. 입체 공간 설계도 + 시각 평면도 인셋 (NEW V3.5) ⭐

V3.0의 텍스트 블록을 **시각 평면도 인셋**으로 강화.

### Step 1: 공간 평면도 정의

```
씬 그룹별 평면도 (위에서 본 TOP-DOWN 뷰):

  ┌─────────────────────┐
  │  N: 북쪽 벽 (구조물)  │
  │                       │
  │ W:        E:          │
  │ 서쪽       동쪽         │
  │ 벽         벽           │
  │      [캐릭터]            │
  │      ↓향한 방향          │
  │                       │
  │  S: 남쪽 벽            │
  └─────────────────────┘
```

### Step 2: 카메라별 배경 매핑 (180도 룰)

```
같은 공간 = 같은 인테리어 = 다른 카메라 각도 = 다른 배경

C1 정면샷 (남쪽 향함) → BG: 북쪽 벽
C1 측면샷 (동쪽 향함) → BG: 동쪽 벽
와이드샷 (서쪽 → 동쪽) → BG: 서쪽+동쪽 일부

⛔ 마주보는 두 캐릭터 + 두 정면샷 모두 같은 배경 = 비상식 = 즉시 탈락
```

### Step 3: 인테리어 / 소품 픽스 (씬 내내 고정)

```
- 책상 위 커피잔 위치 (왼쪽 끝)
- 의자 색상 (검정 가죽)
- 모니터 화면 내용
- 시계 시간
→ 모든 패널에서 동일하게 유지
```

### Step 4: 스케치보드 시트에 **시각 평면도 인셋** 내장 ⭐ NEW V3.5

V3.0과의 차이점: 단순 텍스트 블록이 아니라 **하단 우측에 시각적 평면도 그림**으로 내장.

```
스케치보드 시트 레이아웃:

┌──────────────────────────────────────────┐
│ [상단] 시트 제목 + 부제                    │
├──────────────────────────────────────────┤
│                                          │
│       [메인 패널 영역 — 2 or 3패널]         │
│                                          │
├──────────────────────────────┬───────────┤
│                              │           │
│ [하단 좌측] Notes / Camera    │ [하단 우측]│
│ Story / Color Palette        │ SPATIAL  │
│                              │ DESIGN   │
│                              │ 시각      │
│                              │ 평면도    │
│                              │ ⭐ 인셋    │
│                              │           │
└──────────────────────────────┴───────────┘

평면도 인셋 내용:
- Location 표기 (구체적 장소명)
- N/S/E/W 4방위 벽 정의
- 캐릭터 위치 + 향한 방향 (화살표)
- 📷 카메라 위치 (패널별 마커)
- Props (locked) — 소품 고정 위치
- Panel별 BG 매핑 텍스트
```

### SPATIAL DESIGN 프롬프트 표준 (V3.5)

```
[SPATIAL DESIGN — GROUP X: 장소명]
Location: [구체적 장소 + 시대]
North wall: [북쪽 벽 구조물]
South wall: [남쪽 벽 구조물]
East wall: [동쪽 벽]
West wall: [서쪽 벽]
Character [이름] position: facing [방향]
Character [이름] sits/stands at: [위치]

Props (locked across all panels):
- [소품 1 + 위치]
- [소품 2 + 위치]

Panel별 배경:
Panel 01 [샷 종류 + 방향] BG: [카메라 각도에서 보이는 배경]
Panel 02 [샷 종류 + 방향] BG: [다른 카메라 각도의 배경]
Panel 03 [샷 종류 + 방향] BG: [측면 또는 와이드 배경]

⭐ V3.5: 스케치보드 시트 하단 우측 인셋에 위 평면도 시각화 강제
   (텍스트 블록만으로는 불충분 — Grok이 평면 구조 인식 X)
```

## 5-C. 픽사식 스케치보드 시트 표준 (V3.0 유지 + V3.5 보강)

```
스케치보드 시트 = 영화 콘티 = I2V 작업지시서

✅ 러프 연필 스케치 (= I2V가 패널 흐름 읽음)
❌ 완성된 일러스트 (= I2V가 독립 장면으로 오해)

V3.5 보강 — 시트 필수 5요소 (FB-015 위반 시 탈락):
1. 빨간 박스 = 카메라 프레임 (Camera/Framing)
2. 파란 화살표 = 움직임/에너지 방향
3. 손글씨 영문 주석 (English annotations)
4. 우측 캐스팅 칼럼 (시대별/씬별 등장 캐릭터만)
5. 하단 우측 SPATIAL DESIGN 평면도 인셋 ⭐ NEW V3.5
```

### V3.5 스케치보드 프롬프트 표준

```
[이미지 레퍼런스]
@Image2: character_sheet_ALL.jpg

STYLE: Hand-drawn pencil and ink storyboard sheet,
loose gestural pencil sketches with rough graphite lines,
NO color rendering inside panels (black and white pencil only,
except small color palette swatches at bottom),
NO finished illustration quality,
NO digital art polish,
authentic film production storyboard aesthetic
(Pixar / DreamWorks animation pre-production style reference),
white paper background with slight texture,
each panel framed with thin red rectangle (camera frame indicator),
blue arrows showing movement/breath/energy direction,
handwritten English annotations beside each panel,
character casting reference column on RIGHT side,
bottom section with Notes / Camera Story / Color Palette in handwritten style.

[Layout for Storyboard Sheet]
Title at top (handwritten): "[씬 제목] — [채널명]"
Subtitle (handwritten): "Scene [N]/[Total] — [블록명]"
Legend: "□=Camera/Framing  →=Movement/Energy  ⬤=Character"

Main panel grid (centered, 70% width):
- 16:9 롱폼: [N] panels in horizontal row (OR 2-column grid for 4+ panels)
- 9:16 숏폼: [N] panels stacked vertically, each panel 16:9 within

[SPATIAL DESIGN 평면도 — 반드시 내장 ⭐ V3.5 핵심]
[위에서 본 TOP-DOWN 배치도 — 하단 우측 인셋에 시각적으로 그림]
Location: [장소]
[방위별 벽/구조물 텍스트]
CHARACTER positions: [캐릭터별 위치 + 향한 방향]
Camera positions: [패널별 📷 마커]
Props (locked): [소품 고정 위치]
Panel별 BG 매핑 (Panel 1: ___ / Panel 2: ___ / Panel 3: ___)

Panel 01 [샷 종류 + 시간 마커]:
- Number circle top-left: "(01)" handwritten
- Shot label top: "[샷 종류] — [나레이션 핵심 키워드]"
- Inside panel (ROUGH PENCIL SKETCH):
  [나레이션이 말하는 장면을 정확히 시각화]
  [구체적 묘사: 배경 / 캐릭터 위치 / 핵심 동작]
- Red rectangle = camera frame
- Blue arrow: [움직임 방향]
- Right annotation (handwritten 2-3줄):
  "• [나레이션 매칭 노트]
   • BG: [패널별 배경]
   • [카메라 노트]"

Panel 02 [샷 종류 + 시간 마커]:
(동일 구조)

(Panel 03 필요 시 동일 구조 — 50~59자 + 감정 전환에만)

RIGHT COLUMN (Character Design + Casting):
Title: "CHARACTER DESIGN + CASTING"
[해당 씬 등장 캐릭터만 — 시대별/씬별 분리]
"CHAR N — [역할], [성격 키워드]" [portrait sketch]
"Match @Image2 for ALL appearances"

BOTTOM LEFT BOX — "NOTES / FLOW INTENTIONS":
• "[나레이션 핵심 내용 요약]"
• "[블록 분위기]"
• "Draw EXACTLY what narration says"

BOTTOM CENTER BOX — "CAMERA / STORY NOTES":
• "Panel→Panel: HARD CUT each"
• "Each panel = [초]s (V3.5 패널수 기준)"
• "0s already in motion — NO build-up"

BOTTOM RIGHT BOX — "COLOR PALETTE (mood reference)":
• [색상 HEX] "[감정 키워드]" (4-5개)

[네거티브]
NO color rendering inside panels (pencil only — except small palette swatches),
NO finished illustration quality,
NO digital painting,
NO clean vector lines,
NO 3D rendering,
NO photorealistic backgrounds inside panels,
NO scene number watermark inside panels,
NO English meta-tags floating outside annotations,
characters must match @Image2 reference style ([스타일]),
loose rough sketch aesthetic only.

[비율]
16:9 horizontal 1920x1080 (롱폼)
OR 9:16 vertical 1080x1920 (숏폼)
```

## 5-D. 캐릭터시트 ALL (V3.0 유지 + V3.5 보강)

```
모든 등장 캐릭터를 1장 시트로 통합:
- 파일명: character_sheet_ALL.jpg 또는 character_sheet_EP##.jpg
- 포함: 캐릭터별 turnaround + 6 표정 + 포즈 표 + 캐스팅 정보
- @Image2로 모든 씬 스케치보드 + I2V 생성 시 레퍼런스

V3.5 보강:
- 시대별/씬별 분리 원칙 (NEW)
- "Match @Image2 for ALL appearances" 강제 문구
- 캐스팅 정보에 역할 + 성격 키워드 명시
```

## 5-E. 그록 Aurora I2V Panel as Shot 표준 (V3.5 완전 개정)

### 핵심 원리 (FB-020 학습)

```
[FB-020]
문제: 스케치보드 시트를 @Image1으로 업로드해도
      Grok Aurora가 이미지 시트를 그대로 애니메이션화함.
      패널 3개 → Shot 3개로 자동 분할 X.

원인:
1. "@Image1 Panel N as Shot N" 형식 없이 추상적 액션만 기술
2. 구체적 신체 동작 지시 없음 → AI가 첫 프레임 고정
3. 볼륨 지시 없음 → 조용한 립 무빙만 생성
4. "Render in final style" 누락 → 연필 스케치 그대로 나옴

해결: V3.5 룰 12개 완전 적용
```

### V3.5 I2V 프롬프트 완전 표준

```
[이미지 업로드]
@Image1: scene[N]_board.jpg (스토리보드 시트)
@Image2: character_sheet_EP##.jpg (캐릭터 시트)

IMPORTANT: @Image1 is a HAND-DRAWN STORYBOARD SHEET.
Each numbered panel inside @Image1 is a SHOT to render.
Render each panel as a finished [EP STYLE] animated scene
(NOT as pencil sketch — translate the rough sketch into final illustrated style).

[N] shots, 10 seconds total, [9:16 OR 16:9]

@Image1 Panel 01 as Shot 1:
[배경 먼저 — 장소·조명·분위기 1줄]
Camera: [무브 1개 — Shot당 1개만]
[캐릭터 구체적 신체 동작 — 룰10 준수]
  어느 쪽 손/발 / 방향 / 속도 / 표정 세부 (눈썹/입술/턱/시선) 명시
he/she says [감정 태그], "[한국어 발음 변환 나레이션]"

@Image1 Panel 02 as Shot 2:
[배경 먼저]
Camera: [무브 1개]
[캐릭터 구체적 신체 동작]
Narration continues: "[나레이션 계속]"

(Panel 03 필요 시 동일 — 50~59자 씬만)

speak loudly and clearly, strong vocal projection, no whispering,
confident and audible tone throughout.

[전체 분위기 1줄]

SFX: [구체적 환경음 + 효과음]
BGM: no music

[Voice Performance]
TTS 톤: [성별] [연령], [음역], [감정 톤]
Type: Korean [성별] documentary narrator, [연령대]
Overall emotion: [전체 감정]
Sentence 1: '[나레이션 첫 문장]'
  → Tempo: [속도] | Tone: [톤] | Emphasis: [강조 단어] | End: [종결 방향]
Sentence 2: '[나레이션 둘째 문장]'
  → Tempo: [속도] | Tone: [톤] | Emphasis: [강조 단어] | End: [종결 방향]
Overall texture: [전체 음색]

Korean dialogue lip-sync, accurate mouth movement matching Korean phonemes.
Visible mouth opening and closing synced to Korean syllable rhythm.
Lip movement must follow Korean phonetic patterns (not English timing).
Mouth area must be visible and unobstructed during dialogue.

Render in [EP 비주얼 스타일]
(NOT pencil sketch — convert rough storyboard to final [스타일명] art).
Frame composition matches @Image1 panels exactly.

Maintain exact character appearance from @Image2 throughout.
No deformation or drift. Face identity locked. Clothing unchanged.
Preserve exact composition and colors from @Image1.
Follow composition guidance from @Image1 storyboard panels.

SPACE CONTINUITY: All elements consistent with scene location.
CHARACTER CONTINUITY: [시대/씬] characters only.
PROP CONTINUITY: Props consistent unless explicitly changed.
TIME CONTINUITY: Same time of day lighting throughout.

10 seconds. [16:9 OR 9:16].
```

### V3.5 I2V 절대 룰 12개

```
룰 1: 외관 묘사 금지 (이미지 의존)
  ⛔ "Korean man in his 30s, weathered face..." (외관 텍스트 묘사)
  ✅ "Maintain exact character appearance from @Image2"

룰 2: 배경 → 전경 순서 (v2.8 흡수)
  Shot 기술 순서: 배경 먼저 → 전경/캐릭터 → 동작
  ✅ "Dim interior, amber light. Camera push-in. C1's hand stops mid-air."
  ❌ "C1 stops his hand in the room." (배경 없이 동작 먼저)

룰 3: 타임코드 X, 패널 번호 사용
  ⛔ "[00:00-00:03] wide establishing..."
  ✅ "@Image1 Panel 01 as Shot 1: ..."

룰 4: 패널 = Shot 의무 명시 문구
  필수 2줄:
  "IMPORTANT: @Image1 is a HAND-DRAWN STORYBOARD SHEET.
   Each numbered panel inside @Image1 is a SHOT to render."

룰 5: 카메라 무브 Shot당 1개
  ✅ Shot 1: slow push-in / Shot 2: locked-off / Shot 3: zoom in
  ❌ Shot 1: "push-in then pan then zoom" (1 Shot에 3개 혼합)

룰 6: 고정 문구 항상 포함
  - Maintain exact character appearance from @Image2 throughout.
  - No deformation or drift. Face identity locked.
  - Preserve exact composition and colors from @Image1.
  - Follow composition guidance from @Image1 storyboard panels.
  - 10 seconds. [9:16 or 16:9].

룰 7: 한국어 립싱크 (모든 씬 의무)
  필수 문구:
  - Korean dialogue lip-sync
  - accurate mouth movement matching Korean phonemes
  - Visible mouth opening and closing synced to Korean syllable rhythm
  - Mouth area must be visible and unobstructed during dialogue
  
  모음별 mouth shape:
  ㅏ/ㅑ wide open / ㅓ/ㅕ medium / ㅗ/ㅛ round
  ㅡ narrow flat / ㅣ stretched horizontal / ㅜ/ㅠ small pursed
  
  실패 차단:
  ⛔ 뒷모습/측면 끝각 = 입 안 보임
  ⛔ 마스크/손으로 입 가림
  ✅ 정면 또는 3/4 각도 / 입 영역 frame center

룰 8: TTS 성별·연령·음역·톤 명시 강제
  형식: TTS 톤: [성별][연령대] [음역] [감정 톤]
  ✅ "남성 30대, 중저음, 차분한 경제 애널리스트"
  ✅ "여성 40대, 중고음, 분노 폭발 톤 — drop heavy end"
  ❌ "차분한 톤" (성별·연령 누락)
  ❌ "다큐 톤" (디테일 부족)

룰 9: 최종 스타일 명시 (EP별)
  ✅ "Render in Korean webtoon caricature style
       (NOT pencil sketch — convert rough storyboard to final cartoon)"
  ❌ Render in 명시 누락 = 연필 스케치 그대로 나옴

룰 10: 행동 지시 구체화 강제 (NEW V3.5) ⭐
  ❌ "화가 난 표정으로 손을 든다" (추상)
  ✅ "오른손 검지를 카메라 방향으로 천천히 들어올리며,
      턱을 당기고 눈썹을 찌푸린 채 입술을 꽉 다문다" (구체)
  
  체크리스트:
  □ 어느 쪽 손/발인지 (left/right)
  □ 어떤 방향으로 (upward / forward / toward camera)
  □ 속도 (slowly / suddenly / gradually)
  □ 얼굴 표정 세부 (눈썹 / 입술 / 턱 / 시선 방향)
  □ 몸 전체 자세

룰 11: 볼륨 강제 (NEW V3.5) ⭐
  모든 I2V 프롬프트에 필수 포함:
  "speak loudly and clearly, strong vocal projection, no whispering,
   confident and audible tone throughout"
  
  ⛔ 금지: whispering / soft voice / quiet tone / gentle murmur
  ✅ 허용: 울면서도 목소리 크게, 떨리더라도 명확하게
  
  이유: 이 문구 없으면 Grok이 조용한 립 무빙만 생성 → 음성 거의 없음

룰 12: 패널 수 결정 기준 (NEW V3.5) ⭐
  나레이션 60자 이상 → 2패널 (Shot당 5초)
  나레이션 50~59자 + 감정 전환 → 3패널 (Shot당 3.3초)
  나레이션 49자 이하 → 침묵/CUT 씬 후보
  
  ⛔ 무조건 3패널 = 위반
  ⛔ SPLIT 화면 = 금지 (Grok 구현 불가)
  필요 시 씬 분리 (N-A / N-B)
```

## 5-F. Voice Performance 문장별 명시 표준 (NEW V3.5)

V3.0의 TTS 톤 1줄을 문장별 4요소로 강화.

```
[V3.5 표준 — 모든 씬 I2V 블록에 추가]

[Voice Performance]
TTS 톤: [성별] [연령대], [음역], [감정 톤]
Type: Korean [성별] documentary narrator, [연령대]
Overall emotion: [이 씬의 메인 감정]

Sentence 1: '[나레이션 첫 문장]'
  → Tempo: [slow/measured/fast]
  → Tone: [warm/cold/urgent/authoritative]
  → Emphasis: [강조 단어] [어떻게: 늘림/낮춤]
  → End direction: [drop/rise/trail off]

Sentence 2: '[나레이션 둘째 문장]'
  → Tempo: [속도]
  → Tone: [톤]
  → Emphasis: [강조 단어]
  → End direction: [종결 방향]

Overall texture: [전체 음색 — slight husky/clear/breathy]
```

### 채널별 Voice Performance 디폴트 매핑

```
[후킹 씬 (씬 001~003)]
Overall emotion: urgent shock
Tempo: measured but firm
Tone: cold authoritative
Emphasis: 핵심 충격 단어 (드롭 톤)
End direction: drop heavy

[통계/구조 분석 씬]
Overall emotion: corrective firmness
Tempo: medium
Tone: confident corrective
Emphasis: 수치, 핵심 단어
End direction: weighted statement

[자기의심 / 1인칭 흔적 씬]
Overall emotion: honest hesitation
Tempo: slower (10% 느림)
Tone: warm vulnerable
Emphasis: "솔직히", "저는"
End direction: gentle trail off

[킬러라인 / 클로징]
Overall emotion: quiet weight
Tempo: slowest
Tone: warm reflective
Emphasis: 마지막 단어
End direction: long quiet drop
```

## 5-G. 카메라 무브 사전 (V3.0 유지)

```
| 무브 | 키워드 | 감정 |
|---|---|---|
| 푸시인 | slow push-in | 압박, 내면 |
| 풀백 | slow pull-back | 고독, reveal |
| 정지 | locked-off static camera | 긴장 |
| 핸드헬드 | natural handheld sway | 현장감 |
| 트래킹 | lateral tracking shot | 이동 |
| 크레인 | slow crane descend | 장대함 |
| 오르빗 | slow 360 orbit | 히어로샷 |
| 랙포커스 | rack focus from foreground to background | 관심 전환 |
| 줌인 | slow zoom in to face | 클라이맥스 |
| 줌아웃 | slow zoom out to reveal context | 진실 폭로 |
| 하드컷 | hard cut to [next shot] | 임팩트 |

룰: Shot당 카메라 무브 1개만. 혼합 금지.
```

---

# 📋 PHASE 5-H — 씬 패키지 출력 표준 포맷 V3.5 ⭐

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
씬 [N/총씬수] | 10초 | [블록명] | [챕터명]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

【씬 정보 + 연출 의도】

장소: [구체적 장소 + 시대]
등장인물: [해당 씬 등장 캐릭터 — 시대별/씬별 분리]
나레이션 (시각 표기): "[원문 그대로]"
나레이션 글자수: __자 (V3.5 패널수 결정 기준)
패널 수: [2패널 OR 3패널] (V3.5 룰 12 적용)
핵심 액션: [이 씬이 시각적으로 보여주는 것 1줄]
연출 의도 (1줄): [감정적으로 전달하는 것]

패널 구성:
  Panel 01 [0s — 샷 종류]: [핵심 동작 1줄] / [연출 노트]
  Panel 02 [5s OR 3.3s — 샷 종류]: [핵심 동작 1줄] / [연출 노트]
  (Panel 03 [6.6s — 샷 종류]: [핵심 동작 1줄] / [연출 노트])  ← 3패널만

표정 코드: [각 캐릭터 시그니처 표정]
TTS 톤 (V3.5 4요소): "[성별] [연령대], [음역], [감정 톤]"
립싱크 강제: ✅ 정면/3-4 각도 + 입 보임 확보

──────────────────────────────────────────
【A. 나노바나나2 스케치보드 프롬프트】
──────────────────────────────────────────

[이미지 레퍼런스]
@Image2: character_sheet_ALL.jpg

STYLE: Hand-drawn pencil and ink storyboard sheet,
loose gestural pencil sketches with rough graphite lines,
NO color rendering inside panels (black and white pencil only,
except small color palette swatches at bottom),
NO finished illustration quality,
authentic film production storyboard aesthetic
(Pixar / DreamWorks animation pre-production style reference),
white paper background with slight texture,
each panel framed with thin red rectangle (camera frame indicator),
blue arrows showing movement/breath/energy direction,
handwritten English annotations beside each panel,
character casting reference column on RIGHT side,
bottom section with Notes / Camera Story / Color Palette in handwritten style.

[Layout for Storyboard Sheet]
Title at top (handwritten): "[씬 제목] — [채널명]"
Subtitle (handwritten): "Scene [N]/[Total] — [블록명]"
Legend: "□=Camera/Framing  →=Movement/Energy  ⬤=Character"

Main panel grid (centered, 70% width):
- [N] panels in horizontal row (V3.5 룰 12 적용)
- [16:9 OR 9:16] format

[SPATIAL DESIGN — 평면도 시각 인셋 ⭐ V3.5 핵심]
[하단 우측 인셋에 TOP-DOWN 평면도 시각화]
Location: [장소 + 시대]
North wall: [구조물]
South wall: [구조물]
East/West: [구조물]
Character [이름] position: facing [방향]
Character [이름] sits/stands at: [위치]
📷 Camera positions:
  Panel 01 cam: [위치]
  Panel 02 cam: [위치]
Props (locked across all panels):
- [소품 1 + 위치]
- [소품 2 + 위치]
Panel별 BG 매핑:
Panel 01 BG: [카메라 각도에서 보이는 배경]
Panel 02 BG: [다른 카메라 각도의 배경]
(Panel 03 BG: [측면 또는 와이드 배경])

[패널별 상세]

Panel 01 [0s — 샷 종류]:
- Number circle top-left: "(01)" handwritten
- Shot label top: "[샷 종류] — [나레이션 핵심 키워드]"
- Inside panel (ROUGH PENCIL SKETCH):
  [나레이션이 말하는 장면 정확히 시각화]
  [구체적 묘사: 배경 / 캐릭터 위치 / 핵심 동작]
- Red rectangle = camera frame
- Blue arrow: [움직임 방향]
- Right annotation (handwritten 2-3줄):
  "• [나레이션 매칭 노트]
   • BG: [패널별 배경]
   • [카메라 노트]"

Panel 02 [5s OR 3.3s — 샷 종류]:
(동일 구조)

(Panel 03 필요 시 동일 구조 — V3.5 룰 12 따라)

RIGHT COLUMN (Character Design + Casting):
Title: "CHARACTER DESIGN + CASTING"
[해당 씬 등장 캐릭터만]
"CHAR N — [역할], [성격 키워드]" [portrait sketch]
"Match @Image2 for ALL appearances"

BOTTOM LEFT BOX — "NOTES / FLOW INTENTIONS":
• "[나레이션 핵심 내용 요약]"
• "[블록 분위기]"
• "Draw EXACTLY what narration says"

BOTTOM CENTER BOX — "CAMERA / STORY NOTES":
• "Panel→Panel: HARD CUT each"
• "Each panel = [5s OR 3.3s]"
• "0s already in motion — NO build-up"

BOTTOM RIGHT BOX — "COLOR PALETTE (mood reference)":
• [색상 HEX] "[감정 키워드]" (4-5개)

[네거티브]
NO color rendering inside panels (pencil only — except small palette swatches),
NO finished illustration quality,
NO digital painting,
NO clean vector lines,
NO 3D rendering,
NO photorealistic backgrounds inside panels,
NO scene number watermark inside panels,
NO English meta-tags floating outside annotations,
characters must match @Image2 reference style,
loose rough sketch aesthetic only.

[비율]
[16:9 horizontal 1920x1080 (롱폼) OR 9:16 vertical 1080x1920 (숏폼)]

──────────────────────────────────────────
【B. 그록 Aurora I2V 프롬프트】
──────────────────────────────────────────

[이미지 업로드]
@Image1: scene[N]_board.jpg (스토리보드 시트)
@Image2: character_sheet_EP##.jpg (캐릭터 시트)

IMPORTANT: @Image1 is a HAND-DRAWN STORYBOARD SHEET.
Each numbered panel inside @Image1 is a SHOT to render.
Render each panel as a finished [EP 비주얼 스타일] animated scene
(NOT as pencil sketch — translate the rough sketch into final illustrated style).

[N] shots, 10 seconds total, [16:9 OR 9:16]

@Image1 Panel 01 as Shot 1:
[배경 먼저 — 장소·조명·분위기 1줄]
Camera: [무브 1개]
[캐릭터 신체 동작 — V3.5 룰 10 구체화]
  어느 쪽 손/발 / 방향 / 속도 / 표정 세부 (눈썹/입술/턱/시선) 명시
he/she says [감정 태그], "[한국어 나레이션]"

@Image1 Panel 02 as Shot 2:
[배경 먼저]
Camera: [무브 1개]
[캐릭터 구체적 신체 동작]
Narration continues: "[나레이션 계속]"

(Panel 03 필요 시 — V3.5 룰 12)

speak loudly and clearly, strong vocal projection, no whispering,
confident and audible tone throughout.

[전체 분위기 1줄]

SFX: [구체적 환경음 + 효과음]
BGM: no music

[Voice Performance — V3.5 문장별 명시]
TTS 톤: [성별] [연령대], [음역], [감정 톤]
Type: Korean [성별] documentary narrator, [연령대]
Overall emotion: [전체 감정]
Sentence 1: '[나레이션 첫 문장]'
  → Tempo: [속도] | Tone: [톤] | Emphasis: [강조] | End: [종결]
Sentence 2: '[나레이션 둘째 문장]'
  → Tempo: [속도] | Tone: [톤] | Emphasis: [강조] | End: [종결]
Overall texture: [전체 음색]

Korean dialogue lip-sync, accurate mouth movement matching Korean phonemes.
Visible mouth opening and closing synced to Korean syllable rhythm.
Lip movement must follow Korean phonetic patterns (not English timing).
Mouth area must be visible and unobstructed during dialogue.

Render in [EP 비주얼 스타일]
(NOT pencil sketch — convert rough storyboard to final [스타일명] art).
Frame composition matches @Image1 panels exactly.

Maintain exact character appearance from @Image2 throughout.
No deformation or drift. Face identity locked. Clothing unchanged.
Preserve exact composition and colors from @Image1.
Follow composition guidance from @Image1 storyboard panels.

[V3.5 연속성 4항목]
SPACE CONTINUITY: All elements consistent with scene location.
CHARACTER CONTINUITY: [시대/씬] characters only.
PROP CONTINUITY: Props consistent unless explicitly changed.
TIME CONTINUITY: Same time of day lighting throughout.

10 seconds. [16:9 OR 9:16].

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

# 🔍 PHASE 6 — 자체 평가 (V3.5 100점 만점)

V3.0 평가표 그대로 유지 + V3.5 보강 항목 4개 추가:

```
[V3.5 신규 4점 항목 — V3.0 기준 22점에 추가]

행동 지시 구체화 (V3.5 룰 10)              : 1점
볼륨 강제 문구 (V3.5 룰 11)                : 1점
패널 수 결정 룰 적용 (V3.5 룰 12)          : 1점
Voice Performance 문장별 + 연속성 4항목    : 1점

[기존 V3.0 22점 항목 유지]
글자수 60~80자 강제                        : 6점
TTS 성별·연령 명시                         : 4점
립싱크 정확도                              : 4점
빙산 원칙                                  : 4점
비선형 점프                                : 2점
자기 의심 + 1인칭                          : 2점

[기존 V3.0 78점 항목 그대로]
... (V3.0 유지)
```

---

# ✅ PHASE 7 — 자동 검증 (V3.5 30항목)

```python
def validate_content_v35(content, format_type, scene_data):
    """V3.5 30항목 자동 검증"""
    checks = {}
    
    # V3.0 22항목 유지 (위 내용 참조)
    # ...
    
    # V3.5 신규 8항목 ────────────────────────
    
    # 23. 패널 수 결정 룰 (V3.5 룰 12)
    panel_mismatches = []
    for scene_label, scene in scene_data.items():
        narr_len = len(re.sub(r'\s', '', scene['narration']))
        actual_panels = scene['panel_count']
        if narr_len >= 60 and actual_panels != 2:
            panel_mismatches.append((scene_label, narr_len, actual_panels))
        elif 50 <= narr_len <= 59 and actual_panels != 3:
            panel_mismatches.append((scene_label, narr_len, actual_panels))
    checks['패널수 룰'] = (len(panel_mismatches) == 0, panel_mismatches)
    
    # 24. 행동 지시 구체화 (V3.5 룰 10)
    abstract_patterns = ['화가 난 표정', '슬픈 표정', '기쁜 표정', '손을 든다',
                          '쳐다본다', '바라본다', '걷는다']
    abstract_found = sum(content.count(p) for p in abstract_patterns)
    checks['행동 구체화'] = (abstract_found == 0, f'추상 표현 {abstract_found}건')
    
    # 25. 볼륨 강제 문구 (V3.5 룰 11)
    volume_pattern = "speak loudly and clearly"
    volume_count = content.count(volume_pattern)
    i2v_count = content.count('@Image1 Panel') // 2  # 각 I2V에 1회씩
    checks['볼륨 강제'] = (volume_count >= i2v_count * 0.95,
                          f'{volume_count}/{i2v_count}')
    
    # 26. Voice Performance 문장별 (V3.5)
    vp_count = content.count('Voice Performance')
    sentence_count = content.count('Sentence 1:')
    checks['VP 문장별'] = (sentence_count >= vp_count * 0.95,
                          f'{sentence_count}/{vp_count}')
    
    # 27. 연속성 4항목 (V3.5)
    cont_items = ['SPACE CONTINUITY', 'CHARACTER CONTINUITY',
                  'PROP CONTINUITY', 'TIME CONTINUITY']
    cont_count = min(content.count(item) for item in cont_items)
    checks['연속성 4항목'] = (cont_count >= i2v_count * 0.95,
                              f'각 항목 {cont_count}회')
    
    # 28. SPATIAL DESIGN 평면도 인셋 명시 (V3.5)
    spatial_inset = content.count('SPATIAL DESIGN 평면도') + \
                    content.count('TOP-DOWN') + \
                    content.count('평면도 인셋')
    checks['SPATIAL 인셋'] = (spatial_inset >= i2v_count * 0.95,
                              f'{spatial_inset}회')
    
    # 29. Render in [final style] (V3.5 룰 9)
    render_count = content.count('Render in') + content.count('NOT pencil sketch')
    checks['Render 명시'] = (render_count >= i2v_count * 0.95,
                            f'{render_count}/{i2v_count}')
    
    # 30. 실패 패턴 6가지 자동 검출
    failure_patterns = {
        '이미지시트 그대로': content.count('@Image1 Panel') == 0,
        '추상 동작 (룰10 위반)': abstract_found > 5,
        'Identity Drift 위험': content.count('Maintain exact character') == 0,
        '배경 다름 (SPATIAL 누락)': spatial_inset == 0,
        '음성 안 들림 (볼륨 누락)': volume_count == 0,
        '스케치 그대로 (Render 누락)': render_count == 0,
    }
    failures = [k for k, v in failure_patterns.items() if v]
    checks['실패 패턴 차단'] = (len(failures) == 0, failures)
    
    return checks
```

---

# 📦 PHASE 8 — 풀패키지 출력 (V3.5 5개 파일)

```
1. {EP번호}_FINAL.md            (씬 패키지 한 쌍 — V3.5 풀 포맷)
2. {EP번호}_SEO.md              (제목/설명/태그/연관키워드)
3. {EP번호}_SCRIPT_TEXT.md      (순수 나레이션만)
4. {EP번호}_SPATIAL_DESIGN.md   (시각 평면도 그룹별 — V3.5 인셋 포함)
5. {EP번호}_CHARSHEET.md        (캐릭터시트 ALL — V3.5 캐스팅 정보)
```

---

# ⚠️ V3.5 핵심 원칙 (V3.0 25원칙 유지 + V3.5 7원칙 추가)

```
[V3.0 25원칙 모두 유지]

[V3.5 신규 7원칙]

26. 패널 수 가변 룰
    60자+ = 2패널 / 50~59자 = 3패널 / 49자- = 침묵
    무조건 3패널 금지

27. 행동 지시 구체화 강제
    어느 손/발 / 방향 / 속도 / 얼굴 세부 (눈썹/입술/턱/시선)
    "hand stops mid-air" 같은 추상 = 위반

28. 볼륨 강제 문구
    모든 I2V에 "speak loudly and clearly" 필수
    없으면 Grok 조용한 립 무빙만 생성

29. Voice Performance 문장별
    TTS 톤 1줄 = 위반
    Sentence 1/2/3 별 Tempo/Tone/Emphasis/End direction 명시

30. SPATIAL DESIGN 평면도 시각 인셋
    텍스트 블록만 = 위반
    하단 우측 인셋에 TOP-DOWN 시각화 의무

31. 연속성 4항목 명시
    SPACE/CHARACTER/PROP/TIME CONTINUITY 모두 명시
    매 I2V 마지막 블록에 의무

32. 실패 패턴 6가지 자동 검출
    매 씬 출력 전 자동 검수:
    이미지시트 그대로 / 움직임 뻣뻣 / Identity Drift /
    배경 다름 / 음성 안 들림 / 스케치 그대로
```

---

# 📝 메타 정보

```
버전: V3.5
작성일: 2026.05.18
기준: V3.0 + 시간의발굴자 v3.2 (hamong-tv-v2.8) 흡수
적용 범위: 모든 유튜브 채널 카테고리 (롱폼 + 쇼츠)

V3.0 → V3.5 핵심 차별점:
- I2V 룰 12개 정밀화 (룰 10/11/12 신규 추가)
- 씬 패키지 출력 포맷 완전 표준 (PART 35)
- SPATIAL DESIGN 평면도 시각 인셋 의무화
- Voice Performance 문장별 명시 강제
- 연속성 4항목 (SPACE/CHARACTER/PROP/TIME) 명시
- I2V 실패 패턴 6가지 자동 검출 시스템
- 자동 검증 22항목 → 30항목

호환성:
- V3.0 기능 100% 유지
- V3.0 산출물 V3.5에서 보강만 추가 (재작업 불필요)
- EP.05부터 V3.5 풀 적용 가능

메모리 신규 저장: #20~#26 (총 7개)
```

---

*V3.5는 V3.0의 모든 기능을 유지하면서 시간의발굴자 v3.2의 실전 검증된 7개 신규 룰을 통합했습니다.*
*EP.05부터 V3.5 풀 적용 가능합니다.*
*마스터 워크플로우 + 메모리 26개 + 부속 자산 = 풀 오토메이션 트라이앵글.*
