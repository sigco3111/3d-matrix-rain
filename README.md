# 🟢 3D Matrix Rain — 영화 *매트릭스*의 디지털 비를 3차원으로 재해석한 인터랙티브 타이포그래피 아트

> **Three.js** 기반 몰입형 시각화 — 빛나는 코드 문자열이 화면 깊숙한 곳에서 쏟아지고, 마우스 스크롤로 그 사이를 다이브합니다. `Bloom · DoF · Chromatic Aberration` 5-pass 포스트 프로세싱 체인.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](#english)

---

## 🎬 라이브 데모 (Live Demo)

> **👉 [https://3d-matrix-rain.vercel.app/](https://3d-matrix-rain.vercel.app/)** — 브라우저에서 바로 실행 (WebGL · 60fps)

| | |
|---|---|
| ![Demo](https://img.shields.io/badge/Live-Demo-7C3AED?style=for-the-badge&logo=vercel&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2F3d--matrix--rain-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/3d-matrix-rain) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Three.js_r160-000000?style=flat-square&logo=three.js&logoColor=white) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-0-9CA3AF?style=flat-square) |

### 🎮 빠른 사용법

1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기
2. **스크롤** — 카메라가 코드 비 속을 따라 다이브 (Z축 종단 이동)
3. **마우스 이동** — 카메라 시차 틸트 (스프링 댐핑)
4. **1 / 2 / 3 / 4** — green / amber / cyan / violet 팔레트 즉시 전환
5. **Space** — 일시정지 / 재개
6. **R** — 카메라 위치 리셋
7. **↑↑↓↓←→←→BA** — 코나미 이스터에그 (무지개 팔레트)
8. **H** 또는 우상단 × — 컨트롤 가이드 토글

---

## 🤖 생성 정보 (How this was made)

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

### 📝 사용된 프롬프트 (원문)

```
영화 매트릭스의 디지털 비 효과를 3차원 공간으로 재해석하여, 빛나는 녹색 코드 문자열들이 화면 깊숙한 곳에서부터 쏟아져 내리며 마우스 스크롤에 따라 카메라가 코드 사이를 뚫고 지나가는 듯한 깊이감(Depth of Field)과 속도감이 느껴지는 몰입형 3D 타이포그래피 아트를 구현해줘.

Implementation Advice: Use Three.js. Create text columns using `TextGeometry` or sprites. For performance with many characters, a texture atlas approach with `InstancedBufferGeometry` is best. Use Post-processing for the glow/bloom effect. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

### 구현 핵심 기술

| 항목 | 접근법 |
|---|---|
| **3D 컬럼 분포** | 코드 컬럼이 X·Z 평면에 무작위 배치 → DoF + 안개로 원근감 |
| **대량 인스턴싱** | 수천 글자를 `InstancedBufferGeometry` + Atlas 텍스처로 묶어 60fps 안정 |
| **카메라 다이브** | 마우스 스크롤 → Z축 종단 이동, 마우스 이동 → 시차 틸트 (스프링 댐핑) |
| **리드 글리터** | 프레임마다 머리 글자 일부가 환하게 깜빡임 (`Math.random` 기반) |
| **컬럼 글리치** | 컬럼 단위로 짧은 펄스(2× 밝기) → 사이버 글리치 느낌 |
| **포스트 체인** | `UnrealBloom → Bokeh(DoF) → ChromaticAberration → FilmPass → OutputPass` 5-pass |
| **적응형 품질** | FPS가 47 미만으로 떨어지면 인스턴스 수 30% 자동 감소 (`rAF` 모니터) |

### 생성 환경

| 항목 | 값 |
|------|-----|
| **AI 도구** | OpenCode CLI |
| **모델** | `MiniMax-M3` |
| **입력 방식** | 위 프롬프트 1-shot |
| **방식** | 단일 HTML + ESM CDN 인라인 임포트 |
| **후처리** | 사람이 README 작성 및 구조 정리 |

---

## ✨ Features

- 🟢 **3D 깊이감** — 코드 컬럼이 Z축으로 분포, DoF + 안개로 원근 표현
- 🖱️ **몰입 카메라** — 스크롤 다이브 + 마우스 시차 틸트 (스프링 댐핑)
- ✨ **리드 글리터** — 머리 글자가 프레임마다 환하게 깜빡임
- ⚡ **컬럼 글리치** — 컬럼 전체 펄스 (사이버 글리치 톤)
- 🎨 **4종 팔레트** — `1` green / `2` amber / `3` cyan / `4` violet 즉시 전환
- 🌈 **코나미 이스터에그** — `↑↑↓↓←→←→BA` → 무지개 팔레트 회전
- 🌫️ **미스트 입자** — 300개 드리프트 점 (가산 블렌딩)
- 🎭 **크로마틱 어버레이션** — 밝은 픽셀 가장자리 미세한 RGB 분리 (ShaderPass)
- 📉 **적응형 품질** — FPS < 47 감지 시 인스턴스 30% 자동 감소
- 💡 **Bloom + DoF + OutputPass** — 5-pass EffectComposer 체인
- 📦 **제로 의존성** — 단일 HTML, ESM CDN 한 줄로 즉시 실행
- 🌌 **60fps 안정** — 풀 인스턴싱 + 적응형 품질 + `rAF` 루프

---

## 🚀 실행 방법 (Quick Start)

### 방법 1: 로컬 서버 (권장)
```bash
cd path/to/3d-matrix-rain
python3 -m http.server 8000
# → http://localhost:8000 접속
```

> ⚠️ `index.html` 더블클릭은 CORS / ESM 제약으로 일부 모듈이 차단될 수 있어요. **로컬 서버 권장.**

### 방법 2: 라이브 데모
별도 설치 없이 바로 확인:
👉 **https://3d-matrix-rain.vercel.app/**

---

## 🎮 조작법 (Controls)

| 입력 | 효과 |
|---|---|
| **스크롤** | 비 속을 가로지르며 다이브 (Z축 종단 이동) |
| **마우스 이동** | 카메라 시차 틸트 (스프링 댐핑) |
| **Space** | 일시정지 / 재개 |
| **R** | 카메라 위치 리셋 |
| **1 / 2 / 3 / 4** | green / amber / cyan / violet 팔레트 즉시 전환 |
| **H** 또는 우상단 × | 컨트롤 가이드 표시/숨김 |
| **↑↑↓↓←→←→BA** | 코나미 이스터에그 (무지개 팔레트 0.5초 주기 회전) |

---

## 🛠️ 기술 스택 (Tech Stack)

| 영역 | 사용 기술 |
|---|---|
| **렌더링** | Three.js r160 · WebGL2 |
| **씬 그래프** | InstancedMesh + BufferGeometry |
| **글리프** | 단일 Canvas → Texture Atlas → UV 샘플링 |
| **포스트 프로세싱** | EffectComposer · UnrealBloomPass · BokehPass (DoF) · ChromaticAberration · FilmPass · OutputPass |
| **루프** | `requestAnimationFrame` + 적응형 FPS 모니터 |
| **의존성** | 없음 (ESM CDN `unpkg.com/three@0.160.0` 한 줄) |

---

## 🎨 디자인 결정 (Design Choices)

브레인스토밍 단계에서 내린 결정:

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **구조** | 단일 HTML (모든 인라인) | 아트워크 성격 + 의존성 제로 + 즉시 공유 가능 |
| **3D 방식** | `InstancedBufferGeometry` + Atlas 텍스처 | 수천 글자 60fps 유지 (TextGeometry보다 100× 가볍움) |
| **모션 깊이** | 2단 (스크롤 다이브 + 시차 틸트) | 단순한 종단 이동만으론 부족, 두 입력을 결합해 몰입 강화 |
| **팔레트** | 4종 (green / amber / cyan / violet) | TFT 시네마틱 톤 + 사용자 즉시 전환 |
| **글리치 톤** | 리드 깜빡임 + 컬럼 펄스 (저강도) | 과하지 않게 코드 비의 "데이터 손상" 느낌만 |
| **이스터에그** | 코나미 커맨드 → 무지개 회전 | 데모 공유 시 발견 재미 |

### 직접 커스터마이즈하고 싶다면

`index.html` 상단에서 다음 상수를 조정하면 분위기를 바꿀 수 있어요:

```js
const CONFIG = {
  COLUMN_COUNT: 60,        // 코드 컬럼 수 (성능 트레이드오프)
  CHARS_PER_COLUMN: 30,    // 컬럼당 글자 수
  PALETTE: 'green',        // 시작 팔레트 (green/amber/cyan/violet)
  DOF_FOCUS: 12.0,         // DoF 초점 거리
  BLOOM_STRENGTH: 1.6,     // Bloom 발광 강도
  FPS_MIN: 47,             // 적응형 품질 발동 임계치
  // ... 더 많은 옵션은 코드 내 주석 참조
};
```

---

## 🗺️ Roadmap

- [x] **v0.0** — 저장소 초기화 + README
- [x] **v0.1** — 단일 HTML 베이스라인: 정적 매트릭스 레인 + Bloom
- [x] **v0.2** — 카메라 종단 스크롤 + DoF (Bokeh)
- [x] **v0.3** — 풀 인스턴싱 (수천 글자 60fps 안정화)
- [x] **v0.4** — 글리프 라이프사이클 (리드 캐릭터 깜빡임, 컬럼 글리치)
- [x] **v0.5** — UI 폴리시 (컨트롤 가이드 · 팔레트 전환 · 코나미 이스터에그)
- [x] **v1.0** — Vercel 배포 + 라이브 데모 + README 다층 구조화 ✅
- [ ] **v1.1 (예정)** — 오디오 리액티브 (마이크 입력 → 발광 강도)
- [ ] **v2.0 (예정)** — WebXR 모드 (`VREntry` 진입으로 immersive 다이브)

---

## 📂 프로젝트 구조

```
3d-matrix-rain/
├── README.md        # 이 문서 (다층 구조 + 한/영 통합)
├── index.html       # 단일 HTML (모든 코드 인라인, ESM CDN)
└── preview.png      # README 미리보기 캡처
```

> **단일 파일 구조 채택 이유** — 아트워크 성격 + 의존성 제로 + 즉시 공유. 빌드 단계 없이 CDN 한 줄로 어디서든 실행됩니다.

---

## 📜 License

MIT © 2026 sigco3111

---

## 🇺🇸 English

### Overview

**3D Matrix Rain** is an immersive reinterpretation of the iconic *Digital Rain* from *The Matrix*, rebuilt in full 3D space. Glowing green code cascades from deep within the scene and the camera dives through the rain as the user scrolls. Built on **Three.js r160** with a 5-pass post-processing chain (Bloom · DoF · Chromatic Aberration · Film).

### AI Generation

The code in this repository was authored via **OpenCode CLI** using the **MiniMax-M3** model with the prompt shown in the Korean section above. All design choices and prompt engineering were performed by the repository owner.

| Item | Value |
|---|---|
| **Model** | `MiniMax-M3` |
| **Runtime** | OpenCode CLI |
| **Output** | Single HTML (ESM CDN importmap) |
| **License** | MIT |
| **Dependencies** | None |

### Features

- 🟢 **3D Depth** — Code columns distributed on X/Z plane with DoF + fog
- 🖱️ **Immersive Camera** — Scroll-driven Z-axis dive + spring-damped parallax tilt
- ✨ **Lead Glitter** — Head characters randomly flicker brighter each frame
- ⚡ **Column Glitch** — Whole column pulses 2× brighter for a short moment
- 🎨 **4 Palettes** — `1` green / `2` amber / `3` cyan / `4` violet, instant swap
- 🌈 **Konami Easter Egg** — `↑↑↓↓←→←→BA` triggers rainbow palette rotation
- 🌫️ **Mist Particles** — 300 faint drifting dots (additive blend)
- 🎭 **Chromatic Aberration** — Subtle RGB split on bright edges (ShaderPass)
- 📉 **Adaptive Quality** — When FPS drops below 47, instance count auto-decreases to 70%
- 💡 **Bloom + DoF + OutputPass** — 5-pass EffectComposer chain
- 📦 **Zero Dependencies** — Single HTML, ESM CDN one-liner

### Controls

| Input | Effect |
|---|---|
| **Scroll** | Dive through the rain (Z-axis camera dolly) |
| **Mouse Move** | Camera parallax tilt |
| **Space** | Pause / resume |
| **R** | Reset camera position |
| **1 / 2 / 3 / 4** | green / amber / cyan / violet palette |
| **H** or top-right × | Toggle controls guide |
| **↑↑↓↓←→←→BA** | Konami easter egg (rainbow palette rotation) |

### Quick Start

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

Or just open the live demo: **https://3d-matrix-rain.vercel.app/**

### Stack

- **Three.js r160** — WebGL2 rendering + scene graph
- **EffectComposer** — UnrealBloom · BokehPass (DoF) · ChromaticAberration · FilmPass · OutputPass
- **InstancedBufferGeometry** — thousands of glyphs in one draw call
- **Texture Atlas** — single glyph canvas + UV sampling
- **Vanilla JS** (ESM modules, ESM CDN importmap)

### Roadmap

- [x] **v0.0** — Initial repo + README
- [x] **v0.1** — Single-HTML baseline: static matrix rain + Bloom
- [x] **v0.2** — Camera scroll dolly + DoF
- [x] **v0.3** — Full instancing (thousands of glyphs at 60fps)
- [x] **v0.4** — Glyph lifecycle (lead flicker, column glitch)
- [x] **v0.5** — UI polish (control guide · palette swap · Konami easter egg)
- [x] **v1.0** — Vercel deploy + live demo + multi-layer README
- [ ] **v1.1 (planned)** — Audio-reactive (mic input → glow intensity)
- [ ] **v2.0 (planned)** — WebXR mode (immersive dive via `VREntry`)

### Customize

Top of `index.html`:

```js
const CONFIG = {
  COLUMN_COUNT: 60,        // code columns (perf tradeoff)
  CHARS_PER_COLUMN: 30,    // chars per column
  PALETTE: 'green',        // green / amber / cyan / violet
  DOF_FOCUS: 12.0,         // DoF focus distance
  BLOOM_STRENGTH: 1.6,     // bloom intensity
  FPS_MIN: 47,             // adaptive quality threshold
};
```

### License

MIT © 2026 sigco3111

---

## 🙏 Credits

- **Three.js** — WebGL 렌더링 엔진 + 씬 그래프 (mrdoob & contributors)
- **EffectComposer / post-processing addons** — UnrealBloomPass, BokehPass, FilmPass (Three.js examples)
- **Konami Code** — 클래식 이스터에그 영감
- **AI 생성** — OpenCode CLI + `MiniMax-M3`
- **코딩미션 참조 페이지**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)

---

<p align="center">
  <sub>🟢 Built with Three.js · ESM CDN · sigco3111 · MIT · AI-generated by MiniMax-M3</sub>
</p>
