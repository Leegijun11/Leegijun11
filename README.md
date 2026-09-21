# Lee Gi Jun
**Backend Developer | LLM / RAG**

AI 기능(LLM, RAG)을 실제 서비스로 설계하고 배포하는 백엔드 개발자를 목표로 하고 있습니다.
텍스트 분류, 검색 증강 생성(RAG) 등 다양한 방식으로 AI 모델을 서비스에 연동하는 경험을 쌓고 있습니다.

<hr>

📋 Languages<br /><br />
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
<br /><br />

🤖 AI / Machine Learning<br /><br />
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logo=langgraph&logoColor=white)
![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6F00?style=for-the-badge&logoColor=white)
<br /><br />

⚙️ Backend<br /><br />
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
<br /><br />

🎨 Frontend<br /><br />
![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![Axios](https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white)
<br /><br />

☁️ Cloud & Infra<br /><br />
![AWS](https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![ArgoCD](https://img.shields.io/badge/ArgoCD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=github&logoColor=white)
<br /><br />

🛠️ Tools<br /><br />
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![pytest](https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white)
<br /><br />

📜 Certifications<br /><br />
![정보처리기사](https://img.shields.io/badge/정보처리기사-blue?style=for-the-badge)
![SQLD](https://img.shields.io/badge/SQLD-blue?style=for-the-badge)
<br /><br />

🏆 Awards<br /><br />
> IBM x RedHat AI Transformation - AX Academy 최종 프로젝트 최우수상
>
> IBM x RedHat AI Transformation - AX Academy 우수훈련생 개인상

📬 Contact<br />
> Tistory : [개발자 이기준 블로그](https://myblog73329.tistory.com/)
>
> Email : <dlrlwms11@gmail.com>


<hr>

🚀 Featured Projects<br /><br />

### HANDOVER — 인수인계 업무보조 챗봇 + 신입 적응도 리포트 (2026.08.31 ~ 2026.09.20)

**팀 프로젝트(3인, 팀장) | 인수인계서를 근거로 답하는 RAG 챗봇으로 신입의 반복 질문을 줄이고, 체크리스트 완료를 질문 기록과 교차 검증해 사수에게 신입의 적응도 리포트를 제공하는 서비스입니다.**

**담당 역할 (팀장)**
- 데이터 모델·API 명세·프롬프트 브리프를 먼저 확정해 병렬 개발 충돌 최소화
- 챗봇 RAG, 체크리스트 초안 생성, 적응도 리포트 등 AI 파이프라인 전체 설계·구현
- 비용·트래픽 방어, 보안 검증, 테스트 코드 담당

**핵심 구현**
- LangGraph 기반 RAG 챗봇: 배정 조회 → ChromaDB 검색(배정된 문서 범위로 제한) → 판단·생성 → 로그 저장. "검색된 내용에 답이 실제로 있는지"를 LLM이 함께 판단해 없으면 지어내지 않고 정직하게 거절. 거리 임계값 대신 LLM 판단을 택한 근거는 실측(정답 청크 거리 1.46 > 무관한 질문 1.42)
- 적응도 리포트: 신입의 자가 체크(완료)를 질문 기록과 교차해 "완료 후에도 같은 업무를 계속 묻는 항목" 등 4개 신호를 **서버가 계산**하고, LLM은 사수용 요약만 작성하도록 분리. 업무별 질문 12건을 "12명이 긍정 반응"으로 잘못 서술하는 오해석을 재현해 신호별 해석 가이드를 프롬프트에 추가
- 비용·트래픽 방어: 사용자별+IP별 rate limit, LLM 호출 `max_tokens` 상한, 부하 테스트로 DB 커넥션 풀 병목(기본 15) 확인 후 40으로 조정, 이벤트 루프를 막던 `async` 업로드 API 수정
- 보안: 다른 사수가 남의 신입 리포트·챗로그를 조회할 수 있는 결함을 직접 재현해 수정하고 통합 테스트로 회귀 방지
- 테스트: 단위 55개(LLM·ChromaDB mock) + 통합 18개(실제 MySQL). 통합 테스트용 별도 DB는 프로젝트 규모상 불필요하다고 판단해 도입하지 않음

**GitHub: https://github.com/Leegijun11/Handover_rag** <br>

**Tech**<br>
AI/RAG: <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white"> <img src="https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logo=langgraph&logoColor=white"> <img src="https://img.shields.io/badge/ChromaDB-FF6F00?style=for-the-badge&logoColor=white">
<br>
BE: <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"> <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
<br>
FE: <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black">
<br>
Test: <img src="https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white">

<hr>

### 스미싱 문자 판별 및 대처 가이드 (2026.07.29 ~ 2026.08.17)

**개인 프로젝트 | BERT로 스미싱 문자 유형을 분류하고, RAG로 검색한 유형별 공식 대처방법을 바탕으로 LLM이 위험도와 행동 가이드를 안내하는 서비스입니다.**

**핵심 구현**
- BERT 기반 스미싱 유형 분류 모델 학습 및 검증
- ChromaDB 기반 RAG 파이프라인 설계 및 구현
- 분류 확신도가 낮은 경우 후보 유형을 함께 검색해 LLM이 최종 판단하도록 하는 로직 설계
- LLM 응답 검증(Pydantic) 및 형식 오류 발생 시 자동 재시도 로직 구현

**GitHub: https://github.com/Leegijun11/Smishing-guard** <br>

**Tech**<br>
AI: <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"> <img src="https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black"> <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white">
<br>
RAG/DB: <img src="https://img.shields.io/badge/ChromaDB-FF6F00?style=for-the-badge&logoColor=white">
<br>
Validation: <img src="https://img.shields.io/badge/Pydantic-E92063?style=for-the-badge&logo=pydantic&logoColor=white">

<hr>

### 자취생 요리 추천 (2026.08.18 ~ 2026.08.30)

**개인 프로젝트 | 집에 있는 재료·조리도구와 원하는 요리 종류만 고르면, AI가 만들 수 있는 메뉴를 골라 레시피를 생성하고 스스로 평가까지 해주는 LLM + Multi-Agent 서비스입니다.**

**핵심 구현**
- 생성 에이전트(요리사)와 평가 에이전트(미식가)를 분리한 Multi-Agent 구조로 LangGraph 기반 State 관리 및 조건부 재생성 사이클 구현
- 보유 재료·조리도구와 카테고리에 맞는 레시피 후보를 코드로 매칭하고, 부족한 재료는 대체재 테이블로 인정하는 로직 설계
- 생성된 레시피에 대체재·필수 재료·맵기/굽기 반영 여부를 문자열 검증으로 직접 확인 후 재시도 여부 판단 (미식가 에이전트의 자체 판단에만 의존하지 않도록 설계)
- LLM에게 맡길 판단(레시피 생성·평가)과 코드로 처리할 로직(재고 대조, 조건 분기, 검증)을 명확히 분리

**GitHub: https://github.com/Leegijun11/home_cook** <br>

**Tech**<br>
BE: <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"> <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
<br>
FE: <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black"> <img src="https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white">
<br>
AI/Agent: <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white"> <img src="https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge&logo=langgraph&logoColor=white">

<hr>

### 아이 성장 일기 AI (2026.06.10 ~ 2026.08.04)

**프로젝트 한 줄 소개: AI가 아이의 성장 과정을 분석·기록하여 생일마다 "디지털 성장 일기(북)"을 자동 생성해주는 육아 기록 서비스입니다.**

🏆 IBM x RedHat AX Academy 최종 프로젝트 최우수상

**담당 역할 (팀장)**
- 프로젝트 주제 선정 및 기획 추진
- 프론트엔드 아키텍처 설계 및 개발
- 백엔드-프론트엔드 연결 최종 점검 및 트러블슈팅
- CI/CD·K8s 기반 배포 인프라 구축

**GitHub(Frontend): https://github.com/Leegijun11/dearbaby-ai-fe** <br>
**GitHub(Backend/Infra): https://github.com/Leegijun11/k8s_backend_final** <br>
**회고: https://myblog73329.tistory.com/104**

**Tech**<br>
BE: <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white">
<br>
DB: <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white">
<br>
Infra/CI-CD: <img src="https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white"> <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white"> <img src="https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white"> <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"> <img src="https://img.shields.io/badge/ArgoCD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white">

