# GPU 온도는 최대한 70도 이하를 유지
- 스펙상으로 90도 이상도 가능하지만 장시간 유지시 gpu 수명에 문제 생길수 있음



# 우분투에서 GPU 사용량 실시간 확인
```shell
# 1. 1초마다 nvidia-smi 명령을 실행 시킨다.
nvidia-smi -| 1

# 2. 0.5초마다 nvidia-smi 화면을 갱신한다 (-n)
watch -d -n 0.5 nvidia-smi     # 수정되는 부분만 강조 (d)

# 3. 학습도중 취소시 GPU의 PID가 남을 경우 강제 삭제
kill -9 PID
```
