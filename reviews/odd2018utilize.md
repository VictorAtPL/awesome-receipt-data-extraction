# Utilize OCR text to extract receipt data and classify receipts with common Machine Learning algorithms

[Browse](http://liu.diva-portal.org/smash/get/diva2:1215460/FULLTEXT01.pdf)

### Pipeline

| Receipt preprocessing | Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
| :-------------------: | :---------------: | :------------------: | :-------------------: | :--------------------: | :---------------------------: | :---------------: |
|           ❌           |         ❌         |          ❌           |           ❌           |           ❌            |               ❗               |         ✔️         |

#### Optical character recognition

- Azure Computer Vision API and Google Drive REST Api tested.

#### Semantic analysis

- Fields extracted:
  - date
  - total price
- n-gram model used. They took tri-grams (A B C) and calculated co-occurence so they learn that B can  be total price, because it usually is between A and C. 