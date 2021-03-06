Orthogonal Weight Normalization
======================================

This project is the Torch implementation of the paper : Orthogonal Weight Normalization: Solution to Optimization over Multiple Dependent Stiefel Manifolds in Deep Neural Networks (arXiv:1709.06079 )
* bibtex:
```Bash
@article{Huang_2017_arxiv,
    author = {Lei Huang and Xianglong Liu and  Bo Lang and Adams Wei Yu and Bo Li},
    title = {Orthogonal Weight Normalization: Solution to Optimization over Multiple Dependent Stiefel Manifolds in Deep Neural Networks},
   journal   = {CoRR},
  volume    = {abs/1709.06079},
  year      = {2017}}
 ```
 
 ### Updates
* Add the [' pytorch module'](./module_pytorch/OWN.py)  of OWN.     2019-11-23.



 
 
## Requirements and Dependency
* Install [Torch](http://torch.ch) with CUDA GPU
* Install [cudnn v5](http://torch.ch)
* Install dependent lua packages optnet by run:
luarocks install optnet
* Install Magma (you can follow the instruction in the file  ['Install Magma.txt'](./Install_Magga.txt) )
	Note: Magma is used for the SVD on GPU. If you don't install Magma, you can not run the code on GPU (For all the experiment on CNNs, we run the experiment on GPU)

## Experiments in the paper

#### 1.  Reproduce the results for sovling OMSDM problem:

*	Run script:
```Bash
 bash 0_execute_MLP_MNIST_b1024.sh
 ```
This script will download MNIST dataset automatically and you should put the 'mnist.t7'(directory) to the './dataset/' directory. 
You can try more small learning rate, and add more layer, or use different batch size based on this script.
	
#### 2. Reproduce the results on MLP architecture:
* Dataset preparations: you should download the [PIE dataset](https://www.dropbox.com/sh/5pkrtv02wemqxzp/AADlVOs3vDMOEsOpRFa20Uqha?dl=0), and put the data file in the directory: './dataset/' (The final paths of the data files are:'./dataset/PIE/PIE_train.dat' and './dataset/PIE/PIE_test.dat')

* Execute:
```Bash
  bash 1_execute_MLP_PIE_sgd.sh   
  bash 1_execute_MLP_PIE_adam.sh
 ```
-----------------------------Note that the experiment above is under MLP and run on CPU, and therefore it is not necessary to install Magma for above experiemnt --------------------
 
#### 3. Reproduce the results on VGG style, BN-Incption and Wide residual network over CIFAR datset: 

 *	Dataset preparations: you should download the [CIFAR-10](https://yadi.sk/d/eFmOduZyxaBrT) and [CIFAR-100](https://yadi.sk/d/ZbiXAegjxaBcM) datasets, and put the data file in the directory: './dataset/' 
 

  *	To reproduce the experimental results, you can run the script below, which include all the information of experimental configurations: 
```Bash
  bash 2_execute_Conv_CIFAR_VggStyle.sh  
  bash 3_execute_Conv_CIFAR_BNInception.sh 
  bash 4_execute_Conv_CIFAR_wr.sh  
 ```
 The Inception model is based on the project on: https://github.com/soumith/imagenet-multiGPU.torch.

The wide residual network model is based on the facebook torch project: https://github.com/szagoruyko/wide-residual-networks


#### 4. Run the experiment on imageNet dataset. 

 *  (1) You should clone the facebook residual network project from:https://github.com/facebook/fb.resnet.torch
 *  (2) You should download imageNet dataset and put it on: '/tmp/dataset/imageNet/' directory (you also can change the path, which is set in 'opts_imageNet.lua')
 *  (3) Copy  'opts_imageNet.lua', 'exp_Conv_imageNet_expDecay.lua', 'train_expDecay.lua', 'module' and 'models' to the project's root path.
 *  (4)	Execute: 
```Bash
th exp_Conv_imageNet_expDecay.lua -model imagenet/resnet_OLM_L1
 ```
You can training other respective models by using the parameter '-model'

## Contact
huanglei@nlsde.buaa.edu.cn, Any discussions and suggestions are welcome!

