# Structure-emphasized Multimodal Style Transfer
Pytorch(1.0+) implementation of My master paper ["Structure-emphasized Multimodal Style Transfer"](https://drive.google.com/open?id=1TbbuokSGiPBaHcCwlxA7dHIfNKcTDZ9N).

We proposed 2 models, called SEMST_Original and SEMST_Auto in this work. More details can be founed in the paper.

This repository provides  pre-trained models for you to generate your own image given content image and style image. Also, you can download the training dataset or prepare your own dataset to train the model from scratch.

If you have any question, please feel free to contact me. (Language in English/Japanese/Chinese will be ok!)

---

## Requirements

- Python 3.7+
- PyTorch 1.0+
- TorchVision
- Pillow

Anaconda environment recommended here!

(optional)

- GPU environment 

---
---

## Notice: The train and test procedures as follow are the same for SEMST_Original and SEMST_Auto.
---
---

## Test
1. Clone this repository 

   ```bash
   git clone https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer
   cd Structure-emphasized-Multimodal-Style-Transfer
   cd SEMST_XXX(XXX means Original or Auto)
   ```

2. Prepare your content image and style image. I provide some in the `content` and `style` and you can try to use them easily.

3. Download the pretrained model [SEMST_Original](https://drive.google.com/file/d/1G9S9nxaMa9N9QJwPfwfP9iZ6LMFYWrln/view?usp=sharing), [SEMST_Auto](https://drive.google.com/file/d/151Fo-O-ImtKNrr5n82oUbRH5ajAlpit9/view?usp=sharing) and put them under the SEMST_XXX respectively.

4. Generate the output image. A transferred output image w/&w/o style image and a NST_demo_like image will be generated.

   ```python
   python test.py -c content_image_path -s style_image_path
   ```

  ```
  usage: test.py [-h] [--content CONTENT] [--style STYLE]
                [--output_name OUTPUT_NAME] [--alpha ALPHA] [--gpu GPU]
                [--model_state_path MODEL_STATE_PATH]

   ```

   If output_name is not given, it will use the combination of content image name and style image name.


------

## Train

1. Download [COCO](http://cocodataset.org/#download) (as content dataset)and [Wikiart](https://www.kaggle.com/c/painter-by-numbers) (as style dataset) and unzip them, rename them as `content` and `style`  respectively (recommended).

2. Modify the argument in the` train.py` such as the path of directory, epoch, learning_rate or you can add your own training code.

3. Train the model using gpu.

4. ```python
   python train.py
   ```

   ```
   usage: train.py [-h] [--batch_size BATCH_SIZE] [--epoch EPOCH] [--gpu GPU]
                [--learning_rate LEARNING_RATE]
                [--snapshot_interval SNAPSHOT_INTERVAL] [--alpha ALPHA]
                [--gamma GAMMA] [--train_content_dir TRAIN_CONTENT_DIR]
                [--train_style_dir TRAIN_STYLE_DIR]
                [--test_content_dir TEST_CONTENT_DIR]
                [--test_style_dir TEST_STYLE_DIR] [--save_dir SAVE_DIR]
                [--reuse REUSE]
   ```



# Result

Some results of content image will be shown here.

![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_1.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_2.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_3.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_4.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_5.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_6.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_7.png)
![image](https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer/blob/master/result/5_8.png)

---
If you find this work useful for you, please cite it as follow in your paper. Thanks a lot.

```
@misc{Chen2020,
  author = {Chen Chen},
  title = {Structure-emphasized Multimodal Style Transfer},
  year = {2020},
  month = 2,
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/irasin/Structure-emphasized-Multimodal-Style-Transfer}},
}
```
---
## Abstract
Neural style transfer refers to a class of algorithms that render an image with characteristics of the style image while maintaining the arrangement of the content image.
Inspired by the power of convolutional neural networks(CNNs) for image recognition, Gatys et al.(2016) first studied how to use VGGNet to extract the content representation and the style representation and proposed an image-optimization-based method. Since then, neural style transfer has received increasing attention from both computer vision researchers and industries.

Recently, significant effort has been devoted to ASPM(Arbitrary Style Per Model), which aims at transferring an arbitrary style from only one single model, especially the gram-matrix-matching-based methods. However, most of them have an assumption that image styles should be represented as a unimodal distribution so that style transfer can be formulated as the matching of the global statistic of gram matrix or covariance matrix. Zhang et al.(2019) first introduced a multimodal style transfer method called MST which uses K-means to split style patterns from style image and combinate them with content image via graph-cut. However, due to the high-dimensional and low-resolution characteristics of the feature space and the characteristics of the graph cut method, there are problems such as the inability to consider the structural information of the content image, and this may produce undesirable results.

In this work, we analyze the shortcomings of MST and propose a structure-emphasized multimodal style transfer(SEMST). Specifically, instead of using VGGNet's high-dimensional feature space, we extract structural information from CIELAB color space via a K-means-based clustering algorithm which automatically determines the optimal number of clusters based on the area of clusters. Next, we design an approach that can flexibly match the content cluster and the style cluster even if the number of clusters differs, by using automatic matching based on the cluster center norm or manual matching defined according to user 's demand and preferences. Finally, WCT is performed between the corresponding clusters, and the target image is generated by the decoder.

In experiments, it was confirmed that the proposed method can generate more beautiful and natural images by explicit structure extraction and matching. Since the proposed method can render images in less than one second and can change various hyperparameters, it is considered to be a fairly fast and highly flexible method.
