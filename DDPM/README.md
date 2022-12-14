## DDPM

- Hugging Face에서 잘 정리를 해두어, 한글로 정리하면서 코드를 공부하였습니다. 
- 링크 : https://huggingface.co/blog/annotated-diffusion
- 번역 : https://github.com/kgh6784/Diffusion/blob/main/DDPM/DDPM_HuggingFace.ipynb


## 결과 
<p align="center">
   <img src='./diffusion 2.gif', alt="diffusion result"  width="350" />
</p>

## 수학 모를 때 도움이 된 곳들
- ELBO : https://hugrypiggykim.com/2018/09/07/variational-autoencoder%EC%99%80-elboevidence-lower-bound/
- MLE : https://bubilife.tistory.com/33
- NLL : https://gaussian37.github.io/dl-concept-nll_loss/

## 혼자 스터디(22/12/01)

### Q1) Training 시 object function
- ϵ과 ϵ_θ의 loss를 계산하는 것은 실제 forward 과정을 거쳐 나온 t 시점에서의 알려진 noise를 U-Net을 통과시켜 나온 pure한 noise와 t=T에서부터 reverse과정을 거쳐서 나온 nerual net을 통해 나온 추측된 noise사이의 loss function을 계산하는 것 같다.
(공식 코드를 보면 noise끼리의 loss를 계산하는 것이 기본, x_0을 예측하는 경우가 있는데 이는 아직 논문을 더 자세히 봐야할 듯)

### Q2) SILU
- 처음 사용해본다.
- Simgoid Linear Unit : 시그모이드 함수에 입력값을 곱한 함수
<p align="center">
   <img src='./DDPM_study/SILU_function.png', alt="SILU_function"  width="600" />
</p> 
<p align="center">
   <img src='./DDPM_study/SILU_IMAGE.png', alt="IMAGE"  width="400" />
</p> 

- 기존의 activation보다 훨씬 부드럽게 구성되어 있다. 

</p> 
<p align="center">
   <img src='./DDPM_study/compare_SILU.png', alt="compare"  width="700" />
</p>

### Q3) Position encoding 들어가는 위치
- `ResNet` 또는 `ConvNext` block을 사용할 때, 이 block에서 한 번 conv2d를 거친 후에 Position encoding 추가해준다. (공통)
- 내가 이해한 것이 맞다면 downsample - mid_block - upsampling시 각각 2번씩 Position encoding 추가하고, 최종 final_conv에서도 Position encoding 추가해준다. 

### Q4) Linear Attention
- k * v를 먼저 해주고 q를 해주는데 정확하게 잘 모르겠어서 찾아보았다.
> Vanilla attention의 시간복잡도를 O(N^2)으로 만드는 주범 중 하나는 softmax입니다. query와 key vector들의 (scaled) dot-product를 취하고, scaling을 한 뒤에, 각 query마다 softmax를 취해서 query별 key의 attention probability를 계산하고, 이를 weight으로써 value vector들의 weighted average를 취함으로써 attention layer의 output이 얻어집니다. 하지만, 잘 생각해보면, 굳이 softmax 함수를 써서 attention probability를 구해야 할 이유는 없습니다. 이러한 점에서 착안하여, softmax를 다른 함수로 대체한 뒤 여기서 약간의 "트릭"을 이용해서 시간복잡도를 O(N)으로 줄인 것이 바로 Linearized Attention입니다. (참고 링크 : https://seewoo5.tistory.com/5)
<p align="center">
   <img src='./DDPM_study/Linear Attention.png', alt="compare"  width="400" />
</p>

> 위의 식에서 합에 들어있는 부분은 query와 상관없는 값이기 때문에 미리 O(N)만에 계산해 놓고 각 query마다 미리 계산된 값을 이용해서 attention layer의 output을 계산하면 되기 때문에 총 시간복잡도가 O(N)으로 줄어들게 됩니다. 공간복잡도 (memory complexity) 역시 분모, 분자의 sum에 해당되는 값을 미리 저장해놓기만 하면 (각각 D by D 혹은 D by N 행렬이기 때문에 N이 D에 비해서 매우 큰 경우 O(1) 혹은 O(N)으로 볼 수 있습니다.) 이 역시 O(N)으로 줄어들게 됩니다. 

### Q5) Noise
- noise와 position encoding에서 혼선이 있었다.
- noise는 각 step 이전의 이미지에 그냥 들어가는 거다. 
- noise 추가된 이미지 = `sqrt_alphas_cumprod_t*x_start + sqrt_one_minus_alphas_cumprod_t*noise`


## MODUPOP 질문 정리
### Q1) β_t는 어떻게 설정하는 것인가요?
- 첫 β_1는 0.001에서 시작하고 β_T는 0.2로 끝을 낸다.
- T = 1000(일반적)
- β를 어떻게 스케쥴링하는가에 따라서 노이즈 변화도 달라진다. 

### Q2) β를 설정하는 기준이 따로 있나? Learnable하게 할 수 없나?
- T를 현재 1000정도로 설정을 했는데, 이 쯤되면 pure한 Gaussian Noise가 되어야 되는데, 이렇게 천천히 noise를 주다가 점점 강하게 noise를 주는 것이 실험적으로 좋아서 그러지 않았을까 싶다. 
- (지혜 님) beta는 learnable parameter로 둘 수도 있지만, 실험을 해보니 상수로 두었을 때랑 별차이 없어서(성능차이) 그냥 constant로 두었다고 논문에 나왔던 것 같습니다

### Q3) cosine scheduling을 사용하는 이유?
- 이것도 실험적인 결과
