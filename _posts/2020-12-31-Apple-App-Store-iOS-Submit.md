
---
title: “ 애플 앱 스토어에 심사 통과되기 까지의 과정!🎉 “
excerpt: “ 애플에 제출한 iOS 앱이 심사 통과 되었고 애플 앱 스토어에 정식 출시 되기까지 5번 거절 당하고 디버깅한 험난한 과정“
header:
	teaser: /assets/images/2020-12-31.jpg
	overlay_image: /assets/images/2020-12-31.jpg
	overlay_filter: rgba(0, 0, 0, 0.5)
categories:
- Hybrid-App
tags:
- iOS
- Ionic-react
---

#### 2020/12/31 개발일지
🎉축🎉 드디어 애플에 제출한 iOS 앱이 심사 통과 되었고 애플 앱 스토어에 정식으로 앱 등록이 되었다! 2020년 12월 14일에 앱 업로드를 하고 리뷰 요청을 하였고 2020년 12월 31일에 드디어 심사 통과가 되었다. 첫 애플 앱 심사에 통과 하기까지 총 17일 걸렸고 5번이나 거절 당했었다. 이렇게 거절을 많이 당했던 이유는 메디컬 관련된 앱이라 이것저것 요구 사항이 많아서였다. 보통 리뷰 요청을 하면 1~2일 내로 답변을 해줬고 꽤 자세하게 거절 이유를 짚어서 얘기해주어 아래와 같이 하나씩 해결해 나갔다.

1. 첫 번째 거절 이유
	* 메타 데이터와 스크린샷이 앱의 내용과 일치하지 않는다는 이유 - 메타 데이터와 스샷 삭제함
	* 약검색 및 자가진단에 출처를 표기하라 - 출처 표기함
	* 카메라 접근시 허용 문구 분명하게 표기하라 - 프로필 사진 업로드를 원하시면 카메라 및 사진 앨범 접근을 허용해주세요. 라고 Xcode 의 plist 를 수정함
2. 두 번째 거절 이유
	* medical diagonoses 또는 treatment advice 에 required medical disclaimer 가 들어있지 않음 - 면책 조항을 표기함
	* 아이패드용 스크린샷에 아이폰으로 보이는 스크린샷이 들어가 있음 - 아이패드용으로 앱 스토어에 제출하지 않을 예정이라 아이패드에 앱을 구동시켜서 화면 스크린샷을 찍어 그대로 제출함
![애플 심사 거절 이유](/assets/images/2020-12-31-1.jpg)
3. 세 번째 거절 이유
	* 앱 설명에 disclaimer 추가해야 함 - 앱 제출 시 description 에 면책 조항 추가함
	* COVID-19 관련한 앱이므로 공신력있는 기관(정부 기관, 대학교, 병원)과 associate 된 회사여야 함 - 일단 코로나 관련 내용을 제거하여 제출함
	* 어프 이름을 대표하는 회사 이름으로 앱을 출시해야 함 - 개인 애플 개발자 계정에 관리자 권한 부여하고 진행하였으나 회사 개발자 계정으로 재빌드하여 제출함
![애플 심사 거절 이유](/assets/images/2021-12-31-2.jpg)
4. 네 번째 거절 이유
	* 어프 이름을 대표하는 회사 이름으로 앱을 출시해야 함 - certificate 을 회사 개발자 계정으로 새로 만들어서 재빌드한 앱을 제출 함
5.  다섯 번째 거절 이유
	*  어프 이름을 대표하는 회사 이름으로 앱을 출시해야 함 - 계속 같은 이유로 2번 거절을 당해서 더 자세히 알아보니 회사 애플 계정이 organization 으로 되어있지 않고 individual 로 되어있어서 문제가 된거였음을 확인함. 애플 멤버쉽을 organization 으로 변경 요청하였음. 자세한 방법은 아래 <애플 멤버쉽을 individual 에서 organization 으로 변경 요청하는 방법> 참고.
6. organization 으로 변경 후 여섯 번째 제출 후 심사 통과! 🎉


### 애플 멤버쉽을 individual 에서 organization 으로 변경 요청하는 방법
1. 애플 개발자 페이지에서 계정 로그인 ->  [Sign In - Apple](https://developer.apple.com/account/)
2. Membership 탭 -> Entity Type - Individual 확인
![애플 멤버쉽 변경하는 방법](/assets/images/2020-12-31-3.jpg)
3. 가장 아래에 `Need to edit this information?` 클릭
4. Provide your new organization information 클릭
![애플 멤버쉽 변경하는 방법](/assets/images/2020-12-31-4.jpg)
5. 정보 기입 후 Send
	* 정보를 기입할 때 Organization D-U-N-S 넘버가 있어야 제출가능하다.
	* Organization D-U-N-S 넘버 발급받아야 하는데 평균 14일 소요된다.
