# 프로젝트 설명
- 2022년 서울대학교 생물정보학 및 실습1 과목 실습 프로젝트
- 공현승(협동과정 생물정보학전공 박사과정)

## Subject
LIN28A binding sequence predictor 만들기
- Fig S3C를 만드는 도중 얻을 수 있는 LIN28A-bound sequence들로 기계학습으로 예측 모델을 만들고 평가
- CNN이나 random forest, kNN 같은 걸 쓸 수도 있지만 단순하게 PSSM을 보정해서 쓰는 것도 가능합니다.

## Dataset
- CLIP-35L33G.bam: CLIP-seq을 통해 LIN28 RNA-binding protein이 붙은 위치 정보

## Procedure
1. Project1: CLIP-35L33G.bam파일에서 LIN28A-bound sequence를 추출합니다.
2. Project2: Pretrained DNA-Bert model을 이용해 sequences를 벡터공간상에 임베딩하고, 시각화 한 후, binary classification을 수행합니다.

### Project1
1. samtools를 이용해 CLIP-seq 파일을 pile-up 합니다.
2. 각 서열별 shannon entropy를 계산하고, CRES를 계산합니다.
3. read depth와 CREW에 cutoff를 적용해 LIN28A-bound sequence를 선별합니다(positive data).
4. 랜덤 시퀀스로 negative data를 만들어내고 positive data와 합쳐, dataset을 csv로 제작합니다.

### Project2
1. 각 서열을 overlapped 3-mer로 인덱싱하고, pretrained model의 pooler layer output을 이용해 768차원 vector로 임베딩합니다.
2. 벡터공간상에서 랜덤 시퀀스와 LIN28A-bound sequence를 시각화합니다.
3. Project1에서 만든 데이터세트를 학습검증세트와 테스트세트 8:2로 나눠주고, 학습검증데이터세트를 학습데이터세트와 검증데이터세트로 8:2로 나눠줍니다.
4. DNA BERT를 fine-tunnning하여 LIN28A-bound sequence와 random sequence를 분류하는 binary-classification model로 만들어 줍니다.
5. 모델을 학습하고, accuracy를 검증합니다. Project1에서 데이터세트를 balanced dataset으로 만들어 주었음으로, accuracy면 충분합니다.
