

## View Controller Catalog for iOS

### Navigaition Controllers

1. ####Navigation Controller의 역할과 Navigation Interface 의 구조

   VC의 [^presentation] 을 관리하고, 사용자 정의 뷰를 제공하는 역할을 한다. 특히 navigation bar를 커스텀하여 사용할 수 있음. 선택적으로 navigation toolbar 를 제공하고 커스텀 button로 채울 수도 있음

   <br>

   ![스크린샷 2019-11-27 오후 6.39.01](/Users/kimhyowon/Desktop/스크린샷 2019-11-27 오후 6.39.01.png)

   <center>Custom View + Navigation View + Tab bar View + Window = Assembled views</center>
_Navigation bar와 toolbar를 커스텀 하는 것은 오직 UINavigationController와 UIViewController 클래스의 매서드를 이용해서만 가능하다. (직접 navigation 구조에 접근하는 것은 불가하다.)_
   
<br>
   
2. ####Navigation Interface 의 Objects

   **Navigation Controller**

   - Navigation Controller는 여러 객체를 사용하여 Navigation Interface를 구현한다. 이러한 객체 중 일부를 제공하고(특히 표시하려는 컨텐츠를 뷰 컨트롤러에 제공해야함), 나머지는 Navigation Controller 자체에서 생성된다. 
   - navigation controller 알림에 응답하기 위해 delegate를 제공할 수도 있다.
   - Navigation bar와 toolbar는 일부 모양과 동작만 커스텀 할 수 있고, navigation controller만 구성 및 표시를 담당함.

   - Navigation Controller는 내비게이션 인터페이스에 사용되는 navigation bar 및 toolbar와 같은 view를 작성하고 해당 view를 관리한다.

   - Navigation Controller는 `UINavigationBar`의 delegate를 자동으로 자신으로 할당해 다른 객체가 해당 관계를 변경하지 못하게 한다.
   - Navigation Controller는 새로운 VC를 Navigation stack에 넣거나 VC를 stack에서 가져와 사용자 작업에 응답하는 동작을 한다.

   <br>

   **UINavigationController 가 관리하는 Objects**

   <br>

   ![스크린샷 2019-11-27 오후 6.37.33](/Users/kimhyowon/Desktop/스크린샷 2019-11-27 오후 6.37.33.png)

   <br>

   - viewControllers : NSArray
   - navigationBar : UINavigationBar (delegate 제공)
   - toolbar : UIToolbar
   - delegate 제공 => 커스텀 하여 사용할 수 있음

   <br>

   **Navigation Stack**

   - navigation controller가 관리되는 커스텀 view controller들을 담는 LIFO 형태의 collection 이다. 
   - stack에 가장 먼저 추가 된 컨트롤러가 root view가 되며, root는 stack에서 pop 되지 않는다. 
   - navigation stack 에서 delegate 및 다른 view controller를 수정할 수 있다.

   <br>

   UINavigation Controller와 Navigation Stack의 관계

   - viewControllers : navigation stack에 있는 모든 vc
   - topViewController: 최상위에 있는 vc
   - visibleViewController: 보여지는 vc (최상위뷰가 visibleVC가 아닐 수 있음)

   <br>

3. ####Navigation Interface 만들기

   - Navigation Interface를 위한 View Controller 정의 할때, 레벨 정하기
   - Storyboard 를 사용해 Navigation Interface 만들기
   - Code로 Navigation Interface 만들기

   <br>

4. ####View가 전체 화면을 사용해야하는지 결정할 때 Navigation Controller가 고려해야할 사항 및 설정 방법

   Navigation Controller가 전체화면을 위해 크기 조정 여부를 결정할때 고려하는 요소

   - 기본 창 (또는 부모 view)이 전체 화면 경계를 채우도록 크기가 조정 되었습니까?
   - navigation bar 가 반투명하도록 구성되어 있습니까?
   - navigation toolbar (사용 된 경우)이 반투명하도록 구성되어 있습니까?
   - 기본 뷰 컨트롤러의 `wantsFullScreenLayout`속성이 `YES`로 설정되어 있습니까?

   <br>

   전체화면을 위해 navigation view를 구성할 때 따라야 하는 것

   1. 화면 경계를 채우도록 커스텀 view 프레임을 구성

      view의 자동 크기 조정 속성도 구성해야한다. 이는 view의 크기를 조정해야 할 경우 그에 따라 컨텐츠를 조정한다. 또는 view의 크기를 조정할 때 view의 `setNeedsLayout`메서드를 호출하여 sub view의 위치를 조정해야 함을 나타낼 수 있다.

   2. navigation bar을 언더 랩하려면 탐색 컨트롤러 의 `translucent` 속성을 "Y"로 설정

   3. optional toolbar을 언더 랩하려면 도구 모음의 `translucent속성을 "Y"로 설정

   4. status bar를 언더 랩하려면 `wantsFullScreenLayout`뷰 컨트롤러 의 속성을 "Y"로 설정

   5.  `applicationFrame` 과 `UIScreen` 클래스의 `bounds`속성과 일치하도록 크기를 설정

   <br>

   + 내비게이션 컨트롤러를 modal로 표시할 경우 해당 내비게이션 컨트롤러가 제공하는 컨텐츠는 presentation을 수행하는 view controller의 view에 의해 제한됩니다.

   <br>

5. ####Navigation Stack을 관리하기 위한 옵션

   - pushViewController(), segue

     : 새로운 view controller를 navigation stack 에 push

   - popViewController()

     : 이전화면으로 돌아가는 기능을 위해 최상위 뷰 컨트롤러를 제거한다.

   - setViewController()

     : navigation stack을 이전상태로 복원할 수 있다. 이 방법은 사용자가 앱을 종료할 때 종료한 위치를 저장해두고 있어야 한다. 이 방법으로 임의의 위치로 이동할 수 있으나, 혼동될 수 있으므로 주의를 기울여야함.

   - popToRootViewController()

     : 사용자를 root view controller로 되돌린다. 즉, stack에서 root VC를 제외하고 모두 제거한다.

   - popToViewController()

     : 최상위 VC와 임의의 VC사이의 여러 개의 view를 stack에서 한번에 제거할 수 있다.

   <br>

6. ####Navigation Stack에 발생하는 event의 과정과 Navigation Controller가 보내는 메세지에 대하여

   vc를 push/pop 할 때 navigation controller는 영향을 받는 vc에게  메세지를 보내고, stack이 변경될 때 delegate를 통하여 vc들에게 메세지를 보낸다. 이때 변경 시 보내지는 알림의 순서는 아래와 같다.

   <br>

   1. **view에게 첫 알림을 보낸다.**
      - viewWillDisappear() - 가장 위에 있는 vc에게
      - viewWillAppear() - 새로 push 되는 vc에게

   2. **delegate에게 첫 알림을 보낸다.**
      - navigationController(), willShowViewController()

   3. **새 view를 자리로 이동**

   4. **이동한 후 view에게 알림을 보낸다.**
      - viewDidDisappear() - 가장 위에 있는 vc에게
      - viewDidAppear() - 새로 push 되는 vc에게

   5. **이동한 후 delegate에게 알림을 보낸다.**
      - navigationController(), didlShowViewController()

   <br>

7. ####Navigation Bar를 커스텀하는 방법

   **Navigation Bar**_는 navigation interface에서 컨트롤을 관리하는 view이며 navigation controller object로써 관리 할 때 특별한 역할을 수행합니다. 일관성을 유지하고, navigation interface를 구축하는 데 필요한 작업량을 줄이기 위해 각 navigation controller object가 고유한 navigation bar을 만들어서 해당 bar에 대한 책임을 가집니다. 필요에 따라 navigation controller는 콘텐츠 view controller 와 같은 다른 object와 상호 작용하여 이 프로세스에 도움을줍니다._

   > navigation bar를 독립적 view로 생성해 원하는대로 사용할 수도 있습니다. `UINavigationBar`클래스 의 메소드 및 특성 사용에 대한 자세한 정보는 *[UINavigationBar 클래스 참조를 참조하십시오](https://developer.apple.com/documentation/uikit/uinavigationbar)* .

   <br>

   - navigation bar object의 구성

     navigation bar의 소유자 (navigation controller 또는 custom code)는 item을 stack에서 필요에 따라 push 또는 pop 한다. 적절한 navigation을 제공하기 위해 navigation bar은 stack에서 object를 선택하기 위한 포인터를 유지한다. 대부분 navigation bar의 content는 최상위 navigation item에서 가져오지만, back item에 대한 포인터가 유지되어 back button(이전 item의 제목이 포함된)이 생성될 수 있다. 

     ![스크린샷 2019-11-27 오후 6.26.00](/Users/kimhyowon/Desktop/스크린샷 2019-11-27 오후 6.26.00.png)

     > **중요** : navigation controller와 함께 navigation bar를 사용하는 경우 navigation bar delegate 는 항상 소유하고 있는 navigation controller object로 설정됩니다. delegate를 변경하려고하면 예외가 발생합니다.

   <br>

   ​	현재 보여지고 있는 view controller와 연관된 navigation item은 가운데와 오른쪽, 이전 view contorller의 navigation item은 왼쪽에 배치된다. `UIBarButtonItem`객체 를 지정해야하지만 그림과 같이 bar button item으로 view를 추가할 수 있다.

   <br>

   ![스크린샷 2019-11-28 오후 2.59.51](/Users/kimhyowon/Desktop/스크린샷 2019-11-28 오후 2.59.51.png)

   <br>

8. ####Navigation Toolbar를 표시/숨기는 방법과 Toolbar Item에 대하여

   - Navigation Toolbar 표시하거나 숨길 때  `UINavigationController`의   `setNavigationBarHidden:animated:` 메서드를 사용해야한다.  `UINavigationBar`객체의 `hidden` 속성을 직접 수정하여 navigation bar를 숨기면 안됨. 

   - 숨기는 가장 일반적인 방법은 터치 이벤트를 가로 채서 navigation bar의 가시성을 토글하는 것이다. 예를 들어 사진 앱에서 단일 이미지를 전체 화면으로 표시 할 때 navigation bar를 숨긴다.

[^presentation]: 화면에 표기되는 방식