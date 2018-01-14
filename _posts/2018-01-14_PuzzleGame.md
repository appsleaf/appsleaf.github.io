##### cocos2d-x 2.x 버전 GameLayer.h
```c++
//  GameLayer.h

#ifndef GameLayer_h
#define GameLayer_h

#include "cocos2d.h"

class GameLayer : public cocos2d::CCLayer
{
public:
	bool init();
	static cocos2d::CCScene* scene();
	CREATE_FUNC(GameLayer);
};

#endif /* GameLayer_h */
```

##### cocos2d-x 3.x 버전 GameLayer.h
```c++
//  GameLayer.h
#ifndef GameLayer_h
#define GameLayer_h

#include "cocos2d.h"

class GameLayer : public cocos2d::Layer
{
public:
    bool init();
    static cocos2d::Scene* scene();
    CREATE_FUNC(GameLayer);
};

#endif /* GameLayer_h */
```

##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
//  GameLayer.cpp
#include "GameLayer.h"

bool GameLayer::init()
{
	if ( CCLayer::init() == false)
	{
		return false;
	}
	
	return true;
}

cocos2d::CCScene* GameLayer::scene()
{
	cocos2d::CCScene* pScene = cocos2d::CCScene::create();
	
	GameLayer* pLayer = GameLayer::create();
	pScene->addChild(pLayer);
	
	return pScene;
}
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
//  GameLayer.cpp
#include "GameLayer.h"

bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

    return true;
}

cocos2d::Scene* GameLayer::scene()
{
    cocos2d::Scene* pScene = cocos2d::Scene::create();

    GameLayer* pLayer = GameLayer::create();
    pScene->addChild(pLayer);

    return pScene;
}
```

### Helloworld Scene 대신 GameLayer Scene이 나타내게 변경.

##### cocos2d-x 2.x AppDelegate.cpp
```c++
//  AppDelegate.cpp
#include "GameLayer.h"

bool AppDelegate::applicationDidFinishLaunching()
{
	// initalize director
	CCDirector *pDirector = CCDirector::sharedDirector();
	pDirector->setOpenmGLView(CCEGLView::sharedOpenGLView());
	
	// turn on display FPS
	pDirector->setDisplayStats(true);
	
	// set FPS. the default value is 1.0/60 if you don't call this
	pDirector->setAnimationInterval(1.0 / 60);
	
	// create a scene. it's an autorelease object
	CCScene *pScene = Helloworld::scene();
	
    // run
    pDirector->runWithScene(pScene);

	return true;
}
```

##### cocos2d-x 3.x 버전 AppDelegate.cpp
```c++
//  AppDelegate.cpp
#include "GameLayer.h"

bool AppDelegate::applicationDidFinishLaunching() 
{
    // initialize director
    auto director = Director::getInstance();

    // turn on display FPS
    director->setDisplayStats(true);

    // set FPS. the default value is 1.0/60 if you don't call this
    director->setAnimationInterval(1.0f / 60);

    register_all_packages();

    // create a scene. it's an autorelease object
    //auto scene = HelloWorld::createScene();
    auto pScene = GameLayer::scene();
    // run
    director->runWithScene(pScene);

    return true;
}

```



### 백그라운드 이미지를 넣어준다.

##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
//  GameLayer.cpp

bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

    cocos2d::CCSprite* pBackgroundSprite = cocos2d::CCSprite::create("Background.png");
    pBackgroundSprite->setPosition(cocos2d::CCPointZero);
    pBackgroundSprite->setAnchorPoint(ccp(0.0f, 0.0f));
    addChild(pBackgroundSprite);

    return true;
}

```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
//  GameLayer.cpp

bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

    cocos2d::Sprite* pBackgroundSprite = cocos2d::Sprite::create("Background.png");
    pBackgroundSprite->setPosition(cocos2d::Vec2(0,0));
    pBackgroundSprite->setAnchorPoint(cocos2d::Vec2(0,0));
    this->addChild(pBackgroundSprite);

    return true;
}
```

> ## 오리엔테이션(Orientation)
> 화면 방향을 지정하는 용어
> 세로 : Portait 모드, 가로 : Landscape 모드
> 


### 해상도 설정.
##### cocos2d-x 2.x AppDelegate.cpp
```c++
//  AppDelegate.cpp
#include "GameLayer.h"

bool AppDelegate::applicationDidFinishLaunching()
{
	// initalize director
	CCDirector *pDirector = CCDirector::sharedDirector();
	pDirector->setOpenmGLView(CCEGLView::sharedOpenGLView());
	
	// 추가 
	CCSize winSize = CCDirector::sharedDirector()->getWinSize();
	CCEGLView::sharedOpenGLView()->setFrameSize(winSize.width, winSize.height);
	CCEGLView::sharedOpenGLView()->setDesignResolutionSize(768.0f, 1024.0f, kResolutionShowAll);
	// 추가
	
	// turn on display FPS
	pDirector->setDisplayStats(true);
	
	// set FPS. the default value is 1.0/60 if you don't call this
	pDirector->setAnimationInterval(1.0 / 60);
	
	// create a scene. it's an autorelease object
	CCScene *pScene = Helloworld::scene();
	
    // run
    pDirector->runWithScene(pScene);

	return true;
}
```
> 이미지 비율
> 
> * kResolutionExactFit : 화면에 맞춰서 채움.
> * kResolutionNoBorder : 있는 그대로 보여줌. 해상도에 따라 이미지가 잘릴 수 있음.
> * kResolutionShowAll : 비율에 맞게 보여줌. 비율에 맞춰 레터박스가 생길 수 있음.

##### cocos2d-x 3.x 버전 AppDelegate.cpp
```c++
//  AppDelegate.cpp
#include "GameLayer.h"

bool AppDelegate::applicationDidFinishLaunching() 
{
    // initialize director
    auto director = Director::getInstance();
    
    // 추가
    auto glview = director->getOpenGLView();
    if(!glview) {
        director->setOpenGLView(glview);
    }
    
    // Set the design resolution
    glview->setDesignResolutionSize(768.0f, 1024.0f, ResolutionPolicy::SHOW_ALL);
    // 추가

    // turn on display FPS
    director->setDisplayStats(true);

    // set FPS. the default value is 1.0/60 if you don't call this
    director->setAnimationInterval(1.0f / 60);

    register_all_packages();

    // create a scene. it's an autorelease object
    //auto scene = HelloWorld::createScene();
    auto pScene = GameLayer::scene();
    // run
    director->runWithScene(pScene);

    return true;
}
```
> ResolutionPolicy
> 
> * EXACT_FIT : 화면에 맞춰서 채움.
> * NO_BORDER : 있는 그대로 보여줌. 해상도에 따라 이미지가 잘릴 수 있음.
> * SHOW_ALL : 비율에 맞게 보여줌. 비율에 맞춰 레터박스가 생길 수 있음.
> * FIXED_HEIGHT : 높이를 고정
> * FIXED_WIDTH : 너비를 고정.


### 5.1.6 공통 선언 파일
* 상수 및 편의를 위한 코드를 관리.


##### cocos2d-x 2.x 버전 Common.h
```c++
//  Common.h
#ifndef Common_h
#define Common_h

#define DESIGN_WIDTH	768.0f
#define DESIGN_HEIGHT	1024.0f

#endif /* Common_h */
```

##### cocos2d-x 3.x 버전 Common.h
```c++
//  Common.h
#ifndef Common_h
#define Common_h

#define DESIGN_WIDTH	768.0f
#define DESIGN_HEIGHT	1024.0f

#endif /* Common_h */
```

##### cocos2d-x 2.x AppDelegate.cpp
```c++
//  AppDelegate.cpp
// 추가
#include "Common.h"
// 추가

bool AppDelegate::applicationDidFinishLaunching()
{
	/* 변경
	CCEGLView::sharedOpenGLView()->setDesignResolutionSize(768.0f, 1024.0f, kResolutionShowAll);
	*/ 
	
	CCEGLView::sharedOpenGLView()->setDesignResolutionSize(DESIGN_WIDTH, DESIGN_HEIGHT, kResolutionShowAll);
	// 변경
}
```

##### cocos2d-x 3.x 버전 AppDelegate.cpp
```c++
//  AppDelegate.cpp
// 추가
#include "Common.h"
// 추가

bool AppDelegate::applicationDidFinishLaunching() 
{
    /* 변경
    glview->setDesignResolutionSize(768.0f, 1024.0f, ResolutionPolicy::SHOW_ALL);
    */
    
    glview->setDesignResolutionSize(DESIGN_WIDTH, DESIGN_HEIGHT, ResolutionPolicy::SHOW_ALL);
    // 변경
}
```

### 5.1.7 네임스페이스(Namespace)
* 네임스페이스로 서로 다른 라이브러리 등에서 같은 클래스 이름을 사용할 때 충돌나지 않도록 보호.
* cocos2d 네임스페이스를 매번 입력하지 않도록 <b>USING\_NS\_CC</b> 를 이용.


##### cocos2d-x 2.x 버전 Common.h
```c++
//  Common.h
#ifndef Common_h
#define Common_h

//추가
#include "cocos2d.h"

USING_NS_CC;
// 추가

#endif /* Common_h */
```

##### cocos2d-x 3.x 버전 Common.h
```c++
//  Common.h
#ifndef Common_h
#define Common_h

//추가
#include "cocos2d.h"

USING_NS_CC;
// 추가

#endif /* Common_h */
```

#### USING\_NS\_CC 반영.
##### cocos2d-x 2.x 버전 GameLayer.h
```c++
//  GameLayer.h
/* 변경
#include "cocos2d.h"

class GameLayer : public cocos2d::CCLayer
{
public:
	bool init();
	static cocos2d::CCScene* scene();
	CREATE_FUNC(GameLayer);
};
*/
#include "Common.h"

class GameLayer : public CCLayer
{
public:
	bool init();
	static CCScene* scene();
	CREATE_FUNC(GameLayer);
};
```
##### cocos2d-x 3.x 버전 GameLayer.h
```c++
/* 변경
#include "cocos2d.h"

class GameLayer : public cocos2d::Layer
{
public:
    bool init();
    static cocos2d::Scene* scene();
    CREATE_FUNC(GameLayer);
};
*/

#include "Common.h"

class GameLayer : public Layer
{
public:
    bool init();
    static Scene* scene();
    CREATE_FUNC(GameLayer);
};
// 변경
```


##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
//  GameLayer.cpp
/* 변경
bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

    cocos2d::CCSprite* pBackgroundSprite = cocos2d::CCSprite::create("Background.png");
    pBackgroundSprite->setPosition(cocos2d::CCPointZero);
    pBackgroundSprite->setAnchorPoint(ccp(0.0f, 0.0f));
    addChild(pBackgroundSprite);

    return true;
}

cocos2d::CCScene* GameLayer::scene()
{
	cocos2d::CCScene* pScene = cocos2d::CCScene::create();
	
	GameLayer* pLayer = GameLayer::create();
	pScene->addChild(pLayer);
	
	return pScene;
}
*/
bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

   	CCSprite* pBackgroundSprite = CCSprite::create("Background.png");
    pBackgroundSprite->setPosition(CCPointZero);
    pBackgroundSprite->setAnchorPoint(ccp(0.0f, 0.0f));
    addChild(pBackgroundSprite);

    return true;
}

CCScene* GameLayer::scene()
{
	CCScene* pScene = CCScene::create();
	
	GameLayer* pLayer = GameLayer::create();
	pScene->addChild(pLayer);
	
	return pScene;
}
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
//  GameLayer.cpp
/* 변경
bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

    cocos2d::Sprite* pBackgroundSprite = cocos2d::Sprite::create("Background.png");
    pBackgroundSprite->setPosition(cocos2d::Vec2(0,0));
    pBackgroundSprite->setAnchorPoint(cocos2d::Vec2(0,0));
    this->addChild(pBackgroundSprite);

    return true;
}

cocos2d::Scene* GameLayer::scene()
{
    cocos2d::Scene* pScene = cocos2d::Scene::create();

    GameLayer* pLayer = GameLayer::create();
    pScene->addChild(pLayer);

    return pScene;
}
*/

bool GameLayer::init()
{
    if ( Layer::init() == false)
    {
        return false;
    }

    Sprite* pBackgroundSprite = Sprite::create("Background.png");
    pBackgroundSprite->setPosition(Vec2(0,0));
    pBackgroundSprite->setAnchorPoint(Vec2(0,0));
    this->addChild(pBackgroundSprite);

    return true;
}

Scene* GameLayer::scene()
{
   	Scene* pScene =Scene::create();

    GameLayer* pLayer = GameLayer::create();
    pScene->addChild(pLayer);

    return pScene;
}
```

## 5.2.1 게임 오브젝트 그리기.

##### cocos2d-x 2.x 버전 GameLayer.h
```c++
class GameLayer : public CCLayer
{
public:
	// 추가
	void StartGame();
	// 추가
// 추가
protected:
	CCSize m_winSize;
// 추가
}
```

##### cocos2d-x 3.x 버전 GameLayer.h
```c++
class GameLayer : public Layer
{
public:
	// 추가
	void StartGame();
	// 추가
// 추가
protected:
	Size m_winSize;
// 추가
}
```

##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
bool GameLayer::init()
{
	...
	addChild(pBackgroundSprite);
	
	// 추가
	m_winSize = CCDirector::sharedDirector()->getWinSize();
	
	StartGame();
	// 추가
	
	return ture;
}

// 추가
void GameLayer::StartGame()
{
	CCSprite* pGameObject = CCSprite::create("Blue.png");
	pGameObject->setPosition(ccp(m_winSize.width / 2, m_winSize.height /2 ));
	addchild(pGameObject);
}
// 추가
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
bool GameLayer::init()
{
	...
	this->addChild(pBackgroundSprite);
	
	// 추가
   	m_winSize = Director::getInstance()->getWinSize();
	
	StartGame();
	// 추가
	
	return ture;
}

// 추가
void GameLayer::StartGame()
{
    Sprite* pGameObject = Sprite::create("Blue.png");
    pGameObject->setPosition(m_winSize.width / 2, m_winSize.height / 2);
    this->addChild(pGameObject);
}
// 추가
```

```c++
m_winSize = Director::getInstance()->getWinSize();
```
> m_winSize 변수에 스크린의 크기를 저장.


## 5.2.2 게임 오브젝트 모두 배치하기.
* 8x8 게임판 만들기
* 이미지 크기 : 96x96
* 이미지 종류 : 7
* MAX_ROW_COUNT : 보드에 배치할 수 있는 게임 오브젝트의 총 행의 수.

##### cocos2d-x 3.x 버전 Common.h
```c++
// 추가
#define ROW_COUNT		8
#define COLUMN_COUNT	8
#define MAX_ROW_COUNT	10

#define TYPE_COUNt		7

#define OBJECT_WIDTH	96
#define OBJECT_HEIGHT	96
// 추가
```

##### cocos2d-x 2.x 버전 GameLayer.h
```c++
class GameLayer : public CCLayer
{
protected:

	CCSize m_winSize;
	// 추가
	CCSprite* m_pBoard[COLUMN_COUNT][MAX_ROW_COUNT];
	// 추가
}
```

##### cocos2d-x 3.x 버전 GameLayer.h
```c++
class GameLayer : public Layer
{

protected:
	Size m_winSize;
	// 추가
	Sprite* m_pBoard[COLUMN_COUNT][MAX_ROW_COUNT];
	// 추가
}
```

##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
void GameLayer::StartGame()
{
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
            CCSprite* pGameObject = CCSprite::create("Blue.png");
            m_pBoard[x][y] = pGameObject;

            float xPos = floorf(x * OBJECT_WIDTH);
            float yPos = m_winSize.height - floorf(y * OBJECT_HEIGHT);

            pGameObject->setAnchorPoint(ccp(0.0f, 1.0f));
            pGameObject->setPosition(ccp(xPos,yPos));

            addChild(pGameObject, 1);
        }
    }
}
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
void GameLayer::StartGame()
{
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
            Sprite* pGameObject = Sprite::create("Blue.png");
            m_pBoard[x][y] = pGameObject;

            float xPos = floorf(x * OBJECT_WIDTH);
            float yPos = m_winSize.height - floorf(y * OBJECT_HEIGHT);

            pGameObject->setAnchorPoint(Vec2(0, 1));
            pGameObject->setPosition(Vec2(xPos,yPos));

            this->addChild(pGameObject, 1);
        }
    }
}
```
> cocos2d-x의 좌표계는 좌측 하단이 (0,0) 우측 상단으로 갈수록 x,y 증가한다. <br/>
> 보드는 좌측 상단이 (0,0)임으로 화면 높이를 기준으로 역계산해준다.


## 5.2.3 7가지 종류의 게임 오브젝트 배치하기.
##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
void GameLayer::StartGame()
{
	srand(time(NULL));
	
	static std::string objectNames[TYPE_COUNT] = 
	{
		"Blue.png",
		"Brown.png",
		"Green.png",
		"Pink.png",
		"Purple.png",
		"Red.png",
		"Yellow.png",
	};
	
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
            int type = rand() % TYPE_COUNT;
            
            CCSprite* pGameObject = CCSprite::create(objectNames[type].c_str());
            m_pBoard[x][y] = pGameObject;

            float xPos = floorf(x * OBJECT_WIDTH);
            float yPos = m_winSize.height - floorf(y * OBJECT_HEIGHT);

            pGameObject->setAnchorPoint(ccp(0.0f, 1.0f));
            pGameObject->setPosition(ccp(xPos,yPos));

            addChild(pGameObject, 1);
        }
    }
}
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
void GameLayer::StartGame()
{
    srand(time(NULL));

    static std::string objectNames[TYPE_COUNT] =
    {
        "Blue.png",
        "Brown.png",
        "Green.png",
        "Pink.png",
        "Purple.png",
        "Red.png",
        "Yellow.png",
    };

    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
            int type = rand() % TYPE_COUNT;

            Sprite* pGameObject = Sprite::create(objectNames[type].c_str());
            m_pBoard[x][y] = pGameObject;

            float xPos = floorf(x * OBJECT_WIDTH);
            float yPos = m_winSize.height - floorf(y * OBJECT_HEIGHT);

            pGameObject->setAnchorPoint(Vec2(0, 1));
            pGameObject->setPosition(Vec2(xPos,yPos));

            this->addChild(pGameObject, 1);
        }
    }
}
```
> srand(time(NULL)) : 랜덤 함수를 사용하려면 먼저 seed 값을 입력해야함. <br/>
> time 함수를 이용해서 항상 다른 랜덤값이 나오게 됨.

## 5.2.4 좌표 계산 유틸리티 클래스

##### cocos2d-x 3.x 버전 Common.h
```c++
// 추가
class Common
{
public:
    static float ComputeX(float x);
    static float ComputeY(float y);
    static CCPoint ComputeXY(float x, float y);

    static int ComputeBoardX(float x);
    static int ComputeBoardY(float y);
};
// 추가
```

##### cocos2d-x 3.x 버전 Common.h
```c++
// 추가
class Common
{
public:
    static float ComputeX(float x);
    static float ComputeY(float y);
    static Vec2 ComputeXY(float x, float y);

    static int ComputeBoardX(float x);
    static int ComputeBoardY(float y);
};
// 추가
```

##### cocos2d-x 2.x 버전 Common.cpp
```c++
#include "Common.h"

float Common::ComputeX(float x)
{
    return floorf(x * OBJECT_WIDTH);
}
float Common::ComputeY(float y)
{
    return CCDirector::sharedDirector()->getWinSize().height - floorf(y * OBJECT_HEIGHT);
}
CCPoint Common::ComputeXY(float x, float y)
{
    return ccp(ComputeX(x), ComputeY(y));
}
int Common::ComputeBoardX(float x)
{
    return (int)(x / floorf(OBJECT_WIDTH));
}
int Common::ComputeBoardY(float y)
{
    return (int)(y / floorf(OBJECT_HEIGHT));
}
```

##### cocos2d-x 3.x 버전 Common.cpp
```c++
#include "Common.h"

float Common::ComputeX(float x)
{
    return floorf(x * OBJECT_WIDTH);
}
float Common::ComputeY(float y)
{
    return Director::getInstance()->getWinSize().height - floorf(y * OBJECT_HEIGHT);
}
Vec2 Common::ComputeXY(float x, float y)
{
    return Vec2(ComputeX(x), ComputeY(y));
}
int Common::ComputeBoardX(float x)
{
    return (int)(x / floorf(OBJECT_WIDTH));
}
int Common::ComputeBoardY(float y)
{
    return (int)(y / floorf(OBJECT_HEIGHT));
}
```


##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
void GameLayer::StartGame()
{
    srand(time(NULL));
	... 
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
            int type = rand() % TYPE_COUNT;
            
            CCSprite* pGameObject = CCSprite::create(objectNames[type].c_str());
            m_pBoard[x][y] = pGameObject;

            pGameObject->setAnchorPoint(ccp(0.0f, 1.0f));
            pGameObject->setPosition(Common::ComputeXY(x, y)));

            addChild(pGameObject, 1);
        }
    }
}
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
void GameLayer::StartGame()
{
    srand(time(NULL));
	... 
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
            int type = rand() % TYPE_COUNT;

            Sprite* pGameObject = Sprite::create(objectNames[type].c_str());
            m_pBoard[x][y] = pGameObject;

            float xPos = floorf(x * OBJECT_WIDTH);
            float yPos = m_winSize.height - floorf(y * OBJECT_HEIGHT);

            pGameObject->setAnchorPoint(Vec2(0, 1));
            pGameObject->setPosition(Common::ComputeXY(x, y));

            this->addChild(pGameObject, 1);
        }
    }
}
```

## 5.2.5 Z Order(우선 순위)
```c++
addChild(pGameObject, 1);
```
* addChild 두번째 인자가 Z Order로 불리는, 여러 오브젝트들의 그리는 순서를 결정해주는 값.
* 두번째 인자가 없는 경우, 0 값을 사용하게 됨.
* Z Order가 작은 순서부터 차례대로 그려짐.


##### cocos2d-x 2.x 버전 GameLayer.cpp
```c++
// 추가
enum
{
	zBackground = 0,
	zGameObject = 1,
};
// 추가

bool GameLayer::init()
{
	...
	
	/* 변경
	addChild(pBackgroundSprite);
	*/
	addChild(pBackgroundSprite, zBackground);
}

void GameLayer::StartGame()
{
	... 
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
			...
			/* 변경
            addChild(pGameObject, 1);
            */
            addChild(pGameObject, zGameObject);
        }
    }
}
```

##### cocos2d-x 3.x 버전 GameLayer.cpp
```c++
// 추가
enum
{
	zBackground = 0,
	zGameObject = 1,
};
// 추가

bool GameLayer::init()
{
	...
	
	/* 변경
	this->addChild(pBackgroundSprite);
	*/
	this->addChild(pBackgroundSprite, zBackground);
}

void GameLayer::StartGame()
{
	... 
    for (int x = 0; x < COLUMN_COUNT; ++x)
    {
        for (int y = 0; y < ROW_COUNT; ++y)
        {
        	...
        	/* 변경
            this->addChild(pGameObject, 1);
            */
            this->addChild(pGameObject, zGameObject);
        }
    }
}
```


 