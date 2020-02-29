# A document detection technique using convolutional neural networks for optical character recognition systems

## Lorand Dobai, Mihai Teletin

[Browse](https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2019-17.pdf)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ✔️                   | ✔️                    | ❌                      | ❌                             | ❌                 |

#### Receipt localization

* > detect the key points of the document
* MobileNet backbone
* > Given x, the model computes the location of 4 points in the image domain representing the corners of the cash receipt.
* > the pairwise angles formed by the estimated points have to be as close as possible to the ground truth.
* > loss function which combines mean squared error and the angular error

#### Receipt normalization

* > skew correction (deskewing), the process of aligning the document in order to make the lines of text as horizontally straight as possible
* > OpenCV was used for the projective transformation

### Notes

* > jointly detect and deskew documents
