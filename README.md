## Convolutional Neural Networks for text Classification

### Requirements
Code is written in Python (2.7) and requires Theano (0.7).

Using the pre-trained `word2vec` vectors will also require downloading the binary file from
https://code.google.com/p/word2vec/


### Data Preprocessing
To process the raw data, run

```
python process_data.py path
```

where path points to the word2vec binary file (i.e. `GoogleNews-vectors-negative300.bin` file).
This will create a pickle object called `mr.p` in the same folder, which contains the dataset
in the right format.

Note: This will create the dataset with different fold-assignments than was used in the paper.
You should still be getting a CV score of >81% with CNN-nonstatic model, though.

### Running the models (CPU)
Example commands:

```
THEANO_FLAGS=mode=FAST_RUN,device=cpu,floatX=float32 python conv_net_sentence.py -nonstatic -rand
THEANO_FLAGS=mode=FAST_RUN,device=cpu,floatX=float32 python conv_net_sentence.py -static -word2vec
THEANO_FLAGS=mode=FAST_RUN,device=cpu,floatX=float32 python conv_net_sentence.py -nonstatic -word2vec
```

This will run the CNN-rand, CNN-static, and CNN-nonstatic models respectively in the paper.

### Using the GPU
GPU will result in a good 10x to 20x speed-up, so it is highly recommended.
To use the GPU, simply change `device=cpu` to `device=gpu` (or whichever gpu you are using).
For example:
```
THEANO_FLAGS=mode=FAST_RUN,device=gpu,floatX=float32 python conv_net_sentence.py -nonstatic -word2vec
```

### Example output
CPU output:
```
epoch: 1, training time: 219.72 secs, train perf: 81.79 %, val perf: 79.26 %
epoch: 2, training time: 219.55 secs, train perf: 82.64 %, val perf: 76.84 %
epoch: 3, training time: 219.54 secs, train perf: 92.06 %, val perf: 80.95 %
```
GPU output:
```
epoch: 1, training time: 16.49 secs, train perf: 81.80 %, val perf: 78.32 %
epoch: 2, training time: 16.12 secs, train perf: 82.53 %, val perf: 76.74 %
epoch: 3, training time: 16.16 secs, train perf: 91.87 %, val perf: 81.37 %
```

### Other Implementations
#### TensorFlow
[Denny Britz](http://www.wildml.com) has an implementation of the model in TensorFlow:

https://github.com/dennybritz/cnn-text-classification-tf

He also wrote a [nice tutorial](http://www.wildml.com/2015/12/implementing-a-cnn-for-text-classification-in-tensorflow) on it, as well as a general tutorial on [CNNs for NLP](http://www.wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp).

#### Torch
[HarvardNLP](http://harvardnlp.github.io/) group has an implementation in Torch.

https://github.com/harvardnlp/sent-conv-torch
