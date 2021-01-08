---
title: "아이오닉 모바일 앱에 PDF 뷰어 및 줌 확대 축소 기능 만들기"
excerpt: "모바일 PDF 및 사진 뷰어 구현 단계와 소스 코드 공유"
header:
  teaser: /assets/images/2021-1-6.jpg
  overlay_image: /assets/images/2021-1-6.jpg
  overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Hybrid-App
tags:
- 모바일앱
- React
- Ionic-react
---


#### 2021년 1월 6일 개발일지 - 현재 진행 중인 일과 기술 스택:
안드로이드와 iOS 를 한 번에 빌드하는 하이브리드 모바일 앱의 프론트엔드를 개발하고 있으며 프레임워크로 아이오닉 (Ionic) 과 리액트 (React) 를 사용하고 있다.

## PDF/사진 뷰어 구현 하는 단계
1. 서버에서 파일 이미지들을  `data` 에 url 을 `string[]` 으로 받아서 `setData()` 한다.
2. 모든 이미지를 `map` 하여 화면 아래에 넣고 `overflow: sroll` 로 설정한다. 자세한 CSS 는 아래 코드에서 확인 가능하다.
3. 화면 아래에 각 이미지를 클릭하면 해당 사진이 `currentView` state 에 세팅이 되고 해당 사진이 화면에 보여지도록 한다.
4. 줌인 버튼(+)을 생성하고 줌을 클릭하면 이미지 사이즈를 200%로 확대하고 줌아웃 버튼(-) 으로 변경한다.
5. 줌으로 화면이 확대 된 상태에서 스크롤을 하면 모든 사진 부분이 보여지도록   `overflow: sroll` 로 설정한다.

### PDF/사진 뷰어 구현 화면
![PDF/사진 뷰어 구현 화면](/assets/images/2021-1-6-1.png)


### PDF/사진 뷰어 구현을 위한 Ionic-React 소스 코드 일부
```tsx

const [data, setData] = useState<any>()
const [currentView, setCurrentView] = useState<number>()
const [zoom, setZoom] = useState(false)
const cName = 'mypage-trial-agreement-sign-'

const clickedImage = (i: number) => {
  setCurrentView(i)
}

const clickZoom = () => {
  setZoom(!zoom)
}

const close = () => {
  history.goBack()
}

return (
<IonPage id="mypage-trial-agreement-sign-page">
      <AppHeaderModal title="PDF/사진 뷰어" closeActionRightEnd={close} />
      <IonContent>
        {data && (
          <div className={cName + 'container'}>
            <div className="round-btn-div" onClick={clickZoom}>
              {zoom ? '-' : '+'}
            </div>
            <img
              src={data.agreeFormFileList[currentView || 0]}
              alt={'사진' + currentView}
              className={
                zoom ? cName + 'current-view zoom' : cName + 'current-view'
              }
            />
          </div>
        )}
      </IonContent>
      <IonFooter>
        <div
          className={
            isNeedSafearea
              ? cName + 'bottom-div ' + cName + 'bottom-div-safearea'
              : cName + 'bottom-div'
          }
        >
          <div className={cName + 'bottom-div-viewer'}>
            { data &&
              data.map((file, i) => (
                <img
                  src={file}
                  key={i}
                  alt={'사진' + i}
                  className={
                    currentView === i ? cName + 'bottom-div-selected' : ''
                  }
                  onClick={() => clickedImage(i)}
                />
              ))}
          </div>
        </div>
      </IonFooter>
    </IonPage>
)
```

### PDF/사진 뷰어 구현을 위한 SCSS
```scss
#mypage-trial-agreement-sign-page {
  .mypage-trial-agreement-sign {
    &-sign-btn {
      position: fixed;
      bottom: 120px;
      right: 30px;
    }
    &-sign-btn-safearea {
      position: fixed;
      bottom: 170px;
      right: 30px;
    }
    &-container {
      overflow: scroll;
      padding: 10px;
      background-color: var(--ion-color-light);

      img {
        width: 100%;
        height: 100%;
        max-width: none;
      }
      img.zoom {
        width: 200% !important;
        height: 200% !important;
      }
      .round-btn-div {
        height: 26px;
        width: 26px;
        background-color: var(--ion-color-white);
        color: var(--ion-color-primary);
        border: 1px solid #7bbeff;
        box-shadow: 0 3px 6px 0 rgba(0, 0, 0, 0.5);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        font-size: 18px;
        font-weight: 700;
        position: absolute;
        right: 30px;
        top: 30px;
      }
    }
  }
  .mypage-trial-agreement-sign-bottom-div {
    &-safearea {
      padding-bottom: 50px;
      background-color: var(--ion-color-medium);
    }

    &-viewer {
      width: 100vw;
      height: 100px;
      background-color: var(--ion-color-medium);
      display: flex;
      align-items: center;
      overflow-x: scroll;
      padding: 0px 10px;

      img {
        height: 84px;
        width: 70px;
        margin-right: 10px;
        border: 1px solid var(--ion-color-medium-tint);
      }
    }
    &-selected {
      border: 3px solid var(--ion-color-primary) !important;
    }
  }
}
```
