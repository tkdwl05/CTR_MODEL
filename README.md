# 토스 경진대회 - CTR 예측

본 저장소는 클릭률(CTR) 예측을 위한 실험용 노트북과 데이터 로딩 예시를 포함합니다. 노트북들은 EDA, 시퀀스 모델(LSTM+MLP) 베이스라인, NVIDIA Merlin 기반 XGBoost 파이프라인 등을 다룹니다.

- 저장소: https://github.com/tkdwl05/CTR_MODEL.git
- Python: 3.12 (노트북 메타데이터 기준)

## 파일 구성
```
[Baseline]_Sequence LSTM + MLP 기반 CTR 예측.ipynb   # LSTM+MLP 시퀀스 베이스라인

NVIDIA_Merlin XGBoost(full-data train in 2min).ipynb # Merlin + XGBoost 파이프라인(옵션, GPU 권장)

Simple_EDA Starter - 클릭률 관련 분석.ipynb           # 기본 EDA

[public_0.34707] 코드 공유합니다..ipynb               # 공유된 참고 노트북

CTR_Model.ipynb                                        # parquet 로드/간단 실험 스켈레톤

train.parquet, test.parquet                            # 학습/테스트 데이터(대용량, .gitignore 처리)

sample_submission.csv                                   # 제출 양식 샘플

open.zip                                                # 추가 리소스(압축)
```

## 빠른 시작
1) 환경 구성(권장)
`powershell
conda create -n ctr python=3.12 -y
conda activate ctr
pip install pandas pyarrow jupyter scikit-learn xgboost
`
- NVIDIA Merlin 사용 시 별도 CUDA/GPU 환경과 라이브러리 설치가 필요합니다.

2) 데이터 로드 예시
`python
import os, pandas as pd
os.chdir(r'C:/Users/tkdwl/Desktop/토스 경진대회')
train = pd.read_parquet('train.parquet')
test  = pd.read_parquet('test.parquet')
`

3) 노트북 실행
- Simple_EDA Starter - 클릭률 관련 분석.ipynb: 데이터 분포/특성 파악
- [Baseline]_Sequence LSTM + MLP 기반 CTR 예측.ipynb: 시퀀스 특성 반영 베이스라인
- NVIDIA_Merlin XGBoost(full-data train in 2min).ipynb: 테이블/세션 피처 엔지니어링 + XGBoost(옵션)
- CTR_Model.ipynb: 최소 재현 스켈레톤

## 데이터 & 버전 관리
- .gitignore에 *.parquet, open.zip, 캐시 디렉터리 등이 포함되어 대용량 파일은 기본적으로 커밋되지 않습니다.
- 대용량 데이터를 버전 관리하려면 Git LFS 사용을 고려하세요.

## 재현 팁
- 난수 시드 고정, 동일 파이썬/패키지 버전 사용을 권장합니다.
- 실행 순서: EDA  피처/베이스라인  고급 파이프라인(Merlin/XGBoost)

## 라이선스
- 별도 명시 전까지 내부 실험 용도로 사용하세요.

## 링크
- 저장소: https://github.com/tkdwl05/CTR_MODEL.git

## 토스 경진대회 주의 사항

1. 개인 또는 팀 참여 규칙
개인 또는 팀을 이루어 참여할 수 있으며, 동일인이 개인 또는 복수팀에 중복하여 등록 불가
개인 참가 방법 : 팀 신청 없이, 자유롭게 제출탭에서 제출 가능
팀 참가 방법 : 팀 탭에서 가능, 상세 내용은 팀 탭에서 팀 병합 정책 확인
팀 구성 방법: 팀 페이지에서 팀 구성 안내 확인
팀 최대 인원: 4인
'토스' 및 토스 계열사 임직원 참여 불가
  

2. 대회 규칙
	1) 사전 학습 모델 사용 가능 범위

2025년 9월 8일 전(~2025.09.08)에 공식적으로 가중치가 공개되었으며, 최소 상업적 이용이 허용된 오픈소스 라이선스 (예: MIT, Apache 2.0 등)로 배포된 사전 학습 모델만 사용 가능합니다. 해당 조건을 충족하지 않는 모델은 사용할 수 없습니다.
	2) API 사용 제한

원격 서버를 통해서만 접근 가능한 API 형태의 모델(예: OpenAI API, Gemini API 등)은 사용이 불가능합니다. 모든 모델은 로컬 환경에서 직접 실행 가능해야 하며, 외부 서버에 의존하는 방식은 허용되지 않습니다.
	3) 외부 데이터 사용 금지

본 경진대회에서 제공한 데이터 외의 모든 외부 데이터는 사용이 금지됩니다. 단, 제공된 학습 데이터를 바탕으로 사전 학습 모델 또는 허용된 도구를 활용해 데이터 증강 또는 생성하는 것은 가능합니다.
	4) 평가 데이터 누수(Data Leakage)

일반적인 AI 경진대회 원칙과 동일하게 테스트 데이터에 대한 사전 접근·활용 그로 인한 Data Leakage 행위는 일체 금지됩니다. 참가자는 학습 데이터 기반으로만 모델을 개발해야 합니다.

3. 본선 산출물 제출 규칙
		대회 종료 후 본선 진출 후보팀은 아래의 양식에 맞추어 산출물(코드, 보고서)을 dacon@dacon.io 메일로 기한 내에 제출해야합니다.

		[코드 제출 관련]

			🔹코드에 데이터 입/출력 경로를 상대 경로로 표기

			🔹코드와 주석 인코딩: UTF-8

			🔹모든 코드는 오류 없이 설치되고 실행될 수 있어야함

			🔹라이브러리 버전 기재 (requirement.txt)

			🔹모델 학습 및 추론 재현을 위한 환경설정 정보를 반드시 포함해야함

			🔹추론(Inference) 코드는 반드시 별도의 코드 파일로 작성(예시: inference.py 혹은 inference.ipynb)해야 하며, 추론에 활용하는 모델 가중치(Weight) 파일을 필수로 포함

		[산출물 목록]

			1) Private Score 복원이 가능한 전체 개발 코드: 학습과 추론 코드는 반드시 분리

			2) Private Score 복원이 가능한 추론용 모델 가중치(Weight) 파일

			3) 모델 개발 보고서: 본선 평가 항목을 포함한 자유 양식으로 작성



4. 유의 사항
1일 최대 제출 횟수: 3회
사용 가능 언어: Python
모든 csv 형식의 데이터와 제출 파일은 UTF-8 인코딩을 적용합니다.
모든 학습, 추론의 과정 그리고 추론의 결과물들은 정상적인 코드를 바탕으로 이루어져야 하며, 비정상적인 방법으로 얻은 제출물들은 적발 시 규칙 위반에 해당됩니다.
대회 규칙 위반 사항이 적발되는 경우, 최대 실격에 해당할 수 있습니다.
최종 순위는 선택된 파일 중에서 채점되므로 참가자는 제출 창에서 자신이 최종적으로 채점 받고 싶은 파일 1개를 선택해야 합니다.
대회 직후 공개되는 Private 랭킹은 최종 순위가 아니며 2차 평가 이후 수상자가 결정됩니다.
데이콘은 부정 제출 행위를 금지하고 있으며 데이콘 대회 부정 제출 이력이 있는 경우 평가가 제한됩니다. 자세한 사항은 아래의 링크를 참고해 주시기 바랍니다.
https://dacon.io/notice/notice/13

 

5. 문의
대회 운영 및 데이터 이상에 관한 질문을 제외한 모든 문의는 데이콘이 직접 답변하지 않습니다. 기타 질문이나 토론은 토크 게시판을 통해 자유롭게 진행해 주시기 바랍니다.
데이콘의 공식 답변을 희망하는 경우에는 반드시 토크 게시판 게시글 또는 댓글로 문의를 등록해 주셔야 하며, 토크 게시판 이외의 창구를 통해 들어온 문의에는 답변을 드리지 않습니다.
