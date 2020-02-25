# A Novel Machine Learning Based Approach for Retrieving Information from Receipt Images

## Roland Szabo

[Browse](http://docplayer.net/35942009-A-novel-machine-learning-based-approach-for-retrieving-information-from-receipt-images.html)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ✔️                   | ❌                     | ✔️                     | ✔️                            | ❌                 |

#### Receipt localization

* > binarizing the images, using Otsu’s method

* > straighten the images - horizontal projection (summing the pixel values row-wise) is done for each resulting image. The straight image is assumed to be the one were are the most variations between the peaks and valleys of the histogram

* > removing the edges of the image, to keep only the receipt, removing any background
  
  > look at the horizontal and vertical projections and to remove the section from the top and bottom that is over a threshold

#### Text line segmentation

* > detecting the lines in the receipt - identify the peaks in the horizontal histogram in the image

#### Optical character recognition

- > The random forest was used as a model for the character segmentation problem.
- > The SVM was used for the character recognition problem.

### Notes

* > other papers for extracting information from receipts focus on improving either the image preprocessing step or on the parsing of text that was extracted using an off-the-shelf OCR engine
* > The bounding boxes of the characters were extracted from the images.
* > For the character segmentation problem, positive and negative patches were extracted from the images, each containing 40 columns of pixels.
* > For the character recognition problem, the labels corresponding to each character were converted to a vector of 74 dimensions,
* > For the character segmentation problem, it might help if the problem was
  > presented differently. Now, for each column the classifier has to make a decision if it is a space between letters or not. Other approaches would be to instead predict the length of the current letter or to move to make a more global decision, to determine the best way to segment a line in a way that maximizes an energy function.
