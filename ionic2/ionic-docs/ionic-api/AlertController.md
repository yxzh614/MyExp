### AlertController

An Alert is a dialog that presents users with information or collects information from the user using inputs. An alert appears on top of the app's content, and must be manually dismissed by the user before they can resume interaction with the app. It can also optionally have a title, subTitle and message.

`alert`是一个对话框,用于向用户显示信息或使用`input`向用户收集信息.`alert`在应用的最顶层显示并且在用户想要和应用互动前被手动的关闭.它也可以添加额外的标题,小标题或信息.

You can pass all of the alert's options in the first argument of the create method: create(opts). Otherwise the alert's instance has methods to add options, such as setTitle() or addButton().

你可以将所有的alert选项通过构造方法`create(opts)`的第一个参数传递进去.此外`alert`也有一些方法添加选项,例如`setTitle()`或`addButton()`.

### Alert Buttons


In the array of buttons, each button includes properties for its text, and optionally a handler. If a handler returns false then the alert will not automatically be dismissed when the button is clicked. All buttons will show up in the order they have been added to the buttons array, from left to right. Note: The right most button (the last one in the array) is the main button.

在按钮数组中,每个按钮包含文本属性,并且可以添加一个`handler`.如果`handler`返回`false`那么这个`alert`不会在点击按钮后自动关闭.所有的按钮会根据它们在数组中的位置从左到右的显示.**注意:最右面的按钮(数组中最后一个)是主按钮.**

Optionally, a role property can be added to a button, such as cancel. If a cancel role is on one of the buttons, then if the alert is dismissed by tapping the backdrop, then it will fire the handler from the button with a cancel role.

你也可以给button添加role属性，例如cancel。如果这些按钮中有role属性为cancel的按钮，在你通过点击背景来关闭alert时这个按钮的handler就会被触发。

### Alert Inputs添加输入框

Alerts can also include several different inputs whose data can be passed back to the app. Inputs can be used as a simple way to prompt users for information. Radios, checkboxes and text inputs are all accepted, but they cannot be mixed. For example, an alert could have all radio button inputs, or all checkbox inputs, but the same alert cannot mix radio and checkbox inputs. Do note however, different types of "text"" inputs can be mixed, such as url, email, text, etc. If you require a complex form UI which doesn't fit within the guidelines of an alert then we recommend building the form within a modal instead.

alert也可以带有几个不同的输入框来将数据传给应用。这是一种简单的方式来提示用户输入信息。可以使用radios，checkboxs，和text inputs但是不能混用。然而你要注意了，不同的text inputs是可以混用的，例如url，email，text等等。如果你需要一个完整的表单UI然而在教程中的alert里没有合适的选择，我们推荐你使用model来新建表单。

Usage用法
```
import { AlertController } from 'ionic-angular';

constructor(private alertCtrl: AlertController) {

}

presentAlert() {
  let alert = this.alertCtrl.create({
    title: 'Low battery',
    subTitle: '10% of battery remaining',
    buttons: ['Dismiss']
  });
  alert.present();
}

presentConfirm() {
  let alert = this.alertCtrl.create({
    title: 'Confirm purchase',
    message: 'Do you want to buy this book?',
    buttons: [
      {
        text: 'Cancel',
        role: 'cancel',
        handler: () => {
          console.log('Cancel clicked');
        }
      },
      {
        text: 'Buy',
        handler: () => {
          console.log('Buy clicked');
        }
      }
    ]
  });
  alert.present();
}

presentPrompt() {
  let alert = this.alertCtrl.create({
    title: 'Login',
    inputs: [
      {
        name: 'username',
        placeholder: 'Username'
      },
      {
        name: 'password',
        placeholder: 'Password',
        type: 'password'
      }
    ],
    buttons: [
      {
        text: 'Cancel',
        role: 'cancel',
        handler: data => {
          console.log('Cancel clicked');
        }
      },
      {
        text: 'Login',
        handler: data => {
          if (User.isValid(data.username, data.password)) {
            // logged in!
          } else {
            // invalid login
            return false;
          }
        }
      }
    ]
  });
  alert.present();
}
```
Instance Members 实例成员

 config

 create(opts)

Display an alert with a title, inputs, and buttons

Param	|Type|	Details
-|-|-
opts|	AlertOptions	|Alert. See the table below

#### Advanced

Alert options

Property|	Type|	Description
-|-|-
title	|string	|alert的标题.
subTitle|	string	|alert的小标题.
message|	string	|alert的消息.
cssClass|	string|	附加的CSS类, 使用空格分隔.
inputs|	array	|一组inputs，见Input options.
buttons	|array|	An array of buttons for the alert. See buttons options.
enableBackdropDismiss|	boolean|	Whether the alert should be dismissed by tapping the backdrop. Default true.

Input options

Property|	Type|	Description
-|-|-
type	|string	|The type the input should be: text, tel, number, etc.
name|	string|	The name for the input.
placeholder|	string|	The input's placeholder (for textual/numeric inputs)
value|	string|	The input's value.
label|	string|	The input's label (only for radio/checkbox inputs)
checked|	boolean|	Whether or not the input is checked.
id|	string|	The input's id.
Button options

Property	Type	Description
text	string	The buttons displayed text.
handler	any	Emitted when the button is pressed.
cssClass	string	An additional CSS class for the button.
role	string	The buttons role, null or cancel.
Dismissing And Async Navigation
After an alert has been dismissed, the app may need to also transition to another page depending on the handler's logic. However, because multiple transitions were fired at roughly the same time, it's difficult for the nav controller to cleanly animate multiple transitions that may have been kicked off asynchronously. This is further described in the Nav Transition Promises section. For alerts, this means it's best to wait for the alert to finish its transition out before starting a new transition on the same nav controller.

In the example below, after the alert button has been clicked, its handler waits on async operation to complete, then it uses pop to navigate back a page in the same stack. The potential problem is that the async operation may have been completed before the alert has even finished its transition out. In this case, it's best to ensure the alert has finished its transition out first, then start the next transition.

let alert = this.alertCtrl.create({
  title: 'Hello',
  buttons: [{
    text: 'Ok',
    handler: () => {
      // user has clicked the alert button
      // begin the alert's dismiss transition
      let navTransition = alert.dismiss();

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

alert.present();
It's important to note that the handler returns false. A feature of button handlers is that they automatically dismiss the alert when their button was clicked, however, we'll need more control regarding the transition. Because the handler returns false, then the alert does not automatically dismiss itself. Instead, you now have complete control of when the alert has finished transitioning, and the ability to wait for the alert to finish transitioning out before starting a new transition.