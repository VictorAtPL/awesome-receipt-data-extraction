# Mobile Scanner and OCR (A first step towards receipt to spreadsheet)

## Clement Ntwari Nshuti

[Browse](https://web.stanford.edu/class/ee368/Project_Spring_1415/Reports/Nshuti.pdf)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ✔️                   | ✔️                    | ❌                      | ❗                             | ❌                 |

#### Receipt localization

* > denoised using a gaussian blur
* > sharpened
* > a canny edge detector with [75, 200] as the thresholds
* > extract the largest quadrilateral by approximating all closed regions in the output of the edge detector by quadrilaterals and keeping the largest from these.

#### Receipt normalization

* > This quadrilateral is the extracted from the original (undenoised and unsharpened) image and warped into a straight rectangle.
* > binarized using adaptive threshold

#### Optical character recognition

- Tesseract

### Notes

* 7 conditions tested:
  * DARK.
    
    > The best conditions underwhich a picture can be taken is from the top with a dark background. This will be used as the baseline. Other configurations will be just a variation from this. We’ll either vary the background color, the camera orientation or the document quality.
  
  * BRIGHT.
    
    > Pictures of the document from the top with a bright background
  
  * NOISY
    
    > Pictures of the document with a background that has several small patterns.
  
  * SIDE
  
  * FRONT
  
  * FOLDED
  
  * CRINKLED
