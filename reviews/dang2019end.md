# End-to-End Information Extraction by Character-Level Embedding and Multi-Stage Attentional U-Net

## Tuan Anh Nguyen Dang, Dat Nguyen Thanh

[Browse](https://bmvc2019.org/wp-content/uploads/papers/0870-paper.pdf)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ❌                     | ❌                      | ❌                             | ✔️                |

#### Semantic analysis

- Fields extracted:
  
  - Toyota invoices dataset:
    - date_issue,
    - sender_name,
    - receiver_name,
    - total_amount,
    - tax,
    - item_name,
    - item_amount,
    - ...
  - Daiichi medical receipts dataset:
    - date_issue,
    - billing_period,
    - insurance_amount,
    - patient_co-payment_ratio,
    - surgery_fee,
    - hospitalization_fee
    - ...

- > network performs pixel-level semantic segmentation task to label and extract the relevant information

- > multi-stage encoder-decoders - former encoder-decoder blocks focus on the textual components to identify the important elements (e.g. headers/keywords), and the later ones attempt to learn the spatial
  > relations between elements and propagate that information from the intermediate context to the target values.

- > Long-range dependencies and correlations between spatial positions on the document are captured by an additional self-attention mechanism  and the box convolution layer

- coupled U-Nets 
  
  > we are considered the problems of progressive information extraction (i.e. first the ‘key’ is segmented before the whole ‘key-value’ is segmented)
  
  > forcing the middle U-Net block to segment key and/or description while the final end outputs the full segmentation of all key/value collections.

- > the char-grid is chosen and tweaked over the hierarchical levels of subword, word or sentence level embedding

- > we incorporate the Box-Convolution layer in to a variant of ResBlock, which helps modeling long range vertical and horizontal interaction, making it a suitable alternative to conventional convolution blocks

- > expansion paths (also known as skip-connection) from the same level of downsampling blocks to upsampling blocks are added, with self-attention mechanism (non-local network) [31] (see Figure 3) to promote global information propagation between each encoder-decoder pair of an U-Net block

- Focal Loss

### Notes

* > end-to-end information extraction on the 2D character-grid embedding of the document
* > annotated manually - the location and content of text-boxes as well as the key information boxes that need to be extracted
