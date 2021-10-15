# B Tree

 B Tree는 데이터를 정렬하여 탐색, 삽입, 삭제 및 순차 접근이 가능하도록 유지하는 트리형 자료구조 이다.

DBMS에서 Index를 만들 때 B Tree를 이용한 자료구조를 많이 사용한다. 

B Tree는 모든 리프노드들이 같은 레벨을 가질 수 있도록 자동으로 밸런스를 맞추는 트리이다.

따라서 이진 탐색의 장점을 살릴 수 있다. 

### 개념

하나의 노드에 최대 M개의 자료를 넣을 수 있으며, M차 B Tree라고 부른다. 

루트노드를 제외한 다른 모든 노드는 적어도 M/2개의 자료를 가지고 있어야 한다.

자료는 정렬된 상태로 저장된다. 

노드는 M/2 ~ M+1 개의 자식을 가질 수 있다.



### 연산

#### 검색

이진탐색을 통해 검색할 수 있다. 

차수가 홀수냐 짝수냐에 따라 알고리즘이 다르다.

아래는 홀수 차수에 대한 내용이다.

![img](https://blog.kakaocdn.net/dn/cikell/btqBRvDU1xF/CdIhvg8XEhHKaP23vE4Ju1/img.jpg)

#### 삽입

자료는 항상 리프 노드에 추가 된다.

자료를 추가할 리프노드는 루트부터 시작해 하향식으로 탐색하며 결정한다.

자료를 추가할 리프노드에 여유가 있다면 삽입,

여유가 없다면 분할해야 한다. 

분할 과정은 상향식으로 이루어진다. 

![btree삽입](https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_6.png)

#### 삭제

##### case 1. 리프노드, 삭제해도 B Tree가 유지되는 경우 

그냥 삭제한다.

![btree삭제](https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_7.png)

##### case 2. 리프노드, 삭제시 B tree 구조 깨짐

이 경우에는, 

1) 부모노드와 형제노드를 merge한다.
2) 이 과정을 root까지 올라가며 B Tree 조건에 맞을 때 까지 1번을 반복한다. 

![btree삭제](https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_8.png)

##### case 3. 리프노드가 아닌 중간에 위치한 데이터를 삭제할 경우

1) 노드에서 해당 데이터를 삭제한다.
2) 왼쪽 서브트리에서 최댓값을 찾아 노드에 넣는다. 
3) 부모노드와 형제노드를 merge하는 과정을 root까지 올라가며 B Tree조건에 맞을 때 까지 반복한다. (case2번 방법)

<img src="https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_9.png" alt="btree삭제" style="zoom: 25%;" />

![btree삭제](https://hyungjoon6876.github.io/jlog/assets/img/20180720/btree_10.png)



### 추가

[B tree 연산을 시각적으로 볼 수 있는 사이트](https://www.cs.usfca.edu/~galles/visualization/BTree.html) 

B+ tree

- 모든 내부 노드(internel node)는 자료의 키값만 저장하고, 각 자료의 데이터는 오직 Leaf node에만 저장(리프 노드가 linked list로 구성됨)leaf 노드에 저장된 키와 동일한 키를 저장하는 내부 노드도 있을 수 있음.
- 각 leaf node에는 다음 형제 노드에 대한 포인터를 가지고 있어 중위 순회 없이도 순차적으로 접근 가능

B* tree

- 루트 노트가 아닌 노드는 최대 저장 공간의 2/3 이상의 자료가 저장되어야 함

  (B-tree는 [m/2]-1 조건에 의해 최소 1/2 이상의 자료가 저장되어야 함.)

- 노드에 저장되는 자료가 넘치는 경우(overflow), 일단 형제 노드들로 재분배시킴. 그리고 모든 형제 노드들이 가득 찬 경우에만 B-tree의 분할 연산을 수행

  (B-tree는 무조건 중간값을 가지는 자료를 부모 노드로 올려 보내고 분할하였음)



### 출처

https://swycha.tistory.com/236
