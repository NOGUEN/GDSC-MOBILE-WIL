# 새롭게 알게 된 내용들

## Stateless & Stateful

### Stateless

지금까지 이용한 위젯들은 모두 Statless Widget들로 상태가 없는 위젯이다.

상태가 없는 위젯은 표시할 상태자체가 없는 것이기 때문에 변화가 없다.

그러므로 정적이고 처음 보여준 그대로 멈춰있다.

쉽게 말하면 새로고침이 없는 위젯이다.

### Stateful

하지만 지금부터 새롭게 알게된 위젯인 Stateful은 다르다.

이름을 그대로 대추 해석하면 상태가 넘치는 위젯으로 그냥 상태가 있는 위젯이다.

상태가 있기에 변화할 것이 있다는 의미로도 해석할 수 있다.

그러므로 동적이고 처음 보여준 모습에서 많은 부분이 바뀔 수 있다.

쉽게 말하면 새로고침이 있는 위젯이다.

우리가 지금까지 사용한 유저 상호작용이 있는 앱들은 대부분 이런 Stateful 위젯으로 제작이 되었다고 해도 무방하다.

```dart
class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  CalendarFormat calenderFormat = CalendarFormat.month;
  DateTime selectedDate = DateTime.now();
  @override
  Widget build(BuildContext context) {
    return Container();
  }
}
```

위와 같이 이런 식으로 코드 템플릿이 제작되어있고, `setState`라는 함수가 있어서 이 함수에 매개변수로 람다 함수를 넣어줌으로서 상태를 변화시킨 것을 적용할 수 있다.

조금 길게 이야기했는데 조금 잘라서 이야기하면, 

`setState()` 함수의 역할은 위젯을 다시 그려주는 것

`setState(() {})` 의 매개변수는 위젯을 다시 그려주기 전에 수행할 명령어 집합 이라고 이해하면 쉽다.

## Provider

상태 관리 패키지로 Provider라는 것을 배웠다.
