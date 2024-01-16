# AIR - Group Project

## Idea
The plan was to create an automated pipeline that can process a folder full of pictures and make them searchable. Since automated image captioning is still not perfect or at least good enough to make this viable for all pictures, we wanted to try and expand the results of the search by altering and generalizing the generated captions. Usually in IR it is the query that gets modified to improve the results but we wanted to see if expanding the photo captions would work.

## Image Captioninng
In our first version we tried using the already provided example [Image Captioninng Using CNN and LSTM](https://www.kaggle.com/code/ghazouanihaythem/image-captioninng-using-cnn-and-lstm/notebook#Modelling) where we trained the model with [flickr8k](https://www.kaggle.com/datasets/adityajn105/flickr8k/data) 8000 images and then save the trained model on kaggle in 'keras' format.
The overall result was not as good as we expected so we decided to use the pretrained model from [huggingface](https://huggingface.co/nlpconnect/vit-gpt2-image-captioning).

## Caption Generalizer
In the first version we loaded our trained model and use in with pretrained [gpt2-xl](https://huggingface.co/gpt2-xl) for our image caption generalization. This sadly did not perform well because the model was not sophisticated enough. At first we tried promts like:" please generalize the words in the following sentence: ..." but it would just generate loosely related sentences. We then started removing stopwords and just promted "Generalize: ..." for every single word that was left but this was also met with little success.
We also tested the smaller version [gpt2-large](https://huggingface.co/openai-community/gpt2-large) but this performed even poorer and was scrapped immediately.
In the end we settled on using a the synonym function from the nltk corpus wordnet to just generate synonyms for each word in the query after removing stoppwords.

## Searching
We implemented a simple binary search as we wanted to make sure that the differences in results stem from the generalization of the captions and not the performance of the fuzzy search or similar that we implemented.

## Final Version
In the final version for the image captioning model we used trained [nlpconnect/vit-gpt2-image-captioning](https://huggingface.co/nlpconnect/vit-gpt2-image-captioning) pytorch version.

For Image (Captions) Generalizer we used the [```>>> from nltk.corpus import wordnet```](https://www.nltk.org/howto/wordnet.html)

## Testing
We picked out 300 images from [flickr30k](https://www.kaggle.com/datasets/eeshawn/flickr30k) more or less randomly and then wrote queries that we thought should yield some results on that image corpus. We wrote ten short, one-word queries, ten medium length queries, and ten long queries that asked for relationships between objects. In order to have a ground truth to compare against we manually selected all pictures that we thought applied to the queries out of our 300 and noted them down in the ground_truths.csv file.

## Results and Conclusion
The results for the short queries where somewhat promising as we did get more correct results and only a little more false positives. However with the medium and long queries the amount of false positives far outstripped the amount of extra true positives and the overall results were negligible at best. 
We think that this is for two resons: Firstly synonyms are not often more generalized that the word they stem from and thus don't make the captions easier to find in a search. 
Secondly the results are still greatly depentend on the performance of the image captioning model used. When the initial caption that we generalize for an image is wildly wrong, there is no way that our pipeline can improve the performance of the search.

We encourage everyone to download the pipeline and try it with their own pictures. It does not take long and under the "Searching" section there is a testing code field in which you can try out the search on your own images.