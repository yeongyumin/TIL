# 삶 속에서의 통계학

## 확률 분포 편

### Ep1: 사람의 특징과 확률 분포

- 너는 혼혈인데 왜 안이쁘니?
  - 아는 지인에게서 자신의 친구가 저러한 이야기를 들었다고 한다.
  - 물론 저렇게 타인에게 이야기하는 것 자체도 실례이다.
  - 하지만 통계학적으로 "너는 혼혈인데 왜 안이쁘니?" 라는 말은 확률 분포를 잘 이해하지 못했기 때문에 발생하는 논리적 오류이다.
  - 어떠한 절대적인 이쁨이 있다고 가정하고, 이를 0 ~ 100사이의 양의 실수를 이용해서 나타낼 수 있다고 하자.
  - 그럴 때 우리는, x축이 절대적 이쁨도, y축이 그렇게 될 확률을 기준으로 확률 밀도 함수를 작성할 수 있다.
  - 물론 이 분포는 일반 한국인과는 다르게, 우리가 혼혈은 경험적으로 더 이쁠 확률이 높다는 것을 알 수 있는 것 처럼, 오른쪽으로 봉우리가 치우쳐진 보아뱀 곡선을 그릴 수 있을 것이다.
  - 여기서 알 수 있는 것은, 언제까지나 이쁨도가 낮은 사람도 존재할 수 있다는 사실이다. 물론 그 확률은 다소 낮을 수 있다.
  - 따라서 "너는 혼혈인데 왜 안이쁘니?" 라고 말한 것은, 혼혈은 반드시 이뻐야한다는 오류에 빠져서, 혼혈 절대 이쁨도가 낮은 사람도 있을 수 있다는 확률을 고려하지 않은 것이 된다.
- 감상
  - 우리가 평소에 생각하는 것들을 통계적 관점으로 생각해보면 오류일 때가 다소 존재한다. 그것을 잘 캐치해서 최대한 논리적으로 의사결정을 할 수 있도록 하면, 보다 나은 의사선택을 할 수 있지 않을까 싶다.

## 통계적 추정 편

### Ep1: 스시집 뽑기의 당첨 확률을 몇퍼센트일까?

- 배경
  - 일본의 쿠라스시에는 스시 5접시마다 1회 장난감 뽑기 찬스가 있음
  - 나와 지인이 함께 스시집을 가면 보통 20접시를 먹음
    - 10번 갔을때, 7번은 꽝이 되고
    - 10번 갔을때, 3번은 당첨이 됨
  - 그렇다면 스시집 뽑기의 당첨 확률은 몇 퍼센트일까?
- 관점
  - 애초에 5번에 한 번 정도 뽑힐 수 있도록 프로그램을 해둠
    - 분명히 가능성이 있음
  - **정말로 확률적으로 정해져있음**
    - 우리는 이 경우에 초점을 맞춰서 생각해보자
- 생각
  - 경우1
    - 예를들어, 뽑기의 꽝이 될 확률 `p`를 `0.6(즉 60%)`이라고 가정하자
    - 그러면 나와 지인은 20접시를 먹으므로 총 4번의 기회가 주어지는데, 대게(70% 확률)는 꽝
    - 여기서 4번다 꽝일 확률은 매번의 뽑기가 독립이라면, `0.6 * 0.6 * 0.6 * 0.6 = 0.1296` 즉, 13% 밖에 되지 않으므로 이는 70%와는 충분히 많은 차이를 보인다.
    - 물론 13%의 확률이 우연적으로 계속 나왔다 라고 생각할 수 있지만, 이는 통계적으로 거의 나오기 힘들다.
      - 사실 여기서 13%의 확률로 참인 경우 나와 지인이 직접 방문한 횟수 n번 시행했을 때 70%의 참의 결과가 나올 확률을 계산해서 그 값의 검정을 해야 엄밀하게 올바르다.
      - e.g
        - 10번 방문했을 때, 13%의 확률로 7번이 참이 될 확률은?
        - 이항분포에 따르면 거의 0에 가까움(p=0.13, x=7)
    - 따라서 가설을 기각할 수 있다.
  - 경우2
    - 예를들어, 뽑기의 꽝이 될 확률 `p`를 `0.9(즉 90%)`라고 가정하자.
    - 뽑기가 모두 꽝이 될 확률은 `0.9 * 0.9 * 0.9 * 0.9 = 0.65` 즉 65% 가 된다
    - 여기서 이항분포에 의하여 65%의 확률로 10번의 방문 중 7번이 꽝일 확률은 `0.25`즉, 25%이다.
    - 이는 자기자신이 정한 5%의 오차 수준의 범위 내에 있음(그렇게 될 확률이 5%이하이면 가설을 기각)
    - 그렇다면 충분히 가설을 채택할 수 있음
      - 사실은 가설을 기각할 수 없다가 맞음
- 결론
  - 이렇게 어떠한 가설의 확률을 p 라고 두고, 그 가설이 참이라고 두었을 때, 많은 경험적 시행을 해서 그 결과가 될 확률을 q라고 했을 때, q가 미리 정한 채택 기준 확률(a) 보다 더 크다면 그 가설은 기각 할 수 없으며, 그 확률 a보다 작다면 그 가설은 기각 된다.
  - 이는 통계적 추정
- 감상
  - 통계학은 우리의 일상에서도 이렇게 찾아볼 수 있어서 너무 재미있었다. 사실 칸아카데미에서 들었던 수업의 설명이 너무 적절했다. 그리고, 그것을 TIL에 적어 둔 덕분에 이러한 발상이 생겼다고 생각한다. 뜬금없이 스시먹다가 말이다.