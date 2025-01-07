# PaperQA_Retrieval
### 한국어 embeddig/retrieval evaluation용 데이터셋
### 국내논문 QA 데이터셋 사용하여 구축하였습니다.
### link: https://aida.kisti.re.kr/data/21b21974-6efd-4581-b9df-699f91f5bc98

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
"qas" 내부의 "question"을 "query"로 사용하였고,  
"context"와 "answer_start"를 이용하여 최대 길이 512의 "context"를 생성했습니다.  
이 때 검색되어야 하는 문서의 앞쪽에 관련 정보들이 모여있을 가능성이 높으므로,  
"answer_start" index 앞에 128 character를 포함하도록 context를 설정하였습니다.

### 총 데이터셋 개수
level: 0,1,2 각각에 해당하는 데이터셋 274,779개씩 포함하여, 총 824,337개의 데이터셋을 구축하였습니다.

### Data Sample
Repository 내 data directory 안의 데이터셋은 총 824,337개의 전체 데이터 셋 중에서  
10,000개를 랜덤 샘플링하여 구성한 sample.json 데이터셋입니다.  
데이터셋 예시는 아래와 같습니다.
```
    {
        "level": 1,
        "question": "SNEP를 사용하기 위해 무엇이 필요한가?",
        "context": [
            "데이터 기밀성과 두 노드 사이에서의 데이터 인증, 무결성 및 데이터 freshness를 제공할 수 있는 SNEP과 데이터 브로드캐스트 시에 데이터 인증을 제공할 수 있는 μTESLA로 이루어져 있다.\nSNEP를 사용하기 위해서는 통신하기를 원하는 두 노드 간에 pairwise key를 공유하고 있어야 하는데 이를 위해서 네트워크의 각 노드들은 배치 이전에 베이스 스테이션과 각각 유일한 대칭키인 개인키를 공유하고 이를 바탕으로 베이스 스테이션이 pairwise key 설립에 참여를 함으로서 노드 간에 키를 설립한다. 이 대칭키에 단방향 함수(one-way function)을 취함으로 노드 사이에 전송될 메시지에 대한 인증키를 각 노드가 스스로 유도해낼 수 있으며 이 키들을 이용하여 노드 간에 각각의 카운터를 교환하여 사용함으로 약한 데이터 freshness를 이룰 수 있다.\n그리고 μTESLA를 이용하면 베이스 스테이션의 브로드캐스팅을 인증할 수 있는데 이는 시간의 지연을 두고 대칭키를 공표함으로 이루어진"
        ],
        "answer": "통신하기를 원하는 두 노드 간에 pairwise key를 공유",
        "id": 33
    }
```