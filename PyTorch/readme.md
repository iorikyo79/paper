# 1. DataParallel 사용시 주의사항
- DataParallel로 감싸진 모델을 저장하면, 모든 매개변수 이름에 'module.' 접두사가 붙음
- 이때, 모델의 상태 사전은 model.state_dict()로 저장
- **Multi-GPU로 학습이 아니라면 DataParallel을 사용하지 말자**

## DataParallel 모델 저장 및 로드 예제
1. DataParallel로 모델 학습 및 저장
```bash
import torch
import torch.nn as nn

# 예시 모델 정의
class MyModel(nn.Module):
    def __init__(self):
        super(MyModel, self).__init__()
        self.fc = nn.Linear(10, 10)

    def forward(self, x):
        return self.fc(x)

# 모델 생성 및 DataParallel로 감싸기
model = MyModel()
model = nn.DataParallel(model)
# 모델을 학습하고 저장
torch.save(model.state_dict(), 'model_dataparallel.pth')
```

2. DataParallel 모델 로드 및 Single GPU로 학습
```
# 모델 생성
model = MyModel()

# 상태 사전 로드
state_dict = torch.load('model_dataparallel.pth', map_location=torch.device('cuda'))

# 상태 사전에서 'module.' 접두사 제거
from collections import OrderedDict
new_state_dict = OrderedDict()
for k, v in state_dict.items():
    if k.startswith('module.'):
        name = k[7:]  # remove 'module.' prefix
        new_state_dict[name] = v
    else:
        new_state_dict[k] = v

# 모델에 상태 사전 로드
model.load_state_dict(new_state_dict)

# 모델을 GPU로 이동
model = model.cuda()

# 모델 학습 (추가 학습)
# 여기서 model은 이제 Single GPU로 학습됨
optimizer = torch.optim.Adam(model.parameters(), lr=1e-5)
# ... 추가 학습 코드 ...
```

# 2. torch.load()
## 2.1 torch.load('model.pth')에서 내부적으로 일어나는 일들
- **파일 읽기**: torch.load는 지정된 파일 경로에서 저장된 데이터를 읽음. 이 파일은 보통 모델의 가중치(state_dict), 옵티마이저 상태, 기타 학습 관련 정보 등을 포함할 수 있는 딕셔너리임.
- **데이터 역직렬화**: 파일에서 읽은 **데이터를 PyTorch 객체로 변환**. PyTorch는 데이터를 저장할 때 직렬화(serialization) 과정을 거쳐 저장하며, torch.load는 이를 다시 역직렬화(deserialization)하여 원래의 PyTorch 객체로 복원.
- **딕셔너리 반환**: 이 과정이 끝나면 **파일의 내용을 담고 있는 딕셔너리를 반환**. 이 딕셔너리에는 모델의 상태 사전(state_dict), 옵티마이저 상태 등이 포함.


## 2.2 load_state_dict 에서 내부적으로 일어나는 일들
```
model.load_state_dict(state_dict)
```
- 상태 사전 검사: load_state_dict는 전달받은 딕셔너리가 모델의 현재 아키텍처와 호환되는지 확인. 즉, 딕셔너리의 키(매개변수 이름)와 모델의 매개변수 이름이 일치하는지 확인.
- 매개변수 로드: 일치하는 경우, 딕셔너리에 저장된 값을 모델의 매개변수와 버퍼에 할당.
- 모델 업데이트: 모델의 모든 학습 가능한 매개변수(nn.Parameter 객체)와 버퍼가 전달받은 딕셔너리의 값으로 업데이트.
