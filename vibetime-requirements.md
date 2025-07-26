# VibeTime 서비스 요구사항 문서

## 0. 프로젝트 배경 및 목적

### 0.1 프로젝트 목적
이 프로젝트는 "바이브 코딩" 책의 실습 예제로 개발되는 애플리케이션입니다. 

**핵심 목표:**
- 📚 **교육 목적**: 독자들이 Claude Code와 함께 실제 작동하는 서비스를 만들어보는 학습 경험 제공
- 🚀 **실전 개발**: 단순한 예제가 아닌, 실제로 배포 가능한 수준의 완성도 높은 앱 구현
- 📖 **단계별 학습**: 각 챕터별로 기능을 추가하며 점진적으로 완성해가는 과정

### 0.2 개발 접근 방식
- 각 챕터는 독립적인 Git 브랜치로 관리되어 독자가 어느 시점에서든 따라할 수 있음
- 실제 서비스 런칭보다는 "완성도 있는 앱을 만들 수 있다"는 것을 보여주는 것이 목적
- Claude Code와의 대화를 통해 모든 기능을 구현하는 바이브 코딩 방식 실천

## 1. 서비스 개요

### 1.1 프로젝트 명
- **서비스명**: VibeTime
- **도메인**: vibetime.dev
- **슬로건**: "AI와 함께하는 스마트한 시간 관리"

### 1.2 서비스 설명
VibeTime은 AI 기반 적응형 시간 관리 애플리케이션입니다. 사용자의 집중 패턴을 학습하여 15-90분 사이의 최적 작업 시간을 자동으로 조절하고, 생산성을 극대화할 수 있도록 돕습니다.

### 1.3 타겟 사용자
- 재택근무하는 프리랜서
- 집중력 향상을 원하는 학생
- 생산성을 높이고 싶은 직장인
- 시간 관리가 필요한 모든 사용자

### 1.4 차별점
- 고정된 25분 뽀모도로가 아닌 15-90분 가변 타이머
- AI가 사용자의 생산성 패턴을 학습
- 시간대별, 작업 유형별 최적화
- 에너지 레벨 기반 시간 추천

## 2. 기술 스택

### 2.1 Frontend
- **모바일**: Flutter 3.x
  - State Management: Provider / Riverpod
  - Navigation: go_router
  - UI Components: Material Design 3
  
- **웹**: React + TypeScript + Vite
  - State Management: Zustand / Context API
  - UI Library: Material-UI / Tailwind CSS
  - Build Tool: Vite

### 2.2 Backend
- **Firebase**:
  - Authentication (이메일/Google 로그인)
  - Cloud Firestore (데이터베이스)
  - Firebase Storage (프로필 이미지 등)
  - Firebase Analytics
  - Cloud Functions (서버리스 로직)

### 2.3 AI/ML
- 사용자 패턴 분석 로직 (클라이언트 사이드)
- 시간대별 생산성 예측
- 작업 완료율 기반 학습

## 3. 핵심 기능 요구사항

### 3.1 적응형 타이머 시스템
```
요구사항:
- 기본 시작 시간: 25분
- 범위: 15분 ~ 90분
- 조절 요소:
  - 시간대별 생산성 (오전/오후/저녁)
  - 최근 5개 세션 완료율
  - 현재 에너지 레벨 (사용자 입력)
  - 작업 유형 (deep_work, meeting, creative, general)
```

### 3.2 작업 관리 시스템
```
Task 모델:
- id: string
- title: string
- description?: string
- priority: low | medium | high | urgent
- dueDate?: DateTime
- estimatedMinutes: number
- actualMinutes: number
- status: pending | inProgress | completed | cancelled
- tags: string[]
- createdAt: DateTime
```

### 3.3 스마트 스케줄링
```
기능:
- 우선순위와 마감일 기반 자동 정렬
- AI 기반 최적 시간 블록 할당
- 휴식 시간 자동 삽입 (25분 이상 작업 시 5분, 50분 이상 시 10분)
- 드래그 앤 드롭으로 일정 재배치
```

### 3.4 통계 및 분석
```
제공 데이터:
- 일별/주별/월별 집중 시간
- 시간대별 생산성 히트맵
- 작업 카테고리별 시간 분포
- 목표 달성률
- 집중력 향상 추이
```

### 3.5 알림 시스템
```
알림 종류:
- 작업 시작 30분 전 리마인더
- 타이머 완료 알림
- 휴식 시간 종료 알림
- 일일 리포트 (선택적)
```

## 4. UI/UX 요구사항

### 4.1 디자인 원칙
- **미니멀리즘**: 집중을 방해하지 않는 깔끔한 디자인
- **다크 모드 우선**: 눈의 피로를 줄이는 다크 테마 기본
- **직관적 UX**: 복잡한 설정 없이 바로 사용 가능

### 4.2 색상 팔레트
```dart
Primary Blue: #2196F3
Primary Blue Dark: #1976D2
Primary Blue Light: #64B5F6

Secondary Orange: #FF7043
Secondary Orange Dark: #E64A19
Secondary Orange Light: #FFAB91

Success: #4CAF50
Error: #F44336
Warning: #FFC107

Background Light: #FAFAFA
Background Dark: #121212
```

### 4.3 주요 화면
1. **온보딩** (3페이지)
   - 서비스 소개
   - 주요 기능 설명
   - 초기 설정

2. **홈 대시보드**
   - 오늘의 집중 시간
   - 현재 진행 중인 작업
   - 빠른 타이머 시작

3. **타이머 화면**
   - 원형 프로그레스 인디케이터
   - 남은 시간 표시
   - 일시정지/재개/종료 버튼
   - 현재 작업 정보

4. **작업 목록**
   - 우선순위별 정렬
   - 상태별 필터링
   - 검색 기능
   - 스와이프 액션 (완료/삭제)

5. **통계 화면**
   - 생산성 차트
   - AI 인사이트
   - 목표 설정 및 추적

6. **설정**
   - 프로필 관리
   - 알림 설정
   - 테마 변경
   - 데이터 백업/복원

## 5. 데이터 모델

### 5.1 User
```typescript
interface User {
  uid: string;
  email: string;
  displayName: string;
  photoURL?: string;
  createdAt: Date;
  settings: UserSettings;
  stats: UserStats;
}

interface UserSettings {
  theme: 'light' | 'dark' | 'system';
  notifications: {
    taskReminders: boolean;
    timerAlerts: boolean;
    dailyReport: boolean;
    dailyReportTime?: string; // "09:00"
  };
  defaultTimerDuration: number; // minutes
  soundEnabled: boolean;
}

interface UserStats {
  totalFocusMinutes: number;
  currentStreak: number;
  longestStreak: number;
  hourlyProductivity: Record<number, number>; // 0-23 시간대별 생산성
}
```

### 5.2 Task
```typescript
interface Task {
  id: string;
  userId: string;
  title: string;
  description?: string;
  priority: 'low' | 'medium' | 'high' | 'urgent';
  status: 'pending' | 'inProgress' | 'completed' | 'cancelled';
  dueDate?: Date;
  estimatedMinutes: number;
  actualMinutes: number;
  tags: string[];
  projectId?: string;
  createdAt: Date;
  updatedAt: Date;
  completedAt?: Date;
}
```

### 5.3 Session
```typescript
interface Session {
  id: string;
  userId: string;
  taskId?: string;
  startTime: Date;
  endTime: Date;
  plannedDuration: number; // minutes
  actualDuration: number; // minutes
  completionRate: number; // 0-1
  productivityScore: number; // 0-1
  taskType?: 'deep_work' | 'meeting' | 'creative' | 'general';
  interruptions: number;
  notes?: string;
}
```

### 5.4 TimeBlock (스케줄링용)
```typescript
interface TimeBlock {
  id: string;
  taskId?: string;
  startTime: Date;
  duration: number; // minutes
  isBreak: boolean;
  isCompleted: boolean;
}
```

## 6. API 엔드포인트 (Firebase Functions)

### 6.1 통계 관련
```
GET /api/stats/daily?date=2024-01-25
GET /api/stats/weekly?week=2024-W04
GET /api/stats/monthly?month=2024-01
```

### 6.2 AI 추천
```
POST /api/recommendations/timer
Body: {
  currentTime: string,
  taskType?: string,
  energyLevel: number
}

Response: {
  recommendedDuration: number,
  reason: string
}
```

### 6.3 스케줄 생성
```
POST /api/schedule/generate
Body: {
  tasks: Task[],
  startTime: string,
  endTime: string
}

Response: {
  blocks: TimeBlock[]
}
```

## 7. 테스트 케이스

### 7.1 적응형 타이머 테스트
```javascript
describe('AdaptiveTimer', () => {
  test('기본 시간은 25분이어야 함', () => {
    const timer = new AdaptiveTimer();
    const duration = timer.getOptimalDuration({
      currentTime: new Date('2024-01-25T10:00:00'),
      taskType: null,
      currentEnergy: 1.0
    });
    expect(duration).toBe(25);
  });

  test('에너지가 낮을 때 시간이 줄어들어야 함', () => {
    const timer = new AdaptiveTimer();
    const lowEnergyDuration = timer.getOptimalDuration({
      currentTime: new Date('2024-01-25T10:00:00'),
      taskType: null,
      currentEnergy: 0.5
    });
    expect(lowEnergyDuration).toBeLessThan(25);
  });

  test('최소/최대 시간 제한이 작동해야 함', () => {
    const timer = new AdaptiveTimer();
    const duration = timer.getOptimalDuration({
      currentTime: new Date('2024-01-25T10:00:00'),
      taskType: null,
      currentEnergy: 0.1
    });
    expect(duration).toBeGreaterThanOrEqual(15);
    expect(duration).toBeLessThanOrEqual(90);
  });
});
```

### 7.2 작업 관리 테스트
```javascript
describe('TaskManager', () => {
  test('작업 생성 및 조회', async () => {
    const task = await createTask({
      title: '테스트 작업',
      priority: 'high',
      estimatedMinutes: 30
    });
    
    expect(task.id).toBeDefined();
    expect(task.status).toBe('pending');
  });

  test('우선순위별 정렬', () => {
    const tasks = [
      { priority: 'low' },
      { priority: 'urgent' },
      { priority: 'medium' }
    ];
    
    const sorted = sortByPriority(tasks);
    expect(sorted[0].priority).toBe('urgent');
  });
});
```

### 7.3 UI 테스트
```javascript
describe('TimerScreen', () => {
  test('타이머 시작/일시정지/재개', async () => {
    render(<TimerScreen duration={25} />);
    
    const startButton = screen.getByText('시작');
    fireEvent.click(startButton);
    
    expect(screen.getByText('일시정지')).toBeInTheDocument();
    
    fireEvent.click(screen.getByText('일시정지'));
    expect(screen.getByText('재개')).toBeInTheDocument();
  });
});
```

## 8. 성능 요구사항

### 8.1 응답 시간
- 화면 전환: < 300ms
- 데이터 로딩: < 1s
- 타이머 업데이트: 실시간 (1초 단위)

### 8.2 오프라인 지원
- 로컬 데이터 캐싱
- 오프라인 작업 기록
- 온라인 복귀 시 자동 동기화

### 8.3 배터리 최적화
- 백그라운드 작업 최소화
- 효율적인 타이머 구현
- 불필요한 네트워크 요청 방지

## 9. 보안 요구사항

### 9.1 인증 및 권한
- Firebase Auth 기반 사용자 인증
- 이메일 인증 필수
- 사용자별 데이터 격리

### 9.2 데이터 보호
- HTTPS 통신 필수
- 민감 정보 암호화
- 안전한 토큰 관리

## 10. 배포 요구사항

### 10.1 플랫폼
- **Android**: Google Play Store
  - 최소 SDK: 21 (Android 5.0)
  - 타겟 SDK: 33 (Android 13)
  
- **iOS**: App Store
  - 최소 iOS: 12.0
  - Swift 호환성 필수

- **웹**: vibetime.dev
  - Vercel 배포
  - PWA 지원

### 10.2 CI/CD
- GitHub Actions 설정
- 자동 테스트 실행
- 스테이징/프로덕션 환경 분리

## 11. Git 브랜치 전략 및 챕터별 개발 계획

### 11.1 브랜치 구조
독자들이 각 챕터의 완성 상태를 확인하고 따라할 수 있도록 체계적인 브랜치 전략을 사용합니다.

```
main (최종 완성본)
├── chapter-3-warmup (워밍업 - 계산기 앱)
├── chapter-4-flutter-basics (Flutter 기초)
├── chapter-5-design-system (디자인 시스템)
├── chapter-6-navigation (네비게이션)
├── chapter-7-core-features (핵심 기능)
├── chapter-8-firebase (Firebase 연동)
├── chapter-9-advanced (고급 기능)
├── chapter-10-deployment (배포 준비)
├── chapter-11-web (웹 버전)
└── chapter-12-final (최종 완성)
```

### 11.2 챕터별 구현 내용

#### Chapter 3: 워밍업 (chapter-3-warmup)
```
구현 내용:
- 간단한 계산기 앱 (Flutter & React)
- 기본 UI 구성
- 상태 관리 기초

학습 목표:
- Claude와 대화하는 방법
- 에러 해결 프로세스
- 코드 개선 요청하기
```

#### Chapter 4: Flutter 기초 (chapter-4-flutter-basics)
```
구현 내용:
- VibeTime 프로젝트 생성
- 기본 Widget 구조
- 프로필 카드 UI
- Instagram 스타일 포스트 UI

커밋 예시:
- "프로젝트 초기 설정"
- "프로필 카드 위젯 추가"
- "포스트 UI 구현"
```

#### Chapter 5: 디자인 시스템 (chapter-5-design-system)
```
구현 내용:
- 색상 팔레트 정의
- 커스텀 테마 설정
- FocusButton 컴포넌트
- Input Field 컴포넌트
- 반응형 레이아웃

커밋 예시:
- "색상 팔레트 및 테마 설정"
- "재사용 가능한 버튼 컴포넌트"
- "반응형 레이아웃 시스템"
```

#### Chapter 6: 네비게이션 (chapter-6-navigation)
```
구현 내용:
- 온보딩 화면
- go_router 설정
- 하단 네비게이션 바
- 딥링크 지원

커밋 예시:
- "온보딩 화면 구현"
- "go_router 마이그레이션"
- "딥링크 및 URL 기반 라우팅"
```

#### Chapter 7: 핵심 기능 (chapter-7-core-features)
```
구현 내용:
- 적응형 타이머 로직
- 작업 관리 CRUD
- 드래그 앤 드롭 스케줄러
- Provider 상태 관리

커밋 예시:
- "적응형 타이머 시스템 구현"
- "작업 관리 기능 추가"
- "스마트 스케줄링 UI"
```

#### Chapter 8: Firebase 연동 (chapter-8-firebase)
```
구현 내용:
- Firebase 프로젝트 설정
- 이메일/Google 로그인
- Firestore 데이터 모델
- 실시간 동기화

커밋 예시:
- "Firebase 초기 설정"
- "인증 시스템 구현"
- "Firestore 데이터 동기화"
```

#### Chapter 9: 고급 기능 (chapter-9-advanced)
```
구현 내용:
- 생산성 차트 (fl_chart)
- 로컬 알림
- AI 추천 시스템
- 데이터 시각화

커밋 예시:
- "생산성 대시보드 추가"
- "알림 시스템 구현"
- "AI 기반 시간 추천"
```

#### Chapter 10: 배포 준비 (chapter-10-deployment)
```
구현 내용:
- 성능 최적화
- 테스트 코드
- 앱 아이콘/스플래시
- 스토어 메타데이터

커밋 예시:
- "성능 최적화 및 프로파일링"
- "단위/위젯 테스트 추가"
- "배포 준비 완료"
```

#### Chapter 11: 웹 버전 (chapter-11-web)
```
구현 내용:
- Flutter Web 빌드
- React 버전 시작
- 컴포넌트 변환
- Vercel 배포

커밋 예시:
- "Flutter Web 지원 추가"
- "React 프로젝트 설정"
- "주요 컴포넌트 React 변환"
```

### 11.3 독자를 위한 가이드

#### 브랜치 체크아웃 방법
```bash
# 특정 챕터의 완성 코드 확인
git checkout chapter-7-core-features

# 챕터 간 차이점 확인
git diff chapter-6-navigation chapter-7-core-features

# 자신의 브랜치에서 작업
git checkout -b my-chapter-7
```

#### 커밋 메시지 컨벤션
```
feat: 새로운 기능 추가
fix: 버그 수정
refactor: 코드 개선
style: 코드 스타일 변경
docs: 문서 수정
test: 테스트 추가
```

## 12. 향후 확장 계획

### Phase 1 (책 완성 시점 - MVP)
- 기본 타이머 기능
- 작업 관리
- 로컬 저장소
- Firebase 연동
- 웹 버전

### Phase 2 (독자 확장 가능 영역)
- 팀 협업 기능
- 더 정교한 AI 추천
- 다국어 지원
- 플러그인 시스템

### Phase 3 (커뮤니티 기여)
- Apple Watch 앱
- 위젯 지원
- API 공개
- 오픈소스화

## 13. 교육적 성공 지표

### 13.1 학습 목표 달성
- ✅ 독자가 Claude Code와 대화하여 완전한 앱을 만들 수 있음
- ✅ Flutter와 React 모두에서 동일한 서비스 구현 가능
- ✅ 실제 배포 가능한 수준의 품질 달성
- ✅ AI와 협업하는 개발 방식 체득

### 13.2 프로젝트 완성도
- 모든 핵심 기능이 실제로 작동
- 테스트 코드 포함
- 성능 최적화 완료
- 스토어 배포 가능 상태

### 13.3 독자 피드백 (예상)
- "실제로 작동하는 앱을 만들 수 있어서 놀랍다"
- "각 챕터별로 따라하기 쉽게 구성되어 있다"
- "AI와 대화하는 방법을 제대로 배웠다"
- "이제 나만의 앱을 만들 자신감이 생겼다"

---

## 참고사항

### 문서의 성격
이 문서는 "바이브 코딩" 책의 실습 프로젝트인 VibeTime 서비스의 전체 요구사항을 정의합니다. 

**중요**: 
- 📚 이 프로젝트는 **교육 목적의 예제 프로젝트**입니다
- 🎯 실제 서비스 런칭보다 **"실제로 작동하는 앱을 만들 수 있다"**는 것을 보여주는 것이 핵심입니다
- 👥 독자들이 각 챕터를 따라하며 점진적으로 앱을 완성해가는 과정을 중시합니다
- 🤖 모든 코드는 Claude Code와의 대화를 통해 생성됩니다

### 활용 방법
1. **독자**: 각 챕터의 브랜치를 참고하여 따라하기
2. **강사**: 워크샵이나 강의 자료로 활용
3. **AI 도구 사용자**: Claude Code 외 다른 AI 도구로도 구현 가능

**문서 버전**: 2.0  
**최종 수정일**: 2024-01-26  
**작성자**: 바이브 코딩 팀