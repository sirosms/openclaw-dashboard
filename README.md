# 🤖 OpenClaw Dashboard (Frontend)

바이낸스 Futures + Spot + 업비트 통합 모니터링 대시보드. 음성 명령 지원.

## 🏗 MSA 아키텍처

```
┌────────────────────────────────────────────────────┐
│  📱 핸드폰 / 💻 PC                                │
│  ↓                                                 │
│  🌐 GitHub Pages (Frontend) — 이 저장소           │
│     https://USERNAME.github.io/openclaw-dashboard │
│  ↓ HTTPS API 호출                                 │
│  🔒 Backend API (별도 — 맥북 + Cloudflare Tunnel) │
│     - 바이낸스/업비트 API 키 안전 보관             │
│     - CORS 허용된 도메인만 접근                    │
│  ↓                                                 │
│  🤖 Trading Bots (multiScalp, Trailer, ...)       │
└────────────────────────────────────────────────────┘
```

## 🚀 빠른 시작

### 1️⃣ Frontend 배포 (GitHub Pages)
```bash
# 이 저장소를 GitHub에 push
git init
git remote add origin https://github.com/USERNAME/openclaw-dashboard.git
git add .
git commit -m "Initial dashboard"
git push -u origin main

# GitHub 저장소 → Settings → Pages → Source: GitHub Actions
# Actions가 자동 배포 → https://USERNAME.github.io/openclaw-dashboard
```

### 2️⃣ Backend 외부 노출 (Cloudflare Tunnel — 무료)
```bash
# 맥북에서 실행
brew install cloudflared
cloudflared tunnel --url http://localhost:3000

# 출력된 URL 복사 (예: https://random-name.trycloudflare.com)
```

### 3️⃣ Frontend에서 Backend URL 설정
```
방법 A: URL 쿼리
  https://USERNAME.github.io/openclaw-dashboard?api=https://random-name.trycloudflare.com

방법 B: 핸드폰에서 한 번 접속 → localStorage에 저장됨
  이후 https://USERNAME.github.io/openclaw-dashboard 만 접속해도 작동
```

## 🔐 보안

- Backend의 API 키는 GitHub에 절대 push 안 함
- CORS로 허용된 도메인만 백엔드 접근 가능
- Backend에서 .env 환경변수만 사용
- 매도/매수 명령은 텔레그램 봇으로 (대시보드는 읽기 전용)

## 🎤 음성 명령 (Web Speech API)

| 음성 | 동작 |
|------|------|
| "포지션 보여줘" | 포지션 새로고침 |
| "잔고" | 잔고 표시 |
| "수익률" | 전체 PnL |
| "봇 상태" | 가동 봇 목록 |

매도/매수 명령은 보안상 텔레그램 @jarvis_coin_bot으로 사용.

## 📦 구조

```
.
├── index.html              # 단일 페이지 대시보드
├── .github/workflows/
│   └── deploy.yml          # GitHub Pages 자동 배포
└── README.md
```

## 🌈 색상 테마
주황(#ff6b35) 그라데이션 + 다크 브라운 배경.

---

Backend repo: `binance-coin-trading/trading-future`
