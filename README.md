# 토스 경진대회 - CTR 예측

본 저장소는 클릭률(CTR) 예측을 위한 실험용 노트북과 데이터 로딩 예시를 포함합니다. 노트북들은 EDA, 시퀀스 모델(LSTM+MLP) 베이스라인, NVIDIA Merlin 기반 XGBoost 파이프라인 등을 다룹니다.

- 저장소: https://github.com/tkdwl05/CTR_MODEL.git
- Python: 3.12 (노트북 메타데이터 기준)

## 파일 구성
`
[Baseline]_Sequence LSTM + MLP 기반 CTR 예측.ipynb   # LSTM+MLP 시퀀스 베이스라인
NVIDIA_Merlin XGBoost(full-data train in 2min).ipynb # Merlin + XGBoost 파이프라인(옵션, GPU 권장)
Simple_EDA Starter - 클릭률 관련 분석.ipynb           # 기본 EDA
[public_0.34707] 코드 공유합니다..ipynb               # 공유된 참고 노트북
CTR_Model.ipynb                                        # parquet 로드/간단 실험 스켈레톤
train.parquet, test.parquet                            # 학습/테스트 데이터(대용량, .gitignore 처리)
sample_submission.csv                                   # 제출 양식 샘플
open.zip                                                # 추가 리소스(압축)
`

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
