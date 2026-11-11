# FashionRAG Assistant

CLIP 이미지 검색과 GPT 비전 모델로 만든 **멀티모달 RAG 패션 스타일링 어시스턴트** 실습입니다.
한국어로 질문하면 비슷한 패션 사진을 찾아 보여주고, 그 사진을 근거로 스타일링 조언을 해 줍니다.

## 동작 흐름

```
한국어 질문
  → ① 번역 (gpt-4o-mini)
  → ② CLIP 텍스트 임베딩 → Chroma 유사도 검색 (Retrieval)
  → ③ 검색된 이미지를 base64로 바꿔 질문과 함께 프롬프트 구성 (Augmentation)
  → ④ 비전 모델이 이미지를 보고 답변 (Generation)
  → ⑤ 한국어로 번역해서 출력
```

## 사용 기술

| 라이브러리 | 역할 |
|---|---|
| `datasets` | Fashionpedia 데이터셋 스트리밍 |
| `open-clip-torch` | 텍스트·이미지를 같은 벡터 공간에 임베딩 |
| `chromadb` | 이미지 벡터 저장 및 유사도 검색 |
| `langchain-core`, `langchain-openai` | LCEL 번역 체인, 비전 체인 |

## 실행 방법

Python 3.11 기준입니다.

```bash
# 1. 가상환경 만들고 패키지 설치
python -m venv .venv
.venv\Scripts\activate          # macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt

# 2. API 키 설정
copy .env.example .env          # macOS/Linux: cp .env.example .env
# .env 파일을 열어 OPENAI_API_KEY 값을 실제 키로 바꾸기
```

3. `notebooks/FashionRAG_멀티모달RAG_수업.ipynb`를 열고 위에서부터 셀을 차례로 실행합니다.
   - 처음 실행하면 데이터셋 이미지(`notebooks/fashion_dataset/`)와 벡터 DB(`notebooks/img_vdb/`)가 만들어집니다.
   - 두 폴더는 다시 만들 수 있어서 저장소에는 올리지 않습니다.

## 폴더 구조

```
fashionRAG-assistant/
├── notebooks/
│   └── FashionRAG_멀티모달RAG_수업.ipynb   # 실습 노트북
├── requirements.txt
├── .env.example                             # API 키 예시 (.env 는 올리지 않음)
└── README.md
```
