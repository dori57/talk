[README.md](https://github.com/user-attachments/files/33380970/README.md)
# 소나기 소년과 대화하는 웹앱

황순원 「소나기」의 소년과 대화한 뒤 작품 근거를 비교하고 감상 노트를 작성하는 Streamlit 앱입니다. 대화 시점은 소년이 소녀의 죽음을 알게 된 뒤이며 결말을 포함합니다.

## 1 앱 파일 준비

이 폴더의 `app.py`가 앱 코드이며 `requirements.txt`가 배포에 필요한 패키지 목록입니다. `.streamlit/config.toml`은 화면 색상 설정으로 선택 사항입니다. API 키는 파일에 포함되어 있지 않습니다.

키 없이 실행하면 미리 작성된 네 가지 예시 질문과 답변으로 체험합니다. AI 자유 대화는 서버에 API 키를 설정하면 사용할 수 있습니다. 예시 답변과 AI 답변은 원문 대사가 아닌 가상 답변입니다.

## 2 GitHub에 올리기

1. GitHub에 로그인하고 새 저장소를 만듭니다.
2. ZIP을 압축 해제합니다. ZIP 자체가 아니라 `app.py`와 `requirements.txt`를 저장소의 맨 위에 올립니다.
3. 선택적으로 `.streamlit/config.toml`과 `.gitignore`도 올립니다.
4. 태블릿에서는 Add file → Create new file로 파일을 하나씩 만들고 내용을 붙여넣습니다. 파일명은 정확히 `app.py`, `requirements.txt`로 지정합니다.

## 3 Streamlit Cloud 배포

1. https://share.streamlit.io 에 접속하고 GitHub 계정을 연결합니다.
2. 새 앱 생성 화면에서 저장소와 브랜치를 선택합니다.
3. Main file path를 `app.py`로 지정합니다.
4. Deploy를 실행합니다. 완료된 주소로 앱을 열어 봅니다.

## 4 AI 자유 대화 설정

Streamlit Cloud의 앱 설정에서 Secrets에 다음을 넣습니다.

```toml
OPENAI_API_KEY = "발급받은_API_키"
OPENAI_MODEL = "gpt-4.1-mini"
```

예시 문자열은 실제 키로 바꾸세요. 키는 GitHub나 `app.py`에 넣지 않습니다. 로컬 실행 시에는 `.streamlit/secrets.toml`에 위 내용을 저장하거나 `OPENAI_API_KEY` 환경변수를 설정합니다. 모델은 계정에서 접근 가능한 Responses API 및 Structured Outputs 지원 모델로 바꿀 수 있습니다.

AI API 이용은 ChatGPT 구독과 별개로 비용이 발생할 수 있습니다. AI 모드에서 질문과 최근 12번의 문답, 교사 제공 자료가 OpenAI에 전송됩니다. 앱은 `store=False`로 응답을 요청합니다. 이 설정이 모든 제공자 로그나 보존 정책을 없앤다는 뜻은 아닙니다.

## 5 수업에서 활용하기

1. 예시 모드에서 네 가지 질문을 눌러 대화 화면을 확인합니다.
2. 각 답변 아래의 관련 장면과 해석 구분을 펼쳐 원문과 비교합니다.
3. AI 설정 후에는 자유롭게 후속 질문을 이어 갑니다.
4. 감상 노트에 인물 이해, 원문 근거, 가상 답변과의 비교를 적고 저장합니다.
5. 복습 탭에서 비어 있는 항목과 원문 확인 여부를 살펴봅니다.
6. 기록을 내려받습니다. 대화와 노트는 현재 접속 세션에만 저장되므로 새 세션에서는 유지되지 않습니다.

교사용 자료 설정에서 발췌문이나 장면 정리를 입력할 수 있습니다. 해당 접속 세션에만 적용되며 자료를 바꾸면 이전 대화와 노트를 초기화합니다. 모든 학생에게 같은 자료를 제공하려면 `app.py`의 `SCENES`를 수정한 뒤 다시 배포합니다.

## 6 테스트 후 수정하기

다음을 확인하고 문제가 있으면 해당 질문과 답변을 AI에게 전달해 `app.py` 수정을 요청하세요.

- 자료에 없는 사건이나 소녀의 속마음을 사실처럼 말하는가
- 소년이 모르는 의학적 사망 원인 등을 단정하는가
- 관련 장면과 답변의 연결이 적절한가
- 예시 질문, 후속 대화, API 오류 안내, 감상 노트, 기록 다운로드, 초기화가 작동하는가

복습 기능은 입력 누락과 원문 확인 표시를 점검합니다. 해석의 옳고 그름을 자동 채점하지 않습니다. 근거 ID 검증은 등록된 자료 ID인지 확인할 뿐, 답변의 사실성을 보장하지 않습니다. 수업에서 사용하는 판본으로 교사가 장면 요약과 AI 답변을 검토하세요.

## 로컬 실행

```bash
python -m pip install -r requirements.txt
streamlit run app.py
```

## 구현 참고 문서

- Streamlit 채팅 앱: https://docs.streamlit.io/develop/tutorials/chat-and-llm-apps/build-conversational-apps
- Streamlit Cloud Secrets: https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/secrets-management
- OpenAI Python SDK: https://developers.openai.com/api/reference/python
- 사용 모델: https://developers.openai.com/api/docs/models/gpt-4.1-mini
