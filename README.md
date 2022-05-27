# Bioinfo1
Bioinfo1-Pr

## Subject
LIN28A binding motif predictor 만들기
- Fig S3C를 만드는 도중 얻을 수 있는 LIN28A-bound sequence들로 기계학습으로 예측 모델을 만들고 평가
- CNN이나 random forest, kNN 같은 걸 쓸 수도 있지만 단순하게 PSSM을 보정해서 쓰는 것도 가능합니다.

## Dataset
- CLIP-35L33G.bam: CLIP-seq을 통해 LIN28 RNA-binding protein이 붙은 위치 정보
