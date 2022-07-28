## 0. FreeSurfer reconstruction using MP2RAGE from 7T.

This is different from MPRAGE images. MP2RAGE generates three sets of images, which are two sets of images at two different TI with one TI specified with nulled gray matter signal and one set of images as the ratio between the two. The ratio images have much better gray/white matter contrast. It is that set of images (ratio images) to be used for FreeSurfer reconstruction.

The images below are three sets of images from one subject at 7T using MP2RAGE. The one in the middle should be used for FreeSurfer reconstruction.
[[https://github.com/fahsuanlin/labmanual/blob/master/images/mp2rage.png]]

## 1. Expand the cortical surfaces between white/gray matter boundary and pial surface boundary

Run the following commands to get 9 intermediate equi-spaced surfaces between gray/white matter boundary (?h.white) and gray matter/pial surface boundary (?h.pial).

```
mris_expand -thickness lh.white 0.1 lh.gray01
mris_expand -thickness lh.white 0.2 lh.gray02
mris_expand -thickness lh.white 0.3 lh.gray03
mris_expand -thickness lh.white 0.4 lh.gray04
mris_expand -thickness lh.white 0.5 lh.gray05
mris_expand -thickness lh.white 0.6 lh.gray06
mris_expand -thickness lh.white 0.7 lh.gray07
mris_expand -thickness lh.white 0.8 lh.gray08
mris_expand -thickness lh.white 0.9 lh.gray09

mris_expand -thickness rh.white 0.1 rh.gray01
mris_expand -thickness rh.white 0.2 rh.gray02
mris_expand -thickness rh.white 0.3 rh.gray03
mris_expand -thickness rh.white 0.4 rh.gray04
mris_expand -thickness rh.white 0.5 rh.gray05
mris_expand -thickness rh.white 0.6 rh.gray06
mris_expand -thickness rh.white 0.7 rh.gray07
mris_expand -thickness rh.white 0.8 rh.gray08
mris_expand -thickness rh.white 0.9 rh.gray09
```

## 2. Correct distortion in EPI data

Use the following codes to correct distortion by `topup `in FSL. These include the steps to prepare data acquired with "blipped-up" and "blipped-down" phase encoding steps. Merge these data as one single file. Estimate the distortion map. Then, apply distortion map to the original EPI data to restore the right shape.
