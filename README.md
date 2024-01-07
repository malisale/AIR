# AIR - Group Project


## Image Captioninng Using CNN and LSTM

In our first version we tried using the already provided example [Image Captioninng Using CNN and LSTM](https://www.kaggle.com/code/ghazouanihaythem/image-captioninng-using-cnn-and-lstm/notebook#Modelling) where we trained the model with [flickr8k](https://www.kaggle.com/datasets/adityajn105/flickr8k/data) 8000 images and then save the trained model on kaggle in 'keras' format.
The overall result was not good as we expected so we decided to use the pretrained model from huggingface.

## Image Generalizer
In the first version we loaded our trained model and use in with pretrained [gpt2-xl](https://huggingface.co/gpt2-xl) for our image generalization. Also, we have created our own queries.csv and for images we used 300 images from [flickr30k](https://www.kaggle.com/datasets/eeshawn/flickr30k) to test the image generalizer.
The end results were not that good so we again used other version.

## Final Version
In the final version for the image captioning model we used trained [nlpconnect/vit-gpt2-image-captioning](https://huggingface.co/nlpconnect/vit-gpt2-image-captioning) pytorch version.

For Image (Captions) Generalizer we used the [```>>> from nltk.corpus import wordnet```](https://www.nltk.org/howto/wordnet.html)
