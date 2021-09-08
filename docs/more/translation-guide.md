---
layout: default
title: 번역 지침
parent: 더 보기
nav_order: 1
---

# 번역 지침

이 번역의 목적은 번역자 본인이 참고하기 위한 한글 자료를 만드는 데 있습니다. 번역 방식이 일반적이지 않을 수 있습니다.

## 번역 원칙

1. 한글로서 자연스럽게 읽히도록 합니다.
   1. 한글 맞춤법을 따릅니다. 
   2. 문장과 단어는 모두 번역하는 것을 원칙으로 합니다.
      1. 단, [번역하지 않는 부분](#번역하지-않는-부분)은 원어 그대로 표기합니다.
      2. 번역하는 부분에는 원어를 \(괄호를 포함하여\) 어떤 식으로든 표기하지 않습니다.
   3. 자주 등장하는 단어는 [번역 표](terminology.md)에 명시한 대로 번역하여 일관성을 유지합니다. 
   4. 복잡하거나 긴 문장은 짧게 쪼개고, 한국어 표현 상 필요 없는 부분은 생략합니다.
   5. 한국어에 맞지 않는 표현이나 구조는 적절히 수정합니다.
   6. 경어체를 일반적으로 사용하며, 구어체나 속어는 사용하지 않습니다.
   7. [번역 시 우선 순위](#번역-시-우선-순위)을 따릅니다.

## 번역하지 않는 부분

1. 프로그래밍 언어 등의 고유한 이름
2. 코드 블럭으로 표기되는 부분. 단, 코드 블럭 내 주석은 번역하기도 합니다.
3. Swift에 지정된 키워드

## 번역 시 우선 순위

1. 이미 관습적으로 굳어진 한국어 표현이 있다면 그 표현을 채택합니다.
   1. 외래어가 아닌 한자어나 순우리말 표현이 흔하다면 그 표현을 채택합니다.

      예시: 함수\(function\), 연산자\(operator\)

   2. 외래어, 한자어, 순우리말 표현이 모두 흔하다면 외래어가 아닌 한자어나 순우리말을 채택합니다.

      예시: 객체\(object, 오브젝트가 아님\), 오류\(error, 에러가 아님\)

   3. 흔한 한자어나 순우리말 표현이 없다면 외래어를 채택합니다.

      예시: 인스턴스\(instance\), 디버그\(debug\)
2. 관습적으로 굳어진 표현이 없더라도 원어로 표기하지 않고 번역합니다.

   1. 원어의 의미를 잘 나타내는 한자어, 순우리 표현이 있다면 그 표현을 채택합니다.

      예시: 강제 개봉\(forced unwrapping\), 보장문\(assertion\)

   2. 원어의 의미를 잘 나타내는 한자어나 순우리말이 없다면 외래어를 채택합니다.
