### Unity의 기본이 되는 5개의 View

1. Project View : 게임을 만들데 사용되는 파일들(Assets)을 관리.
2. Hierarchy View : 오브젝트들을 관리.
3. Scene View : 게임을 제작.
4. Game View : Scene View 에서 만든 게임이 사용자에게 어떻게 보이는지 볼 수 있는.
5. Inspector View : 파일이나 오브젝트들의 정보를 보거나 설정을 변경 관리.


### Project View
* import : 어떤 파일들(Assets)를 프로젝트에 넣는 것.
* Meta : Assets의 정보를 뜻하며 Assets를 넣으면 자동으로 생성된다.

### Hierarchy View(계층)
Game Object : Game을 만들 때 Scene 내에서 사용되는 물체의 기본 단위. Object들이 하는 역할을 Component를 통하여 정의를 해준다.


### Inspector View
Component : 하나의 독립적인 기능을 수행하는 것.

* Transfrom 
	* Object들의 크기, 위치 등 기본 정보를 위한 컴포넌트
	* 모든 Object가 가지고 있음.
	* 삭제가 되지 않는다.
* Sprite Renderer
	* 화면에 2D 이미지를 그려주기 위한 컴포넌트
	* Sprite : 이미지를 지정.
	* Color : 지정한 색으로 변경.
	* Filp : X축 반전, Y축 반전.
	* Order in Layer : Object 들이 겹쳤을 때 명시적으로 오브젝트의 순서를 고정.

### Scene View
Object를 실질적으로 배치를 하고, Scene을 만들어 내는 공간.

Scene View Toolbar
* Hand Tool(Q) : Scene 화면을 이동.
* Move Tool(W) : Object 위치를 변경.
* Rotate Tool(E) : Object를 회전.(XYZ)
* Scale Tool(R) : Object 크기를 변경.
* Rect Tool(T) : 위의 기능을 한번에 다할 수 있음.


### Game View
* Scene View에서 작업한 내용을 사용자들에게 어떻게 보여지는지 확인.
* 카메라 영역에서 제외된 Object는 보여지지 않는다.
* 원하는 해상도의 View 를 볼 수 있다.

Play Toolbar 
* 재생버튼(ctrl+p), 일시정지(ctrl+shift+p), 프레임 이동.



