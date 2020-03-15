# Utilize OCR text to extract receipt data and classify receipts with common Machine Learning algorithms

## Joel Odd, Emil Theologou

[Browse](http://liu.diva-portal.org/smash/get/diva2:1215460/FULLTEXT01.pdf)

```latex
@phdthesis{odd2018utilize, title={Utilize OCR text to extract receipt data and classify receipts with common Machine Learning algorithms}, url={http://urn.kb.se/resolve?urn=urn:nbn:se:liu:diva-148350}, abstractNote={This study investigated if it was feasible to use machine learning tools on OCR extracted text data to classify receipts and extract specific data points. Two OCR tools were evaluated, the first was Azure Computer Vision API and the second was Google Drive REST Api, where Google Drive REST Api was the main OCR tool used in the project because of its impressive performance. The classification task mainly tried to predict which of five given categories the receipts belongs to, and also a more challenging task of predicting specific subcategories inside those five larger categories. The data points we where trying to extract was the date of purchase on the receipt and the total price of the transaction. The classification was mainly done with the help of scikit-learn, while the extraction of data points was achieved by a simple custom made N-gram model.The results were promising with about 94 % cross validation score for classifying receipts based on category with the help of a LinearSVC classifier. Our custom model was successful in 72 % of cases for the price data point while the results for extracting the date was less successful with an accuracy of 50 %, which we still consider very promising given the simplistic nature of the custom model.}, author={Odd, Joel and Theologou, Emil}, year={2018}}
```



### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ❌                     | ❌                      | ❗                             | ✔️                |

#### Optical character recognition

- Azure Computer Vision API and Google Drive REST Api tested.

#### Semantic analysis

- Fields extracted:
  - date
  - total price
- n-gram model used. They took tri-grams (A B C) and calculated co-occurence so they learn that B can  be total price, because it usually is between A and C. 
