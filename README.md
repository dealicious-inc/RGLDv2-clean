# S2D2R : Single-Stage Pipeline for Detected-to-Retrieval using Revisiting Google Landmark DataSets V2



**NEW**: Explore the clean dataset index table
[here](https://googledrive/deali/gldv2_new_clean). #이거 우리가 공개하면 바꿔야함
The dataset was presented in our [CVPR'24 paper](아카이브주소).

This is the clean version of the Google Landmarks dataset (GLDv2), which contains images index.
The dataset can be used for landmark recognition and retrieval experiments. 

Original Google Landmark DataSets V2 details [here](https://github.com/cvdfoundation/google-landmark.git).
You can download images annotated with labels representing human-made and natural landmarks. 

## Download `index` set

There are 761,757 images in the `index` set.

### Download the list of images and metadata

**IMPORTANT**: Note that the integer landmark id's mentioned here are different
from the ones in the train set above.

-   `index_clean.csv`: single-column CSV with id field. `id` is a 16-character string.
    Available at:
    [`https://s3.amazonaws.com/deali-google-landmark/metadata/index_clean.csv).
