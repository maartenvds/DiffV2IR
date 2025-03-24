<div align="center">
<h1>DiffV2IR: Visible-to-Infrared Diffusion Model via  Vision-Language Understanding </h1>

<div>
    Lingyan Ran<sup>1</sup>, Lidong Wang<sup>1</sup>, Guangcong Wang<sup>2</sup>, Peng Wang<sup>1</sup>, Yanning Zhang<sup>1</sup>
</div>
<div>
    Northwestern Polytechnical University<sup>1</sup>, Great Bay University<sup>2</sup>
</div>

>**Abstract:** The task of translating visible-to-infrared images (V2IR) is inherently challenging due to three main obstacles: 1) achieving semantic-aware translation, 2) managing the diverse wavelength spectrum in infrared imagery, and 3) the scarcity of comprehensive infrared datasets. Current leading methods tend to treat V2IR as a conventional image-to-image synthesis challenge, often overlooking these specific issues. To address this, we introduce DiffV2IR, a novel framework for image translation comprising two key elements: a Progressive Learning Module (PLM) and a Vision-Language Understanding Module (VLUM). PLM features an adaptive diffusion model architecture that leverages multi-stage knowledge learning to infrared transition from full-range to target wavelength. 
>To improve V2IR translation, VLUM incorporates unified Vision-Language Understanding. 
>We also collected a large infrared dataset, IR-500K, which includes 500,000 infrared images compiled by various scenes and objects under various environmental conditions. Through the combination of PLM, VLUM, and the extensive IR-500K dataset, DiffV2IR markedly improves the performance of V2IR. Experiments validate DiffV2IR's excellence in producing high-quality translations, establishing its efficacy and broad applicability. The code, dataset, and DiffV2IR model will be available.

<div align="center">
<tr>
    <img src="img/main.png" width="90%"/>
</tr>
</div>



>**Framework Overview:** DiffV2IR mainly consists of two components, i.e., Progressive Learning Module (PLM) and Vision-Language Understanding Module (VLUM). 
>Specifically, 1) as for PLM, we first establish foundational knowledge of infrared imaging properties utilizing our collected IR-500K dataset. Then we use visible-infrared image pairs to learn cross-modal transformation and finally conduct the refinement on the specific infrared imaging style. 
>2) as for VLUM, we incorporate unified vision-language understanding, including detailed language descriptions and segmentation maps, to make DiffV2IR semantic-aware and structure-preserving. 

## 1. Installation
We recommend using the virtual environment (conda) to run the code easily.

```
conda create -n DiffV2IR python=3.10.15
conda activate sparsenerf
pip install -r requirements.txt
```

## 2. Dataset

### 2.1 Download IR-500K dataset
- Download the IR-500K dataset here(coming soon)
### 2.2 Use your own dataset
- Our training scripts expect the dataset to be in the following format
```
dataset_name
├── rgb
│   ├── 000000.png
│   ├── 000001.png
│   └── ...
├── ir
│   ├── 000000.png
│   ├── 000001.png
│   └── ...
├── seg
│   ├── 000000.png
│   ├── 000001.png
│   └── ...
├── seeds.json
```

The subfolder seg can be produced by generating masks from the entire image under the guidance of  and then running "process_masks.py".


## 3. Training 

Please set the variables in configs/train.yaml and run:
```
python main.py --base configs/train.yaml --name your_name --gpus 1 --train
```

## 4. Test 
Please set the variables in configs/generate.yaml and run:
```
python infer.py --ckpt your_ckpt --input input_folder --output output_folder
```

## 5 Pretrained Checkpoints
We will update the pretrained checkpoint after Stage 2 of PLM for further training and the pretrained checkpoint of M3FD Dataset   and FLIR Dataset mentioned in the paper.

## 6 Comments

Our codebase is based on the [Stable Diffusion codebase](https://github.com/CompVis/stable-diffusion).



