---
title: Sample Tasks for the Playground
contributors: [ikoevska, akiraei]
---

만약 당신이  [NativeScript Playground](https://play.nativescript.org?template=play-vue)을 시작하고 싶다면, 당신은 간단한 to-do-app을 만들 수 있습니다. 아래의 요구사항을 따라오세요.

* 기본 디자인
  * Two-tab layout
  * 한 탭은 활성중인 task들을 보여주고 당신이 새로운 task를 추가할 수 있습니다.
  * 다른 탭은 완료된 task를 보여줍니다.
* (Coming soon) 기본 기능
  * (Coming soon) task 추가: 텍스트인 task를 추가할 수 있습니다.
  * (Coming soon) task 보기
      * (Coming soon) 새롭게 더해진 task는 활성 상태이며 탭될 수 있습니다.
      * (Coming soon) 완료된 task는 분리된 탭에 정렬됩니다.
  * (Coming soon) 완료된 task: 활성 task를 누르면 다른 탭으로 이동합니다. 
  * (Coming soon) task 삭제: "X" 버튼을 누르면 활성이든 완료된 상태이든 task가 삭제 됩니다.
* (Coming soon) 추가 기능
  * (Coming soon) 스켸줄 task: task에 데드라인을 정할 수 있습니다. 캘린더 위젯을 사용해서 날자를 정합니다.
  * (Coming soon) 태스크를 대량으로 관리할 수 있습니다.

> **TIP:** 이 투토리얼이 갖는 모든 섹션은  *Some NativeScript basics* 과 *Requirement implementation* 의 부분 섹션입니다. 당신은 기본적인 부분 섹션을 그냥 지나치고 바로 다음 단계로 넘어갈 수 있습니다.

## The bare Vue.js template

![](/screenshots/ns-playground/playground-home.png)

이 튜토리얼에 따른 모든 개발의 노력은 `app.js`와 `app.css`에서 구현됩니다. 앱의 기능과 앱의 스타일에 대해서 말이죠.

`app.js`은 Vue.js 프로젝트로, `template` 선언으로 새롭게 구성되며 어떠한 기능도 없습니다. 사용자 인터페이스를 앱으로 drag and drop 하면, 플레이그라운드는 `methods` 또한 추가합니다. 이는 앱의 기능적인 코딩을 채웁니다.

`app.js`에서는, `template` 블락에서 유저 인터페이스 디자인을 할 수 있고, `methods` 블락에서 앱의 기능을 만들 수 있습니다. `template` 블락은 Nativescript-compativle XML이 요구됩니다. `methods` 블락은 Vue.js와 NativeScript JavaScript 코드를 모두 허락합니다.


## Basic design

### Section progress

이건 당신의 앱이 섹션의 처음과 끝을 어떻게 보는지 보여줍니다.

| Initial screen | Tab 1 | Tab 2 |
|-------|-----|-----|
| ![Bare Vue.js template](/screenshots/ns-playground/two-tabs-start.jpg) | ![First tab](/screenshots/ns-playground/two-tabs-tab-1.jpg) | ![Second tab](/screenshots/ns-playground/two-tabs-tab-2.jpg) |

### Some NativeScript basics

`<Page>` 요소는 모든 NativeScript+Vue.js app의 최상위 유저 인터페이스 요소입니다. 모든 다른 유저 인터페이스 요소는 이 안에 포함됩니다.

`<ActionBar>`요소는 action 바를 보여줍니다. `<Page>`는 두개 이상의 `<ActionBar>`를 갖을 수 없습니다

대부분, `<ActionBar>` 이후에, 당신은 네비게이션 컴포넌트 (drawer나 탭뷰)나 레이아웃 컴포넌트를 갖을 것 입니다. 이 요소들은 당신의 앱의 레이아웃을 조절하고 다른 사용자 인터페이스 요소를 내부에 배치하는 방법을 결정할 수 있습니다.

### Requirement implementation
 
탭이 2개인 앱을 만들기 위해서 `<TabView>` 컴포넌트를 사용합니다.

1. 기본`<ScrollView>`블록과 템플릿과 함께 제공되는 모든 내용을 제거합니다. <br/>`<ScrollView>`구성 요소는 스크롤 가능한 내용을 위한 최상위 레이아웃 컨테이너입니다.
1. `<TabView>`컴포넌트를 그 자리에 드래그 앤 드롭하십시오. <br/> 플레이그라운드는 코드 포맷팅을 적용하지 않으며 새 컴포넌트를 삽입 할 때 들여쓰기를 처리하지 않습니다.
1. 화면을 채우도록`<TabView>`의 높이를 구성하십시오 (100 %로 설정). <br/> iOS 장치에서 기본 높이 설정으로 인해 탭이 화면 중앙 어딘가에 표시됩니다.
1. `<TabViewItem>`요소의 제목과 내용을 목적에 맞게 변경하십시오. <br/>이 시점에서 탭의 텍스트 내용은 스타일과 서식이없는`<Label>`구성 요소에 표시됩니다. `textWrap = "true"`속성을 해당`<Label>`컴포넌트에 적용하여 텍스트의 시각화를 개선하십시오.

```JavaScript
new Vue({

  template: `
    <Page class="page">
      <ActionBar title="My Tasks" class="action-bar" />
      
      <TabView height="100%">
        <TabViewItem title="To Do">
          <Label text="This tab will list active tasks and will let users add new tasks." textWrap="true" />
        </TabViewItem>
        <TabViewItem title="Completed">
          <Label text="This tab will list completed tasks for tracking." textWrap="true" />
        </TabViewItem>
      </TabView>

    </Page>
  `,

}).$start();
```
