# AnimeSR (NeurIPS 2022)

### :open_book: AnimeSR: Learning Real-World Super-Resolution Models for Animation Videos
> [![arXiv](https://img.shields.io/badge/arXiv-Paper-<COLOR>.svg)](https://arxiv.org/abs/2206.07038)<br>
> [Yanze Wu](https://github.com/ToTheBeginning), [Xintao Wang](https://xinntao.github.io/), [Gen Li](https://scholar.google.com.hk/citations?user=jBxlX7oAAAAJ), [Ying Shan](https://scholar.google.com/citations?user=4oXBp9UAAAAJ&hl=en) <br>
> [Tencent ARC Lab](https://arc.tencent.com/en/index); Platform Technologies, Tencent Online Video


## Web Demo and API

[![Replicate](https://replicate.com/cjwbw/animesr/badge)](https://replicate.com/cjwbw/animesr) 

## Video Demos

https://user-images.githubusercontent.com/11482921/204205018-d69e2e51-fbdc-4766-8293-a40ffce3ed25.mp4

https://user-images.githubusercontent.com/11482921/204205109-35866094-fa7f-413b-8b43-bb479b42dfb6.mp4

## Video Frames Demos(Left:Low Resolution Video Frame  Right:Super Resolution[Desired Output])

<div align=center>
<img  src="inputs/inputimages/Screenshot (3835).png" width="400" height="320">
<img  src="outputs/outimage/Screenshot (3845).png" width="400" height="320"> 
</div> 

<div align=center>
<img  src="inputs/inputimages/Screenshot (3834).png" width="400" height="320">
<img  src="hazy/Dehazed/2a_dehazed.jpg" width="400" height="320"> 
</div> 

<div align=center>
<img  src="inputs/inputimages/Screenshot (3837).png" width="400" height="320">
<img  src="hazy/Dehazed/2a_dehazed.jpg" width="400" height="320"> 
</div> 

<div align=center>
<img  src="inputs/inputimages/Screenshot (3828).png" width="400" height="320">
<img  src="hazy/Dehazed/2a_dehazed.jpg" width="400" height="320"> 
</div>

<div align=center>
<img  src="inputs/inputimages/Screenshot (3831).png" width="400" height="320">
<img  src="hazy/Dehazed/2a_dehazed.jpg" width="400" height="320"> 
</div>

## :wrench: Dependencies and Installation
- Python >= 3.7 (Recommend to use [Anaconda](https://www.anaconda.com/download/#linux) or [Miniconda](https://docs.conda.io/en/latest/miniconda.html))
- [PyTorch >= 1.7](https://pytorch.org/)
- Other required packages in `requirements.txt`

### Installation

1. Clone repo

    ```bash
    git clone https://github.com/TencentARC/AnimeSR.git
    cd AnimeSR
    ```
2. Install

    ```bash
    # Install dependent packages
    pip install -r requirements.txt

    # Install AnimeSR
    python setup.py develop
    ```

## :zap: Quick Inference
Download the pre-trained AnimeSR models [[Google Drive](https://drive.google.com/drive/folders/1gwNTbKLUjt5FlgT6PQQnBz5wFzmNUX8g?usp=share_link)], and put them into the [weights](weights/) folder. Currently, the available pre-trained models are:
- `AnimeSR_v1-PaperModel.pth`: v1 model, also the paper model. You can use this model for paper results reproducing.
- `AnimeSR_v2.pth`: v2 model. Compare with v1, this version has better naturalness, fewer artifacts, and better texture/background restoration. If you want better results, use this model.

AnimeSR supports both frames and videos as input for inference. We provide several sample test cases in [google drive](https://drive.google.com/drive/folders/1K8JzGNqY_pHahYBv51iUUI7_hZXmamt2?usp=share_link), you can download it and put them to [inputs](inputs/) folder.

**Inference on Frames**
```bash
python scripts/inference_animesr_frames.py -i inputs/tom_and_jerry -n AnimeSR_v2 --expname animesr_v2 --save_video_too --fps 20
```

After run the above command, you will get the SR frames in `results/animesr_v2/frames` and the SR video in `results/animesr_v2/videos`.

**Inference on Video**
```bash
# single gpu and single process inference
CUDA_VISIBLE_DEVICES=0 python scripts/inference_animesr_video.py -i inputs/TheMonkeyKing1965.mp4 -n AnimeSR_v2 -s 4 --expname animesr_v2 --num_process_per_gpu 1 --suffix 1gpu1process
# single gpu and multi process inference (you can use multi-processing to improve GPU utilization)
CUDA_VISIBLE_DEVICES=0 python scripts/inference_animesr_video.py -i inputs/TheMonkeyKing1965.mp4 -n AnimeSR_v2 -s 4 --expname animesr_v2 --num_process_per_gpu 3 --suffix 1gpu3process
# multi gpu and multi process inference
CUDA_VISIBLE_DEVICES=0,1 python scripts/inference_animesr_video.py -i inputs/TheMonkeyKing1965.mp4 -n AnimeSR_v2 -s 4 --expname animesr_v2 --num_process_per_gpu 3 --suffix 2gpu6process
```

SR videos are saved in `results/animesr_v2/videos/$video_name` folder.

If you are looking for portable executable files, you can try our [realesr-animevideov3](https://github.com/xinntao/Real-ESRGAN/blob/master/docs/anime_video_model.md) model which shares the similar technology with AnimeSR.


