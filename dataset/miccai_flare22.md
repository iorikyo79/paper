# MICCAI FLARE22 Challenge Dataset (50 Labeled Abdomen CT Scans)

https://zenodo.org/records/7860267

- 용도 : MedSAM Tuning용 데이터로 사용.


## 소개

- MICCAI FLARE 2022 챌린지(https://flare22.grand-challenge.org/)에서 라벨링된 훈련 세트
- CT 이미지와 췌장 어노테이션은 http://medicaldecathlon.com/ 에서 가져왔음.
- 다른 장기 주석은 AbdomenCT-1K에서 가져온 것(연구 목적으로만 사용됨).

### Data preprocessing
1. Download the Lite-MedSAM [checkpoint](https://drive.google.com/file/d/18Zed-TUTsmr2zc5CHUWd5Tu13nb6vq6z/view?usp=sharing) and put it under the current directory.
2. Download the [demo dataset](https://zenodo.org/records/7860267). This tutorial assumes it is unzipped it to `data/FLARE22Train/`.
3. Run the pre-processing script to convert the dataset to `npz` format:
```bash
python pre_CT_MR.py \
    -img_path data/FLARE22Train/images \ ## path to training images
    -img_name_suffix _0000.nii.gz \ ## extension of training images
    -gt_path data/FLARE22Train/labels \ ## path to training labels
    -gt_name_suffix .nii.gz \ ## extension of training labels
    -output_path data \ ## path to save the preprocessed data
    -num_workers 4 \ ## number of workers for preprocessing
    -modality CT \ ## modality of the preprocessed data
    -anatomy Abd \ ## anatomy of the preprocessed data
    -window_level 40 \ ## window level for CT
    -window_width 400 \ ## window width for CT
    --save_nii ## Also save the preprocessed data in nii.gz format for visual inspection in other software
```
* Split dataset: first 40 cases of the demo dataset for training, saved in `MedSAM_train`, the last 10 for testing, saved in `MedSAM_test`.
* For detailed usage of the script, see `python pre_CT_MR.py -h`.

4. Convert the training `npz` to `npy` format for training:
```bash
python npz_to_npy.py \
    -npz_dir data/MedSAM_train \ ## path to the preprocessed npz training data
    -npy_dir data/npy \ ## path to save the converted npy data for training
    -num_workers 4 ## number of workers for conversion in parallel
```









### 이 데이터 세트 사용시 두 논문을 인용 필요:

- A large annotated medical image dataset for the development and evaluation of segmentation algorithms [here](https://arxiv.org/abs/1902.09063)
- AbdomenCT-1K: Is Abdominal Organ Segmentation a Solved Problem? [here](https://ieeexplore.ieee.org/document/9497733)


