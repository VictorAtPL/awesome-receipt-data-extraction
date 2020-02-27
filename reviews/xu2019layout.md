# LayoutLM: Pre-training of Text and Layout for Document Image Understanding

## Yiheng Xu, Minghao Li, Lei Cui, Shaohan Huang, Furu Wei, Ming Zhou

[Browse](https://arxiv.org/pdf/1912.13318v3)

### Pipeline

| Receipt detection | Receipt localization | Receipt normalization | Text line segmentation | Optical character recognition | Semantic analysis |
|:-----------------:|:--------------------:|:---------------------:|:----------------------:|:-----------------------------:|:-----------------:|
| ❌                 | ❌                    | ❌                     | ❌                      | ❌                             | ✔️                |

#### Semantic analysis

- Fields extracted:
  - FUNSD:
    
    > 9,707 semantic entities and 31,485 words. These forms are organized as a list of semantic entities that are interlinked. Each semantic entity comprises a unique identifier, a label (i.e., question, answer, header or other), a bounding box, a list of links with other entities, and a list of words
  - SROIE:
    - company,
    - date,
    - address,
    - total
- based on BERT model
  
  > attention-based bidirectional language modeling
  
  > tokens processed using WordPiece, the input embeddings are computed by summing the corresponding word embeddings, position embeddings, and segment embedding
- > When it comes to visually
  > rich documents, there is much more information that can be encoded into the pre-trained model
  - Document Layout Information
    
    > relative positions of words in a document contribute a lot to the semantic representation
  - Visual Information
- > add two types of new input embeddings: a 2-D position embedding and an image embedding
  - 2-D Position Embedding
  - Image Embedding
    
    > the bounding box of each word from OCR results, we split the image into several pieces, and they have a one-to-one correspondence with the words. We generate the image region features with these pieces of images from the Faster R-CNN (Ren et al., 2015) model as the token image embeddings
    
    > ResNet-101 model as the backbone network in the Faster R-CNN model, which is pre-trained on the Visual Genome dataset
- Pretraining on two tasks:
  - Masked Visual-Language Model
    
    > randomly mask some of the input tokens but keep the 2-D position embeddings and other text embeddings, then the model is trained to predict the masked tokens given the contexts
  - Multi-label Document Classification
- Fine-tuning
  
  > For the form and receipt understanding tasks, LayoutLM predicts {B, I, E, S, O} tags for each token and uses sequential labeling to detect each type of entity in the dataset

### Notes

* ![](/Users/piotr-mac/repos/awesome-receipt-data-extraction/reviews/images/xu2019layout/architecture.png)
* > LayoutLM to jointly model the interaction between text and layout information across scanned document images
* > pre-training method of text and layout for document image understanding tasks
* Limitation of other methods:
  * > They only relied on a few human-labeled training samples, yet did not fully explore the possibility of using large-scale unlabeled training samples
  * > They usually leveraged either pre-trained CV models or NLP models, but did not consider a joint training of textual and layout information
* > 8 NVIDIA Tesla V100 32GB GPUs with a total batch size of 80
* > 80 hours to finish one epoch on 11M documents
* SOTA on SROIE dataset
