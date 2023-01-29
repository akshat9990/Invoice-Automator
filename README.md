# Invoice Automator

The current process of claiming health insurance through reimbursement can be time-consuming for both
patients and claim agents. The process involves submitting invoices and bills from the hospital to the insurance
company, which are then reviewed and approved or rejected by claim agents. The manual process of viewing
and entering information on these bills can lead to inefficiencies and the potential for errors. To address this
issue, there is a need for a more efficient method of capturing this information in a structured manner. This
would enable the extraction of provider and treatment information for analysis purposes, as well as the detection
of potential fraud.

My solution for this problem can be generalized into two parts:
- OCR of the input invoice image to extract the whole text
- Using a custom NER tool to extract information from that raw text



## Tech Stack Used

- Python
- PaddleOCR
- Spacy
- Dataframes
- NLP Tools
## Dataset

The dataset that we are working with is composed of 1000 scanned receipts, each of which contains several key text fields such as the name of the goods, the unit price, and the total cost. These text fields are annotated with text bounding boxes and the transcript of each box, and the locations are marked as rectangles with four vertices arranged in a clockwise order starting from the top. The annotations for each image are stored in a separate text file with the same file name as the image. In addition to this, the information extraction dataset comprises of extracted entities such as company names, addresses, and phone numbers, which have been meticulously collected and stored in a separate text file for easy access by our NLP model. The text annotated in the dataset mainly consists of digits and English characters, making it an ideal use case for the OCR task. The dataset link is below. <br>
 [Dataset Link](https://drive.google.com/drive/folders/1Jl50NDOyIU4da5krdgpU2g00GlLDn66B?usp=share_link)


## OCR of the Invoice Image

The first part of our problem is to extract the raw text from the invoice image. The steps involved in this process is:   
- Import the required dependencies (PaddleOCR and draw_ocr).

- Initialize an instance of the PaddleOCR class.

- Define a helper function "save_ocr" to plot the recognition results onto the input image and save it.

- Perform the OCR on the input image.

- Save the raw text in a text file


## Information Extraction from raw text

- Custom Natural Language Understanding (NLU) model was trained using SpaCy's named entity recognition (NER) component for text generated from receipts

- SpaCy is a well-known NLU package that uses a combination of residual CNNs, incremental parsing, and Bloom embeddings for NER

- Model predicts entity tags by applying 1D convolutional filters to input text

- Input sequence is embedded with Bloom embeddings capturing characters, prefix, suffix, and part of speech of each word

- Residual blocks and beam search used to choose filter sizes in the CNNs

- Simple memory tagger implemented to identify proper nouns such as company names and addresses in the test strings

- Tagger searches through a dictionary of company names and addresses if NER model fails to identify the entity.


## Model Output
Evaluation metric used to measure the model performance is **F1 score**.<br>
F1 score of the above mentioned Custom NER model on the test data set is **0.78** or **78%**.


## Sample Input Image

![X510056849111](https://user-images.githubusercontent.com/71962566/215330639-0ea82f10-3d14-4076-98ee-9e0ad124c959.jpg)

## Sample Output (Information Extracted)
![image](https://user-images.githubusercontent.com/71962566/215330685-bf82c42a-4735-4acb-94f0-32335172009c.png)


## Output Files 
The output of the Test Dataset is in the output folder above

## References

- https://spacy.io/usage/linguistic-features#named-entities
- https://spacy.io/usage/training
- https://aihub.cloud.google.com/u/0/p/products%2F2290fc65-0041-4c87-a898-0289f59aa8ba
- https://github.com/PaddlePaddle/PaddleOCR
- https://github.com/PaddlePaddle
- https://medium.com/mysuperai/what-is-named-entity-recognition-ner-and-how-can-i-use-it-2b68cf6f545d
- https://turbolab.in/build-a-custom-ner-model-using-spacy-3-0/
- https://www.youtube.com/playlist?list=PL2VXyKi-KpYvuOdPwXR-FZfmZ0hjoNSUo
- https://learnopencv.com/optical-character-recognition-using-paddleocr/

