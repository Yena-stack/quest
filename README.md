- 코더 : 최예나
- 리뷰어 : 최한준


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  - 다만, 최종적으로 좋은 성능을 내는 척도 중 RMESLE loss 대신 RESE loss를 사용했습니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 위 항목에 대한 근거 작성 필수
- [O] 코드가 에러를 유발할 가능성이 없나요?
  >위 항목에 대한 근거 작성 필수
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 위 항목에 대한 근거 작성 필수
- [O] 코드가 간결한가요?
  > 위 항목에 대한 근거 작성 필수

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.

# 참고 링크 및 코드 개선

```python
# 지금 구현된 부분은 RMSLE라고 썼지만, RMSE인 듯 하다.
def rmsle(y, y_pred):
    return np.sqrt(mean_squared_error(y, y_pred))
def rmse_expm1(y, y_pred):
    return np.sqrt(mean_squared_error(np.expm1(y), np.expm1(y_pred)))

# 수정
def rmsle(predicted, actual):
    # 예측 값과 실제 값의 로그를 취합니다.
    predicted = np.log1p(predicted)
    actual = np.log1p(actual)
    
    # 예측 값과 실제 값의 제곱 오차를 계산합니다.
    squared_error = np.square(predicted - actual)
    
    # 제곱 오차의 평균을 계산합니다.
    mean_squared_error = np.mean(squared_error)
    
    # 평균 제곱 오차의 제곱근을 구합니다.
    rmsle_score = np.sqrt(mean_squared_error)
    
    return rmsle_score
```