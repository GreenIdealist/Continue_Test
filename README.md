# Continue 프롬프트 작성법 #    
     
프롬프트에 대한 설명은 하기 전 전제는     
프롬프트는 LLM의 성능을 끌어올리기 위한 입력방법입니다. 프롬프트를 통해 없던 LLM 성능이 향상되는건 아닙니다.   
그렇기 때문에, 먼저 LLM 학습시 질 좋은 데이터를 가지고 와서 학습시켜 최대한의 성능을 끌어올렸다는 전제로 시작합니다.   
===================================================================================================================   
LLM 프롬프트 하기전 LLM의 성능을 끌어올리는 방법
     
1. LLM에 학습 할 만한 데이터가 부족할 경우      
코딩 규칙에 맞는 문법으로 학습시킬 데이터가 부족할수 있습니다. 이 경우 사용하는 방법이 대표적인 방법으로 ROLA 입니다.
LLM은 기본적으로 질 좋은 데이터가 많이 필요합니다. 그래서 원하는 결과가 나올때까지 학습시키기 위해서는 비용과 시간이 많이듭니다.
그래서 나온 방법이 ROLA입니다. 원하는 결과물이 나오고 싶은 비교적 적은 데이터를, 작은 모델에 학습시키고 그 모델을 LLM이나 생성형 AI에 붙여서 사용합니다.
이럴 경우, 생성형 AI가 나오는 결과물이 제가 원하는 방향으로 나옵니다.     
     
      [ROLA자체를 사용하는 것이 아니라 LLM이나 생성형 AI에 붙여서 사용한다는 점입니다. LLM이나 생성형 AI의 성능을 통해 결과물이 정상적으로 나오고 이것을 ROLA를 통해 방향을 잡아주는 것입니다]

2. 모델 크기를 줄일경우     
   모델 크기를 줄여야 할 필요도 있습니다. LLM의 경우, 굉장히 질 좋고 많은 데이터를 충분히 큰 모델에 학습시키면 좋은 모델이 탄생합니다.
   하지만 큰 모델과 같은 경우 핸드폰과 같은 작은 기기에서 작동하기 어렵기 때문에 모델 크기를 줄일려는 노력이 있는 것입니다.
   양자화 기본 원리는 다음과 같습니다.
   float는 소수점자리까지 표시되며 32bit입니다. (signed) int의 경우 정수형이며 16bit 입니다.
   이렇게 자료형을 바꿔 모델자체를 줄이는 방법이 양자화 방법의 기본원리입니다.      
       
3.VectorDB
각 글자들을 백터화 시켜는 방법입니다. 예를 들어 고양이와 개는 의미론적 관계를 반영해 서로 가깝지만     
행복과 슬픔은 반대방향이므로 대조 되는 의미임을 알 수 있습니다.     
고양이 [0.2, -0.4, 0.7]           
개 [0.6, 0.1, 0.5]      
와 같이 변형하는 것입니다. 그럼 이런 단어들을 어떻게 백터화 시키냐면,      
Embedding Model를 사용하여 백터화합니다.        
embedding vector들간의 거리를 계산하면 이들간의 의미적 관계를 파악할 수 있습니다.        
VectorDB는 임베딩을 통해 생성된 고차원의 백터 데이터들을 효율적으로 저장하고, 조회할 수 있도록 설계된 데이터베이스입니다.      
검색한 단어와 벡터간의 거리나 유사도가 가장 유사항 백터를 통해 원하는 정보를 찾는 방법입니다.
     
RAG나 이외의 방법은 있지만 이러한 방법을 통해 LLM 성능을 끌어올리고 나서, 프롬프트를 통해 정확하게 입력하는 겁니다.     
     
     
LLM 프롬프트 방법     
      
1. 명확하고 구체적으로 질문하기(예시)     
프롬프트 입력시 구체적으로 입력해야 합니다. 구체적일때 예시를 들면 좋습니다.      
Misra rule 이라는 자동차 산업 소프트웨어 코딩 규칙에 맞는 코드로 바꾸고 싶다고 하겠습니다.
[      
     
###Instruction####      
change Example code to Misra rule      
      
###Example###      
val = n++ + arrn[n];
  
]      
이와 같이 지시와 예시로 성능을 향상시킬수 있습니다.     
이와 같은 방법은 제가 실제 프로젝트에서 사용했던 방법입니다.     
     
     
2. 필터 이용방법      
프롬프트 입력시 단어들을 필터를 통해 검열이나 방향을 잡아주는 것이 좋습니다.     
예를 들어, 웹사이트에 코드를 입력하면 앞에서 설명한 구체적으로 질문하는 방법과 함께 작성한 코드가 입력되서 정확한 결과를 얻을수 있습니다.     
아니면 C언어에서 금지한 printf 같은 문법이 감지되면, 다시 입력하라는 경고창이 나오는 방법을 통해     
사용자가 입력시 어떤 방향으로 입력해야 하는지 알게 하는 방법이 있습니다.      
      
3.
