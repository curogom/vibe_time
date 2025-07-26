# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 중요: 사용자와의 소통 언어
사용자와 대화할 때는 **한국어를 사용하는 것을 원칙**으로 합니다. 코드, 명령어, 기술 용어는 영어를 유지하되, 설명과 안내는 한국어로 제공합니다.

## Project Overview

VibeTime은 "바이브 코딩" 책의 실습 예제 프로젝트로, AI 기반 적응형 시간 관리 애플리케이션입니다.

### 프로젝트 특성
- **교육용 프로젝트**: 독자들이 Claude Code와 함께 실제 앱을 만들어보는 학습 경험 제공
- **챕터별 브랜치 관리**: 각 챕터의 완성 코드가 별도 브랜치로 관리됨 (chapter-3-warmup ~ chapter-12-final)
- **점진적 개발**: 각 챕터를 통해 기능을 하나씩 추가하며 완성해가는 방식

### 기술 구성
- Mobile app (Flutter)
- Web app (React + TypeScript + Vite)
- Backend (Firebase ecosystem)

## Architecture

### Frontend Structure
- **Mobile (Flutter)**: State management with Provider/Riverpod, adaptive timer system, task management
- **Web (React)**: Component-based architecture with Zustand/Context API for state, Vite for build optimization

### Backend Services
- **Firebase Authentication**: User management and OAuth integration
- **Firestore**: NoSQL database for users, tasks, sessions, analytics
- **Cloud Functions**: AI analysis, scheduled jobs, data aggregation
- **Firebase Storage**: Profile images, data exports

### Key Data Models
- **User**: Profile, preferences, subscription status
- **Task**: Title, priority, tags, estimated/actual time
- **TimerSession**: Duration, productivity rating, task association
- **Analytics**: Productivity patterns, focus time metrics

## Git Branch Strategy

챕터별 브랜치 전략:
```bash
# 특정 챕터 코드 확인
git checkout chapter-7-core-features

# 자신의 작업 브랜치 생성
git checkout -b my-chapter-7

# 챕터 간 차이점 확인
git diff chapter-6-navigation chapter-7-core-features
```

## Development Commands

Once the project is initialized, use these commands:

### Flutter (Mobile)
```bash
# Initial setup (run once)
flutter create vibetime_mobile --org dev.vibetime
cd vibetime_mobile
flutter pub add provider firebase_core firebase_auth cloud_firestore

# Development
flutter run                  # Run on connected device/emulator
flutter test                # Run unit tests
flutter analyze            # Static analysis
flutter build apk          # Build Android APK
flutter build ios          # Build iOS app
```

### React (Web)
```bash
# Initial setup (run once)
npm create vite@latest vibetime_web -- --template react-ts
cd vibetime_web
npm install zustand firebase react-router-dom

# Development
npm run dev                # Start development server
npm run build             # Build for production
npm run preview           # Preview production build
npm run lint              # ESLint check
npm run type-check        # TypeScript validation
```

### Firebase
```bash
# Initial setup
firebase init              # Initialize Firebase project
firebase deploy           # Deploy all services
firebase deploy --only functions  # Deploy Cloud Functions
firebase emulators:start  # Start local emulators for testing
```

## Core Implementation Guidelines

### Timer System Architecture
The adaptive timer system should track:
- Session duration and breaks
- Productivity ratings (1-5 scale)
- Time-of-day patterns
- Task type correlations

### AI/ML Integration
Implement client-side analysis for:
- Optimal focus duration prediction
- Best time slots for specific task types
- Break duration recommendations
- Productivity trend analysis

### State Management Patterns
- **Flutter**: Use Provider for simple state, Riverpod for complex reactive state
- **React**: Zustand for global state, Context API for component trees

### Testing Strategy
- Unit tests for timer logic and AI algorithms
- Integration tests for Firebase operations
- E2E tests for critical user flows (timer start/stop, task creation)

## Important Considerations

1. **Privacy-First Design**: All AI analysis happens client-side; only aggregated metrics are stored
2. **Offline Support**: Core timer and task features must work offline with sync when online
3. **Performance**: Optimize Firestore queries with proper indexing and pagination
4. **Cross-Platform Sync**: Ensure real-time sync between mobile and web apps
5. **Subscription Logic**: Implement feature gating for free vs premium tiers

## API Endpoints (Cloud Functions)

Key functions to implement:
- `analyzeProductivity`: Process session data for insights
- `generateReport`: Create weekly/monthly productivity reports
- `syncUserData`: Handle cross-platform data synchronization
- `processSubscription`: Manage subscription status changes

## File Naming Conventions

- **Flutter**: `snake_case.dart` for files, `PascalCase` for classes
- **React**: `PascalCase.tsx` for components, `camelCase.ts` for utilities
- **Firebase**: `camelCase.js` for Cloud Functions