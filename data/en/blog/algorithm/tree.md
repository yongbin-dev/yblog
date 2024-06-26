---
title: '[자료구조] 트리'
date: '2021-04-03'
tags: ['Data Structure']
draft: false
summary: 'A guide to using the srcset and sizes attributes to create responsive images'
images: ['/static/images/responsive-image.jpg']
authors: ['default']
---

## 1. 트리(Tree)란?

- 트리: Node와 Branch를 이용해서, 사이클을 이루지 않도록 구성한 데이터 구조
- 실제로 어디에 많이 사용되나?
  - 트리 중 이진 트리 (Binary Tree) 형태의 구조로, 탐색(검색) 알고리즘 구현을 위해 많이 사용됨

## 2. 용어

- Node : 트리에서 데이터를 저장하는 기본 요소
- root node : 최상위 노드
- Level : 최상위 노드를 Level0 으로 하였을 때 그 하위 길이를 나타냄
- Parent Node : 특정 노드의 다음 레벨에 연결된 노드
- Child Node : 특정 노드의 상위 레벨에 연결된 노드
- Leaf node : Child Node가 하나도 없는 노드
- Slbling( Brother Node ) : 동일한 Parent Node를 가진 노드
- Depth : 트리에서 Node가 가질 수 있는 최대 Level

## 3. 이진 트리와 이진 탐색 트리

- 이진트리 : 노드의 최대 Branch가 2인 트리
- 이진 탐색 트리 (Binary Search Tree) : 이진 트리에 다음과 같은 추가적인 조건이 있는 트리
  - 왼쪽 노드는 해당 노드보다 작은 값 , 오른쪽 노드는 해당 노드보다 큰 값을 가지고 있음

<img src="https://www.mathwarehouse.com/programming/images/binary-search-tree/binary-search-tree-insertion-animation.gif" />

(출처: https://www.mathwarehouse.com/programming/gifs/binary-search-tree.php#binary-search-tree-insertion-node)

### 이진트리와 정렬된 배열간의 탐색 비교

<img src="https://www.mathwarehouse.com/programming/images/binary-search-tree/binary-search-tree-sorted-array-animation.gif" />

(출처: https://www.mathwarehouse.com/programming/gifs/binary-search-tree.php#binary-search-tree-insertion-node)

## 4. 자료 구조 이진 탐색 트리의 장점과 주요 용도

- 주요 용도 : 데이터 검색(탐색)
- 장점 : 탐색 속도를 개선할 수 있음
- 단점 : depth(트리의 높이)를 h라고 표기한다면 , O(h)

## 5. 파이썬으로 구현한 트리

```python
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None


class NodeMgmt:
    def __init__(self, head):
        self.head = head

    def insert(self, value):
        self.current_node = self.head
        while True:
            if value < self.current_node.value:
                if self.current_node.left != None:
                    self.current_node = self.current_node.left
                else:
                    self.current_node.left = Node(value)
                    break

            else:
                if self.current_node.right != None:
                    self.current_node = self.current_node.right
                else:
                    self.current_node.right = Node(value)
                    break

    def search(self, value):
        self.current_node = self.head

        while self.current_node:
            if self.current_node.value == value:
                return True

            elif value < self.current_node.value:              # 왼쪽
                self.current_node = self.current_node.left
            else:                                              # 오른쪾
                self.current_node = self.current_node.right
        return False

    def delete(self, value):
        searched = False
        self.current_node = self.head
        self.parent = self.head

        # 삭제할 노드를 찾는 과정
        while self.current_node:
            if self.current_node.value == value:
                searched = True
                break
            elif value < self.current_node.value:
                self.parent = self.current_node
                self.current_node = self.current_node.left
            else:
                self.parent - self.current_node
                self.current_node = self.current_node.right

        if searched == False:
            return False

        # 이후부터 Case 들을 분리해서 , 코드 작성

        # Case 1 : 삭제할 Node 가 Leaf Node 인 경우
        # self.current_node가 삭제할 Node , self.parent는 삭제할 Node의 Parent Node인 상태
        if self.current_node.left == None and self.current_node.right == None:
            if value < self.parent.value:
                self.parent.left = None
            else:
                self.parent.right = None

        # Case2 : 삭제할 Node가 Child Node를 한 개 가지고 있을 경우

        elif self.current_node.left != None and self.current_node.right == None:
            if value < self.parent.value:
                self.parent.left = self.current_node.left
            else:
                self.parent.right = self.current_node.left
        elif self.current_node.left == None and self.current_node.right != None:
            if value < self.parent.value:
                self.parent.left = self.current_node.right
            else:
                self.parent.right = self.current_node.right

        # Case 3-1-1 : 삭제할 Node 가 Parent Node의 왼쪽에있고 , 삭제할 Node의 오른쪽 자식 중 , 가장 작은 값을 가진 Node의 Child Node가 없을 때
        # Case 3-1-2 : 삭제할 Node가 Parent Node의 왼쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 오른쪽에 Child Node가 있을 때
        #  - 가장 작은 값을 가진 Node의 Child Node가 왼쪽에 있을 경우는 없음, 왜냐하면 왼쪽 Node가 있다는 것은 해당 Node보다 더 작은 값을 가진 Node가 있다는 뜻이기 때문임

        elif self.current_node.left != None and self.current_node.right != None:
            # case3-1
            if value < self.parent.value:
                self.change_node = self.current_node.right
                self.change_node_parent = self.current_node.right
                while self.change_node.left != None:
                    self.change_node_parent = self.change_node
                    self.change_node = self.change_node.left
                if self.change_node.right != None:
                    self.change_node_parent.left = self.change_node.right
                else:
                    self.change_node_parent.left = None
                self.parent.left = self.change_node
                self.change_node.right = self.current_node.right
                self.change_node.left = self.change_node.left

        #  Case3-2-1: 삭제할 Node가 Parent Node의 오른쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 Child Node가 없을 때
        #  Case3-2-2: 삭제할 Node가 Parent Node의 오른쪽에 있고, 삭제할 Node의 오른쪽 자식 중, 가장 작은 값을 가진 Node의 오른쪽에 Child Node가 있을 때
        #  가장 작은 값을 가진 Node의 Child Node가 왼쪽에 있을 경우는 없음, 왜냐하면 왼쪽 Node가 있다는 것은 해당 Node보다 더 작은 값을 가진 Node가 있다는 뜻이기 때문임
        else:
            self.change_node = self.current_node.right
            self.change_node_parent = self.current_node.right
            while self.change_node.left != None:
                self.change_node_parent = self.change_node
                self.change_node = self.change_node.left
            if self.change_node.right != None:
                self.change_node_parent.left = self.change_node.right
            else:
                self.change_node_parent.left = None
            self.parent.right = self.change_node
            self.change_node.right = self.current_node.right
            self.change_node.left = self.current_node.left

    return True
```
