# SGPT

- a large-scale generative pre-trained transformer model for search and embeddings
- It’s trained on a diverse set of data sources, including web pages, books, and scientific papers.
- Model training used both supervised & unsupervised learning.
    - Unsupervised learning → involves training SGPT on a large corpus of text data, allowing it to learn the underlying structure of the language and generate high-quality search results and embeddings
    - Supervised learning → involves fine-tuning SGPT on specific downstream tasks, such as question answering, sentiment analysis, and machine translation
- 2 Main components of SGPT: <br>
  ![Source: https://github.com/Muennighoff/sgpt/blob/main/other/sgpt_graphic.png](https://raw.githubusercontent.com/Muennighoff/sgpt/main/other/sgpt_graphic.png)
  *Source: https://github.com/Muennighoff/sgpt/blob/main/other/sgpt_graphic.png.*
    ## Cross Encoder
    
    - responsible for generating search results and embeddings for a given query
    - It does this by encoding the query and the documents in the corpus, and then calculating the similarity between the query and the documents.
    - It encodes query and document together at the same time.
    
    ## Bi-Encoder
    
    - responsible for generating embeddings for a given document.
    - It does this by encoding the document and then generating an embedding vector that represents the document's content.
    - It encodes query and document separately.
- Both are trained separately, but can be used together to generate high-quality search results & embeddings.

<aside>
💡 Cross-Encoders tend to outperform Bi-Encoders, but are slower as vectors cannot be cached and reused.

</aside>

## Symmetric Vs. Asymmetric Search

| Asymmetric Search | Symmetric Search |
| --- | --- |
| process of searching for relevant documents using a single encoder, either the Cross-encoder or the Bi-encoder | process of searching for relevant documents using both the Cross-encoder and the Bi-encoder |
| encoder is responsible for both encoding the query and the documents in the corpus | Cross-encoder is used to encode the query, while the Bi-encoder is used to encode the documents in the corpus |
| The encoder then generates a search result for each document in the corpus, based on the similarity between the query and the document. The search result is a ranked list of documents, with the most relevant document at the top of the list. | The encodings are then used to calculate the similarity between the query and the documents. The search result is a ranked list of documents, with the most relevant document at the top of the list. |
| faster and requires less computational resources | more accurate and can provide better search results |
| may not be as accurate as symmetric search | slower and requires more computational resources |

> SGPT-BE produces semantically meaningful sentence embeddings by contrastive fine-tuning of only bias tensors and position-weighted mean pooling.
> 
- Contrastive fine tuning is a training technique where the model learns by comparing similar & dissimilar sentences. It essentially refines the model’s ability to distinguish between sentences with close & distant meanings.
- Bias tensors are a type of parameter within the model that helps to learn the underlying data patterns. By fine-tuning only these, SGPT-BE achieves good results while modifying a minimal portion of the original GPT model.
- Position-weighted mean pooling refers to how SGPT-BE considers the importance of each word in the sentence when creating the embedding. It takes into account the fact that words at different positions might hold varying importance for understanding the meaning.

> SGPT-CE uses log probabilities from GPT models without any fine-tuning.
> 
- Log probabilities from GPT models is the approach that directly uses the probabilities assigned by a pre-trained GPT model to each word in a sentence instead of fine-tuning.  These probabilities represent how likely the model thinks each word is in that context, & they indirectly capture semantic meaning.
- Without any fine-tuning means that SGPT-CE leverages the existing knowledge of the pre-trained GPT model without any further training required, making it more faster & efficient than SGPT-BE.
