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

---

# 한국어 데이터로 챗봇 만들기 프로젝트


- 코더 : 최예나
- 리뷰어 : 김성진


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [O] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네, 정상적으로 잘 작동합니다.
- [O] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네, 잘 주석과 헤더로 잘 이해됩니다.
- [O] 코드가 에러를 유발할 가능성이 없나요?
  > 네, 없습니다.
- [O] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 코드 흐름이 잘 이어져 있어 그렇게 판단됩니다.
- [O] 코드가 간결한가요?
  > 네, 모듈마다 헤더로 구분되어 있고, 간결하게 짜여져 있습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.

- 모듈별 헤더와 주석

```markdown
## Step 2. 데이터 전처리하기
### 전처리 함수 작성 (데이터셋 가공)
#### 정규 표현식(Regular Expression)을 사용하여 구두점(punctuation)을 제거하고, 이를 통해 단어 토크나이징(tokenizing)에 방해가 되지 않도록 정제함을 목표로 함.
```

```python
# 전처리 함수

import re

def preprocess_sentence(sentence):    
    sentence = sentence.lower().strip() # 입력받은 sentence를 소문자로 변경하고 양쪽 공백을 제거

    # 단어와 구두점(punctuation) 사이의 거리를 만듦.
    sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
    sentence = re.sub(r'[" "]+', " ", sentence)

    # (한글, 알파벳, 숫자 ".", "?", "!", ",")를 제외한 모든 문자를 공백으로 대체
    sentence = re.sub(r"[^가-힣a-zA-Z0-9?.!,]+", " ", sentence)
    sentence = sentence.strip()
    return sentence

```


# 참고 링크 및 코드 개선

- 저의 같은 경우 최대 단어 길이를 조정했더니, 정확도가 좀 더 올라갔습니다.
  - 분포도를 보시고, 최대 길이를 줄여주면 정확도가 더 올라갈 수도 있을 것 같습니다.
  - 예나님 코드에서 최대 길이 10으로 줄이고, 20 에포크를 돌려봤는데, 63% 정도까지 올라가네요.

```python
plt.hist(question_len) # 길이 히스토그램

# 샘플의 최대 허용 길이 또는 패딩 후의 최종 길이
MAX_LENGTH = 10
print(MAX_LENGTH)
```