## PyTorch 모델을 ONNX 형식으로 추출하는 방법

### ONNX란?
　ONNX는 Open Neural Network Exchange의 약어로, 머신러닝·딥러닝에서 자주 사용되는 표준 포맷입니다.  
　Pytorch나 Keras 같은 머신러닝 프레임워크 등에서 추출할 수 있으며, ONNX Runtime이나 TensorRT, ailia SDK에 특화된 SDK를 사용해서 에지 환경을 포함한 다양한 환경에서 모델을 사용한 예측을 가능케 합니다.

### PyTorch에서 추출하는 방법
　PyTorch로 작성한 모델을 ONNX 형식으로 추출하는 순서는 매우 간단합니다. 예를 들어, 이 책의 11.8절에서 사용한 모델을 통해 추출해보겠습니다.  
　11.8절에서 학습이 끝난 상태로 아래의 코드를 셀에 추가해서 실행해보기 바랍니다.

```py3
# 더미 데이터 작성
dummy_input = torch.randn((1, 3, 32, 32)).to(device)

# onyx형식으로 export
# keep_initializers_as_inputs 옵션이 중요하며, 이것이 없으면 에러가 발생함
torch.onnx.export(net, dummy_input, "cifar10-pytorch-sample.onnx", 
                  keep_initializers_as_inputs=True, verbose=True)

```

　이것으로, Google Colab의 로컬 디렉터리에 ``cifar10-pytorch-sample.onnx``이라는 ONNX 형식의 파일이 생겼을 것입니다.  
　그 다음은


```py3
from google.colab import files
files.download('cifar10-pytorch-sample.onnx')
```

처럼, 파일을 PC로 다운로드한 다음, 필요에 따라 이 파일을 다른 환경으로 디플로이하는 식입니다.
다운로드에 꽤 긴 시간이 걸리는 점에 주의하기 바랍니다.

### ONNX 파일의 사용 예시
　추출 후 ONNX 파일을 배포(deploy)하는 순서는 실행 환경에 따라 다르므로, 아래의 가이드를 참조하기 바랍니다.  
　일례로, IBM사의 퍼블릭 클라우드인 Watson Studio에서 배포하는 순서는 qiita에 내용을 기재해 두었으니 참고하기 바랍니다.

[PyTorchのDL ModelをWatson MLで動かす](https://qiita.com/makaishi2/items/641466cbe99ad9575df3) (일본어)

<hr>

[메인 페이지로 돌아가기](../README.md)
