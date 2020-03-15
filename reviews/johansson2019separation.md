# Separation and Extraction of Valuable Information From Digital Receipts Using Google Cloud Vision OCR

## Elias Johansson

[Browse](http://www.diva-portal.org/smash/get/diva2:1349283/FULLTEXT01.pdf)

```latex
@misc{johansson2019separation,
  title={Separation and extraction of valuable information from digital receipts using Google Cloud Vision OCR.},
  author={Johansson, Elias},
  year={2019}
}
```

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ✔️                    | ❌                      | ❗                             | ✔️                |

#### Receipt normalization

* resize
* grayscal or binarization

#### Optical character recognition

- Google Cloud Vision

#### Semantic analysis

- Fields extracted:
  
  - total cost,
  - vat rate
  - date

- > rely on manipulating strings and looking for substrings of text extracted by the OCR-engine

- > Three extraction methods have been developed in order to extract the valuable information and the corresponding values from the text. These work in a similar way: given a keyword the script will iterate over each word of the text until the keyword has been found; given that the OCR works as intended the values corresponding to the keyword will be found in close proximity to the keyword

- spellchecker
  
  > given a keyword the script will iterate over all the words within the text and look for words that are similar to the keyword. The similarity is calculated using a ratio of how similar the words are

### Notes

* no novelty

* problem formulation, motivation and outline are added as subsections

* receipts
  
  > not wrinkled nor damaged in order maintain the proper text alignment of the receipt. It is also important that the receipts do not contain any colour variation in form of stains which may reduce the contrast of the colours
  
  not
  
  > low-quality ink on a low-quality paper it may result in an illegible text

* 
