# S4AL - Semantic Segmentation with Active Semi-Supervised Learning

## Training Env
We use PyTorch 1.8 with CUDA 11.1 for training all networks. These are the steps to set up the Anaconda environment:
```
conda create --name pyt18 anaconda python=3.7
conda activate pyt18
pip install torch==1.8.0+cu111 torchvision==0.9.0+cu111 torchaudio==0.8.0 -f https://download.pytorch.org/whl/torch_stable.html
pip install opencv-python tensorboardX tabulate
```

Note: We observed on Windows, Pytorch throws some errors with respect to the dataloaders. As Ubuntu is our primary OS, a quick fix for the Windows error is to set `num_workers` to `0` in `helpers\dataset_builder.py`.

## Datasets
We use CamVid and CityScapes in our paper. Please download CamVid from [here](https://github.com/alexgkendall/SegNet-Tutorial) and CityScapes from [here](https://www.cityscapes-dataset.com/). We  preprocess CityScapes images to a resolution of 688 x 688, and keep original resolution for CamVid. The `datasets` folder is organized as:
- datasets
  - CamVid
      - annots
      - images
      - imagesets
  - CityScapes
      -  annots
          - train
          - val
      - images
          - train
          - val 
      - imagesets

## Training Scripts

For training S4AL on CamVid:
```
python --dataset camvid --generations 2 --unsup_weight 1 --coldstart --region_size 30 --num_regions 4 --max_buffer_length 50 --save_dir camvid_s4al_run1
```

For training S4AL on CityScapes:
```
python --dataset cityscapes --generations 5 --unsup_weight 1 --coldstart --region_size 43 --num_regions 4 --max_buffer_length 500 --save_dir cityscapes_s4al_run1
```

## References

List of open-source repositories used or referred for this code:
- [ReCo](https://github.com/lorenmt/reco)
- [DEAL](https://github.com/Shuai-Xie/DEAL)
- [ViewAL](https://github.com/nihalsid/ViewAL)
- [Nvidia SemSeg](https://github.com/NVIDIA/semantic-segmentation)
- [Pytorch Torchvision](https://github.com/pytorch/vision)
