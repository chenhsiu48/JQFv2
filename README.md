# JQF: JPEG Quantization Table Fusion

This repository contains the JPEG quantization table fusion code and pretrained model for the paper: **Optimal JPEG Quantization Table Fusion by Optimizing Texture Mosaic Images and Predicting Textures**.

## Requirements

```
$ pip install -r requirements.txt
```

## Usage

Simply execute the script ```predict.py``` with a list of images to encode, defaults to JPEG quality at Q=95. This program predicts the input image's texture distribution first, then fuses a per image optimized quantization table at targeted quality.

```
$ python3 predict.py image/lighthouse.png
load ./data/JQF-Texture.pth to cuda
load ./data/qtables.json at quality 95
texture_id 73: 23.38%
texture_id 17: 16.88%
texture_id 83: 9.09%
texture_id 92: 5.19%
texture_id 56: 5.19%
...
...
fused table
  53   54   51   59   51   65   75   82 
  47   45   46   58   63   78   76   73 
  62   42   49   57   62   75   76   79 
  58   52   46   65   75   95   91   82 
  55   63   56   81   84  115  109   93 
  67   68   79   77   98  105  118  105 
  77   79   93   95  108  120  120  105 
  89  105   99  106  117  106  103  105 

scaled table at Q=95
   5    5    5    6    5    7    8    8 
   5    5    5    6    6    8    8    7 
   6    4    5    6    6    8    8    8 
   6    5    5    7    8   10    9    8 
   6    6    6    8    8   12   11    9 
   7    7    8    8   10   11   12   11 
   8    8    9   10   11   12   12   11 
   9   11   10   11   12   11   10   11 

encode ./lighthouse-95-std.jpg using standard table, 149035 bytes
encode ./lighthouse-95-jqf.jpg with fused optimized table, 106784 bytes, 28.35% size reduction
```

You can override the default quality with argument ```-q 80```:  

```
$ python3 predict.py -q 80 image/r69076d90t.png
```
