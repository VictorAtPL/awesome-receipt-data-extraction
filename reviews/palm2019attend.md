# Attend, Copy, Parse - End-to-end information extraction from documents

## Rasmus Berg Palm, Florian Laws, Ole Winther

[Browse](https://arxiv.org/pdf/1812.07248.pdf)

```latex
@article{palm2019attend,
  title={Attend, Copy, Parse End-to-end Information Extraction from Documents},
  author={Palm, Rasmus Berg and Laws, Florian and Winther, Ole},
  journal={2019 International Conference on Document Analysis and Recognition (ICDAR)},
  year={2018},
  pages={329-336}
}
```



### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ❌                     | ❌                      | ❌                             | ✔️                |

#### Semantic analysis

- Fields extracted:
  - the invoice number,
  - the order number,
  - the date,
  - the total,
  - the sub total before tax,
  - the tax total
  - the tax percent
- > The proposed architecture takes the spatial structure into account by using convolutional operations on the concatenated document text and image modalities.
- > We assume the text of the document is given or extracted using an Optical Character Recognition (OCR) engine.
- > The main idea is to build an external memory bank the same size as the document image, containing the words encoded as a sequence of characters at the memory positions corresponding to the positions of the words in the image. The attend module attends to this memory bank and the copy module copies out the attended string. The parse module parses the attended string into the desired output format, optionally given a context vector computed from the inputs.
- > we train separate models for each of the K fields
- Components:
  - External memory - contains n-grams assigned to "slots"
  - Attend - attention vector obtained from features which were processed with dilatated blocks
  - Copy - weighted sum (using attend and memory)
  - Context - weighted sum (attention and last dilatated block in attend module)
  - Parse - char-based seq2seq:
    - no-op
    - optional
    - date-parser - cnns + MLP for 10 chars
    - amount parser - pointer-generator network

### Notes

* Very technical, a great explanation of steps in each component
* > the Attend, Copy, Parse architecture, a deep neural network model that can be trained directly on end-to-end data, bypassing the need for word-level labels
* > The distinction between end-to-end data and data labeled on the word level is subtle but important. In the invoice example the end-to-end data simply tells us what the total is, whereas data labeled on the word level tells us where it is.
* > 37% of the invoices are scanned document images, the rest are digital PDF files
* > it is not known which words in the document corresponds to the fields we wish to extract, we simply know the target value of each field
* > The presented architecture can only extract non-recurring fields as opposed to recurring, structured fields such as invoice lines. Theoretically it should be possible to output the lines by recurrently outputting the fields of a single line at a time, and then conditioning the attention module on the previously
  > outputted line.
