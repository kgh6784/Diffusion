# Diffusion

### Core

Number | Title | Paper | Year | Code | Summary
:---: | :---: | :---: | :---: | :---: | :---:
1 | DDPM | [[paper]](https://arxiv.org/abs/2006.11239) | 2020 | [[code]](https://github.com/kgh6784/Diffusion/tree/main/DDPM) | [[summary]](https://jihun222.notion.site/DDPM-40238918c6cc4ccc99ebb91e057f0c32)
2 | DDIM | [[paper]](https://arxiv.org/abs/2010.02502) | 2020 | [[code]] | [[summary]](https://jihun222.notion.site/DDIM-7b2234d8ea1b43b4802a75a3d1758869)


### with Segmentation

Number | Title | Paper | Year | Code | Summary
:---: | :---: | :---: | :---: | :---: | :---:
1 | Diffusion Models for Implicit Image Segmentation Ensembles | [[paper]](https://arxiv.org/pdf/2112.03145.pdf) | 2021 | [[code]] | [[summary]](https://jihun222.notion.site/Diffusion-Models-for-Implicit-Image-Segmentation-Ensembles-76b16eaf78894bde9e2b4d4275575196)
2 | LABEL-EFFICIENT SEMANTIC SEGMENTATION WITH DIFFUSION MODELS | [[paper]](https://arxiv.org/pdf/2112.03126v3.pdf) | 2021 | [[code]] | [[summary]](https://jihun222.notion.site/LABEL-EFFICIENT-SEMANTIC-SEGMENTATION-WITH-DIFFUSION-MODELS-2fa7010b23ee477c814de32812160326)

### 발표자료 정리
- 1회차 : DDPM / Generative Modeling by Estimating Gradients of the Data Distribution | [[ppt]](https://github.com/kgh6784/Diffusion/blob/main/presentation/Diffusion%20%EC%8A%A4%ED%84%B0%EB%94%94%201%ED%9A%8C%EC%B0%A8.pptm)

### Guide
- `DDPM` Pretrain된 모델 사용하려면 [[링크]](https://github.com/pesser/pytorch_diffusion)를 참고하면 된다.
  - 제공 pretrain weights : `cifar10`, `lsun-bedroom`, `lsun-cat` `lsun_church`
- `Diffusion Models Beat GANS on Image Synthesis` pretrain된 weight를 제공해준다.
   * 64x64 classifier: [64x64_classifier.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/64x64_classifier.pt)
   * 64x64 diffusion: [64x64_diffusion.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/64x64_diffusion.pt)
   * 128x128 classifier: [128x128_classifier.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/128x128_classifier.pt)
   * 128x128 diffusion: [128x128_diffusion.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/128x128_diffusion.pt)
   * 256x256 classifier: [256x256_classifier.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/256x256_classifier.pt)
   * 256x256 diffusion: [256x256_diffusion.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/256x256_diffusion.pt)
   * 256x256 diffusion (not class conditional): [256x256_diffusion_uncond.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/256x256_diffusion_uncond.pt)
   * 512x512 classifier: [512x512_classifier.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/512x512_classifier.pt)
   * 512x512 diffusion: [512x512_diffusion.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/512x512_diffusion.pt)
   * 64x64 -&gt; 256x256 upsampler: [64_256_upsampler.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/64_256_upsampler.pt)
   * 128x128 -&gt; 512x512 upsampler: [128_512_upsampler.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/128_512_upsampler.pt)
   * LSUN bedroom: [lsun_bedroom.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/lsun_bedroom.pt)
   * LSUN cat: [lsun_cat.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/lsun_cat.pt)
   * LSUN horse: [lsun_horse.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/lsun_horse.pt)
   * LSUN horse (no dropout): [lsun_horse_nodropout.pt](https://openaipublic.blob.core.windows.net/diffusion/jul-2021/lsun_horse_nodropout.pt)
- `SDE`를 pretrain한 모델도 제공해준다.
  [CelebA-HQ](https://image-editing-test-12345.s3-us-west-2.amazonaws.com/checkpoints/celeba_hq.ckpt),
  [LSUN bedroom](https://image-editing-test-12345.s3-us-west-2.amazonaws.com/checkpoints/bedroom.ckpt),
  and [LSUN church outdoor](https://image-editing-test-12345.s3-us-west-2.amazonaws.com/checkpoints/church_outdoor.ckpt).
