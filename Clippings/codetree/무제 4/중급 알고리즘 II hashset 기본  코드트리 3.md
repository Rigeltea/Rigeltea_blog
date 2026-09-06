---
title: "중급 알고리즘 II: hashset 기본 | 코드트리"
source: "https://www.codetree.ai/ko/trails/complete/curated-cards/intro-the-tree-traversal/introduction"
author:
published:
created: 2026-08-30
description: "Coding Learning Curriculum covering Beginner-Level needs up to high level coding knowledge required for working at top-tier tech companies."
tags:
  - "clippings"
---
Lesson 2. 이진 트리와 탐색

기본 문제에서는 단계별 학습을 위해 각 문제가 하나의 기본개념과 짝을 이룹니다. 연습 문제와 테스트 문제에서는 쉽게 복습할 수 있도록 모든 개념이 함께 제공됩니다.

## 이진트리와 탐색, 그리고 이진탐색트리

## 이진트리 개념 및 구현

트리에서 한가지 제한을 걸어보겠습니다. 바로 자식의 수를 최대 2개로 제한하는 것 입니다. 물론 자식의 수가 1개, 0개가 될 수 있지만, 우리는 이 트리를 이진트리라고 부를 것입니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-1ca43188-0daa-436c-b5a4-bbc6b71146da.png)

다음 그림들 역시도 조건을 만족하므로 이진트리라고 부를 수 있습니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-96ef5cc8-2257-4bf5-9cb6-95c0ad7a9748.png)

일단 간단한 특성에 대해 알아보자면, 구현하기 쉽다는 특성입니다. 놀랍게도 배열로도 구현이 가능합니다!

위의 이진트리를 배열에 넣어보겠습니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-81faa115-a94d-4132-bbbc-1389ad32d754.png)

이진트리의 자식은 두개이기 때문에, 하나는 왼쪽에, 그리고 다른 하나는 오른쪽에 존재한다고 볼 수 있을 것입니다. 우리는 왼쪽/오른쪽 자식이라고 구분하도록 하겠습니다.

배열의 0번 값을 비우고, 루트 노드를 1번에 넣어주도록 합시다. 그리고 왼쪽 자식을 2번에, 오른쪽 자식을 3번에 넣어줍니다. 그 후 왼쪽 자식과 오른쪽 자식을 알맞게 넣어주면 됩니다.

이렇게 넣게 되면, **특정 노드의 위치가 i라고 한다면, 자연스럽게 왼쪽 자식의 위치는 i \* 2, 오른쪽 자식의 위치는 i \* 2 + 1이 되는걸 볼 수 있습니다.** 즉, 이진트리는 배열로 구현이 가능하며 특정 노드 i의 자식 노드를 조회하기 위해서는 i \* 2, i \* 2 + 1을 하면 됩니다. **반대로 부모노드의 위치는 i / 2로 결정된다는 것을 어렵지 않게 알 수 있습니다.**

![](https://contents.codetree.ai/problems/1014/images/introductions-d89f7d99-ee83-42ff-915c-c8de6f7ae042.png)

그렇다면 다음과 같이 모든 자식이 꽉 차있지 않다면 어떨까요?

![](https://contents.codetree.ai/problems/1014/images/introductions-b97cebab-780a-4b07-8434-84841c17463b.png)

당연히 순서대로 넣을 수는 없을 것입니다. 비어있는 값을 채우게 된다면 이후 어떤 위치에 어떤 값이 있는지 판단하기 어려울 것입니다. 따라서 비어있는 자식은 배열에도 칸을 비워두어야 합니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-2e7998c2-7ff2-4b7d-b5b9-e3c14bdc1ed3.png)

이 경우에도 마찬가지로 특정 노드의 위치가 i라고 한다면, 자연스럽게 왼쪽 자식의 위치는 i \* 2, 오른쪽 자식의 위치는 i \* 2 + 1이 되는 것을 볼 수 있습니다

![](https://contents.codetree.ai/problems/1014/images/introductions-fcc3a4b7-38d7-4316-b5bc-73e00bcfefe7.png)

## 이진트리 탐색

이진트리는 재귀를 사용하면 탐색을 비교적 쉽게 구현할 수 있습니다.

어떤식으로 방문하는 순서에 따라 크게 세가지로 나뉩니다. 각각 전위 탐색 (Preorder Traversal), 중위 탐색 (Inorder Traversal), 후위 탐색 (Postorder Traversal)입니다.

- 전위 탐색은 **부모 - 왼쪽 자식 - 오른쪽 자식** 순으로 탐색합니다. 이 뜻은 모든 노드에 대해 부모에 먼저 색칠을 진행한 후, 왼쪽 자식들을 전부 순회하고, 그 이후에 오른쪽 자식들을 방문함을 뜻합니다.
	![](https://contents.codetree.ai/problems/1014/images/introductions-f5ff0830-f936-4abd-abf8-78d5489cdbeb.png)
- 중위 탐색은 **왼쪽 자식 - 부모 - 오른쪽 자식** 순으로 탐색합니다. 이 뜻은 모든 노드에 대해 왼쪽 자식들을 먼저 전부 순회한 후, 부모에 색칠을 진행하고 그 이후에 오른쪽 자식들을 방문함을 뜻합니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-31b7282c-d187-4197-9829-832d51121b33.png)

- 후위 탐색은 **왼쪽 자식 - 오른쪽 자식 - 부모** 순으로 탐색합니다. 이 뜻은 모든 노드에 대해 왼쪽 자식들을 먼저 전부 순회한 후, 오른쪽 자식들을 전부 순회하고 그 이후에 마지막으로 부모에 색칠을 진행함을 뜻합니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-5ab0843c-8582-4022-a4a1-90599854f6a4.png)

중요한 점이라면, 재귀적으로 진행되기 때문에 트리가 조금 복잡해지면 어떤식으로 방문했는지 어려울 수 있습니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-a02601a6-ff62-42c1-8a85-215c03d05672.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-08c32226-ccd6-4d2e-935e-b1a48ee0983a.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-ddd29a9e-b78b-4e89-8c7d-73e1904046c4.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-2618bad9-18e5-45f6-ba82-ec91d7e7eb1b.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-2004963f-f81e-4cec-abcf-3586f7e38c4c.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-b9e792cc-6307-455c-818e-0c9b9531da07.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-d8a797be-5d3f-4110-a4cb-79ed97662291.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-34b48303-582c-4ef7-aac5-bdd846b2f803.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-7d5efd05-3dd3-4e5f-b350-376177e76ce3.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-3c37d134-869f-4be1-9e85-0227f485e525.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-736b796c-d50a-42d5-8207-8fdabad6518b.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-543e132a-2ad2-4b3e-bdb8-1328afbed995.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-c3b5a4fb-4a1c-465d-a3c1-7fdbb6f51db1.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-3d3974a1-1768-42b5-81fc-166d89d77bbd.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-a68ae442-153a-4873-ac82-33c394db638b.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-a16508a0-e623-4101-ad02-6a55b01d50d2.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-472bab01-87ba-45d0-afbf-695018573b64.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-a0472b6b-b24a-4df8-83b3-08bfb208b691.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-ca359b19-8a98-4be2-a451-fa26fef9139a.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-af756fe9-84a9-4452-beab-f747e04f6a0f.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-59711bec-ebf9-4ded-8430-803905004f35.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-2e0741c9-3ec5-4f44-ba23-8fd9ed55933b.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-b19e14c0-0d8c-4ac5-bb07-5cc1a9527345.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-ea712498-8a71-4870-a9a1-087bf198ac6b.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-e1e90a1c-8cce-4ab6-9909-18c76aa9aca1.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-db5d1e0f-ce22-4b4f-b3ba-7ad3db101999.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-1aaa6aaf-5ad2-4d2f-b4f6-98d828f46d27.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-c5cb0e43-2678-4a23-b748-86b1087c57fd.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-681005b7-18a2-40ae-948b-5a8d6bf50eec.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-ead63aae-af2b-46e5-839d-6c339dc811f4.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-de308ed5-1e80-4f22-bb24-6d26ab621343.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-66ff6cc9-3eb2-4c1e-ab5c-8fef467290bf.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-f753ecbd-5207-4cab-8725-58255f5c1f6c.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-63f454ad-4b1c-4957-82ca-70244eafb6c7.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-96b0d714-7a7b-445f-a0e0-653c59a06268.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-85567460-7dbc-4b56-8cad-1e625df625dd.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-d729c323-e91d-4ddb-a435-e572534039d2.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-d227e080-09f5-40fe-ab81-c816e6f401cb.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-9f285e66-0540-4947-9843-48f7add2d459.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-65ac99a6-3536-4f86-8632-a43243c90c22.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-121bda22-d334-487e-87b9-1712b3714149.png)

1 / 41

전위 탐색을 다시 본다면, 왼쪽 자식부터 먼저 방문하게 되는데, 이때 왼쪽 자식에서는 왼쪽 자식을 부모로 지정하여 재귀적으로 전위 탐색을 다시 한 번 진행합니다. 이렇게 계속 왼쪽으로 내려가다 더 이상 왼쪽이 없게 된다면 부모를 방문하고, 자연스럽게 오른쪽까지 방문하여 함수를 종료할 것입니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-43a7a746-b560-4889-b2b3-c2a908d775d8.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-8e5eb76f-4fe8-473a-8243-38e361dcc397.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-a1c33d98-229e-46d8-aa2b-cdcd921c89b2.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-da5e69a4-91f9-4450-b9d0-85a991f0b1ff.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-785b41d1-7332-4d1c-9396-132336c2e104.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-fe1fe240-4bea-4d1d-9ec2-0de69cbd37c6.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-a7fe9f3c-dd95-4add-a960-1f5375a5d095.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-9ec6612f-9a0d-459f-9f6a-e94e14bbba1f.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-98db3562-a138-4102-8fca-62c77cf028ce.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-752c7e8b-7922-4d13-8beb-62e1cfe16e62.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-f159d1b6-7e92-4748-9abd-93cc412d6351.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-b9cdc1fa-9e17-416d-a671-5eec38025198.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-7ccda711-139c-4eaa-8511-d777ebdbe3e4.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-be8d6720-1a5f-4144-8599-4cda38446fc7.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-165e0706-c590-42c7-8f87-48b3535ed4cf.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-49faec89-20ca-46e8-a06b-6a676688848a.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-fae28c5e-cedc-45af-8adf-d280312c109d.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-83fcc989-9f3c-4b73-a059-bb9033d1f616.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-b7c21bb3-9eaf-4109-94eb-28e4d9bab6ba.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-5ce26a02-c6a7-48f6-99a3-120d74a1f083.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-1c347e9e-ccaf-480b-b5f5-6f4aaf34103b.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-94388c75-bf30-4c0b-879b-a70d5acb8a98.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-cd4cf1cf-a56a-4126-9094-cccdc7f6f2df.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-5d867b54-89a9-4062-ad87-81f36be7cd37.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-403de4e9-f20b-4831-949c-a04d9194ce97.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-339d398c-cac1-4764-af67-7e338058a34a.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-bb7175cb-124a-4702-bcff-6bbca048effe.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-0aea881f-da42-48ec-8b83-0c1ba3858c34.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-a4fcec47-673c-407f-9b32-72eac442a270.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-0c9f926e-1133-4366-b9bb-9482c3eab14c.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-52582820-f4ad-4174-9a91-58f111a06255.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-f359fadc-e74e-4c8e-8f1f-0e7f98b6bb74.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-b9bee138-7249-49c7-bb5d-f814b2369592.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-9bb6b0e6-9a25-4563-ae64-3c9e2de8ed4f.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-4d626eda-21c2-4022-b9a9-08c2fb7bf116.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-9ea3d0a8-a963-48b4-b39c-b2428fc507f5.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-885dcc7b-8175-44e1-8223-8d49bc35252c.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-54465af0-69b8-4d8b-8e87-f8414843fad2.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-ba341fa1-aece-4445-91bb-0f487016ccb1.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-26e713a3-eecf-42eb-882d-4e516bcee567.png) ![](https://contents.codetree.ai/problems/1014/images/introductions-acf33937-7ec5-4f12-9bfc-cba0e60e5c41.png)

1 / 41

중위와 후위 탐색도 마찬가지입니다. 재귀적으로 진행된다는 것을 반드시 기억하시고 탐색을 연습해보세요.

## 이진탐색트리

이진트리에서 한가지 조건을 더 추가해봅시다. **부모의 왼쪽 방향에 있는 노드들은 전부 부모 보다 값이 작아야 하고, 부모의 우측 방향에 있는 노드들은 전부 부모 보다 값이 커야만 한다는 것입니다.**

우리는 이런 조건을 통해 만들어지는 트리를 이진 탐색 트리 (Binary Search Tree)라고 부르는데, 이런 트리는 그 고유 특성 때문에 정말 많이 사용됩니다.

예를 들어 다음의 경우 이진탐색 트리입니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-682abdcc-d162-450a-9d8e-233885b4b9d8.png)

하지만 유의하셔야 할 점은 아래 그림은 이진탐색 트리가 아닙니다. 노드 5보다 왼쪽에 있는 자식 노드 중 노드 6이 있기 때문입니다. 하지만 만약 부모와 자식 관계에 대해서만 크고 작은지를 생각한다면 이진탐색 트리라는 착각이 들만한 경우이므로, 꼭 이진탐색 트리는 왼쪽, 오른쪽에 있는 모든 노드가 현재 노드보다 작고, 커야만 함에 유의합니다.

![](https://contents.codetree.ai/problems/1014/images/introductions-8a63f293-4fb7-4ac9-9a8e-78b1e8a8e977.png)

이 콘텐츠가 도움이 되었나요?

주의사항: Copyright © Branch & Bound  
Codetree 사이트의 모든 교육 자료는 저작권법의 보호를 받습니다.  
© Branch & Bound의 동의 없는 무단 복제/복사/배포를 금지합니다.