# DaST: Data-free Substitute Training for Adversarial Attacks
**An adversarial data-free substitute training method for adversarial attacks.
This work has been accepted by CVPR2020 as Oral presentation.**

***Abstract***: Machine learning models are vulnerable to adversarial examples. For the black-box setting, current substitute attacks need pre-trained models to generate adversarial examples. However, pre-trained models are hard to obtain in real-world tasks. In this paper, we propose a data-free substitute training method (DaST) to obtain substitute models for adversarial black-box attacks without the requirement of any real data. To achieve this, DaST utilizes specially designed generative adversarial networks (GANs) to train the substitute models. In particular, we design a multi-branch architecture and label-control loss for the generative model to deal with the uneven distribution of synthetic samples. The substitute model is then trained by the synthetic samples generated by the generative model, which are labeled by the attacked model subsequently. The experiments demonstrate the substitute models produced by DaST can achieve competitive performance compared with the baseline models which are trained by the same train set with attacked models. Additionally, to evaluate the practicability of the proposed method on the real-world task, we attack an online machine learning model on the Microsoft Azure platform. The remote model misclassifies 98.35% of the adversarial examples crafted by our method. To the best of our knowledge, we are the first to train a substitute model for adversarial attacks without any real data.

*Link: https://openaccess.thecvf.com/content_CVPR_2020/html/Zhou_DaST_Data-Free_Substitute_Training_for_Adversarial_Attacks_CVPR_2020_paper.html*

This project built on Pytorch 1.0+.

# Usage:

**Environment:**

`Pytorch 1.0+`\
`Python 3.6`

This work can steal the attacked model without the requirement of any real data. If you want to evaluate the performance of DaST in terms of adversarial attacks, you can use the `evaluate.py` to do it.

**Experiments of original paper:**

1. Train the substitute model.

If you want to train a substitute model in MNIST:

```python
python dast.py --dataset=mnist
```

If you want to train a subsitute model in Azure:
```python
python dast.py --dataset=azure
```

2. Generate the adversarial attacks by white-box attacks and transfer them to the attacked model.

When the substitute model is obtained, you can use the following command to evaluate the substitute model in non-targeted attacks:
```python
python evaluation.py --mode=dast --adv=FGSM --cuda
```


#Notes

(1) I have downloaded the remote model, so you do not need to employ the azure model as a service to evaluate the method.

(2) The attack success rate in the training code is just a rough estimate of attack performance, but it is fast. So you could run the evaluate.py to evaluate the performance of trained model.

(3) If you want to train a substitute model in other dataset (like CIFAR-10), you can add a CIFAR-10's model as the original_net and load the dataset. Note that in this code the output size of generator is [28, 28]. So on the CIFAR-10 dataset, the architecher of generator need to be modified, and the output size need to be [32, 32].

(4) There are some important arguments in this code. The `alpha` controls the weight of label-control loss in (9) of the original paper. The 'beta' determines the attack scenario. If the 'beta' is 0, the attack scenario is DaST-L, if the 'beta' is not 0 (>0), the attack scenario is DaST-P. I define two types of generator architecture, you can switch by 'G_type'. It is hard to say which type is better, you can try to use them in your own dataset. Because of the multi-branch architecture of the generator, the 'batchsize' is best divisible by the number of categories.

# Citation:
If you feel this work is helpful, please cite us:
```latex
@inproceedings{zhou2020dast,
  title={DaST: Data-free Substitute Training for Adversarial Attacks},
  author={Zhou, Mingyi and Wu, Jing and Liu, Yipeng and Liu, Shuaicheng and Zhu, Ce},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  pages={234--243},
  year={2020}
}
```

# Contact:
If you have any question, please contact [Mingyi Zhou](mingyi.zhou@monash.edu).
