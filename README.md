# Revisiting Google Landmark DataSets V2 Clean (RGLDV2)
### S2D2R : Single-Stage Pipeline for Detected-to-Retrieval using Revisiting Google Landmark DataSets V2


**NEW**: Explore the clean dataset index table
[here](https://drive.google.com/file/d/1AV65-pbcG4EceBVw3dqcjQc5KSZK6kLI/view?usp=share_link). 
The dataset was presented in our [CVPR'24 paper](아카이브주소).

This is the revisiting version of the Google Landmarks dataset (GLDv2), which contains images index.
The dataset can be used for landmark recognition and retrieval experiments. 

## Unfaired Landmark Clean Trainset

### Evaluation sets

A key feature of current landmark datasets in field of ILIR is their fragmented origins: training and evaluation sets are often independently collected and released.
Evaluation sets such as Oxford 5k and Paris6k, and their more recent versions, Revisited Oxford (ROxford or ROxf) and Paris (RParis or Rpar), are commoly used.

### Training sets

Neural Code(NC), Neural Code clean(NC-clean), SfM-120k, Google Landmarks V1(GLDv1), and Google Landmarks V2(GLDv2 and GLDv2-clean) are widely applied in ILIR.
Representative clean datasets include NC-clean, SfM-120k, and GLDv2-Clean. They are widely used as regular training sets.

All data should have no common landmark category between the training set and the evaluation set. 

NC-Clean and SfM-120k do not have a common landmark category between the training set and the evaluation set. 
However, the most commonly used GLDV2-clean dataset for retrieval studies is not.

![02](/images/02.jpg)
This figure shows the duplicate results of NC-clean and SfM-120k dataset.
The red box is an Oxford 5k query.
Each row represents the result of applying ANN indexing to the query using data from NC-clean and SfM-120k.
The column displays the top five ranking results.
None of the results from NC-clean and SfM-120k have a similar landmark to the query.

## Confirming Overlapping Landmarks

We first confirm the existence of a common landmark category between the learning set and the evaluation set.

1. Image feature extraction for learning set GLDV2-clean, NC-clean, SfM-120k and evaluation set Oxford5k, Paris6k
2. The image feature extracted from GLDV2-clean is indexed using approximate neighbor search (ANN)
3. Using Oxford5k and Paris6k as queries, search by applying the previously built learning set to ANN indexing (DB)

Through the above process, it was confirmed that the same category image exists in GLDV2-clean.

![A2](/images/A2.png)
This figure displays the overlapping results. 
The green box (on the left) represents the outcome when using Oxford5k as a query, while the blue box (on the right) indicates the result with Paris6k. 
The red box in both sets highlights the query used for input. 

Each row represents the result of applying ANN indexing to the query using data from GLDv2-clean, NC-clean, and SfM-120k. 
The columns display the top-5 ranking results. The pink box identifies images with landmarks that match those in the query. 

Interestingly, none of the results from NC-clean and SfM-120k feature landmarks that resemble the query. 
In contrast, the results from GLDv2-clean include images with landmarks identical to those in the query. 
This suggests that using the GLDv2-clean dataset could lead to artificially inflated accuracy scores in testing when compared to NC-clean and SfM-120k. 

## Verification

1. Extract the local descriptor of top-k using SIFT and try to match it using kd-tree
2. Remove outlier using RANSAC for matching results
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
