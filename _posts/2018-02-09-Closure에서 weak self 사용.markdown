---
layout: post
title:  "Closure에서 weak self 사용"
author: Junho Lee
categories: Develop
tags:	ios swift closure weak self
cover:  "/assets/images/swift_default.jpg"
---

# Closure에서 weak self 사용
*weak self (약한 참조)*는 문서에 명시적으로 *Strong Reference Cycle (강한 순환 참조)*를 벗어나기 위해 사용된다고 설명하고 있다. Closure를 사용하면서 closure 내부에서 컨트롤러의 멤버를 사용하기 위해 *self*가 사용되는데, 일반적인 경우에는 문제가 없지만 특수한 상황에서 문제가 될 여지가 있다.

문제가 발생할 수 있는 코드를 통해 간단하게 살펴보도록 하자.

```swift
class Thing {
	var disposable: Disposable?
	var total: Int = 0

	deinit {
		disposable?.dispose()
	}

	init(producer: SignalProducer<Int, NoError>) {
		disposable = producer.startWithNext { number in
			self.total += number
			print(self.total)
		}
	}
}
```

코드를 살펴보면 closure 내부에서 *total*이라는 클래스 멤버를 사용하기 위해 self를 명시해 주고 있다. Self는 사용과 함께 total 멤버의 *retain count*를 증가시키게 되는데 위의 코드에서 closure가 self를 해제하여 retain count를 낮춰준다면 문제없이 작동하는 코드가 된다.

다만 closure에 대한 참조가 disposable 멤버에 의해 붙잡혀 있을 경우 문제가 발생할 수 있게 된다. 즉, closure는 self가 해제 되기를 기다리고, self는 closure가 해제 되기를 기다리는 strong reference cycle 상황을 만들어 내게 되는 것이다.

이러한 상황을 해결하기 위해 weak self 를 사용하면 strong reference cycle 을 크게 줄일 수 있다.

사용법은 굉장히 단순하다.

```swift
disposable = producer.startWithNext { [weak self] number in
	self?.total += number
	print(self?.total ?? 0)
}
```

기존의 코드와 차이점은 클로져 선언부에 `[weak self] ([parameter]) in`을 명시해주고 self가 사용되는 곳에 옵셔널로 self를 사용해주면 위에서 언급하였던 strong reference cycle 상황을 피해갈 수 있게 된다.

개발을 하다보면 언제 strong reference cycle이 발생할지 미리 예측을 하기가 무척이나 어렵지만 closure 내부에서 만큼이라도 self를 weak으로 만들어주는 습관을 기른다면 발생 확률을 크게 줄일 수 있을 것이다.

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
[liquid]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
