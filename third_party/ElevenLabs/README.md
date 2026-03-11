# ElevenLabs <> Claude 쿡북

[ElevenLabs](https://elevenlabs.io/)는 음성 복제 및 스트리밍 합성 같은 고급 기능을 갖춘, 자연스러운 목소리의 음성 애플리케이션을 만들기 위한 AI 기반 음성 인식(STT) 및 음성 합성(TTS) API를 제공합니다.

이 쿡북은 ElevenLabs의 음성 처리와 Claude의 지능적인 답변을 결합하여 실시간 성능을 위해 점진적으로 최적화된 저지연(Low-latency) 음성 어시스턴트를 구축하는 방법을 보여줍니다.

## 포함된 내용

* **[저지연 음성 어시스턴트 노트북(Low Latency Voice Assistant Notebook)](./low_latency_stt_claude_tts.ipynb)** - 음성 어시스턴트를 단계별로 구축하는 과정을 안내하는 대화형 튜토리얼로, 스트리밍을 통해 지연 시간을 최소화하는 다양한 최적화 기술을 보여줍니다.

* **[WebSocket 스트리밍 스크립트(WebSocket Streaming Script)](./stream_voice_assistant_websocket.py)** - 지속적인 마이크 입력, 끊김 없는 오디오 재생, WebSocket 스트리밍을 사용한 최저 지연 시간을 특징으로 하는 프로덕션 준비 수준의 대화형 음성 어시스턴트입니다.

## 이 쿡북 사용법

이 쿡북을 최대한 활용하려면 다음 순서를 따르는 것을 권장합니다:

### 1단계: 환경 설정

1. **가상 환경 생성:**
   ```bash
   # ElevenLabs 디렉토리로 이동
   cd /path/to/claude-cookbooks/third_party/ElevenLabs

   # 가상 환경 생성
   python -m venv venv

   # 활성화
   source venv/bin/activate  # macOS/Linux의 경우
   # 또는
   venv\Scripts\activate     # Windows의 경우
   ```

2. **API 키 확보:**
   - **ElevenLabs API 키:** [elevenlabs.io/app/developers/api-keys](https://elevenlabs.io/app/developers/api-keys)

     API 키를 생성할 때 다음 최소 권한이 있는지 확인하십시오:
     - Text to speech (음성 합성)
     - Speech to text (음성 인식)
     - Read access on voices (목소리 읽기 권한)
     - Read access on models (모델 읽기 권한)

   - **Anthropic API 키:** [console.anthropic.com/settings/keys](https://console.anthropic.com/settings/keys)

3. **환경 구성:**
   ```bash
   cp .env.example .env
   ```

   `.env` 파일을 편집하고 API 키를 추가합니다:
   ```
   ELEVENLABS_API_KEY=your_elevenlabs_api_key_here
   ANTHROPIC_API_KEY=sk-ant-api03-...
   ```

4. **의존성 설치:**
   ```bash
   # venv가 활성화된 상태에서
   pip install -r requirements.txt
   ```

### 2단계: 노트북 실습

**[저지연 음성 어시스턴트 노트북](./low_latency_stt_claude_tts.ipynb)**부터 시작하십시오. 이 대화형 가이드를 통해 다음을 배울 수 있습니다:

- ElevenLabs를 사용하여 음성을 텍스트로 변환(STT)하는 방법
- Claude의 답변을 생성하고 지연 시간을 측정하는 방법
- 스트리밍이 첫 번째 토큰 생성 시간(TTFT)을 줄이는 방법
- 더 빠른 오디오 재생을 위해 음성 합성(TTS)을 스트리밍하는 방법
- 다양한 스트리밍 접근 방식 간의 트레이드오프
- WebSocket 스트리밍이 지연 시간과 품질 사이에서 최상의 균형을 제공하는 이유

노트북은 각 단계에서 성능 지표와 비교를 포함하고 있어, 각 최적화가 미치는 영향을 이해하는 데 도움을 줍니다.

### 3단계: 프로덕션 스크립트 실행

노트북의 개념을 이해한 후, **[WebSocket 스트리밍 스크립트](./stream_voice_assistant_websocket.py)**를 실행하여 완전히 작동하는 음성 어시스턴트를 경험해 보십시오:

```bash
python stream_voice_assistant_websocket.py
```

**작동 방식:**
1. 엔터(Enter) 키를 눌러 녹음 시작
2. 마이크에 대고 질문 말하기
3. 엔터(Enter) 키를 눌러 녹음 중지
4. 어시스턴트가 자연스러운 음성으로 답변
5. 반복하거나 Ctrl+C를 눌러 종료

이 스크립트는 다음 기능을 프로덕션 수준으로 구현한 예시를 보여줍니다:
- sounddevice를 사용한 실시간 마이크 녹음
- 문맥 유지를 통한 지속적인 대화
- 최소 지연 시간을 위한 WebSocket 기반 스트리밍
- 끊김 없는 재생을 위한 맞춤형 오디오 큐(Queue)

## 문제 해결 (Troubleshooting)

### 오디오 튐 또는 잡음 (Popping or Crackling)
**증상:** 재생 중에 가끔 짧은 튐, 클릭음 또는 오디오 끊김이 들릴 수 있습니다.
**설명:** 이는 ElevenLabs 무료 티어에서 요구하는 MP3 형식을 사용하기 때문에 발생합니다. MP3 데이터를 실시간 청크로 스트리밍할 때 FFmpeg이 간혹 디코딩할 수 없는 불완전한 프레임을 받게 됩니다.
**해결책:** 이는 무료 티어에서 MP3 형식을 사용할 때 발생하는 예상된 동작입니다. 완전히 해결하려면 ElevenLabs 유료 티어로 업그레이드하고 스크립트에서 MP3 대신 `pcm_44100` 형식을 사용하도록 수정하십시오.

### API 키 관련 문제
**증상:** `AssertionError: ELEVENLABS_API_KEY is not set` 등의 에러
**해결책:** `.env.example`을 `.env`로 복사했는지, API 키가 올바르게 설정되었는지 확인하십시오.

### 의존성 문제
**증상:** `ImportError: PortAudio library not found` 또는 오디오 재생 실패
**해결책:** 시스템에 PortAudio와 FFmpeg이 설치되어 있는지 확인하십시오.
- **macOS:** `brew install portaudio ffmpeg`
- **Ubuntu/Debian:** `sudo apt-get install portaudio19-dev ffmpeg`
- **Windows:** [ffmpeg.org](https://ffmpeg.org/download.html)에서 FFmpeg을 설치하고 시스템 PATH에 추가하십시오. PortAudio는 Windows에서 sounddevice와 함께 보통 자동으로 설치됩니다.

### 마이크 권한
**증상:** `OSError: [Errno -9999]` 또는 마이크 접근 불가
**해결책:** 시스템 설정(보안 및 개인정보 보호)에서 터미널이나 Python IDE의 마이크 접근 권한을 허용하십시오.

## 프로젝트 아이디어

- **회의 회의록 작성기** - 실시간으로 회의를 녹음 및 기록하고, Claude를 사용하여 요약, 실행 항목 및 핵심 내용을 생성합니다.
- **언어 학습 튜터** - 실시간 피드백을 받으며 모든 언어로 대화를 연습합니다. Claude가 발음을 교정하고 더 나은 표현을 제안할 수 있습니다.
- **대화형 스토리텔러** - Claude가 이야기를 들려주고 사용자의 말에 따라 대답하는 '나만의 모험 선택' 게임을 만듭니다.
- **핸즈프리 코딩 어시스턴트** - 키보드에서 손을 떼지 않고 말로 코드 변경 사항, 버그 또는 기능을 설명합니다.

## ElevenLabs에 대해 더 알아보기

- [ElevenLabs 플랫폼](https://elevenlabs.io/) - 공식 웹사이트
- [API 문서](https://elevenlabs.io/docs/overview) - 전체 API 참조
- [목소리 라이브러리](https://elevenlabs.io/voice-library) - 사용 가능한 목소리 탐색
- [Python SDK](https://github.com/elevenlabs/elevenlabs-python) - 공식 Python SDK
    