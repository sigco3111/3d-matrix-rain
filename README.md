# 3D Matrix Rain

> 영화 *매트릭스*의 디지털 비(Digital Rain) 효과를 3차원 공간으로 재해석한 몰입형 타이포그래피 아트.
> 빛나는 녹색 코드 문자열이 화면 깊숙한 곳에서부터 쏟아지고, 마우스 스크롤에 따라 카메라가 그 사이를 뚫고 지나갑니다.

![concept](https://img.shields.io/badge/concept-cyberpunk--art-00ff41?style=flat-square)
![engine](https://img.shields.io/badge/Three.js-r160-black?style=flat-square)
![license](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

---

## 🎬 Preview

> *스크린샷/데모 영상은 작업 진행 후 추가됩니다.*

---

## ✨ Features (의도)

| 항목 | 설명 |
|---|---|
| **3D 깊이감** | 코드 컬럼이 Z축으로 분포 → DoF(피사계 심도)로 원근 표현 |
| **몰입 카메라** | 마우스 스크롤 → 카메라가 코드 비 사이를 종단 이동 |
| **성능 최적화** | Texture Atlas + `InstancedBufferGeometry`로 수천 글자 동시 렌더링 |
| **Bloom 효과** | Post-processing으로 네온 그린 발광 |
| **제로 의존성** | 모든 코드를 단일 HTML 파일에 인라인 — CDN 한 줄로 즉시 실행 |

---

## 🤖 AI 생성 정보

이 저장소의 핵심 코드는 **OpenCode CLI의 MiniMax-M3 모델**을 통해 작성되었습니다.

**사용된 프롬프트:**

> 영화 매트릭스의 디지털 비 효과를 3차원 공간으로 재해석하여, 빛나는 녹색 코드 문자열들이 화면 깊숙한 곳에서부터 쏟아져 내리며 마우스 스크롤에 따라 카메라가 코드 사이를 뚫고 지나가는 듯한 깊이감(Depth of Field)과 속도감이 느껴지는 몰입형 3D 타이포그래피 아트를 구현해줘.
>
> **Implementation Advice:** Use Three.js. Create text columns using `TextGeometry` or sprites. For performance with many characters, a texture atlas approach with `InstancedBufferGeometry` is best. Use Post-processing for the glow/bloom effect. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.

- **모델:** `MiniMax-M3` (via OpenCode CLI)
- **방식:** 단일 HTML 파일, 인라인 임포트(ESM CDN)

---

## 🚀 Quick Start

### 로컬 실행

```bash
# 아무 정적 서버로 열면 됩니다
python3 -m http.server 8000
# → http://localhost:8000 접속
```

직접 `index.html` 더블클릭은 CORS/ESM 제약으로 동작이 제한될 수 있어요. **로컬 서버 권장.**

### 의존성

없음. 모든 Three.js / Post-processing 모듈은 ESM CDN(`unpkg` / `esm.sh`)을 통해 인라인 임포트됩니다.

---

## 🛠️ Tech Stack

- **Three.js** — WebGL 렌더링 + 씬 그래프
- **EffectComposer + UnrealBloomPass** — 네온 발광
- **InstancedBufferGeometry** — 대량 글자 인스턴싱
- **Texture Atlas** — 글리프 1장 + UV 샘플링
- **Vanilla JS** (ES Modules)

---

## 🗺️ Roadmap

- [x] 저장소 초기화 + README
- [ ] **v0.1** — 단일 HTML 베이스라인: 정적 매트릭스 레인 + Bloom
- [ ] **v0.2** — 카메라 종단 스크롤 + DoF
- [ ] **v0.3** — 풀 인스턴싱 (수천 글자 60fps)
- [ ] **v0.4** — 코드 문자 랜덤성/꺼짐 효과 (리드 캐릭터 강조)
- [ ] **v0.5** — 사운드/인터랙션 폴리시
- [ ] **v1.0** — Vercel 배포 + 라이브 데모

---

## 📂 Project Structure

```
3d-matrix-rain/
├── README.md        # 이 문서
└── index.html       # 단일 HTML (모든 코드 인라인)
```

> 단일 파일 구조 채택 이유: 아트워크 성격 + 의존성 제로 + 즉시 공유 가능.

---

## 📜 License

[MIT](./LICENSE)

---

## EN — English

**3D Matrix Rain** is an immersive reinterpretation of the iconic *Digital Rain* effect from *The Matrix*, rebuilt in full 3D space. Glowing green code cascades from deep within the scene, and the camera dives through the rain as the user scrolls.

### AI Generation

Core code was authored via **OpenCode CLI** using the **MiniMax-M3** model with the prompt shown above (Korean).

### Stack

Three.js · EffectComposer/UnrealBloomPass · InstancedBufferGeometry · Single-HTML (ESM CDN)

### Run

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

### Roadmap

v0.1 baseline → v0.2 camera scroll + DoF → v0.3 full instancing → v0.4 glyph lifecycle → v0.5 polish → v1.0 deploy.
