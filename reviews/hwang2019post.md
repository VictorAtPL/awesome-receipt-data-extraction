# Post-OCR parsing: building simple and robust parser via BIO tagging

## Wonseok Hwang, Seonghyeon Kim, Minjoon Seo, Jinyeong Yim, Seunghyun Park, Sungrae Park, Junyeop Lee, Bado Lee, Hwalsuk Lee

[Browse](https://openreview.net/pdf?id=SJgjf695UB)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ❌                     | ❌                      | ❗                             | ✔️                |

#### Optical character recognition

* > in-house OCR system consisting of CRAFT text detector and Comb.best text recognizer

#### Semantic analysis

- Fields extracted (CORD-like annotations):
  - store information
  - menu:
    - name
    - unit price
    - total price
    - sub-menu
      - ...
  - payment information
- Serialization:
  - > uses lexical sort to rearrange the text segments according to their  coordinates from top to down and left to right direction using y axis as a primary order
  - > group the text segments placed on the same line in the image
- BIO Tagging:
  - > the text segments are tokenized and mapped to input vectors by adding token-, segment-, (sequential) position-, coordinate-, and line group-embeddings. The first three embeddings are prepared in identical way as BERT. The coordinate embedding represents the spatial information of visually embedded text segments. The line group
    > embedding is prepared by embedding line number found in the serialization process
- Parse generation:
  - > In receipt parsing task, there is an additional group tag (not to be confused with line group) to reflect the hierarchical structure of parses  for example fields such as name, count, and price are grouped together based on the item they represent).
- Refinements:
  - > various special symbols in cnt and price values, and (2) the thousands separator in price are refined to have unified representation
    
    
    

### Notes

* not much details - not sure how serialization works and how embeddings are calculated. Also it looks like it works on tokens, not characters
* ![](/Users/piotr-mac/repos/awesome-receipt-data-extraction/reviews/images/hwang2019post/scheme.png)


