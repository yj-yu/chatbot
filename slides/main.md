name: inverse
class: center, middle, inverse
layout: true
title: chatbot

---
class: titlepage, no-number

# 챗봇 만들기
## .gray.author[Youngjae Yu]

### .x-small[https://github.com/yj-yu/chatbot]
### .x-small[https://yj-yu.github.io/chatbot]

.bottom.img-66[ ![](images/snu-logo.png) ]

---
layout: false

## About

- 챗봇이란?
- 챗봇 쉽게 만들기
- DialogFlow
- Webhook
- Chatterbot
- Flask 서버 만들기
- SNS 연동하기
- Tensorflow 로 챗봇 강화하기
- 챗봇 개선


---

template: inverse

# 챗봇이란?

---

## 심심이

- 사람들이 말을 하면 대답, 응답을 사람들이 가르쳐 줌

.center.img-40[ ![](images/chatbot1.jpg) ]


---

## 카카오 플러스 친구

- 쉽게 챗봇을 만들자

.center.img-80[ ![](images/kakaobot.png) ]


---

## 챗봇 platform

- 다양한 챗봇 빌더 서비스 제공
- API 연동으로 간편하게 해결

.center.img-80[ ![](images/chat_platform.png) ]


- 어떤 서비스를 골라야 할까?

---

## 챗봇 platform 추천?

- 여러 서비스들과 호환성이 좋고
- 강력한 인공지능 / ML 기능을 제공하고 (목소리 인식, 유사도 측정, 감정 분석 등등)
- 쉽게 학습시킬 수 있어야 한다
- 그래서..

.center.img-40[ ![](images/df_logo.png) ]


---

## DialogFlow

- 무료 이용 가능
- 한글 자연어처리 지원
- 비교적 커뮤니티에서 선호, 자료 검색 용이
- 강력한 '구글' 의 지원, 발전 가능성 높음

---


## DialogFlow

- https://dialogflow.com/
- 가입 후 프로젝트 페이지 접속

.center.img-80[ ![](images/dialogflow.png) ]

---

## DialogFlow


- en, ko, cn 등 여러 언어 선택 (다수) 가능
- ko 로 선택, 시간대 설정

.center.img-80[ ![](images/create.png) ]

---
## DialogFlow

- Intent
- Entities
- Knowledge Bases
- Fulfillment
- Training
- History
- Analytics

.center.img-60[ ![](images/menu.png) ]


---
## DialogFlow

- Intents
	- 문장의 의도 및 대답 처리

.center.img-80[ ![](images/menu.png) ]

---
## DialogFlow

- Entities
	- 문장안에 들어있는 개체 정보
	- 일반적인 개념 symbol화, 문장에서 추출하는 핵심 단어
	- 같은 항목에 동의어를 여러개 입력

.center.img-80[ ![](images/entities.png) ]

---
## DialogFlow

- Knowledge Bases
	- 웹페이지나 문서에서 정보를 찾아 대답. 
	- Wiki 등 외부 사이트 참조

.center.img-80[ ![](images/knowledge.png) ]

---
## DialogFlow

- Fulfillment
	- 외부 서버와 API로 정보를 주고받음. Webhook.
	- Inline editor 제공

.center.img-80[ ![](images/fulfillment.png) ]

---
## DialogFlow

- Integrations
	- 메신저나 웹, 음성비서와 연동.
	- Slack, Facebook 등 messenger app 다수 지원

.center.img-80[ ![](images/intergrations.png) ]

---
## DialogFlow

- Training / History
	- 대화했던 내용들에 대해 장려하거나 새로운 대답을 지정해 줄 수 있음
	- 과거 내용들을 보고, 피드백 하는데 사용

.center.img-80[ ![](images/training.png) ]

---
template: inverse

#  챗봇 생성 서비스 
# DialogFlow 활용


---

## Install configuration

.center.img-80[ ![](images/export.png) ]


```bash
git clone https://github.com/yj-yu/chatbot_practice
```
- 설정 (톱니바퀴 모양) 클릭
- Export and Import 탭 클릭
- Restore from zip 에서 chatbot.zip 불러오기


---
## Entity 설정

- 문장에서 추출하는 핵심 단어,
- 같은 항목에 동의어를 여러개 입력 가능

.center.img-80[ ![](images/entities1.png) ]
.center.img-80[ ![](images/entities2.png) ]

---
## Entity 와 Intent

### Intent
- 노래재생
	- \$ARTIST_NAME 노래 들려줘, \$SONG_NAME 틀어줘
- 노래검색
	- \$ARTIST_NAME 노래 찾고싶어, \$SONG_NAME 검색해줘

### Entity
- 아티스트명	\$ARTIST_NAME
	- 아이유, 방탄소년단, EXO ...

- 곡명	\$SONG_NAME
	- 좋은날, 가을아침, 불타오르네 ...

---
## Intent 설정

- Fallback은 일치하는 의도가 없을때 실행. Welcome은 인사말.
- 현재 Fallback은 인공지능 모델이 간단한 smalltalk을 하도록 설정
- 의도에 따라 다양한 액션 설정 가능 

.center.img-80[ ![](images/intent_1.png) ]

---

## Intent 설정

- 입학 관련 인텐트 추가
	- Training phrases에 예시 문장들을 입력

.center.img-80[ ![](images/intent_2.png) ]

---

## Intent 설정

- 액션 반응 추가
	- 아까 설정한 'entrance_type' 입력. 예문에서 자동으로 엔터티 인식.
	- Required를 설정하면 문장에 엔터티가 없을때 prompt 내용을 질문

.center.img-80[ ![](images/intent_3.png) ]

---

## Intent 설정

- Responses 설정
	- 파라미터에서 정의된 엔터티 변수 사용

.center.img-80[ ![](images/intent_4.png) ]

---

## Intent 설정

- 설정한 intent 실험, save 후 오른쪽에 있는 채팅창 이용
	- Training phrases에 없는 문장도 유연하게 대답
	- 문장에 entity가 없는 경우 prompt 응답 띄움
	- 바로 다음에 entity를 직접 입력하여 응답을 받을 수 있음

.center.img-80[ ![](images/intent_test.png) ]

---

## Intent 설정

- 문장 내에서 intent 뿐만 아니라 entity가 있다면 응답으로 판단

.center.img-80[ ![](images/intent_test2.png) ]

---

## Context & Events

- Context : Intent끼리 통신, 기억해야 할 parameter value를 전달
- Events : 날씨, 날짜, 농담 등 미리 설정된 다양한 google assistance 기능을 응답으로 추가 가능

.center.img-80[ ![](images/context.png) ]

---

template: inverse


# 추가 기능을 자유롭게 만들어 넣을 수 있을까?

---
## Fulfillment

- 외부 서비스나 데이터베이스에 접근

.center.img-80[ ![](images/dialog_concept.png) ]

---
## Fulfillment 설정
- Webhook : 웹(Web)에서 내 서버의 URL을 걸어(Hook)놓음
- Webhook과 Inline Editor 중 선택 가능
- Webhook을 이용해 딥러닝이 돌아가는 GPU 서버의 기능을 가져오겠음
- Webhook을 enabled로 켬

.center.img-80[ ![](images/webhook.png) ]

---
## Webhook

- 특정 작업을 외부에 알림
- 응답을 받아 특정 결과를 받아옴

.center.img-80[ ![](images/webhookflow.png) ]




---
## Webhook 파이썬으로 서버 구현하기

```bash
pip install flask
```
- flask 설치

```python
from flask import Flask, request
app = Flask(__name__)

@app.route("/webhook", methods=['post'])
def webhook():
	data = request.get_json()
	return 'success'
	
	
if __name__ == '__main__':
    app.run(host='0.0.0.0')
```
- flask 이용한 웹훅 
	- 'data'로 요쳥을 받고
	- 'success'를 내보낸다.

---
```python
from flask import Flask, request
app = Flask(__name__)

@app.route("/webhook", methods=['post'])
def webhook():
	data = request.get_json()
	#
	# 이 부분에서	
	# Chat bot code 로 data (대화) 를 받아 answer (응답) 을 출력
	#
	#
if __name__ == '__main__':
    app.run(host='0.0.0.0')
```
- chatbot 코드를 넣으면 끝!

---

template: inverse

#  챗봇 생성 서비스 
# 간단한 Chatterbot


---

# Chatterbot 

- 간단한 MachineLearning 알고리즘을 사용한 빠른 opensource 챗봇
- 단어 기반 유사도를 측정하기 때문에 굉장히 빠른 반응속도
- API를 간단하게 pip 명령을 통해 설치 가능

```bash
pip install chatterbot
```

- https://github.com/gunthercox/ChatterBot

.center.img-80[ ![](images/cb.png) ]

---

# Chatterbot
```bash
vi chatbot_training.py
```

```python
 from chatterbot import ChatBot
 from chatterbot.trainers import ChatterBotCorpusTrainer

 # Create a new chat bot named yj
 chatbot = ChatBot('yj') 
 # Create a new Trainer
 trainer = ChatterBotCorpusTrainer(chatbot)

 trainer.train(
     "./my_corpus/korean/"  # 트레이닝할 대화 위치
 )

 # The following loop will execute each time the user enters input
 while True:
     try:
         user_input = input()
         bot_response = chatbot.get_response(user_input)
         print(bot_response)
     # Press ctrl-c or ctrl-d on the keyboard to exit
     except (KeyboardInterrupt, EOFError, SystemExit):
         break
```

---

# Chatterbot

```python
cd my_corpus/korean
ls
```
- food.yml 예제 (원하는 대화 데이터들을 형식에 맞게 준비)

.center.img-50[ ![](images/chat_training.png) ]

---

# Chatterbot

```python
cd my_corpus/korean
ls
```
- 아주 간단한 예로 custom.yml을 준비
- 같은 형식으로 질문과 답을 적어보세요.

.center.img-50[ ![](images/chat_training2.png) ]

---

# Chatterbot

- 트레이닝 
```python 
#chatbot_training.py
   1 from chatterbot import ChatBot
   2 from chatterbot.trainers import ChatterBotCorpusTrainer
   3 # Create a new chat bot
   4 chatbot = ChatBot('yj')
   5 # Create a new Trainer
   6 trainer = ChatterBotCorpusTrainer(chatbot)
   7 trainer.train(
   8     "./my_corpus/korean/"
   9 )
  10 # The following loop will execute each time the user enters input
  11 while True:
  12     try:
  13         user_input = input()
  14         bot_response = chatbot.get_response(user_input)
  15         print(bot_response)
  16         # Press ctrl-c or ctrl-d on the keyboard to exit
  17     except (KeyboardInterrupt, EOFError, SystemExit):
  18         break
```
- 입력을 아무거나 쳐보세요 

---

# Chatterbot

- 서버 띄우기
```python 
 #app_simple.py              
   1 import os
   2 import sys
   3 import requests
   4 import json
   6 from flask import Flask, request, make_response, jsonify
   8 from chatterbot import ChatBot
   9 from chatterbot.trainers import ChatterBotCorpusTrainer
  10 # Create a new chat bot named *
  11 chatbot = ChatBot('yj')
  17
  18 def pred(inputString):
  19     answer = chatbot.get_response(inputString)
  20     return answer
  21
  22 app = Flask(__name__, template_folder='./')
  27
  28 @app.route('/webhook', methods=['GET','POST'])
```
---

# Chatterbot

- 서버 띄우기
```python 

  29 def webhook():
  30     req = request.get_json(force=True)
  31     #print(req)
  32     print(req)
  33     response = str(req['queryResult']['queryText'])
  34     print(response)
  35     response = pred(response)
  36     response = {'fulfillmentText':str(response)}
  37     return response
  38
  39 if __name__ == '__main__':
  40     app.run(port=11111,debug=True,threaded=True)
```
- Port 11111 에 서버가 준비됩니다.
- ngrok 설치하여 public web server로 만들어야 통신이 가능.
---

## ngrok 설치

https://ngrok.com/download

.center.img-80[ ![](images/ngrok.png) ]

- 자신의 컴퓨터 os 에 맞는 ngrok 설치.
- Windows 클릭

```bash
./ngrok http 11111
```

---
## ngrok 설치

.center.img-50[ ![](images/ngrok_term.png) ]

- 다음과 같은 화면이 나오면, https 부분 복사 후 DialogFlow 사이트의 webhook url에 입력

.center.img-50[ ![](images/webhook.png) ]


---

template: inverse

# DialogFlow 프로젝트 페이지에서 
# 직접 테스트 해보세요
# 그리고 추가하고 싶은 대화문을 넣어 
# 트레이닝 후 재실행해 보세요.


---




template: inverse

#  챗봇 생성 서비스 
# SNS 연결하기


---

## SNS service 연동

- 카카오톡, 페이스북, 트위터, 텔레그램, slack 등등 서비스들에 쉽게 연동 가능
- 현재 카카오톡은 openbuilder 정비로 API 신규 사용을 막아 놓음
- 실습환경에 적합치 않으므로 페이스북 메신저로 대체

- 링크 이동
	- m.me/103223574516899
	- 한국어 대화 데이터가 적어 아직 완벽하지는 않음

.center.img-50[ ![](images/platform.png) ]


---

.center.img-50[ ![](images/app_demo.png) ]


---

## 연동하기

- Integrations menu의 Facebook Messenger 를 클릭

.center.img-50[ ![](images/integration2.png) ]

- https://tutorials.botsfloor.com/dialogflow-tutorial-create-facebook-messenger-bot-using-dialogflow-integration-bc77125dff00
- 이 페이지를 참고했습니다.

---

- https://www.facebook.com/pages/ 로 가서 페이지 만들어 봅니다.

.center.img-50[ ![](images/fb1.png) ]

- 페이지 타입 선택하고 시작

.center.img-50[ ![](images/fb2.png) ]

---

- 이름 적당히 지어보세요

.center.img-50[ ![](images/fb4.png) ]

- https://developers.facebook.com/apps/ 로 가서 이 페이지랑 연결할 페이스북 앱을 만듭니다.

.center.img-50[ ![](images/fb3.png) ]

---

- 만드시면서, 저 페이지는 스킵해 주세요.

.center.img-50[ ![](images/fb5.png) ]

- Product 옆에 + 버튼을 누르고 메신저를 추가해주세요.

.center.img-50[ ![](images/fb6.png) ]

---

- 아까 만든 페이지를 선택해 주세요.

.center.img-50[ ![](images/fb7.png) ]

- Page Access Token이 생성되었습니다. 이걸 dialogflow에 알려줘야 합니다.

.center.img-50[ ![](images/fb8.png) ]

---


- Dialogflow의 Integration tab으로 갑니다. 페이스북 메신저를 팝업합니다.

.center.img-50[ ![](images/fb9.png) ]

---

- verifytoken은 비밀번호같은거에요. 아무거나 입력해주고 기억해 둡니다. 
- Page access token 넣고 start를 누릅니다.

.center.img-50[ ![](images/fb10.png) ]

---


- 페이스북으로 돌아와서, 세팅에서 웹훅 셋업을 눌러줍니다.

.center.img-50[ ![](images/fb11.png) ]

- 아까 dialogflow에서 제공해주던 callback url과 입력하셨던 verify token을 넣어줍니다.
- message 와 messaging_postbacks를 구독해 줍니다.

.center.img-40[ ![](images/fb12.png) ]

---

- 웹훅 구독을 눌러줍니다.

.center.img-50[ ![](images/fb18.png) ]

- 세팅 -> 기본으로 가서 필수 정보들을 채워줍니다.

.center.img-50[ ![](images/fb13.png) ]

---


- 윗쪽의 On/Off 로 되어있는 앱 활성화를 눌러줍니다.

.center.img-40[ ![](images/fb14.png) ]

- 페이스북 페이지로 가서 버튼을 추가합니다.
- 여기서 메시지 보내기, 메신저 앱을 선택해 등록해 줍니다.

.center.img-40[ ![](images/fb15.png) ]

- 메시지를 보내 테스트 해 봅시다.

---


template: inverse

# 직접만든 인공지능 챗봇
# Tensorflow 로 챗봇 강화하기


---

## Tensorflow?

1. Build graph
2. Feed data and run
3. Update graph

.center.img-66[ ![](images/TF.png) ]


---

## 인공지능 활용 코드 넣기

- 이 부분은 GPU 서버가 필요합니다. 
- 화면 시청 실습 및 직접 설명으로 대체하겠습니다.
- Tensorflow Keras를 이용해 간단한 모델을 CPU에서 학습해 봅니다.
	- https://github.com/deepseasw/seq2seq_chatbot

---


template: inverse

# 챗봇 개선


---

## 유용한 링크들

- https://cloud.google.com/solutions/building-chatbot-agent-dialogflow?hl=ko
- https://medium.com/@jwlee98/gcp-dialogflow-%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EA%B0%84%EB%8B%A8-%EC%B1%97%EB%B4%87-%EB%A7%8C%EB%93%A4%EA%B8%B0-514ea25e4961
- (주문 챗봇 만들기) https://codevkr.tistory.com/74
- (영화예매 챗봇 만들기) https://m.blog.naver.com/PostView.nhn?blogId=spring1a&logNo=221386879776&proxyReferer=https%3A%2F%2Fwww.google.co.kr%2F
- 다양한 팁 공유 https://ndb796.tistory.com/116 


---



name: last-page
class: center, middle, no-number
## Thank You!


<div style="position:absolute; left:0; bottom:20px; padding: 25px;">
  <p class="left" style="margin:0; font-size: 13pt;">
  <b>Please visit my website</b>: https://yj-yu.github.io/home/ /p>
</div>

.footnote[Slideshow created using [remark](http://github.com/gnab/remark).]




<!-- vim: set ft=markdown: -->
