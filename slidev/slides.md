---
theme: default
background: '#000000'
class: text-center
highlighter: shiki
lineNumbers: true
title: 사제동행세미나 발표
drawings:
  enabled: true
layout: center
---

<h1 class="text-6xl font-bold">조금 더 똑똑하게 바이브코딩하기</h1>

#### 20203040 김성호
---
layout: default
---

# 바이브 코딩(Vibe Coding)이란?

"분위기에 맡기는 코딩, 그 실체는?"

- **극단적 정의**: "코드를 읽지 마라, 완전히 바이브에 맡기고 'Accept All'을 눌러라." (Andrej Karpathy)
- **실무적 접근**: "자연어로 의도를 전달하고 에이전트가 코드를 생성하되, <br> 개발자는 결과를 검증하고 방향을 조정하는 방식"

<div class="mt-16 grid grid-cols-2 gap-4 text-center">
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-blue-300 text-xl font-bold mb-2">Agent</h3>
    <p>코드 생성, 파일 수정, 명령 실행</p>
  </div>
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-green-300 text-xl font-bold mb-2">Human</h3>
    <p>의도 전달, 결과 검증, 최종 의사결정</p>
  </div>
</div>

---
layout: default
---

# 왜 거대한 스펙을 통째로 넣으면 실패할까?

LLM이 가진 4가지 인지적/구조적 한계

1. **Lost in the Middle**: 문서가 길어질수록 중간에 위치한 중요 요구사항을 놓침.
2. **Working Memory의 부재**: 복잡한 다중 지시사항을 잠시 저장하고 하나씩 꺼내 쓰는 '임시 공간'이 없음.
3. **오류의 누적**: Autoregressive 특성상 초반의 작은 오해나 자의적 해석이 전체 시스템의 치명적 오류로 확산됨.
4. **학습 데이터 편향**: 대화가 길어질수록 최신 컨벤션보다 과거에 많이 학습된 패턴으로 회귀함.

<p class="mt-8 text-lg text-blue-400 font-bold border-l-4 border-blue-500 pl-4">
해결책 💡 인간이 메모하고 분업하듯, LLM에게도 '시스템적 작업 공간'을 주어야 한다.
</p>

---
layout: default
---

# 에이전트를 통제하는 3가지 카테고리


<div class="bg-gradient-to-br from-blue-900 to-blue-800 text-white p-6 rounded-lg shadow-xl border border-blue-700">
  <h3 class="text-blue-300 text-xl font-bold mb-2">실행 제어 및 시각화</h3>
  <p class="text-gray-200">행동을 통제하라</p>
</div>

<div class="bg-gradient-to-br from-green-900 to-green-800 text-white p-6 rounded-lg shadow-xl border border-green-700">
  <h3 class="text-green-300 text-xl font-bold mb-2">인지 능력 및 컨텍스트 분산</h3>
  <p class="text-gray-200">복잡도를 나누어라</p>
</div>

<div class="bg-gradient-to-br from-yellow-900 to-yellow-800 text-white p-6 rounded-lg shadow-xl border border-yellow-700">
  <h3 class="text-yellow-300 text-xl font-bold mb-2">기억 관리 및 규칙 자산화</h3>
  <p class="text-gray-200">망각을 방지하라</p>
</div>

---
layout: default
---

# 1. 실행 제어 및 시각화
"오해가 눈덩이처럼 커지기 전에 차단하는 방법"

<div class="grid grid-cols-3 gap-4 mt-8">
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-blue-300 text-lg font-bold mb-3">멀티턴 대화</h3>
    <p class="text-sm text-gray-300">복합 요구사항을 한 번에 주지 않고, 턴(Turn) 단위로 쪼개어 결과 확인 후 다음 지시.</p>
  </div>
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-blue-300 text-lg font-bold mb-3">Plan 모드</h3>
    <p class="text-sm text-gray-300">에이전트가 코드를 수정하기 전, 수정 계획서를 먼저 작성하게 하여 방향성 사전 검증.</p>
  </div>
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-blue-300 text-lg font-bold mb-3">Todo</h3>
    <p class="text-sm text-gray-300">여러 파일을 수정할 때 Todo 리스트를 만들게 하여 'Lost in the middle'에 의한 파일 누락 방지.</p>
  </div>
</div>

<div class="mt-8 bg-gray-900 text-white p-4 rounded text-sm font-mono border border-gray-700">
  <span class="text-gray-400">// Plan 모드 + Todo 조합의 힘</span><br>
  <p class="mt-2">> "인증 리팩토링할 건데, 먼저 수정할 파일들 Todo로 만들고 계획을 보여줘."</p>
</div>

---
layout: default
---

# 2. 인지 능력 및 컨텍스트 분산
"단일 에이전트의 시야 한계를 극복하는 방법"

<div class="grid grid-cols-2 gap-8 mt-8">
<div class="bg-gray-900 text-white p-6 rounded border border-gray-800">
  <h3 class="text-green-400 font-bold text-lg">서브에이전트</h3>
  <p class="text-sm mt-2 text-gray-300">거대한 코드베이스를 한 번에 던져주지 않고, 도메인/역할별로 에이전트를 생성.</p>
  <ul class="text-sm mt-2">
    <li>각 에이전트는 독립된 작은 컨텍스트만 유지</li>
    <li>프론트엔드/백엔드 분리, 혹은 QA 등 역할별 병렬 리뷰</li>
  </ul>
</div>
<div class="bg-gray-900 text-white p-6 rounded border border-gray-800">
  <h3 class="text-purple-400 font-bold text-lg">Extended Thinking</h3>
  <p class="text-sm mt-2 text-gray-300">답변 전 명시적인 '추론(Thinking)' 단계를 강제하여 깊은 사고 유도.</p>
  <ul class="text-sm mt-2">
    <li>복잡한 디버깅, 난해한 아키텍처 설계 시 필수</li>
    <li>단순 CRUD에는 오버헤드, "왜?"가 필요할 때 효과적</li>
  </ul>
</div>
</div>

---
layout: default
---

# 3. 기억 관리 및 규칙 자산화
"에이전트가 시간이 지나도 원칙을 잊지 않게 만드는 방법"

<div class="grid grid-cols-3 gap-4 mt-8">
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-yellow-300 text-lg font-bold mb-3">CLAUDE.md</h3>
    <p class="text-sm text-gray-300">디렉토리별로 프로젝트 컨벤션, 핵심 명령어를 기록해 에이전트가 상시 참고하도록 강제.</p>
  </div>
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-yellow-300 text-lg font-bold mb-3">Agent Skill</h3>
    <p class="text-sm text-gray-300">일회성 프롬프트 대신 커스텀 검사 로직(예: 보안 룰 체크, N+1 쿼리 검사)을 만들어 반복 검증.</p>
  </div>
  <div class="bg-gray-900 text-white p-6 rounded shadow-lg border border-gray-800">
    <h3 class="text-yellow-300 text-lg font-bold mb-3">Compact</h3>
    <p class="text-sm text-gray-300">/compact 명령어로 길어진 대화의 핵심 결정사항만 요약하고, 불필요한 과거 로그는 비워내어 환각 방지.</p>
  </div>
</div>

---
layout: center
class: text-center
---

# 💡 프롬프트의 대원칙: "명확함이 전부다"

"누가 읽어도 같은 것을 상상할 수 있어야 합니다."

| 나쁜 예 (모호함) | 좋은 예 (명확함/수치화) |
| :--- | :--- |
| "적당히, 빠르게 응답해줘" | "API 응답이 3초 넘으면 타임아웃 처리해" |
| "파일이 너무 많으면 안 돼" | "파일 업로드는 최대 5개까지만" |
| "Redux 패턴 쓰지 마" | "상태 관리는 Zustand로 작성해줘" |

<p class="mt-8 text-gray-400 text-sm">※ 부정문보다는 긍정문으로, 경계 조건을 명시할 것.</p>

---
layout: center
---

## **에이전트는 만능이 아닙니다.**
## **우리의 인지 구조를 닮아 편향과 한계가 있습니다.**

1. <span class="text-blue-400">쪼개고 통제하십시오.</span>
2. <span class="text-green-400">역할을 나누고 깊게 생각하게 하십시오.</span> 
3. <span class="text-yellow-400">규칙을 시스템화하고 다이어트 하십시오.</span>

---
layout: center
---

# Q&A

감사합니다!

<div class="mt-10 text-sm text-gray-400">
발표 자료 출처: helloworld.kurly.com - Claude Code 바이브 코딩 전략
</div>