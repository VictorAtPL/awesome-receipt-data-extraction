# Optical Character Recognition on supermarket receipts

## Marco Ziegaus

[Browse](https://www.fim.uni-passau.de/fileadmin/dokumente/fakultaeten/fim/lehrstuhl/sauer/geyer/BA_MA_Arbeiten/BA-ZiegausMarco-201607.pdf)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ✔️                    | ✔️                     | ❗                             | ✔️                |

#### Receipt normalization

* Binarisation:
  * hardcoded threshold
  * Otsu's method

#### Text line segmentation

* A couple of strategies tested:
  
  * White row strategy
  
  * Relative pixel count strategy
  
  * Median pixel count strategy
  
  * Pixel count gain strategy
    
    > it first calculates the number of black pixels for each row and detects rising and falling edges.

#### Optical character recognition

- Character segmentation with monospace strategy
- Recognizing every character one by one:
  - centering of the character in the image
  - generation of templates (how different characters looks - mean)
  - template matching
  - reliability prediction
- Simple autocorrection - correcting errors with regexps; ideas: keyword dictionary, products database, plausibility validation

#### Semantic analysis

- Fields extracted:
  - total price
  - cash given
  - cash drawback
  - list of items:
    - product name
    - quantity
    - price per piece
    - total price for product
  - date
  - time
  - store tax id
- keyword based (levensthein distance) and regular expression based data extraction

### Notes

* > receipt images from a single store with cash payments are used
* > consistent font and layout structure
* Cannot be generalized easily to other stores and templates.
