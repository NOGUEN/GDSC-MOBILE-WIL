# Flutter Spacer에 대해서 알아보자

## Spacer란?

`Spacer`는 `Row`와 `Column`과 같은 `Flex Container` (이는 뒤에서 알아볼 것이다.)의 공간을 조절하는 빈 공간을 만들어주는 위젯이다.

이름 그대로 `Space + er`로 공간을 만들어주는 위젯이다.

`Spacer` 위젯은 추가적인 공간을 잡는 위젯이기 때문에 `Flex container`안에 있는 `Flex.mainAxisAlignment`를

`MainAxisAlignment.spaceAround`,

`MainAxisAlignment.spaceBetween`,

`MainAxisAlignment.spaceEvenly`

로 설정하면 추가 공간을 모두 차지했으므로 재배포할 공간이 남아 있지 않아 가시적인 효과가 없다.

즉, `Spacer`는 `MainAxisAlignment` 속성을 모두 무시한다는 것이다.

## Spacer 사용예시

```dart
Spacer()
```

`Spacer`는 위와 같이 단순히 저렇게 작성하는 것으로 적용이 가능하다.

좀 더 자세한 사용 예시는 아래와 같다.

```dart
class SpacerPractice extends StatelessWidget {
  const SpacerPractice({super.key});

  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        Text(
          "hello",
          style: TextStyle(fontSize: 24),
        ),
        Spacer(),
        Text(
          "I'm",
          style: TextStyle(fontSize: 24),
        ),
        Spacer(),
        Text(
          "Gorani",
          style: TextStyle(fontSize: 24),
        ),
      ],
    );
  }
}
```

이렇게 코드를 작성하고 실행시키면 빈 공간을 꽉 채우게 공간이 할당된다.

<img src=https://user-images.githubusercontent.com/65299607/200558798-ebd64ce2-6f6a-44cb-8a80-2797f9367787.png width="200" height="400">
그러면 `Flex.mainAxisAlignment`를 설정하면 어떻게 될까?

```dart
class SpacerPractice extends StatelessWidget {
  const SpacerPractice({super.key});

  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        Text(
          "hello",
          style: TextStyle(fontSize: 24),
        ),
        Spacer(),
        Text(
          "I'm",
          style: TextStyle(fontSize: 24),
        ),
        Spacer(),
        Text(
          "Gorani",
          style: TextStyle(fontSize: 24),
        ),
      ],
    );
  }
}
```

이렇게 코드를 작성하고 실행시키면 `Flex.mainAxisAlignment`를 설정하지 않은 것과 똑같은 결과가 나타난다.

<img src=https://user-images.githubusercontent.com/65299607/200558798-ebd64ce2-6f6a-44cb-8a80-2797f9367787.png width="200" height="400">


## Properties

`Spacer` 위젯에서 가장 중요한 Property는 `flex Property`다.

### flex

**flex -> int**

첫번째 인자는 `flex`로 `int` 타입을 받는다.

이 `flex`의 의미는 공간을 어느 정도로 차지하는지에 대한 **배율**을 의미한다.

만약에 아래와 같이 `Spacer`를 설정했다고 하면,

```dart
Spacer(flex: 2)
```

<img src=https://user-images.githubusercontent.com/65299607/200558853-d176a3e0-61e7-4f3e-abcf-eb1e14b97662.png width="200" height="400">

공간이 더 할당된 것을 알 수 있다.

다른 위젯들보다 2배 더 공간을 할당한다는 것이다.

다른 Property들로는 `hashCode`와 `Key`, `runtimeType`들이 있는데 이 Property들은 어떤 역할을 하는지 잘 모르겠다...

