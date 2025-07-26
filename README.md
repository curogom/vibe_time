# VibeTime

AI 기반 적응형 시간 관리 애플리케이션

## 프로젝트 구조

```
vibetime/
├── vibetime_mobile/    # Flutter 모바일 앱
├── vibetime_web/       # React 웹 앱
├── firebase/           # Firebase 백엔드
│   └── functions/      # Cloud Functions
├── CLAUDE.md           # Claude Code 가이드
└── README.md           # 프로젝트 문서
```

## 시작하기

### Flutter 모바일 앱
```bash
cd vibetime_mobile
flutter run
```

### React 웹 앱
```bash
cd vibetime_web
npm run dev
```

### Firebase
```bash
cd firebase
firebase init  # 초기 설정
firebase deploy  # 배포
```

## 기술 스택

- **모바일**: Flutter, Provider/Riverpod
- **웹**: React, TypeScript, Vite, Zustand
- **백엔드**: Firebase (Auth, Firestore, Functions, Storage)
- **AI/ML**: 클라이언트 사이드 분석

## 개발 가이드

자세한 개발 가이드는 [CLAUDE.md](./CLAUDE.md)를 참조하세요.