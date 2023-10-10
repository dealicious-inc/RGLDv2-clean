# Revisiting Google Landmark DataSets V2 Clean (RGLDV2)
### S2D2R : Single-Stage Pipeline for Detected-to-Retrieval using Revisiting Google Landmark DataSets V2


**NEW**: Explore the clean dataset index table
[here](https://drive.google.com/file/d/1AV65-pbcG4EceBVw3dqcjQc5KSZK6kLI/view?usp=share_link). #이거 우리가 공개하면 바꿔야함
The dataset was presented in our [CVPR'24 paper](아카이브주소).

This is the revisiting version of the Google Landmarks dataset (GLDv2), which contains images index.
The dataset can be used for landmark recognition and retrieval experiments. 

## Confirming Overlapping Landmarks

The criteria for clean datasets published in NC-clean and SfM-120k should not have a common landmark category between the learning set and the evaluation set. 
Currently, the most commonly used GLDV2-clean dataset for retrieval studies is not.
We first confirm the existence of a common landmark category between the learning set and the evaluation set.
1. Image feature extraction for learning set GLDV2-clean, NC-clean, SfM-120k and evaluation set Oxford5k, Paris6k
2. The image feature extracted from GLDV2-clean is indexed using approximate neighbor search (ANN)
3. Using Oxford5k and Paris6k as queries, search by applying the previously built learning set to ANN indexing (DB)

Through the above process, it was confirmed that the same category image exists in GLDV2-clean.

NC-clean과 SfM-120k 에서 공개한 clean 데이터셋의 기준은 학습셋과 평가셋 사이에 공통 된 landmark카테고리가 없어야한다. 
현재 retrieval 연구에 가장 많이 사용되는 GLDV2-clean데이터셋은 그렇지 못하다.
우리는 먼저 학습셋과 평가셋 사이에 공통 된 landmark 카테고리에 대한 존재 유무를 확인한다.
1. 학습셋 GLDV2-clean, NC-clean, SfM-120k와 평가셋인 Oxford5k, Paris6k에 대한 image feature 추출
2. GLDV2-clean에서 추출 된 image feature에 대해 approximate nearest neighbor search(ANN)을 이용하여 indexing
3. Oxford5k, Paris6k를 쿼리로 이용해 앞서 구축한 학습셋에 대해 ANN indexing(DB)에 적용하여 검색

위 과정을 통해 GLDV2-clean에서 동일한 카테고리 이미지가 존재함을 확인하였다.

## Verification

1. Extract the local descriptor of top-k using SIFT and try to match it using kd-tree
2. Remove outerer using RANSAC for matching results
3. Remove the class information (GID) of the most matched dataset
4. Check the results of 3 times manually with 3 inspectors

Additionally, we examined GLDV2-clean, Oxford5k, and Paris6k collected text queries.
Here, we removed all images contained in the relevant GID for one identical matched query (Hotel des Invalides Paris) regardless of the above steps.

1. SIFT를 사용하여 top-k 의 local descriptor 추출 후 kd-tree를 사용하여 매칭시도
2. 매칭 결과에 대해 RANSAC를 이용하여o utlier제거
3. 가장 많이 매칭 된 데이터셋의 클래스 정보 (GID) 제거
4. 3명의 검수자를 통해 3번의 결과를 수작업으로 확인

추가적으로 우리는 GLDV2-clean, Oxford5k, Paris6k 수집한 텍스트 쿼리를 검사하였다.
여기서, 우리는 1개의 동일한 매칭된 쿼리(Hotel des Invalides Paris)에 대해 위의 단계 여부 관계없이, 그 관련 GID에 포함된 모든 이미지들을 제거하였다.


Original Google Landmark DataSets V2 details [here](https://github.com/cvdfoundation/google-landmark.git).
You can download images annotated with labels representing human-made and natural landmarks. 

## Download `index` set

There are 761,757 images in the `index` set.
We 
### Download the list of images and metadata

**IMPORTANT**: Note that the integer landmark id's mentioned here are different
from the ones in the train set above.

-   `index_image_to_landmark.csv`: CSV with id,landmark_id fields: `id` is a
    16-character string, `landmark_id` is an integer. Available at:
    [`https://s3.amazonaws.com/google-landmark/metadata/index_image_to_landmark.csv`](https://s3.amazonaws.com/google-landmark/metadata/index_image_to_landmark.csv).
