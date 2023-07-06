# StyleAvatar

[Lizhen Wang](https://lizhenwangt.github.io/), Xiaochen Zhao, [Jingxiang Sun](https://mrtornado24.github.io/), Yuxiang Zhang, [Hongwen Zhang](https://hongwenzhang.github.io/), [Tao Yu](https://ytrock.com/), [Yebin Liu](http://www.liuyebin.com/)

ACM SIGGRAPH 2023 Conference Proceedings

Tsinghua University & NNKOSMOS

[[Arxiv]](https://arxiv.org/abs/2305.00942) [[Paper]](https://www.liuyebin.com/styleavatar/assets/StyleAvatar.pdf) [[Project Page]](https://www.liuyebin.com/styleavatar/styleavatar.html) [[Demo Video]](https://www.liuyebin.com/styleavatar/assets/Styleavatar.mp4)

<div align=center><img src="./docs/teaser.jpg"></div>

### Abstract

>Face reenactment methods attempt to restore and re-animate portrait videos as realistically as possible. Existing methods face a dilemma in quality versus controllability: 2D GAN-based methods achieve higher image quality but suffer in fine-grained control of facial attributes compared with 3D counterparts. In this work, we propose StyleAvatar, a real-time photo-realistic portrait avatar reconstruction method using StyleGAN-based networks, which can generate high-fidelity portrait avatars with faithful expression control. We expand the capabilities of StyleGAN by introducing a compositional representation and a sliding window augmentation method, which enable faster convergence and improve translation generalization. Specifically, we divide the portrait scenes into three parts for adaptive adjustments: facial region, non-facial foreground region, and the background. Besides, our network leverages the best of UNet, StyleGAN and time coding for video learning, which enables high-quality video generation. Furthermore, a sliding window augmentation method together with a pre-training strategy are proposed to improve translation generalization and training performance, respectively. The proposed network can converge within two hours while ensuring high image quality and a forward rendering time of only 20 milliseconds. Furthermore, we propose a real-time live system, which further pushes research into applications. Results and experiments demonstrate the superiority of our method in terms of image quality, full portrait video generation, and real-time re-animation compared to existing facial reenactment methods.

<div align=center><img src="./docs/results.jpg" width = 70%></div>
<p align="center">Fig.1 Facial re-enactment results of StyleAvatar.</p>

<div align=center><img src="./docs/pipeline.jpg"></div>
<p align="center">Fig.2 The pipeline of our method.</p>

## Change Log

2023.05.05 We will release code and pre-trained model soon.
2023.07.06 Release the styleunet-related python code.

## Python Requirements
- Python 3.8
- PyTorch 2.0.1
- torchvision 0.15.2
- Cuda 11.7
- opencv-python
- numpy
- tqdm
- ninja
- mediapipe

or

```
conda create -f styleavatar.yaml
```

You need to compile the ops provided by [stylegan2-pytorch](https://github.com/rosinality/stylegan2-pytorch) using ninja:

```
cd styleunet/networks/stylegan_ops
python3 setup.py install
```

## Full StyleAvatar

Coming soon.

## StyleUNet

We propose styleunet for high-resolution image-to-image translation tasks, which also refers to the ablation of "single-styleunet" in our paper. We test this network for some image-to-image translation tasks:

Mode 3 (3dmm-to-portrait image) refers to the ablation of "single-styleunet" in our paper, which can transfer a 3dmm rendering to a real portrait image.

| Mode | Input | Output |
| :--- | :---: | :---: |
| 0 (face inpainting trained on [FFHQ](https://github.com/NVlabs/ffhq-dataset)) | <img src="styleunet/input/inpainting/mode0_test1.png" width="400px" height="400px"> | <img src="styleunet/output/inpainting/mode0_test1.png" width="400px" height="400px"> |
| 0 (face inpainting trained on [FFHQ](https://github.com/NVlabs/ffhq-dataset)) | <img src="styleunet/input/inpainting/mode0_test2.png" width="400px" height="400px"> | <img src="styleunet/output/inpainting/mode0_test2.png" width="400px" height="400px"> |
| 1 (face superresolution trained on [FFHQ](https://github.com/NVlabs/ffhq-dataset)) | <img src="styleunet/input/superresolution/mode1_test1.png" width="400px" height="400px"> | <img src="styleunet/output/superresolution/mode1_test1.png" width="400px" height="400px"> |
| 1 (face superresolution trained on [FFHQ](https://github.com/NVlabs/ffhq-dataset)) | <img src="styleunet/input/superresolution/mode1_test2.png" width="400px" height="400px"> | <img src="styleunet/output/superresolution/mode1_test2.png" width="400px" height="400px"> |
| 2 (face retouching trained on [FFHQR](https://github.com/skylab-tech/ffhqr-dataset)) | <img src="styleunet/input/retouching/mode2_test3.png" width="400px" height="400px"> | <img src="styleunet/output/retouching/mode2_test3.png" width="400px" height="400px"> |
| 2 (face retouching trained on [FFHQR](https://github.com/skylab-tech/ffhqr-dataset)) | <img src="styleunet/input/retouching/mode2_test2.png" width="400px" height="400px"> | <img src="styleunet/output/retouching/mode2_test2.png" width="400px" height="400px"> |
| 3 (3dmm to portrait image trained on a single video) | <img src="styleunet/input/tdmm/mode3_test3.png" width="400px" height="400px"> | <img src="styleunet/output/tdmm/mode3_test3.png" width="400px" height="400px"> |
| 3 (3dmm to portrait image trained on a single video) | <img src="styleunet/input/tdmm/mode3_test2.png" width="400px" height="400px"> | <img src="styleunet/output/tdmm/mode3_test2.png" width="400px" height="400px"> |


### Pretrain Model

Styleunet pretrained models, please put the download models to `styleunet/pretrained/xxx.pt`:

```
model 0 (face-inpainting): https://drive.google.com/file/d/1XCdNiKx0qCJW_BryERJLLJ2ivppW80Cu/view?usp=sharing
model 1 (face-superresolution): https://drive.google.com/file/d/10V4swYfUvcpHMw76hZL-ggtTuIAraLGQ/view?usp=sharing
model 1 with discriminator (face-superresolution): https://drive.google.com/file/d/1hvbXHzAxs9MJfCj8rVNj4iqsrhA5MGUs/view?usp=sharing
model 2 (face-retouching): https://drive.google.com/file/d/1XhVcrQx_pzcfAw7aHsB410i379HWHSsr/view?usp=sharing
model 3 of lizhen (3dmm-to-portrait image): https://drive.google.com/file/d/1kFljZ5uUvcTan6dZG0_m2aq9v7DJzpiP/view?usp=sharing
```

### Training and testing

Train your styleunet model or test the pretrained model or transfer the model to onnx then to tensorrt

The training can start with the pretrained *model 1 with discriminator* above.
```
cd styleunet
# for single GPU
# train, mode 0 for face inpainting; 1 for face superresolution; 2 for face retouching; 3 for 3dmm-to-portriat image
python train.py --batch 3 --ckpt pretrained/xxxx.pt --mode 0 --augment --augment_p 0.01 path-to-dataset
python train.py --batch 3 --ckpt pretrained/xxxx.pt --mode 1 --augment --augment_p 0.01 path-to-dataset
python train.py --batch 3 --ckpt pretrained/xxxx.pt --mode 2 --augment --augment_p 0.01 path-to-dataset
python train.py --batch 3 --ckpt pretrained/xxxx.pt --mode 3 path-to-dataset
```

Use of the pretrained models.
```
cd styleunet
# test, --skin_whiten 0-1 if you want, --use_alignment if your input image is not a 1024x1024 aligned portriat image, --iter 1~3 for iterations of face retouching (only for mode 2)
python test.py --input_dir input/inpainting --ckpt pretrained/inpainting_g_ema.pt --save_dir output/inpainting --mode 0
python test.py --input_dir input/superresolution --ckpt pretrained/superresolution_g_ema.pt --save_dir output/superresolution --mode 1
python test.py --input_dir input/retouching --ckpt pretrained/retouching_g_ema.pt --save_dir output/retouching --mode 2 --skin_whiten 0.5 --iter 2 --use_alignment
python test.py --input_dir input/tdmm --ckpt pretrained/tdmm_lizhen.pt --save_dir output/tdmm --mode 3
```

Training with multi-GPUs or transfer to onnx and tensorrt.
```
cd styleunet
# train, for multi-GPUs
CUDA_VISIBLE_DEVICES=0,1 python -m torch.distributed.launch --nproc_per_node=2 --master_port='1234' train.py --batch 3 --mode 0 --ckpt pretrained/xxxx.pt --augment --augment_p 0.2 /media/data1/wlz/datasets/

# torch2onnx, --for_cpp will add BGR2RGB, BHWC2BCHW, (0,255)-to-(-1,1) into the model 
python torch2onnx.py --test_img path-to-dataset/render/000000.png --ckpt logs/checkpoint/tdmm_xxxxxx.pt --save_name xxx --mode 3 --for_cpp

# onnx2trt on Windows
tensorrt/trtexec.exe --onnx=pretrained/xxx.onnx --saveEngine=pretrained/xxx_16.engine --fp16
```

## Citation

If you use our code for your research, please consider citing:
```
@inproceedings{wang2023styleavatar,
  title={StyleAvatar: Real-time Photo-realistic Portrait Avatar from a Single Video},
  author={Wang, Lizhen and Zhao, Xiaochen and Sun, Jingxiang and Zhang, Yuxiang and Zhang, Hongwen and Yu, Tao and Liu, Yebin},
  booktitle={ACM SIGGRAPH 2023 Conference Proceedings},
  pages={},
  year={2023}
}
```

## Acknowledgement & License
The code is partially borrowed from [stylegan2-pytorch](https://github.com/rosinality/stylegan2-pytorch). And many thanks to the volunteers participated in data collection. Our License can be found in [LICENSE](./LICENSE).

