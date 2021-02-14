# [EC-GAN](https://ayaanzhaque.github.io/EC-GAN/)
This repository contains the implementation of the paper ["EC-GAN: Low-Sample Classification using Semi-Supervised Algorithms and GANs"](https://arxiv.org/abs/2012.15864) by Ayaan Haque. In [(AAAI)](https://aaai.org/Conferences/AAAI-21/), 2021.

Our proposed model combines a Generative Adversarial Network with a classifier to leverage artifical GAN generations to increase the size of restricted, fully-supervised datasets in a semi-supervised method.

For a more in-depth review, refer to this medium article (in Towards Data Science): https://towardsdatascience.com/artificial-data-for-image-classification-5b2ede40640f

## Abstract
Semi-supervised learning has been gaining attention as it allows for performing image analysis tasks such as classification with limited labeled data. Some popular algorithms using Generative Adversarial Networks (GANs) for semi-supervised classification share a single architecture for classification and discrimination. However, this may require a model to converge to a separate data distribution for each task, which may reduce overall performance. While progress in semi-supervised learning has been made, less addressed are small-scale, fully-supervised tasks where even unlabeled data is unavailable and unattainable. We therefore, propose a novel GAN model namely External Classifier GAN (EC-GAN), that utilizes GANs and semi-supervised algorithms to improve classification in fully-supervised regimes. Our method leverages a GAN to generate artificial data used to supplement supervised classification. More specifically, we attach an external classifier, hence the name EC-GAN, to the GAN's generator, as opposed to sharing an architecture with the discriminator. Our experiments demonstrate that EC-GAN's performance is comparable to the shared architecture method, far superior to the standard data augmentation and regularization-based approach, and effective on a small, realistic dataset.

## Model

![Figure](https://github.com/ayaanzhaque/EC-GAN/blob/main/images/EC-GAN.png?raw=true)

We propose an algorithm to improve classification utilizing GAN-generated images in restricted, fully-supervised regimes. Our approach consists of three separate models: a generator, a discriminator, and a classifier. At every training iteration, the generator is given random vectors and generates corresponding images. The discriminator is then updated to better distinguish between real and generated samples.

Simultaneously, a classifier is trained in standard fashion on available real data and their respective labels (note these datasets are fully labeled). We then use generated images as inputs for supplementing classification during training. This is the semi-supervised portion of our algorithm, as the generated images do not have associated labels. To create labels, we use a pseudo-labeling scheme which assumes a label based on the most likely class according to the current state of the classifier. The generated images and labels are only retained if the model predicts the class of the sample with high confidence, or a probability above a certain threshold. This loss is multiplied by a hyperparameter, which controls the relative importance of generated data compared to true samples. 

Note that this classifier is its own network, as opposed to a shared architecture with the discriminator. This is a key contribution of our paper, as most GAN-based classification methods employ a shared discriminator-classifier architecture. We aim to empirically show that an external classifier performs better than a shared architecture. 

## Results
A brief summary of the results are shown below. EC-GAN is compared to the shared architecture method on SVHN at different dataset sizes. The left value is the accuracy of a standard classifier (same architecture as GAN counterpart), followed by the accuracy of the GAN classification algorithm.

![Figure](https://github.com/ayaanzhaque/EC-GAN/blob/main/images/results.png?raw=true)

## Code
The code has been written in Python using the Pytorch framework. Training requries a GPU. We provide a Jupyter Notebook, which can be run in Google Colab, containing the algorithm in a usable version. Open [`EC-GAN.ipynb`](https://github.com/ayaanzhaque/EC-GAN/blob/main/EC-GAN.ipynb) and run it through. The notebook includes annotations to follow along.

## Citation

If you find this repo or the paper useful, please cite:

Ayaan Haque, "EC-GAN: Low-Sample Classification using Semi-Supervised Algorithms and GANs," 2020.

```
@misc{haque2020ecgan,
      title={EC-GAN: Low-Sample Classification using Semi-Supervised Algorithms and GANs}, 
      author={Ayaan Haque},
      year={2020},
      eprint={2012.15864},
      archivePrefix={arXiv},
      primaryClass={cs.LG}
}
```

