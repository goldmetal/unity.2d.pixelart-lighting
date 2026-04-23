# CLAUDE.md

Unity 2D Pixel Art Lighting — Unity Learn ([pixelartlight2d](https://learn.unity.com/project/pixelartlight2d)) 튜토리얼 재현물. 학습/데모용 프로젝트이며 활발한 개발은 없음.

## Unity 버전

- Editor: **6000.0.63f1** (Unity 6) — `ProjectSettings/ProjectVersion.txt` 기준
- Render pipeline: Universal RP `17.0.4` (URP 2D)
- 2D Feature set: `com.unity.feature.2d@2.0.1`
- Input System: `1.16.0`

열 때 정확히 동일 Editor 버전을 사용하는 것이 안전. 다른 버전으로 열면 `ProjectVersion.txt`가 업그레이드되고 머티리얼/Light2D 설정이 변환됨.

## 구조

```
Assets/
  2D_Pixel_Light/         # 튜토리얼 본체
    Scenes/               # Basic.unity, Complete.unity
    Scripts/              # (현재 AIT 관련 스크립트만: AITDeviceSetup, MobileInputToggle)
    Sprites/ Tiles/ Materials/ Shaders/ Animations/ Graphs/
    Settings/             # URP asset, Build Profiles, Presets
  AppsInToss/             # Apps in Toss SDK 통합 (Editor 스크립트, loading.html)
  Settings/Scenes/        # URP2DSceneTemplate.unity
ait-build/                # Apps in Toss 웹 번들러 (Vite + ait CLI), .gitignore됨
webgl/                    # Unity WebGL 빌드 출력, .gitignore됨
```

시작 Scene 후보: `Assets/2D_Pixel_Light/Scenes/Basic.unity` (튜토리얼 시작), `Complete.unity` (완성본).

## Apps in Toss 통합

Toss에서 포크된 브랜치로, `im.toss.apps-in-toss-unity-sdk@release/v2.1.0`을 추가해 Apps in Toss 미니앱으로 배포 가능. 빌드 명령은 `ait-build/`에서:

```bash
cd ait-build
pnpm install
pnpm run build    # ait build
pnpm run deploy   # ait deploy
```

WebGL은 Unity에서 빌드 후 `webgl/`에 출력 → `ait-build/`가 이를 래핑. `AITCredentials.asset`은 `.gitignore`로 보호됨.

## Git LFS

**미설정.** `.gitattributes`가 존재하지 않으며, 스프라이트/텍스처는 일반 Git으로 추적 중. 용량이 크게 늘면 도입 고려.

## 주의

- `Library/`, `Temp/`, `*.csproj`, `*.sln`, `ait-build/`, `webgl/` 모두 `.gitignore` 대상 — 커밋 금지.
- `Assets/WebGLTemplates/`, `Assets/StreamingAssets/build_info`는 AIT SDK가 자동 생성하므로 추적 제외됨.
