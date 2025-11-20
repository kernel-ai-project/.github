# 세금법률 챗붓 서비스 (Tax Law Chatbot Service)

## 📋 프로젝트 개요

세금법률 챗붓 서비스는 청년 사용자를 위한 맞춤형 세금 및 법률 정보 제공 챗봇입니다. 복잡한 세금 용어와 법률 정보를 쉽고 빠르게 찾을 수 있도록 돕는 AI 기반 대화형 서비스입니다.

## 🎯 프로젝트 배경

### 문제 인식
- 청년 사용자들이 세금 관련 정보를 찾기 어려움
- 공공 문서 접근성 및 데이터베이스 부재
- 복잡한 법률 용어로 인한 이해도 저하

## 🛠 기술 스택

### Backend
- **Framework**: Spring Boot 6.x.x
- **API**: FastAPI
- **Database**: Oracle23ai, Redis
- **AI/ML**: LangChain, LangGraph

### Frontend
- **Framework**: React.js

### 캐싱 & 최적화
- **Cache**: Redis (대화 히스토리)

## 📚 발전 과정 및 최적화

### 법률 데이터 범위
프로젝트는 다음 법률 영역을 커버합니다:

**기본 세법**
- 국세기본법
- 소득세법
- 법인세법
- 상속세 및 증여세법
- 종합부동산세법
- 부가가치세법
- 개별소비세법
- 교통·에너지·환경세법
- 주세법

**특수 법률 (국세청 관련)**
- 증권거래세법
- 지방세법
- 지방세기본법
- 지방세징수법
- 법인 공익법인(국세청)
- 법인 부가가치세(국세청)
- 법인 원천징수(국세청)
- 법인 세금 납부(국세청)
- 법인 종합부동산세(국세청)

### 최적화 단계
<img width="2410" height="670" alt="image" src="https://github.com/user-attachments/assets/3632ed23-0b63-4a99-9840-24d76ca4d45e" />

#### 1단계: 쿼리 재작성 노드 개선
- 초기 시스템에서 쿼리 재작성 프로세스 제거
- 불필요한 처리 단계 축소로 응답 속도 개선

#### 2단계: 검색(Retrieve) 노드 최적화
- **하이브리드 검색 도입**: BM25 + Vector 검색 결합
- 키워드 기반 검색과 의미 기반 검색의 장점 결합

#### 3단계: 대화 히스토리 관리
**문제점**
- 매 요청마다 LLM에 전체 대화 히스토리 전송
- 과도한 연산 및 느린 응답 속도

**해결책**
- Redis를 활용한 대화 히스토리 캐싱
- 첫 번째 질문: Oracle DB 조회 후 Redis 저장
- 열번째 질문: 이전 질문/답변 제거 후 최신 대화만 유지
- 요약문 생성 및 저장으로 메모리 최적화

**최종 플로우**
```
채팅방 클릭 → DB에서 최근 대화 이력 조회 → Redis에 저장
              ↓
           대화 진행
              ↓
    아홉번째 대화 ← 특정 소득이나 재산에 대한 문의
              ↓
    열번째 대화 (원천징수란?) ← 소득세의 징수 방법의 하나로...
              ↓
    요약본 생성 및 저장
```

## 🚀 주요 기능

1. **세금 관련 질의응답**: 다양한 세금 관련 질문에 대한 정확한 답변 제공
2. **법률 정보 검색**: 복잡한 법률 용어를 쉽게 설명
3. **대화 히스토리 관리**: Redis 캐싱으로 이전 대화 맥락을 유지하여 연속적인 상담 가능

## 💡 화면
<img width="3024" height="1720" alt="image" src="https://github.com/user-attachments/assets/b92f936d-8e64-4d9e-a132-47369f012de4" />

<img width="3024" height="1720" alt="image" src="https://github.com/user-attachments/assets/c966dd2a-da6f-46c7-afb1-fa86ab89335b" />

<img width="3024" height="1720" alt="image" src="https://github.com/user-attachments/assets/4da8947b-234e-4310-8bc3-600eb8de564a" />

<img width="3024" height="1720" alt="image" src="https://github.com/user-attachments/assets/aa8b35cc-b17a-478b-9a80-2d6069d444ae" />
