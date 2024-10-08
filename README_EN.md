<div align="center">

<img alt="hivision_logo" src="assets/hivision_logo.png" width=120 height=120>
<h1>HivisionIDPhoto</h1>

English / [中文](README.md) / [日本語](README_JP.md) / [한국어](README_KO.md)

[![][release-shield]][release-link]
[![][dockerhub-shield]][dockerhub-link]
[![][github-stars-shield]][github-stars-link]
[![][github-issues-shield]][github-issues-link]
[![][github-contributors-shield]][github-contributors-link]
[![][github-forks-shield]][github-forks-link]
[![][license-shield]][license-link]  
[![][wechat-shield]][wechat-link]
[![][spaces-shield]][spaces-link]
[![][swanhub-demo-shield]][swanhub-demo-link]

[![][trendshift-shield]][trendshift-link]
[![][hellogithub-shield]][hellogithub-link]

<img src="assets/demoImage.jpg" width=900>

</div>

<br>

> **Related Projects**：
>
> - [SwanLab](https://github.com/SwanHubX/SwanLab): Used throughout the training of the portrait matting model for analysis and monitoring, as well as collaboration with lab colleagues, significantly improving training efficiency.

<br>

# Table of Contents

- [Recent Updates](#-recent-updates)
- [Project Overview](#-project-overview)
- [Community](#-community)
- [Preparation](#-preparation)
- [Demo Startup](#-run-gradio-demo)
- [Python Inference](#-python-inference)
- [API Service Deployment](#️-deploy-api-service)
- [Docker Deployment](#-docker-deployment)
- [Contact Us](#-contact-us)
- [Contributors](#contributors)

<br>

# 🤩 Recent Updates

- Online Experience: [![SwanHub Demo](https://img.shields.io/static/v1?label=Demo&message=SwanHub%20Demo&color=blue)](https://swanhub.co/ZeYiLin/HivisionIDPhotos/demo)、[![Spaces](https://img.shields.io/badge/🤗-Open%20in%20Spaces-blue)](https://huggingface.co/spaces/TheEeeeLin/HivisionIDPhotos)

- 2024.09.11: Added **transparent image display and download** feature to Gradio Demo.
- 2024.09.10: Added a new **face detection model** Retinaface-resnet50, which offers higher detection accuracy at a slightly slower speed compared to mtcnn. Recommended for use.
- 2024.09.09: Added a new **Background Removal Model** [BiRefNet-v1-lite](https://github.com/ZhengPeng7/BiRefNet) | Gradio added **Advanced Parameter Settings** and **Watermark** tabs
- 2024.09.08: Added new **Matting Model** [RMBG-1.4](https://huggingface.co/briaai/RMBG-1.4) | **ComfyUI Workflow** - [HivisionIDPhotos-ComfyUI](https://github.com/AIFSH/HivisionIDPhotos-ComfyUI) contributed by [AIFSH](https://github.com/AIFSH/HivisionIDPhotos-ComfyUI)
- 2024.09.07: Added **Face Detection API Option** [Face++](docs/face++_EN.md), achieving higher precision in face detection
- 2024.09.06: Added new matting model [modnet_photographic_portrait_matting.onnx](https://github.com/ZHKKKe/MODNet)
- 2024.09.05: Updated [Restful API Documentation](docs/api_EN.md)
- 2024.09.02: Updated **Adjust Photo KB Size**, [DockerHub](https://hub.docker.com/r/linzeyi/hivision_idphotos/tags)

<br>

# Project Overview

> 🚀 Thank you for your interest in our work. You may also want to check out our other achievements in the field of image processing, feel free to reach out: zeyi.lin@swanhub.co.

HivisionIDPhoto aims to develop a practical and systematic intelligent algorithm for producing ID photos.

It utilizes a comprehensive AI model workflow to recognize various user photo-taking scenarios, perform matting, and generate ID photos.

**HivisionIDPhoto can achieve:**

1. Lightweight matting (purely offline, fast inference with **CPU** only)
2. Generate standard ID photos and six-inch layout photos based on different size specifications
3. Support pure offline or edge-cloud inference
4. Beauty effects (waiting)
5. Intelligent formal wear change (waiting)

<div align="center">
<img src="assets/demo.png" width=900>
</div>

---

If HivisionIDPhoto helps you, please star this repo or recommend it to your friends to solve the urgent ID photo production problem!

<br>

# 🏠 Community

We have shared some interesting applications and extensions of HivisionIDPhotos built by the community:

- [HivisionIDPhotos-windows-GUI](https://github.com/zhaoyun0071/HivisionIDPhotos-windows-GUI): Windows client application built by [zhaoyun0071](https://github.com/zhaoyun0071)
- [HivisionIDPhotos-ComfyUI](https://github.com/AIFSH/HivisionIDPhotos-ComfyUI): ComfyUI ID photo processing workflow built by [AIFSH](https://github.com/AIFSH/HivisionIDPhotos-ComfyUI) 

[![](assets/comfyui.png)](https://github.com/AIFSH/HivisionIDPhotos-ComfyUI)

- [zjzWx](https://github.com/no1xuan/zjzWx): Exquisite open source ID photo WeChat mini program project, contributed by [no1xuan](https://github.com/no1xuan)

<br>

# 🔧 Preparation

Environment installation and dependencies:
- Python >= 3.7 (project primarily tested on Python 3.10)
- OS: Linux, Windows, MacOS

## 1. Clone the Project

```bash
git clone https://github.com/Zeyi-Lin/HivisionIDPhotos.git
cd  HivisionIDPhotos
```

## 2. Install Dependency Environment

> It is recommended to create a python3.10 virtual environment using conda, then execute the following commands

```bash
pip install -r requirements.txt
pip install -r requirements-app.txt
```

## 3. Download Weight Files

**Method 1: Script Download**

```bash
python scripts/download_model.py --models all
```

**Method 2: Direct Download**

Store in the project's `hivision/creator/weights` directory:
- `modnet_photographic_portrait_matting.onnx` (24.7MB): Official weights of [MODNet](https://github.com/ZHKKKe/MODNet), [download](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/download/pretrained-model/modnet_photographic_portrait_matting.onnx)
- `hivision_modnet.onnx` (24.7MB): Matting model with better adaptability for pure color background replacement, [download](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/download/pretrained-model/hivision_modnet.onnx)
- `rmbg-1.4.onnx` (176.2MB): Open-source matting model from [BRIA AI](https://huggingface.co/briaai/RMBG-1.4), [download](https://huggingface.co/briaai/RMBG-1.4/resolve/main/onnx/model.onnx?download=true) and rename to `rmbg-1.4.onnx`
- `birefnet-v1-lite.onnx`(224MB): Open-source matting model from [ZhengPeng7](https://github.com/ZhengPeng7/BiRefNet), [download](https://github.com/ZhengPeng7/BiRefNet/releases/download/v1/BiRefNet-general-bb_swin_v1_tiny-epoch_232.onnx) and rename to `birefnet-v1-lite.onnx`

## 4. Face Detection Model Configuration (Optional)

| Extended Face Detection Model | Description | Documentation |
| -- | -- | -- |
| MTCNN | **Offline** face detection model, high-performance CPU inference, default model, lower detection accuracy | Use it directly after cloning this project |
| RetinaFace | **Offline** face detection model, moderate CPU inference speed (in seconds), and high accuracy | [Download](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/download/pretrained-model/retinaface-resnet50.onnx) and place it in the `hivision/creator/retinaface/weights` directory |
| Face++ | Online face detection API launched by Megvii, higher detection accuracy, [official documentation](https://console.faceplusplus.com.cn/documents/4888373) | [Usage Documentation](docs/face++_EN.md)|

## 5. GPU Inference Acceleration (Optional)

If you need to use NVIDIA GPU for accelerated inference, ensure that you have installed CUDA and cuDNN, then find the corresponding `onnxruntime-gpu` version to install according to the [documentation](https://onnxruntime.ai/docs/execution-providers/CUDA-ExecutionProvider.html#cuda-12x), for example:

```bash
# CUDA 12.x, cuDNN 8
pip install onnxruntime-gpu==1.18.0
```

After completing this, calling models like `birefnet-v1-lite` will utilize GPU acceleration for inference.

<br>

# 🚀 Run Gradio Demo

```bash
python app.py
```

Running the program will generate a local web page where you can perform operations and interact with ID photos.

<img src="assets/harry.png" width=900>

<br>

# 🚀 Python Inference

Core parameters:

- `-i`: Input image path
- `-o`: Save image path
- `-t`: Inference type, options include idphoto, human_matting, add_background, generate_layout_photos
- `--matting_model`: Selection of portrait matting model weights
- `--face_detect_model`: Selection of face detection model

More parameters can be viewed by running `python inference.py --help`

## 1. ID Photo Production

Input 1 photo to obtain 1 standard ID photo and 1 high-definition ID photo in 4-channel transparent png

```python
python inference.py -i demo/images/test.jpg -o ./idphoto.png --height 413 --width 295
```

## 2. Portrait Matting

```python
python inference.py -t human_matting -i demo/images/test.jpg -o ./idphoto_matting.png --matting_model hivision_modnet
```

## 3. Add Background Color to Transparent Image

Input 1 4-channel transparent png to obtain 1 image with added background color

```python
python inference.py -t add_background -i ./idphoto.png -o ./idphoto_ab.jpg  -c 4f83ce -k 30 -r 1
```

## 4. Obtain Six-Inch Layout Photo

Input 1 3-channel photo to obtain 1 six-inch layout photo

```python
python inference.py -t generate_layout_photos -i ./idphoto_ab.jpg -o ./idphoto_layout.jpg  --height 413 --width 295 -k 200
```

<br>

# ⚡️ Deploy API Service

## Start Backend

```
python deploy_api.py
```

## Request API Service

For detailed request methods, please refer to the [API Documentation](docs/api_EN.md), which includes the following request examples:
- [cURL](docs/api_EN.md#curl-request-examples)
- [Python](docs/api_EN.md#python-request-example)
- [Java](docs/api_EN.md#java-request-example)
- [Javascript](docs/api_EN.md#javascript-request-examples)

<br>

# 🐳 Docker Deployment

## 1. Pull or Build Image

> Choose one of the following methods

**Method 1: Pull the latest image:**

```bash
docker pull linzeyi/hivision_idphotos
```

**Method 2: Directly build the image from Dockerfile:**

After ensuring that the model weight file [hivision_modnet.onnx](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/tag/pretrained-model) is placed in `hivision/creator/weights`, execute the following in the project root directory:

```bash
docker build -t linzeyi/hivision_idphotos .
```

**Method 3: Build using Docker Compose:**

Ensure that the model weight file [hivision_modnet.onnx](https://github.com/Zeyi-Lin/HivisionIDPhotos/releases/tag/pretrained-model) is placed in `hivision/creator/weights`, then execute the following in the project root directory:

```bash
docker compose build
```

## 2. Run Services

**Start Gradio Demo Service**

Run the following command, and you can access it locally at [http://127.0.0.1:7860](http://127.0.0.1:7860/).

```bash
docker run -d -p 7860:7860 linzeyi/hivision_idphotos
```

**Start API Backend Service**

```bash
docker run -d -p 8080:8080 linzeyi/hivision_idphotos python3 deploy_api.py
```

**Start Both Services Simultaneously**

```bash
docker compose up -d
```

## Environment Variables

This project provides some additional configuration options, which can be set using environment variables:

| Environment Variable | Type | Description | Example |
|--|--|--|--|
| FACE_PLUS_API_KEY | Optional | This is your API key obtained from the Face++ console | `7-fZStDJ····` |
| FACE_PLUS_API_SECRET | Optional | Secret corresponding to the Face++ API key | `VTee824E····` |

Example of using environment variables in Docker:
```bash
docker run  -d -p 7860:7860 \
    -e FACE_PLUS_API_KEY=7-fZStDJ···· \
    -e FACE_PLUS_API_SECRET=VTee824E···· \
    linzeyi/hivision_idphotos 
```

<br>

# 📖 Cite Projects

1. MTCNN:

```bibtex
@software{ipazc_mtcnn_2021,
    author = {ipazc},
    title = {{MTCNN}},
    url = {https://github.com/ipazc/mtcnn},
    year = {2021},
    publisher = {GitHub}
}
```

2. ModNet:

```bibtex
@software{zhkkke_modnet_2021,
    author = {ZHKKKe},
    title = {{ModNet}},
    url = {https://github.com/ZHKKKe/MODNet},
    year = {2021},
    publisher = {GitHub}
}
```

<br>

# 💻 Development Tips

## How to modify preset sizes and colors?

- Size: After modifying [size_list_EN.csv](demo/assets/size_list_EN.csv), run `app.py` again. The first column is the size name, the second column is the height, and the third column is the width.
- Color: After modifying [color_list_EN.csv](demo/assets/color_list_EN.csv), run `app.py` again. The first column is the color name, and the second column is the Hex value.

## How to Change the Watermark Font?

1. Place the font file in the `hivision/plugin/font` folder.
2. Change the `font_file` parameter value in `hivision/plugin/watermark.py` to the name of the font file.

<br>

# 📧 Contact Us

If you have any questions, please email zeyi.lin@swanhub.co

<br>

# Contributors

<a href="https://github.com/Zeyi-Lin/HivisionIDPhotos/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Zeyi-Lin/HivisionIDPhotos" />
</a>

[Zeyi-Lin](https://github.com/Zeyi-Lin)、[SAKURA-CAT](https://github.com/SAKURA-CAT)、[Feudalman](https://github.com/Feudalman)、[swpfY](https://github.com/swpfY)、[Kaikaikaifang](https://github.com/Kaikaikaifang)、[ShaohonChen](https://github.com/ShaohonChen)、[KashiwaByte](https://github.com/KashiwaByte)

<br>

# StarHistory

[![Star History Chart](https://api.star-history.com/svg?repos=Zeyi-Lin/HivisionIDPhotos&type=Date)](https://star-history.com/#Zeyi-Lin/HivisionIDPhotos&Date)

[github-stars-shield]: https://img.shields.io/github/stars/zeyi-lin/hivisionidphotos?color=ffcb47&labelColor=black&style=flat-square
[github-stars-link]: https://github.com/zeyi-lin/hivisionidphotos/stargazers

[swanhub-demo-shield]: https://swanhub.co/git/repo/SwanHub%2FAuto-README/file/preview?ref=main&path=swanhub.svg
[swanhub-demo-link]: https://swanhub.co/ZeYiLin/HivisionIDPhotos/demo

[spaces-shield]: https://img.shields.io/badge/🤗-Open%20in%20Spaces-blue
[spaces-link]: https://huggingface.co/spaces/TheEeeeLin/HivisionIDPhotos

<!-- WeChat group link -->
[wechat-shield]: https://img.shields.io/badge/WeChat-微信-4cb55e
[wechat-link]: https://docs.qq.com/doc/DUkpBdk90eWZFS2JW

<!-- Github Release -->
[release-shield]: https://img.shields.io/github/v/release/zeyi-lin/hivisionidphotos?color=369eff&labelColor=black&logo=github&style=flat-square
[release-link]: https://github.com/zeyi-lin/hivisionidphotos/releases

[license-shield]: https://img.shields.io/badge/license-apache%202.0-white?labelColor=black&style=flat-square
[license-link]: https://github.com/Zeyi-Lin/HivisionIDPhotos/blob/master/LICENSE

[github-issues-shield]: https://img.shields.io/github/issues/zeyi-lin/hivisionidphotos?color=ff80eb&labelColor=black&style=flat-square
[github-issues-link]: https://github.com/zeyi-lin/hivisionidphotos/issues

[dockerhub-shield]: https://img.shields.io/docker/v/linzeyi/hivision_idphotos?color=369eff&label=docker&labelColor=black&logoColor=white&style=flat-square
[dockerhub-link]: https://hub.docker.com/r/linzeyi/hivision_idphotos/tags

[trendshift-shield]: https://trendshift.io/api/badge/repositories/11622
[trendshift-link]: https://trendshift.io/repositories/11622

[hellogithub-shield]: https://abroad.hellogithub.com/v1/widgets/recommend.svg?rid=8ea1457289fb4062ba661e5299e733d6&claim_uid=Oh5UaGjfrblg0yZ
[hellogithub-link]: https://hellogithub.com/repository/8ea1457289fb4062ba661e5299e733d6

[github-contributors-shield]: https://img.shields.io/github/contributors/zeyi-lin/hivisionidphotos?color=c4f042&labelColor=black&style=flat-square
[github-contributors-link]: https://github.com/zeyi-lin/hivisionidphotos/graphs/contributors

[github-forks-shield]: https://img.shields.io/github/forks/zeyi-lin/hivisionidphotos?color=8ae8ff&labelColor=black&style=flat-square
[github-forks-link]: https://github.com/zeyi-lin/hivisionidphotos/network/members