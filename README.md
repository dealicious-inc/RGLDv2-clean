# Revisiting Google Landmark DataSets v2 Clean (GLDv2-clean)
### On Train-Test Class Overlap and Detection for Image Retrieval
<!-- ### S2D2R : Single-Stage Pipeline for Detected-to-Retrieval using Revisiting Google Landmark DataSets V2 -->

- We revisit Google Landmarks v2 clean, the most popular training set, by identifying and removing class overlap with Revisited Oxford and Paris the most popular training set.

- We introduce Single-stage Detect-to-Retrieve (CiDeR), an end-to-end, single-stage pipeline to detect objects of interest and extract a global image representation. 

## **NEW**

**Explore the clean dataset index table [here](https://drive.google.com/file/d/1AV65-pbcG4EceBVw3dqcjQc5KSZK6kLI/view?usp=sharing).** 
<!-- The dataset was presented in our [CVPR'24 paper](아카이브주소). -->

- This is the revisiting version of the Google Landmarks dataset (GLDv2), which contains images index.
- The dataset can be used for landmark recognition and retrieval experiments. 

## Unfaired Landmark Clean Trainset

### Evaluation sets

A key feature of current landmark datasets in field of ILIR is their fragmented origins: training and evaluation sets are often independently collected and released.
Evaluation sets such as Oxford 5k and Paris6k, and their more recent versions, Revisited Oxford (ROxford or ROxf) and Paris (RParis or Rpar), are commoly used.

### Training sets

Neural Code(NC), Neural Code clean(NC-clean), SfM-120k, Google Landmarks V1(GLDv1), and Google Landmarks V2(GLDv2 and GLDv2-clean) are widely applied in ILIR.
Representative clean datasets include NC-clean, SfM-120k, and GLDv2-Clean. They are widely used as regular training sets.

**All data should have no common landmark category between the training set and the evaluation set.**

NC-Clean and SfM-120k do not have a common landmark category between the training set and the evaluation set. 
However, the most commonly used GLDv2-clean dataset for retrieval studies is not.

## Confirming Overlapping Landmarks

We first confirm the existence of a common landmark category between the learning set and the evaluation set.

1. Image feature extraction for learning set GLDv2-clean, NC-clean, SfM-120k and evaluation set Oxford5k, Paris6k
2. The image feature extracted from GLDv2-clean is indexed using approximate neighbor search (ANN)
3. Using Oxford5k and Paris6k as queries, search by applying the previously built learning set to ANN indexing (DB)

Through the above process, **it was confirmed that the same category image exists in GLDv2-clean.**

<p align="center">
  <img src="/images/A2.png" width="900" alt="A2">
</p>

This figure displays the overlapping results. 

* The green box (on the left) represents the outcome when using Oxford5k as a query, while the blue box (on the right) indicates the result with Paris6k. 
* The red box in both sets highlights the query used for input. 

* Each row represents the result of applying ANN indexing to the query using data from GLDv2-clean, NC-clean, and SfM-120k.
* The columns display the top-5 ranking results.
* The pink box identifies images with landmarks that match those in the query. 

Interestingly, none of the results from NC-clean and SfM-120k feature landmarks that resemble the query.

In contrast, the results from GLDv2-clean include images with landmarks identical to those in the query.

This suggests that using the GLDv2-clean dataset could lead to artificially **inflated accuracy** scores in testing when compared to NC-clean and SfM-120k. 

## Verification

1. Extract the local descriptor of top-k using SIFT and try to match it using kd-tree
2. Remove outlier using RANSAC for matching results
3. Remove the class information (GID) of the most matched dataset
4. Check the results of 3 times manually with 3 inspectors

Additionally, we examined GLDv2-clean, Oxford5k, and Paris6k collected text queries.

Here, we removed all images contained in the relevant GID for one identical matched query (Hotel des Invalides Paris) regardless of the above steps.

## Cleaning Results
**Through the above two steps, a revised GLDv2-clean dataset, RGLDv2-clean, was generated!**

<p align="center">
  <img src="/images/table_01.png" width="460" alt="T1">
</p>

This table presents the statistical values of the filtered data.

In this table, ROxford and RParis have 36 and 38 overlapping landmarks out of 70, respectively which equates to a duplication rate of approximately 51% and 54%, respectively.

<p align="center">
  <img src="/images/table_02.png" width="460" alt="T2">
</p>

This table compares the statistical numbers for the existing clean datasets and the RGLDv2-clean.

Compared to GLDv2-clean, our dataset has reduced Image by 1,565 and Class by 17.

## Download `index` set
### Original: GLDv2(Google Landmark DataSets V2)
Original Google Landmark DataSets V2 details [here](https://github.com/cvdfoundation/google-landmark.git).

You can download images annotated with labels representing human-made and natural landmarks. 
    
### New: RGLDv2(Revisiting Google Landmark DataSets V2 Clean)
New cleared dataset index table released!
Our Revisiting Google Landmark DataSets V2 download [here](https://drive.google.com/file/d/1AV65-pbcG4EceBVw3dqcjQc5KSZK6kLI/view?usp=sharing). 

