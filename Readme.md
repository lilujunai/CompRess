

# CompReSS: Compressing Representations for Self-Supervised Learning

This repository is the official implementation of [CompReSS: Compressing Representations for Self-Supervised Learning
](https://arxiv.org/). 

[comment]: <> (📋Optional: include a graphic explaining your approach/main result, bibtex entry, link to demos, blog posts and tutorials)

## Requirements

To install requirements:

FAISS: 
```setup
# CPU version only
conda install faiss-cpu -c pytorch

# GPU version
conda install faiss-gpu cudatoolkit=10.0 -c pytorch # For CUDA10
```

PyTorch:
```setup
conda install pytorch torchvision cudatoolkit=10.1 -c pytorch
```


[comment]: <>  (📋Describe how to set up the environment, e.g. pip/conda/docker commands, download datasets, etc...)

## Training

To train the student(s) using cached teachers in the paper, run this command:

```train
python train_student_moco.py \
    --teacher_model cached \ 
    --teacher <path_to_cached_features> \
    --student_model alexnet \
    --checkpoint_path <path_to_checkpoint_folder> \
    --data <path_to_imagenet_data>

```


To train the student(s) using pretrained teachers in the paper, run this command:

```train
python train_student_moco.py \
    --teacher_model resnet50 \ 
    --teacher <path_to_pretrained_model> \
    --student_model mobilenet \
    --checkpoint_path <path_to_checkpoint_folder> \
    --data <path_to_imagenet_data>
```


To train the student(s) without Moco framework execute train_student.py instead of train_student_moco.py

[comment]: <> (📋Describe how to train the models, with example commands on how to train the models in your paper, including the full training procedure and appropriate hyperparameters.)
## Evaluation

To evaluate NN models on ImageNet, run:

```eval
python eval_knn.py \
    -a alexnet \
    --weights <path_to_pretrained_model> \
    --save <path_to_save_folder> \
    <path_to_imagenet_data>
```


To evaluate Linear Classifier models on ImageNet, run:

```eval
python save_var_mean.py --x_root <NN_evaluation_save_folder>

python eval_multiple_linear.py \
    --arch alexnet \
    --weights <path_to_pretrained_model> \
    --mean_paths <NN_evaluation_save_folder>/var_mean.pth.tar \
    --save <path_to_save_folder> \
    <path_to_imagenet_data>
```

To evaluate cluster alignment models on ImageNet, run:

```eval
python eval_cluster_alignment.py  \
    --batch-size 256 \ 
    --weights <path_to_pretrained_model> \
    --model resnet18  \
    --save <path_to_save_folder> \
    <path_to_imagenet_data> \ 
    --visualization \ 
    --confusion_matrix
```




## Pre-trained Models

Due to the size limitation we cannot include pre-trained models in supplementary materials. We will add them in the final code release.  





## Results

Our model achieves the following performance :


| Model name         | Top 1 Linear Classifier Accuracy | Top 1 NN Accuracy |
| ------------------ |----------------------------------| ----------------- |
| CompReSS(Resnet50) |               71.6%              |        63.4%        |
| CompReSS(Mobilenet)|               63.0%              |        54.4%        |
| CompReSS(Resnet18) |               61.7%              |        53.4%        |
| CompReSS(Alexnet)  |               57.6%              |        52.3%        |

