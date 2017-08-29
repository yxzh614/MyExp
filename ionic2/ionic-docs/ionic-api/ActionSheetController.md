### ActionSheetController

An Action Sheet is a dialog that lets the user choose from a set of options. It appears on top of the app's content, and must be manually dismissed by the user before they can resume interaction with the app. Dangerous (destructive) options are made obvious in ios mode. There are easy ways to cancel out of the action sheet, such as tapping the backdrop or hitting the escape key on desktop.

`action sheet `是帮助用户从一系列选项中做出选择的提示框。它在整个应用最顶层显示并且必须在用户想要继续和应用互动之前手动将其关闭。

An action sheet is created from an array of buttons, with each button including properties for its text, and optionally a handler and role. If a handler returns false then the action sheet will not be dismissed. An action sheet can also optionally have a title, subTitle and an icon.

`action sheet `由一个按钮数组组成，每一个按钮包括文本属性，并且可以额外添加`handler`和`role`属性。如果`handler`返回了`false`则这个`action sheet` 不会被关闭。另外`action sheet`也可以包含`title`、`subTitle`或`icon`。

A button's role property can either be destructive or cancel. Buttons without a role property will have the default look for the platform. Buttons with the cancel role will always load as the bottom button, no matter where they are in the array. All other buttons will be displayed in the order they have been added to the buttons array. Note: We recommend that destructive buttons are always the first button in the array, making them the top button. Additionally, if the action sheet is dismissed by tapping the backdrop, then it will fire the handler from the button with the cancel role.

按钮的`role`属性可以是`destructive`或者`cancel`。没有`role`属性的按钮会根据平台显示基础的外观。`role`属性为`cancel`的按钮会一直处于底部，无论它在数组中处于什么位置。注意：我们建议永远把`destructive`按钮放在数组中的首位，让它成为顶部的按钮。另外，如果通过点击空白处来关闭`action sheet`，这将会触发`role`属性为`cancel`的按钮的`handler`

You can pass all of the action sheet's options in the first argument of the create method: ActionSheet.create(opts). Otherwise the action sheet's instance has methods to add options, like setTitle() or addButton().

你可以将`action sheet`的所有选项通过构造方法的第一个选项传递进去：
```
ActionSheet.create(opts)
```
或者通过`action sheet`的实例方法来添加内容，例如`setTitle()`和`addButton()`

用法：
```
import { ActionSheetController } from 'ionic-angular'

export class MyClass{

 constructor(public actionSheetCtrl: ActionSheetController) {}

 presentActionSheet() {
   let actionSheet = this.actionSheetCtrl.create({
     title: 'Modify your album',
     buttons: [
       {
         text: 'Destructive',
         role: 'destructive',
         handler: () => {
           console.log('Destructive clicked');
         }
       },
       {
         text: 'Archive',
         handler: () => {
           console.log('Archive clicked');
         }
       },
       {
         text: 'Cancel',
         role: 'cancel',
         handler: () => {
           console.log('Cancel clicked');
         }
       }
     ]
   });

   actionSheet.present();
 }
}
```
Instance Members

实例成员

 `config`

 `create(opts)`

Open an action sheet with a title, subTitle, and an array of buttons

打开一个带有标题、小标题、按钮数组的`action sheet`

|Param参数 |	Type类型 |	Details详细 
---------|----------|---------
|opts	|`ActionSheetOptions`	| `action sheet`选项

Advanced

进阶

ActionSheet create options

Option选项|	Type类型|	Description描述
---------|----------|---------
title|	`string`|	`action sheet`的标题
subTitle|	`string`|	`action sheet`的小标题
cssClass|	`string`|	  额外的css类，用空格分隔
enableBackdropDismiss|`	boolean`|	`action sheet`是否应在点击背景时关闭
buttons|	`array<any>`|	用于显示的button数组


ActionSheet button options

Option选项|	Type类型|	Description描述
--------|----------|-----------
text|	string	|按钮的文本
icon|	icon|	按钮的图标
handler	|any|	An express the button should evaluate.按钮执行的表达式
cssClass|	string|	额外的css类，用空格分隔
role|	string|	按钮的显示形式，可以为`destructive`或`cancel`。如果没有提供`role`属性，按钮将不会带有附加的样式。How the button should be displayed, destructive or cancel. If not role is provided, it will display the button without any additional styles.

Dismissing And Async Navigation

关闭和异步路由

After an action sheet has been dismissed, the app may need to also transition to another page depending on the handler's logic. However, because multiple transitions were fired at roughly the same time, it's difficult for the nav controller to cleanly animate multiple transitions that may have been kicked off asynchronously. This is further described in the Nav Transition Promises section. For action sheets, this means it's best to wait for the action sheet to finish its transition out before starting a new transition on the same nav controller.

当`action sheet`被关闭后，应用可能需要根据handler的逻辑跳转到另一个页面。然而，由于多个跳转大致在同一时间发生， `nav controller`很难清晰的展现多个已经发生的异步路由跳转。这将在`Nav Transition Promises`部分进行深入讲解。对于`action sheet`来说，最好的方式是等待当前的跳转结束后再开始同一`nav controller`的新跳转。

In the example below, after the button has been clicked, its handler waits on async operation to complete, then it uses pop to navigate back a page in the same stack. The potential problem is that the async operation may have been completed before the action sheet has even finished its transition out. In this case, it's best to ensure the action sheet has finished its transition out first, then start the next transition.

在下面的例子中,当按钮被点击后,`handler`等待异步操作结束后使用`pop`返回栈中上一个页面.一个潜在的问题即在`action sheet`完成跳转之前, 异步操作可能已完成了.在这种情况下,最好的办法是先保证`action sheet`已经完成了跳转,然后再开始下一次跳转.

```
let actionSheet = this.actionSheetCtrl.create({
  title: 'Hello',
  buttons: [{
    text: 'Ok',
    handler: () => {
      // user has clicked the action sheet button
      // begin the action sheet's dimiss transition
      let navTransition = actionSheet.dismiss();

      // start some async method
      someAsyncOperation().then(() => {
        // once the async operation has completed
        // then run the next nav transition after the
        // first transition has finished animating out

        navTransition.then(() => {
          this.nav.pop();
        });
      });
      return false;
    }
  }]
});

actionSheet.present();
```
It's important to note that the handler returns false. A feature of button handlers is that they automatically dismiss the action sheet when their button was clicked, however, we'll need more control regarding the transition. Because the handler returns false, then the action sheet does not automatically dismiss itself. Instead, you now have complete control of when the action sheet has finished transitioning, and the ability to wait for the action sheet to finish transitioning out before starting a new transition.

特别注意的是`handler`返回`false`.按钮的`handler`的一个作用是当它被点击时自动关闭`action sheet`,然而我们需要更多的对跳转进行控制.因为`handler`返回`false`所以`action sheet`不会被自动关闭,而是在`action sheet`完成跳转时完全的控制和在更多的新跳转之前等待当前跳转完成的能力.