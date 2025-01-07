# PaperQA_Retrieval
### 한국어 embeddig/retrieval evaluation용 데이터셋
### 국내논문 QA 데이터셋 사용하여 구축 (link: https://aida.kisti.re.kr/data/21b21974-6efd-4581-b9df-699f91f5bc98)

기존 국내논문 QA 데이터셋에서 'context', 'qas'를 사용하여 구축하였습니다.  
```
"context": "질의응답문장이 포함된 논문 풀텍스트",
"qas": [
    {
        "level": "난이도 (0:일반, 1:하, 2:상)",
        "question": "질의",
        "answer": {
            "answer_text": "응답에 해당하는 텍스트",
            "answer_start": "응답 시작 인덱스"
        }
    }
]
```
해당 데이터셋을 일부 수정하여 새로 구축하였습니다.  
"qas" 내부의 "question"을 "query"로 사용하였고, "context"와 "answer_start"를 이용하여 최대 길이 512의 "context"를 생성했습니다. 이 때 검색되어야 하는 문서의 앞쪽에 관련 정보들이 모여있을 가능성이 높으므로, "answer_start" index 앞에 128 character를 포함하도록 context를 설정하였습니다.