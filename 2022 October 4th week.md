# 새롭게 알게 된 내용들

인프런 Flutter 앱 개발 강의 1주차를 들으면서 새롭게 학습한 내용들이다.

## TextField

이름 그대로 텍스트를 입력할 수 있는 영역을 말하는 위젯이다.
대부분의 앱에서 찾아볼 수 있는 부분이고, 유저와 앱이 상호작용하는 가장 대표적인 기능중 하나이다.

```dart
class searchTextField extends StatelessWidget {
  final String hintText;
  const searchTextField(this.hintText, {super.key});

  @override
  Widget build(BuildContext context) {
    return TextField(
      decoration: InputDecoration(
          hintText: hintText,
          border: OutlineInputBorder(
            borderSide: BorderSide(color: Colors.black),
          ),
          suffixIcon: IconButton(
            icon: Icon(Icons.search),
            onPressed: () {
              print('search icon pressed');
            },
          )),
    );
  }
}
```

예제 코드를 보면서 확인해보자.

이 위젯에서 받는 인자는 여러 개가 있겠지만, 단순히 모양을 예쁘게 보이는게 전부라면 `decoration`하나만 넣어도 괜찮다.

### decoration
`decoration`은 `InputDecoration`이라는 클래스를 받는데 `InputDecoration`이라는 클래스가 TextField를 꾸미는 대표적인 역할을 한다.

`hintText`는 입력하기 전에 안내해주는 희미한 문구를 적을 수 있게 해준다.

Swift에서는 이를 **Placeholder**라고 불렀고 다른데서도 그렇게 부르길래 그게 정확한 명칭이라고 알고 있었는데, 여기서는 hintText라는 다소 생소한 단어를 써서 조금 당황했다.


`border`은 TextField의 테두리 부분을 꾸밀 수 있게 해준다.

여기에는 `OutlineInputBorder`라는 클래스가 들어간다.


`suffixIcon`은 우리가 흔히 보는 검색 아이콘자리에 들어가는 아이콘을 설정해준다.

당연히 검색이니까 검색 아이콘을 넣었지만 다른 아이콘을 넣을 수도 있다.

여기서는 `IconButton`이라는 클래스를 넣어서 아이콘을 누를 수 있게 했다.

물론 기능은 없다.

## ListView

리스트 형태로 위에서 아래로 쭉 늘어지게 보여주는 위젯이다.

새 스마트 폰을 사면 기본적으로 들어있는 앱들에서도 볼 수 있고 거의 대부분의 앱, 심지어 게임 앱에서도 볼 수 있는 위젯이다.

```dart
Expanded(
  child: ListView.builder(
    itemCount: dataList.length,
    itemBuilder: ((context, index) {
      Map<String, dynamic> data = dataList[index];
      String category = data["category"];
      String imgUrl = data["imgUrl"];
      return foodContainerButton(imgUrl, category);
    })))
```

예제를 보면서 확인해보자.

`ListView`는 `builder`를 통해 생성한다.

`builder`는 `itemCount`, `itemBuilder`라는 매개변수를 갖는다.

`itemCount`는 말 그대로 아이템의 개수를 받고, `itemBuilder`는 어떤 요소가 들어가는지 람다 함수를 받는다.

대부분 이 람다 함수는 `Card`를 반환하는 것으로 알고 있다. (여기서는 foodContainerButton이 카드이다.)

람다 함수 내부에서 `Card`를 만들어서 반환하면 `ListView.builder`가 이를 받아서 리스트를 보여주는 형태이다.

그렇다면 Card는 무엇일까?

### Card

Card 위젯은 카드 모양의 위젯을 만들어주는 위젯으로 주로 그리드 뷰나 리스트 뷰와 같은데서 사용한다.

사용하면서 든 의문은 굳이 Card라는 것을 만들 필요가 있었을까? 싶을 정도로 뭔가 들어가는게 없었다.

Container를 써도 될 거 같은데라는 생각이 들었는데, 그리드 뷰와 리스트 뷰에는 Container를 쓸 수 없어서 Card를 쓰는 거 같다.

아니 바꿔 말하면 Card는 그리드 뷰와 리스트 뷰만을 위해 나온거 같다.

예제 코드를 보면 이렇다.

```dart
      Card(
        margin: const EdgeInsets.all(8.0),
        child: Stack(
          alignment: Alignment.center,
          children: [
            Image.network(
              imgUrl,
              width: double.infinity,
              height: 120,
              fit: BoxFit.cover,
            ),
            Container(
              width: double.infinity,
              height: 120,
              color: Colors.black.withOpacity(0.5),
            ),
            Text(
              category,
              style: TextStyle(
                color: Colors.white,
                fontSize: 36,
              ),
            ),
          ],
        ));
```

카드는 child를 하나 받을 수 있는데, 이 점까지 `Container`와 거의 유사하다.

여기서도 그냥 `Container`처럼 만들어서 사실 Card가 Container와 어떤 정확한 차이점이 있는지 모르겠다.

아직까지는 그냥 리스트 뷰 용 컨테이너 느낌이 강하다.

## Drawer

지금까지는 `appBar`에는 그냥 타이틀만 들어간다고 생각했다.

사실 그도 그럴만한게 `appBar`에서 `Drawer`를 받는 매개변수가 없어서 의아해했었다.

그런데 `appBar`에서 받는게 아니라 `scaffold`에서 `drawer`인자를 받고 있었다.

`drawer`인자는 `Drawer` 클래스를 받고 `Drawer`에서는 body에서 했던 것과 비슷하게 `Column`을 넣어서 내용을 구성할 수 있다.

예제 코드를 보면 이렇다. 내용이 조금 길다.

```dart
    Drawer(
      child: Column(
        children: [
          DrawerHeader(
            margin: const EdgeInsets.all(0),
            decoration: BoxDecoration(
              color: Colors.amber,
            ),
            child: SizedBox(
              width: double.infinity,
              child: Column(
                children: [
                  CircleAvatar(
                      radius: 36,
                      backgroundColor: Colors.white,
                      child: Padding(
                        padding: EdgeInsets.all(8.0),
                        child: Image.network(
                          "https://i.ibb.co/CwzHq4z/trans-logo-512.png",
                          width: 62,
                        ),
                      )),
                  SizedBox(
                    height: 16,
                  ),
                  Text(
                    "NickName",
                    style: TextStyle(
                      fontSize: 18,
                      fontWeight: FontWeight.bold,
                    ),
                  ),
                  Text(
                    "Email@email.com",
                    style: TextStyle(
                      fontSize: 16,
                    ),
                  ),
                ],
              ),
            ),
          ),
          AspectRatio(
            aspectRatio: 12 / 4,
            child: PageView(
              children: [
                Image.network(
                  "https://i.ibb.co/Q97cmkg/sale-event-banner1.jpg",
                ),
                Image.network(
                  "https://i.ibb.co/GV78j68/sale-event-banner2.jpg",
                ),
                Image.network(
                  "https://i.ibb.co/R3P3RHw/sale-event-banner3.jpg",
                ),
                Image.network(
                  "https://i.ibb.co/LRb1VYs/sale-event-banner4.jpg",
                ),
              ],
            ),
          ),
          customListTile("구매내역"),
          customListTile("저장한 레시피")
        ],
      ),
    );
```

`Drawer`안에서 `Column`을 `child`의 인자로 넘겨주었는데, 잘 보면 `Column`의 `children`안에 `DrawerHeader`라는 것이 들어있다.

### DrawerHeader

`DrawerHeader`는 `Drawer`안에서만 쓸 수 있고, `Drawer`의 윗부분을 구성해주는 역할을 하고 있다. 

`DrawerHeader`도 여기서는 `Container`와 거의 유사하게 작성되었다.

일단은 그저 사진을 보여주고 특별하게 칸을 구성해주는 느낌으로 구성했다.

### AspectRatio

위의 예제 코드와 이어지는데, `AspectRatio`는 일정 비율로 구성 요소를 보여준다.

위에서는 12 / 4 라고 했는데 여기서 이 의미는 가로와 세로가 12 대 4로 3 : 1이라는 비율이라는 뜻이다.

이렇게 설정해놓으면 요소를 저 비율에 맞춰서 보여준다.

### PageView

역시나 위의 예제 코드와 이어진다.

`PageView`는 특정 요소를 가로로 넘기면서 보여주는데 특정 요소에 걸치게 보여준다.

`Column`과 같이 `children`인자를 받는데 이는 당연한 이야기다.

여러 페이지를 가로로 넘기면서 보여줘야하는데 `children`이 아니면 말이 안된다.

# 마치며

이번 주차에는 위의 새로운 위젯들을 배웠다.

전부 외우는건 말도 안되지만, 어느정도 이런게 있었지 하는 심정으로 하나씩 기록해놓으면 좋을거 같다.
