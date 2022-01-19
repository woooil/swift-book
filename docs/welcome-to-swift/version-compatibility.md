---
layout: default
title: 버전 호환성
description: Version Compatibility
parent: 환영합니다
nav_order: 2
---

# 버전 호환성

이 책은 Xcode 13에 포함된 Swift 버전인 Swift 5.5를 설명하고 있습니다. Xcode 13으로는 Swift 5.5 또는 Swift 4.2, Swift 4로 작성된 대상을 빌드할 수도 있습니다.

Xcode 13으로 Swift 4나 Swift 4.2 코드를 빌드하더라도 대부분의 Swift 5.5 기능을 사용할 수 있습니다. 단, 다음의 변경 사항들은 Swift 5.5 이후의 코드에서만 사용할 수 있습니다:

* 불투명형을 반환하는 함수는 Swift 5.1 런타임을 필요로 합니다.
* `try?` 표현식은 옵셔널을 반환하는 표현식에 또 다른 옵셔널을 중첩하지 않습니다.
* 큰 정수 리터럴 초기화 표현식은 알맞은 정수형으로 추론됩니다. 예를 들어 `UInt64(0xffff_ffff_ffff_ffff)`은 오버플로우되는 것이 아닌 올바른 값으로 평가됩니다.

동시성을 사용하기 위해서는 대응되는 동시성 자료형을 지원하는 Swift 표준 라이브러리 버전과 Swift 5.5 이후 버전이 필요합니다. Apple 플랫폼에서는 배포 대상을 iOS 15, macOS 12, tvOS 15, watchOS 8.0 이상으로 설정하세요.

Swift 5.5로 작성된 대상은 Swift 4.2나 Swift 4로 작성된 대상에 의존할 수 있으며, 그 반대도 가능합니다. 따라서 여러분이 여러 프레임워크로 나뉘는 대형 프로젝트를 가지고 있다면, 한 프레임워크씩 코드를 Swift 4에서 Swift 5로 마이그레이션 할 수 있습니다.

