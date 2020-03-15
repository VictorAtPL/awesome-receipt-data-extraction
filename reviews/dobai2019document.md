# A document detection technique using convolutional neural networks for optical character recognition systems

## Lorand Dobai, Mihai Teletin

[Browse](https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2019-17.pdf)

```latex
@article{dobai2019document,
   title={A document detection technique using convolutional neural networks for optical character recognition systems},
   ISBN={9782875870650},
   journal={ESANN 2019 proceedings, European Symposium on Artificial Neural Networks, Computational Intelligence
and Machine Learning},
   author={Dobai, Lorand and Teletin, Mihai},
   year={2019},
   pages={547-552}
}
```

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
