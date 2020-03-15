# Automated Receipt Image Identification, Cropping, and Parsing

## Alex Yue

[Browse](https://www.cs.princeton.edu/courses/archive/spring18/cos598B/public/projects/System/COS598B_spr2018_ReceiptParsing.pdf)

```
@inproceedings{yue2018automated,
  title={Automated Receipt Image Identification, Cropping , and Parsing},
  author={Alex Yue},
  year={2018}
}
```



### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ✔️                   | ✔️                    | ❌                      | ❗                             | ✔️                |

#### Receipt localization

* > The input image is first downscaled to a fixed size and
  > transformed from the RGB color space to grayscale.

* > system uses multiple, independent edge detection implementations that are combined using a statistical, weighted voting average
  > 
  > * Line Segment Detector (LSD)
  
  > it is a line extraction algorithm that uses Gaussian pyramids that are down-sampled and blurred in order to identify line support regions.
  > 
  > * Probabilistic Hough Transform
  
  > A binary image input, usually of edges from detectors such as the Canny Edge Detector, is used for this probabilistic method where possible lines matching the binary input are generated through a stochastic voting process and the randomly generated lines that overlap sufficiently enough with the binary input are subsequently chosen.
  > 
  > * Holistically-Nested Edge Detection
  
  > The advantages of using the HED machine learning model primarily stems from the fact that the machine learning model was trained to discriminate against flagging edges within the background of a given image.

#### Receipt normalization

* Affine Transformation & Unwarping
  
  > Each line segment mask generated from the three independent edge detectors is combined into a single mask to determine the boundaries of the receipt image.
  
  > The lines are then segmented into vertical and horizontal lines using a k-means clustering algorithm that clusters based on the ρ value of polar coordinates. Intersections between vertical lines and horizontal lines are then determined after the clustering is complete. Nearby intersecting points are then merged
  
  > The combination of four points with the lowest box score is chosen as the edges of the receipt. These edges are then used to calculate an affine transformation matrix that will be used to crop the receipt image from its original form into an axis-aligned and in-plane image to be used for the optical character recognition system.

#### Optical character recognition

* > bilateral image filtering in order to remove noise from the image and image thresholding in order to quantize the image into a binarized version

* > median blur algorithm

* Tesseract

#### Semantic analysis

- Fields extracted:
  
  - date,
  - total price

- > Each individual box (from Tesseract) is then filtered to remove clearly incorrect recognitions and recognitions where the system is not confident in.

- > This receipt parsing pipeline then runs a new set of steps in order to regroup semantically and geographically similar groups of text into larger bounding boxes. Such methods are completed by probabilistically selecting pairs of text dependent on the distance of two text bounding boxes. Given two text bounding boxes, boxes are merged if they contain lexically similar content such as address information or numerical information.

- > To parse a given OCR output, words are first tokenized using natural language processing libraries and then keywords for each given category identified. Once each keyword is identified, I ran a spatial search for all given text inputs nearest to the text input containing the keyword for insightful information.
  
  > For example, for parsing pricing data, keywords such as ”price”, ”total”, and ”amount” are first identified from the OCR output.
  
  > Then, for each given positive keyword match, a nearest-neighbor search is conducted to look for text bound- ing boxes containing pricing information. I then select the keyword-price pair for the bounding boxes that are the furthest down on the page, which usually represents the total price for a given receipt image.

### Notes

* > Researchers and academics have mostly focused on developing techniques to improve the recognition and extraction of text from unstructured data whereas industry has focused on creating commercial systems to reduce manual labor costs associated with inputting receipt image data for analysis or reporting
