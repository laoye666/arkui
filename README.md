
鸿蒙应用开发快速体验
安装 IDE
DevEco Studio 是基于 IntelliJ IDEA Community（IDEA社区版）构建，为鸿蒙应用提供了一站式开发环境，集成了开发、运行、调试以及发布应用的各项功能。
获取并安装 DevEco Studio，官方下载地址为：https://developer.huawei.com/consumer/cn/download/
安装中文插件
1. 选择 File -> Settings 

2. 选择 Plugins -> 输入中文 -> 将插件勾选上

3. 点击下方 Apply -> OK，最终重启 IDE 就能生效
创建项目
1. 点击Create Project

2. 选择项目模版，此处选择第一个Empty Ability即可，点击 Next

3. 配置项目
可能需要调整的配置项如下，其余保持默认即可，配置完成后，点击Finish即可
  ○ Project name：项目名称
  ○ Bundle name：包名，通常为公司域名倒置
  ○ Save location：项目目录
● 
4. IDE界面说明
5. 项目结构概述
项目结构相对复杂，先简单了解即可，随之后序学习的深入再逐步为大家介绍

运行项目
DevEco Studio提供了多种方式用于运行项目，包括预览、模拟器、真机运行，下面逐一演示：
Preview 预览
Previewer预览用于查看应用的UI界面效果，方便随时调整界面UI布局。只需打开需要预览的页面文件，例如下图中的Index.ets，然后点击IDE右侧的预览器即可看到预览效果。

模拟器运行
Previewer预览器主要用于查看界面UI效果，如需对项目进行更加深入的测试，可以使用模拟器运行项目。初次使用需要先安装模拟器，安装步骤如下：
1. 点击 No Devices 菜单下的设备管理器，打开设备管理器

2. 新建模拟器

3. 选择一个模拟器，我们选择 Huawei_Phone，点击下一个

注意：第一次使用模拟器需要先下载才能使用。
4. 这里可以修改模拟器名称、内存和存储空间，我们使用默认值即可。点击完成，完成创建模拟器。

5. 若想将项目运行到模拟器，首先需要启动模拟器，点击下图中的启动按钮，等待模拟器开机

6. 开机后的模拟器如下图所示

7. 回到 IDE，在右上角的设备列表中选择刚刚创建的模拟器（默认已经选中），点击运行按钮

8. 查看模拟器


真机运行
目前暂时没有方法使用
使用模拟器运行应用时，会占用电脑较多的资源，并且有些功能无法进行测试。当模拟器不满足要求时，可选择真机运行。真机运行的步骤如下
1. 准备一台装有Harmony OS系统的手机，系统版本最好为4及以上

2. 打开手机的开发者模式。在设置/关于手机中，连续多次单机系统版本号，直至出现您正处在开发者模式!的提示信息 

3. 开启USB调试。在系统与更新/开发人员选项中，打开USB调试开关
 
4. 使用USB数据线将手机和电脑相连，手机会弹框提示选择USB 连接方式，需要选择传输文件。

5. 之后会弹窗询问是否允许USB调试？，可勾选始终允许使用这台计算机进行调试，然后点击确定

6. 回到IDE，在右上角的设备列表中选择连接的手机（默认已选中）

7. 最后点击运行按钮，即可将项目运行到真机中。首次运行会提示缺少签名信息，点击Open signing configs进行配置即可。

8. 生成签名信息需要先登陆华为开发者账号，点击Sign In

9. 浏览器会自动跳转到登录页面，按照要求完成注册、登录即可

10. 登录成功后，回到IDE，再次点击运行按钮，即可将应用运行到真机。

鸿蒙应用开发介绍
我们学习鸿蒙应用开发，主要学习以下内容：
1. 开发语言：ArkTS
2. 开发 UI：ArkUI
3. HarmonyOS SDK开放能力：Kit
4. 应用包知识
鸿蒙应用开发 - ArkTS
概述

HarmonyOS 应用的主要开发语言是 ArkTS，它由 TypeScript（简称TS）扩展而来，在继承 TypeScript 语法的基础上，还扩展了如下能力：组件化、状态管理、渲染控制等
第一个应用
@Entry
@Component
struct Index {
  build() {
    Row() {
      Text('Hello HarmonyOS').fontSize(20).fontColor('red');
    }.width('100%').height('100%').justifyContent(FlexAlign.Center);
  }
}
装饰器
@Entry、@Component都是装饰器，装饰器用于装饰类、属性、方法以及变量等，并赋予其特殊的含义。
1. 装饰器是一个函数，这个函数仅在代码加载阶段执行一次。本质就是编译时执行的函数
2. 装饰器的语法是 @ 后跟一个函数或者一个执行后返回函数的表达式
3. 这个函数要么不返回值，要么返回一个新对象取代所修饰的目标对象
4. 装饰器有两个版本，一个是 2014 年通过的，一个是 2022 年通过的。ArkTS 里使用的是 2014 年通过的
● @Entry表示该自定义组件为入口组件（只有@Entry装饰的组件才能被预览、才能作为应用的页面展示，一个页面只能有一个 @Entry）
● @Component表示自定义组件
struct
是一个关键字，自定义组件必须使用 struct 定义，并且被 @Component装饰器修饰。
定义组件的首字母一般大写。
build
build 函数内部是 ArkTS 的声明式 UI 语法。内部使用 UI 组件完成页面的搭建。
资源分类与访问
应用开发过程中，经常需要用到颜色、字体、间距、图片等资源，在不同的设备或配置中，这些资源的值可能不同。
定义资源
资源组目录包括element、media、profile三种类型的资源文件，用于存放特定类型资源：
目录类型	说明	资源文件
element	表示元素资源，以下每一类数据都采用相应的 JSON 文件来表征。
● boolean，布尔型
● color，颜色
● float，浮点型，范围是-2^128-2^128
● intarray，整型数组
● integer，整型，范围是-2^31-2^31-1
● plural，复数形式
● strarray，字符串数组
● string，字符串	element 目录中的文件名称建议与下面的文件名保持一致。每个文件中只能包含同一类型的数据。
● boolean.json
● color.json
● float.json
● intarray.json
● integer.json
● plural.json
● strarray.json
● string.json
media	表示媒体资源，包括图片、音频、视频等非文本格式的文件。	文件名可自定义，例如：icon.png。
profile	表示自定义配置文件，其文件内容可通过包管理接口获取（目录下只支持json文件类型）。	文件名可自定义，例如：test_profile.json。
访问资源
1. 语法：$r('app.资源目录.资源名称') 
2. 示例：
// 访问图片
Image($r('app.media.startIcon'))
// 访问颜色
Text('Test').fontColor($r('app.color.red_color'))
状态管理
1. 语法：使用 @State 定义状态数据
2. 特点：状态数据是响应式的
3. 示例：
@Entry
@Component
struct Index {
  @State count: number = 0;

  build() {
    Row() {
      Column() {
        Text(`Count is ${this.count}`)
        Button('按钮').onClick(() => {
          this.count++;
        })
      }
    }.width('100%').height('100%').justifyContent(FlexAlign.Center).alignItems(VerticalAlign.Center)
  }
}
条件渲染
1. 语法：if ... else if ... else 或 三元表达式
2. 示例：
@Entry
@Component
struct Index {
  @State isLoveXiJiao: boolean = true;
  @State isLoveAnMo: boolean = false;

  build() {
    Row() {
      Column() {
        if (this.isLoveXiJiao) {
          Text("华哥爱洗脚")
        } else if (this.isLoveAnMo) {
          Text("华哥爱按摩")
        } else {
          Text("华哥爱烫头")
        }
      }
    }.width('100%').height('100%').justifyContent(FlexAlign.Center).alignItems(VerticalAlign.Center)
  }
}

入门案例
下面通过一个简单案例来快速体验这些功能，案例效果如下：

@Entry
@Component
struct ToggleEventPage {
  @State isOn: boolean = false;

  build() {
    Column({ space: 20 }) {
      Image(this.isOn ? $r('app.media.img_light') : $r('app.media.img_dark'))
        .height(300)
        .width(300)
        .borderRadius(20)
      Row({ space: 50 }) {
        Button('关灯').onClick(() => {
          this.isOn = false
        })
        Button('开灯').onClick(() => {
          this.isOn = true;
        })
      }
    }
    .height('100%')
    .width('100%')
    .justifyContent(FlexAlign.Center)
  }
}

案例分析：
● 组件分析：一个图片，两个按钮，对应一个Image和两个Button

● 组件样式：组件样式可通过属性方法进行描述，例如
  ○ width()
  ○ height()
  ○ borderRadius()

● 组件布局：组件布局可通过一系列容器组件进行描述，例如
  ○ Column可实现多个组件的纵向排列
  ○ Row可实现多个组件的横向排列

● 组件状态：开关灯的效果实际上是通过两张图片的切换来实现的。声明式 UI 具有一个显著特征，即由状态数据驱动 UI 更新。因此，我们可以定义一个 @State 状态变量，通过修改该变量来驱动 UI 界面中图片的切换。

● 交互功能：为实现与用户的交互效果，可以通过在按钮上添加点击事件。当用户点击“开灯”按钮时，将isOn变量设为true，页面将重新渲染并显示开灯图片；反之，当用户点击“关灯”按钮时，将isOn变量设为false，页面将重新渲染并显示关灯图片。
事件绑定可通过事件方法实现
循环渲染
1. 语法：ForEach(数据, 返回要渲染的内容, 遍历的key)
2. 示例：
// 定义类型
interface Item {
  id: string;
  text: string;
}

@Entry
@Component
struct Index {
  @State list: Item[] = [
    { id: '1', text: '吃饭' },
    { id: '2', text: '睡觉' },
    { id: '3', text: '敲代码' },
  ];

  build() {
    Row() {
      Column() {
        ForEach(this.list, (item: Item) => {
          Text(item.text)
        }, (item: Item) => item.id)
      }
    }.width('100%').height('100%').justifyContent(FlexAlign.Center).alignItems(VerticalAlign.Center)
  }
}
自定义组件
1. 创建自定义组件
@Component
export default struct MyText {
  build() {
    Text('Hello MyText')
  }
}
2. 页面引入组件并使用
import MyText from './MyText'

@Entry
@Component
struct Index {
  build() {
    Row() {
      MyText()
    }
  }
}
生命周期

页面生命周期
通过 @Entry 装饰的自定义组件为页面
● onPageShow：页面每次显示时触发一次，包括路由过程、应用进入前台等场景。
● onPageHide：页面每次隐藏时触发一次，包括路由过程、应用进入后台等场景。
● onBackPress：当用户点击返回按钮时触发。
组件生命周期
仅通过 @Component 装饰的自定义组件为组件
● aboutToAppear：组件即将出现时回调该接口，具体时机为在创建自定义组件的新实例后，在执行其build()函数之前执行。
● onDidBuild：组件 build() 函数执行完成之后回调该接口，不建议在 onDidBuild 函数中更改状态变量、使用animateTo等功能，这可能会导致不稳定的UI表现。
● aboutToDisappear：aboutToDisappear 函数在自定义组件析构销毁之前执行。不允许在aboutToDisappear 函数中改变状态变量，特别是@Link变量的修改可能会导致应用程序行为不稳定。
鸿蒙应用开发 - ArkUI
文档：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/ts-components-summary-V5
组件导读
所有 UI 组件都有一些通用属性和通用事件，同时每个 UI 组件也有自己私有属性和私有事件。
通用属性：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/5_2_u901a_u7528_u5c5e_u6027-V5
通用事件：https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/5_1_u901a_u7528_u4e8b_u4ef6-V5
基础组件
图片
1. 概述：Image为图片组件，用于在应用中显示图片，参数规则如下：
Image(src: Resource | string)
2. 本地图片：
● 写法一：Image($r('app.media.demo'))
要求：entry/src/main/resources/base/media文件夹中要有名为demo的图片
注意：
● 图片名称只能包含：英文、数字和下划线。一旦包含其他命名的图片，即使你没有使用，运行也会报错。
● media中图片不允许重名，例如：demo.jpg和demo.png即为重名！
● 写法二：Image($rawfile('demo.png'))
要求：entry/src/main/resources/rawfile文件夹中要有名为demo.png的图片
● 写法三：Image('/images/demo.jpg')
要求：entry/src/main/ets/images文件夹中要有名为：demo.jpg 的图片
注意：ets文件夹为根目录

说明：
● $r函数:
  ○ 用于获取应用的特定资源文件或数据值的全局函数
  ○ 参数：特定格式的字符串（一定要根据提示补全编写），格式为："app.xxx.yyy"
● $rawfile函数
  ○ 专门用来获取resources/rawfile下的特定文件资源的全局函数
  ○ 参数：带后缀文件名的字符串（尽量根据提示编写）
3. 网络图片：
● 写法：Image('http://xxx/xxx.jpg')
● 要注意：模拟器或真机运行时，要在当前模块的entry/src/main/module.json5配置文件中申请网络权限，大致内容如下：
{
  "module": {
    // ...
    "requestPermissions":[ // 申请权限
      { "name" : "ohos.permission.INTERNET" }, // 使用网络
    ]
  }
}
● 常用属性：
  ○ width：宽度 / height：高度
    ■ string : 带长度单位或百分比的字符串， 比如："20px"、"20vp" 、"50%"
    ■ number：省略长度单位vp的数值， 比如：20
    ■ Resource:  通过 $r('app.float.xxx') 从float.json资源文件中得到的长度值
  ○ objectFit（图片缩放类型）
名称	描述
None	保持原有尺寸显示。
Contain	保持宽高比进行缩小或者放大，使得图片完全显示在显示区域内。
Cover	保持宽高比进行缩小或者放大，使得图片完全覆盖显示区域。
Fill	不保持宽高比进行放大缩小，使得图片充满显示区域。
ScaleDown	保持宽高比进行缩小或不变，使得图片完全显示在显示区域内。
Auto	自适应显示
  ○ interpolation（图片插值，即减轻低清晰度图片在放大显示时出现的锯齿问题。）
 
长度像素单位
● HarmonyOS中提供的长度像素单位为：px 与 vp
● px: Pixel，屏幕物理像素单位。
  ○ 问题：相同 px 值在不同像素密度的手机上显示的尺寸是不同的（如下图所示）
  ○ 注意：不同于 CSS 中的 px，CSS 中的 px 类似于下面的 vp
● vp: Virtual Pixel，虚拟像素
  ○ 它是屏幕像素密度相关像素
  ○ 应用运行时，会根据屏幕像素密度转换为屏幕物理像素进行显示
  ○ 在不同像素密度的手机上，1vp对应的像素数是不同的，像素密度越高，1vp对应的像素数就越多。从而达到：用 vp 作为长度单位，在尺寸相同但像素密度不同的手机上，显示大小相同。(如下图所示)
  ○ 当数值不带单位时，默认单位为 vp。
  ○ HarmonyOS提供了针对运行设备的vp与px转换的全局计算函数
    ■ px2vp(val): 得到指定px值对应的vp值
    ■ vp2px(val): 得到指定vp值对应的px值
平时开发都用 vp 单位

疑问：不同像素密度，不同尺寸设备（比如平板）如何适配？
● 设计稿是以360vp * 800vp的手机作为标准来设计的，比如图片的尺寸标注为了：10vp * 10vp
● 那代码中如何指定width/height呢？
● 错误写法： 10px / 10vp / 10
● 正确做法： 
  ○ 1.  得到屏幕宽度的像素数  width
  ○ 2.  计算出屏幕宽度的vp值：vp = px2vp(width)
  ○ 3. 计算出适配时需要缩放的比例值：vpScale = vp / 360
  ○ 4.  计算出图片要指定的width和height值：10 * vpScale
文本
概述：文本组件，通常用于展示用户的视图，如显示文章的文字，参数规则如下：
Text(content?: string | Resource)
string字符串：
Text('我是一段文本')
引用Resource资源：
前提要保证：/resources/base/element/string.json中已经配置了test字段
Text($r('app.string.test'))
常用样式：
名称	描述
fontSize	文本大小
fontColor	文本颜色
fontWeight	文字字重
textAlign	文本对齐方式
textOverflow	文本超长时的显示方式。
文字像素单位
● HarmonyOS提供的字体像素单位为：fp
● 官方文档： 与 vp 类似适用屏幕密度变化，随系统字体大小设置变化
● 真机测试结果：
  ○ 不会随系统字体大小设置而变化
  ○ 1fp 就等于 1vp
按钮
● 概述：Button是按钮组件，通常用于响应用户的点击操作，其类型包括胶囊按钮、圆形按钮、普通按钮。Button当做为容器使用时可以通过添加子组件实现包含文字、图片等元素的按钮。参数规则如下：
Button(label?: string, options?: { type?: ButtonType, stateEffect?: boolean })
● 类型：
名称	描述
Capsule	胶囊型按钮（圆角默认为高度的一半）
Circle	圆形按钮
Normal	普通按钮（默认不带圆角）
● 点击效果：
stateEffect	按压态显示效果，true开启，false关闭，默认true
● 子组件：Button组件也可以有子组件，例如一个带有图标的按钮

Button({ type: ButtonType.Capsule, stateEffect: true }) {
  Row() {
    Text('扫一扫').fontSize(12).fontColor(0xffffff).margin({ left: 5, right: 12 })
    Image($r('app.media.ic_public_input_scan')).width(20).height(20))
  }.alignItems(VerticalAlign.Center).width(90).height(40)
}
● 事件
Button('你好').onClick(()=>{
  console.log('hello!')
})
切换按钮
● 概述：勾选框样式、状态按钮样式及开关样式，参数规则如下：
Toggle(options: { type: ToggleType, isOn?: boolean })
● 效果：

● 属性：
selectedColor：设置组件打开状态的背景颜色。
switchPointColor：设置Switch类型的圆形滑块颜色。

● 事件：onChange：开关状态切换时触发该事件。
● 案例：灯光切换效果

文本输入
TextInput是输入框组件，通常用于响应用户的输入操作，比如评论区的输入、聊天框的输入、表格的输入等，也可以结合其它组件构建功能页面，例如登录注册页面
● 概述：显示一个文本输入的组件，参数规则如下：
TextInput({placeholder?: ResourceStr, text?: ResourceStr})
● 常用属性：
  ○ type：输入框类型。
    ■ InputType.Normal   文本
    ■ InputType.Password 密码
    ■ InputType.Number 数值
  ○ maxLength：输入内容最大长度
● 常用事件
  ○ onChange: 输入发生改变
  ○ onFocus: 获取焦点
  ○ onBlur: 失去焦点
● 其它相关语法请参考：官方文档

@Entry
@Component
struct Index {
  @State name: string = ''
  @State pwd: string = ''

  build() {
    Column({space: 10}) {
      TextInput({placeholder: '请输入用户名', text: this.name})
        .maxLength(6)
        .onChange((val) => { // 输入过程中实时触发
          this.name = val
        })
      TextInput({placeholder: '请输入密码', text: this.pwd})
        .type(InputType.Password)
        .onChange((val) => { // 输入过程中实时触发
          this.pwd = val
        })
      Button('登 陆')
        .width('100%')
        .onClick(() => {
          console.log('提交登陆', this.name, this.pwd)
        })
    }
    .width('100%')
    .padding(20)
  }
}
进度条
● 概述：进度条组件，用于显示内容加载或操作处理等进度，参数规则如下：
Progress(options: {value: number, total?: number, type?: ProgressType})
● 常用属性：
名称	参数类型	描述
		
value	number	设置当前进度值。设置小于0的数值时自动为0，
设置大于Total的数值时自动为total，
非法数值不生效。
color	ResourceColor	设置进度条颜色值。默认值：#ff007dff。
backgroundColor	ResourceColor	设置进度条底色值。默认值：#19182431。
style	object	strokeWidth, 设置进度条边框宽度（不支持百分比设置），该属性支持设置进度条两侧半圆的边框宽度，默认值表示进度条两侧的半圆之一。

scaleCount, 设置进度条刻度总数量。默认值：120。
scaleWidth, 设置进度条刻度宽度（不支持百分比设置），刻度相对于进度条宽度尺寸，为绝对值模式。默认值：2.0vp
● 示例效果：

● 示例代码：
  build() {
    Column({ space: 15 }) {
      Text('线性进度条')
      Progress({ value: 10, type: ProgressType.Linear })

      Text('球形进度条')
      Row({ space: 40 }) {
        Progress({ value: 10, type: ProgressType.Eclipse }).width(100)
      }

      Text('刻度环进度条')
      Row({ space: 40 }) {
        Progress({ value: 10, type: ProgressType.3ing }).width(100)
        Progress({ value: 20, total: 150, type: ProgressType.ScaleRing })
          .value(50).width(100)
          .style({ strokeWidth: 15, scaleCount: 15, scaleWidth: 5 })
      }
      Row({ space: 40 }) {
        Progress({ value: 20, total: 150, type: ProgressType.ScaleRing })
          .value(50).width(100)
          .style({ strokeWidth: 20, scaleCount: 20, scaleWidth: 5 })
        Progress({ value: 20, total: 150, type: ProgressType.ScaleRing })
          .value(50).width(100)
          .style({ strokeWidth: 20, scaleCount: 30, scaleWidth: 3 })
      }

      Text('环形进度条')
      Row({ space: 40 }) {
        Progress({ value: 10, type: ProgressType.Ring }).width(100)
        Progress({ value: 20, total: 150, type: ProgressType.Ring })
          .color(Color.Grey).value(50).width(100)
          .style({ strokeWidth: 20, scaleCount: 30, scaleWidth: 20 })
      }

      Text('胶囊形进度条')
      Row({ space: 40 }) {
        Progress({ value: 10, type: ProgressType.Capsule }).width(100).height(50)
        Progress({ value: 20, total: 150, type: ProgressType.Capsule })
          .color(Color.Grey)
          .value(50)
          .width(100)
          .height(50)
      }
    }.width('100%').margin({ top: 30 })
  }
API 弹窗
概述：创建并显示文本提示框、对话框和操作菜单。
import { promptAction } from '@kit.ArkUI';
提示信息（showToast）

promptAction.showToast({
  message: '恭喜，操作成功！',
  duration: 2000,
  bottom:150
});
对话框（showDialog）

promptAction.showDialog({
  title: '确认删除吗？',
  message: '删除后不可恢复，请确认操作',
  buttons: [
    {
      text: '确定',
      color: '#CF4538',
    },
    {
      text: '取消',
      color: '#aaa',
    }
  ],
})
.then(data => {
  console.info('你点了确认或取消' + data.index);
})
菜单（showActionMenu）

promptAction.showActionMenu({
  title: '确认操作',
  buttons: [
    {
      text: '编辑',
      color: '#000000',
    },
    {
      text: '删除',
      color: '#000000',
    },
    {
      text: '锁定',
      color: '#000000',
    },
  ]
}).then((data)=>{
  console.log('你选择了：',data.index)
})
预置弹窗
警告弹窗

AlertDialog.show({
    title: '操作提示', // 弹窗标题
    message: '确认删除吗？', // 弹窗内容
    autoCancel: true, //点击遮障层时，是否关闭弹窗。
    alignment: DialogAlignment.Center, //弹窗位置
    gridCount: 4, // 弹窗容器宽度所占用栅格数
    offset: { dx: 0, dy: -20 }, //弹窗相对alignment所在位置的偏移量

    /* 多个按钮 -- 开始 */
    primaryButton: { //主按钮的文本内容、文本色、按钮背景色和点击回调。
      value: '确认', //按钮文字
      action: () => { //按钮回调
        console.info('你点击了确定按钮')
      },
      fontColor:'#C75450'
    },
    secondaryButton: { //副按钮的文本内容、文本色、按钮背景色和点击回调。
      value: '取消', //按钮文字
      action: () => { //按钮回调
        console.info('你点击了取消按钮')
      },
      fontColor:'#aaa'
    },
    /* 多个按钮 -- 结束 */

    /* 单个按钮 -- 开始 */
    /*confirm: {
      value: 'xxxx',
      action: () => {
        console.info('xxxxxx')
      }
    },*/
  })
列表选择弹窗

ActionSheet.show({
    title: '操作提示', // 弹窗标题
    message: '请选择类型', //弹窗内容
    autoCancel: true, //点击遮障层时，是否关闭弹窗。
    // 确认按钮的文本内容和点击回调
    confirm: {
      value: '确定', //文字内容
      action: () => { //回调
        console.log('你点击了确认按钮')
      }
    },
    // 点击遮障层关闭dialog时的回调
    cancel: () => {
      console.log('弹窗关闭了')
    },
    // 弹窗在竖直方向上的对齐方式。
    alignment: DialogAlignment.Bottom,
    // 弹窗相对alignment所在位置的偏移量
    offset: { dx: 0, dy: -10 },
    // 设置选项内容，每个选择项支持设置图片、文本和选中的回调
    sheets: [
      {
        title: '打折商品', // 标题
        action: () => { // 回调
          console.log('goods1')
        }
      },
      {
        title: '限购商品',
        action: () => {
          console.log('goods2')
        }
      },
      {
        title: 'VIP商品',
        action: () => {
          console.log('goods2')
        }
      },
      {
        title: '预售商品',
        action: () => {
          console.log('goods3')
        }
      }
    ]
  })
日期滑动选择器

@Entry
@Component
struct Index {
  selectedDate: Date = new Date("2024-1-1")
  build() {
    Column({ space: 5 }) {
      Blank()
      Button("日期选择器（阳历）")
        .margin(20)
        .onClick(() => {
          DatePickerDialog.show({
            start: new Date("2000-1-1"),
            end: new Date("2100-12-31"),
            selected: this.selectedDate,
            onAccept: (value: DatePickerResult) => {
              // 通过Date的setFullYear方法设置按下确定按钮时的日期，这样当弹窗再次弹出时显示选中的是上一次确定的日期
              this.selectedDate.setFullYear(value.year, value.month, value.day)
              console.info("DatePickerDialog:onAccept()" + JSON.stringify(value))
            },
            onCancel: () => {
              console.info("DatePickerDialog:onCancel()")
            },
            onChange: (value: DatePickerResult) => {
              console.info("DatePickerDialog:onChange()" + JSON.stringify(value))
            }
          })
        })

      Button("日期选择器（阴历 ）")
        .onClick(() => {
          DatePickerDialog.show({
            start: new Date("2000-1-1"),
            end: new Date("2100-12-31"),
            selected: this.selectedDate,
            lunar: true,
            onAccept: (value: DatePickerResult) => {
              this.selectedDate.setFullYear(value.year, value.month, value.day)
              console.info("DatePickerDialog:onAccept()" + JSON.stringify(value))
            },
            onCancel: () => {
              console.info("DatePickerDialog:onCancel()")
            },
            onChange: (value: DatePickerResult) => {
              console.info("DatePickerDialog:onChange()" + JSON.stringify(value))
            }
          })
        })
      Blank()
      Blank()
    }
    .width('100%').margin({ top: 5 })
    .height('100%')
  }
}
时间滑动选择器

@Entry
@Component
struct Index {
  private selectTime: Date = new Date('2020-12-25T08:30:00')
  build() {
    Column({ space: 5 }) {
      Blank()
      Button("时间滑动选择器 12小时制")
        .margin(20)
        .onClick(() => {
          TimePickerDialog.show({
            selected: this.selectTime,
            onAccept: (value: TimePickerResult) => {
              // 设置selectTime为按下确定按钮时的时间，这样当弹窗再次弹出时显示选中的为上一次确定的时间
              this.selectTime.setHours(value.hour, value.minute)
              console.info("TimePickerDialog:onAccept()" + JSON.stringify(value))
            },
            onCancel: () => {
              console.info("TimePickerDialog:onCancel()")
            },
            onChange: (value: TimePickerResult) => {
              console.info("TimePickerDialog:onChange()" + JSON.stringify(value))
            }
          })
        })
      Button("时间滑动选择器 24小时制")
        .margin(20)
        .onClick(() => {
          TimePickerDialog.show({
            selected: this.selectTime,
            useMilitaryTime: true,
            onAccept: (value: TimePickerResult) => {
              this.selectTime.setHours(value.hour, value.minute)
              console.info("TimePickerDialog:onAccept()" + JSON.stringify(value))
            },
            onCancel: () => {
              console.info("TimePickerDialog:onCancel()")
            },
            onChange: (value: TimePickerResult) => {
              console.info("TimePickerDialog:onChange()" + JSON.stringify(value))
            }
          })
        })
      Blank()
      Blank()
    }
    .width('100%').margin({ top: 5 })
    .height('100%')
  }
}
文本滑动选择器

@Entry
@Component
struct TextPickerDialogExample {
  private select: number = 2
  private fruits: string[] = ['apple1', 'orange2', 'peach3', 'grape4', 'banana5']

  build() {
    Row() {
      Column() {
        Button("文本滑动选择器")
          .margin(20)
          .onClick(() => {
            TextPickerDialog.show({
              range: this.fruits,
              selected: this.select,
              onAccept: (value: TextPickerResult) => {
                // 设置select为按下确定按钮时候的选中项index，这样当弹窗再次弹出时显示选中的是上一次确定的选项
                this.select = value.index
                console.info("TextPickerDialog:onAccept()" + JSON.stringify(value))
              },
              onCancel: () => {
                console.info("TextPickerDialog:onCancel()")
              },
              onChange: (value: TextPickerResult) => {
                console.info("TextPickerDialog:onChange()" + JSON.stringify(value))
              }
            })
          })
      }.width('100%')
    }.height('100%')
  }
}
布局组件
线性布局（Column/Row）
概述
线性布局（LinearLayout）是开发中最常用的布局，通过线性容器Row（行）和Column（列）构建，它是其他布局的基础，其子元素在线性方向上（水平或垂直）依次排列，基本形式如下：
Column（列）

Row（行）

子元素间距
子元素在排列方向上的间距，可以通过组件参数space参数进行控制，基本效果如下：

基本语法如下：
Column({space:10}){
  	......
}

Row({space:10}){
  	......
}
子元素排列与对齐
基本概念
● 主轴：线性布局容器在布局方向上的轴线，Row容器主轴为横向，Column容器主轴为纵向。
● 交叉轴：垂直于主轴方向的轴线。Row容器交叉轴为纵向，Column容器交叉轴为横向。
子元素沿主轴方向的排列方式
可以通过justifyContent 属性进行控制，可选值如下：
1. FlexAlign.Start
2. FlexAlign.Center
3. FlexAlign.End
4. FlexAlign.SpaceBetween
5. FlexAlign.SpaceAround
6. FlexAlign.SpaceEvenly
效果如下：

图一:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
  
}.width('100%').height('100%').justifyContent(FlexAlign.Start)
图二:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').justifyContent(FlexAlign.Center)
图三:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
  
}.width('100%').height('100%').justifyContent(FlexAlign.End)
图四:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').justifyContent(FlexAlign.SpaceBetween)
图五:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').justifyContent(FlexAlign.SpaceAround)
图六:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').justifyContent(FlexAlign.SpaceEvenly)
子元素沿交叉轴方向的对齐方式
可以通过alignItems 属性进行控制，可选值如下：
1. HorizontalAlign.Start
2. HorizontalAlign.Center
3. HorizontalAlign.End
效果如下：

图一:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').alignItems(HorizontalAlign.Start)
图二:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').alignItems(HorizontalAlign.Center)
图三:
Column() {
  Row() {

  }.width('80%').height(50).backgroundColor(Color.Red)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Orange)

  Row() {

  }.width('80%').height(50).backgroundColor(Color.Yellow)
}.width('100%').height('100%').alignItems(HorizontalAlign.End)
实用技巧
利用 Blank 组件，自动填充容器主轴方向上的空余部分，效果如下：

@Entry
@Component
struct BlankPage {
    build() {
        Column() {
            Row() {
                Image($r('app.media.ic_bluetooth'))
                    .width(30)
                    .height(30)
                Text('蓝牙')
                    .fontSize(20)
                    .margin({ left: 5 })
                Blank()
                Toggle({ type: ToggleType.Switch })
            }
            .width('100%')
            .height(60)
            .backgroundColor(Color.White)
            .padding({ left: 10, right: 10 })
            .borderRadius(15)
        }
        .width('100%')
        .height('100%')
        .justifyContent(FlexAlign.Center)
        .padding(10)
        .backgroundColor('#E9E9E8')
    }
}
层叠布局（Stack）
概述
Stack布局是一种常用的布局方式，它允许将子元素沿垂直于屏幕的方向堆叠在一起，类似于图层的叠加。子元素可以按照其添加顺序依次叠加在一起，后添加的子元素会覆盖之前添加的子元素，层叠布局具有较强的页面层叠、位置定位能力，其使用场景有广告、卡片层叠效果等（类似定位）。
基本形式如下：

基本语法：
@Entry
@Component
struct StackAlign {
    @State alignment: Alignment = Alignment.Center;

    build() {
      Column() {
      Stack() {
        Row() {
          Text('1')
        }
        .width(300).height(300).backgroundColor(Color.Brown)

        Row() {
          Text('2')
        }
        .width(150).height(150).backgroundColor(Color.Red)

        Row() {
          Text('3')
        }
        .width(75).height(75).backgroundColor(Color.Yellow)

      }
    }
    .width('100%')
}
对齐方式
通过 alignContent 属性设置子组件的对齐方式，可选值如下：
1. Alignment.TopStart
2. Alignment.Top
3. Alignment.TopEnd
4. Alignment.Start
5. Alignment.Center
6. Alignment.End
7. Alignment.BottomStart
8. Alignment.Bottom
9. Alignment.BottomEnd
效果如下：

 图一:
Stack() {
  Row() {
    Text('1')
  }
  .width(300).height(300).backgroundColor(Color.Brown)

  Row() {
    Text('2')
  }
  .width(150).height(150).backgroundColor(Color.Red)

  Row() {
    Text('3')
  }
  .width(75).height(75).backgroundColor(Color.Yellow)
}
.width('100%').backgroundColor('#ccc').alignContent(Alignment.TopStart)
Z轴控制
Stack容器中的子组件可通过zIndex属性设置其所在的层级，zIndex值越大，层级越高，即zIndex值大的组件会覆盖在zIndex值小的组件上方，例如下图中，我们把Item1的zIndex调整为5，那么Item1就会叠在其他Item上层。

网格布局（Grid）
概述
网格布局（Grid）是一种强大的页面排版方式，通过将页面划分为行和列组成的网格，使得子组件可以在这个二维网格中自由定位。网格布局的容器组件为Grid，子组件为GridItem，如下图所示。

基本语法
@Entry
@Component
struct Index {
  build() {

     Grid(){
       GridItem(){}.backgroundColor(Color.Red)
       GridItem(){}.backgroundColor(Color.Orange)
       GridItem(){}.backgroundColor(Color.Yellow)
       GridItem(){}.backgroundColor(Color.Red)
       GridItem(){}.backgroundColor(Color.Orange)
       GridItem(){}.backgroundColor(Color.Yellow)
       GridItem(){}.backgroundColor(Color.Red)
       GridItem(){}.backgroundColor(Color.Orange)
       GridItem(){}.backgroundColor(Color.Yellow)
     }.width('100%').height(400).rowsTemplate('1fr 1fr 1fr').columnsTemplate('1fr 1fr 1fr').rowsGap(10).columnsGap(10)
  }
}
设置行列数量和尺寸占比
使用rowsTemplate属性和columnsTemplate属性，可以设置行列数量和尺寸占比
@Entry
@Component
struct Index {
  build() {
    Grid(){
      GridItem() {......}
    }
    .rowsTemplate('1fr 1fr 1fr')
    .columnsTemplate('1fr 2fr 1fr')
  }
}
效果如下：

设置子组件所占行列数
使用：columnStart、columnEnd、rowStart、rowEnd属性可以控制子组件所占行列数
@Entry
@Component
struct Index {
  @State message: string = 'Hello World'

  build() {
    Grid(){
      GridItem() {
        Text(`你好1`).textAlign(TextAlign.Center)
      }.border({width:1}).margin(2).rowStart(1).rowEnd(3)
      GridItem() {
        Text(`你好2`).textAlign(TextAlign.Center)
      }.border({width:1}).margin(2).columnStart(1).columnEnd(3)
      GridItem() {
        Text(`你好3`).textAlign(TextAlign.Center)
      }.border({width:1}).margin(2)
      GridItem() {
        Text(`你好4`).textAlign(TextAlign.Center)
      }.border({width:1}).margin(2)
      GridItem() {
        Text(`你好5`).textAlign(TextAlign.Center)
      }.border({width:1}).margin(2)
      GridItem() {
        Text(`你好6`).textAlign(TextAlign.Center)
      }.border({width:1}).margin(2)
    }
    .padding(8)
    .rowsTemplate('1fr 1fr')
    .columnsTemplate('2fr 1fr 1fr 1fr')
    .height(300)
    .backgroundColor('#ddd')
  }
}
效果如下：

设置行列间距
使用rowsGap和columnsGap属性，可以控制行列间距
Grid() {
  ...
}
.columnsGap(10)
.rowsGap(15)
效果如下：

滚动效果
滚动的网格布局常用在文件管理、购物或视频列表等页面中，如下图所示。在设置Grid的行列数量与占比时，如果仅设置行、列数量与占比中的一个，即仅设置rowsTemplate或仅设置columnsTemplate属性，网格单元按照设置的方向排列，超出Grid显示区域后，Grid拥有可滚动能力。
当显示内容超出显示区域时，便需要使用滚动效果。

@Entry
  @Component
  struct Index {
    build() {

      Grid(){
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Red)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Orange)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Yellow)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Red)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Orange)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Yellow)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Red)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Orange)
        GridItem(){}.width('25%').height(100).backgroundColor(Color.Yellow)
      }.width('100%').height(400).rowsTemplate('1fr 1fr').rowsGap(10).columnsGap(10)
    }
  }
列表布局（List）
概述
列表（List）是一种复杂的容器组件，使用列表可以轻松高效地显示结构化、可滚动的列表信息。列表布局的容器组件为List，子组件为ListItem或者ListItemGroup，其中，ListItem表示单个列表项，ListItemGroup用于列表数据的分组展示，其子组件也是ListItem，如下图所示

基本语法：
@Entry
@Component
struct Index {
  build() {
    List({space:10}) {
      ListItem() {
        Text('list1')
      }.width('100%').backgroundColor(Color.Red)

      ListItemGroup() {
        ListItem() {
          Text('list2')
        }.width('100%')

        ListItem() {
          Text('list3')
        }.width('100%')

      }.width('100%').backgroundColor(Color.Orange)

      ListItemGroup() {
        ListItem() {
          Text('list4')
        }.width('100%')

        ListItem() {
          Text('list5')
        }.width('100%')

      }.width('100%').backgroundColor(Color.Orange)
    }.width('100%')
  }
}
列表方向
使用listDirection属性可以设置列表方向，可选值有两种：
1. 默认值是Axis.Vertical表示垂直。
2. 还可以设置成Axis.Horizontal表示水平。

@Entry
  @Component
  struct Index {
    build() {
      List({space:10}) {
        ListItem() {
          Text('list1')
        }.width('100%').height(100).backgroundColor(Color.Red)

        ListItemGroup() {
          ListItem() {
            Text('list2')
          }.width('100%')

          ListItem() {
            Text('list3')
          }.width('100%')

        }.width('100%').height(100).backgroundColor(Color.Orange)

        ListItemGroup() {
          ListItem() {
            Text('list4')
          }.width('100%')

          ListItem() {
            Text('list5')
          }.width('100%')

        }.width('100%').height(100).backgroundColor(Color.Orange)
      }
      .width('100%')
        .listDirection(Axis.Horizontal)
    }
  }
元素对齐
使用alignListItem属性，可控制元素对齐方式

@Entry
  @Component
  struct Index {
    build() {
      List({space:10}) {
        ListItem() {
          Text('list1')
        }.width('50%').height(100).backgroundColor(Color.Red)

        ListItemGroup() {
          ListItem() {
            Text('list2')
          }.width('100%')

          ListItem() {
            Text('list3')
          }.width('100%')

        }.width('50%').height(100).backgroundColor(Color.Orange)

        ListItemGroup() {
          ListItem() {
            Text('list4')
          }.width('100%')

          ListItem() {
            Text('list5')
          }.width('100%')

        }.width('50%').height(100).backgroundColor(Color.Orange)
      }
      .width('100%')
        .listDirection(Axis.Vertical)
        .alignListItem(ListItemAlign.End)

    }
  }
元素间距
使用List({space:10}) 参数：可设置元素间距
元素分割线
使用divider属性可设置分割线样式，基本效果如下：

代码示例：
.divider({
  strokeWidth:1,
  startMargin:10,
  endMargin:10,
  color:Color.Grey
})
滚动条
使用scrollBar属性可控制滚动条样式，基本效果如下：


@Entry
  @Component
  struct Index {
    @State contactsGroups: object[] = [
      {
        title: 'A',
        contacts: [
          '艾佳',
          '安安',
          'Angela'
        ],
      },
      {
        title: 'B',
        contacts: [
          '白叶',
          '伯明'
        ],
      },
      {
        title: 'C',
        contacts: [
          '豪哥',
          '天宇'
        ],
      },
      {
        title: 'D',
        contacts: [
          '白叶',
          '伯明'
        ],
      },
      {
        title: 'E',
        contacts: [
          '鲁班',
          '张飞',
          '貂蝉'
        ],
      }
    ]

    @Builder Header(item){
      Text(item.title).fontSize(30).backgroundColor('#ccc').width('100%')
    }

    build() {

      List(){
        ForEach(this.contactsGroups,(item)=>{
          ListItemGroup({header:this.Header(item)}){
            ForEach(item.contacts,(user)=>{
              ListItem(){
                Text(user)
              }.width('100%').height(50)
                    })
          }
        },item=>JSON.stringify(item));
      }.width('100%').height(300).scrollBar(BarState.On)
    }
  }
组件状态管理
状态管理入门
技术点
● 多种状态数据的定义、读取、更新、传递
● 理解响应式状态数据
● 状态数据的监视
@State
@State用于装饰当前组件的状态变量，@State装饰的变量在发生变化时，会驱动当前组件的视图刷新，语法如下：
@State count: number = 1;
@Prop
@Prop用于装饰子组件的状态变量，@Prop装饰的变量会同步父组件的状态，但只能单向同步，也就是父组件的状态变化会自动同步到子组件，而子组件的变化不会同步到父组件。

● 父组件
@Entry
@Component
struct Parent{
  @State count: number = 1;
  build(){
    Column(){
      Child({ count: this.count });
    }
  }
}
● 子组件
@Component
export struct Child{
  @Prop count: number;
  build(){
    Text('prop.count: ' + this.count);
  }
}
需要注意的是：@Prop装饰的变量必须初始化，要么自己组件本地初始化，要么通过父组件传参进行初始化。
@Link
@Link用于装饰子组件的状态变量，@Prop变量同样会同步父组件状态，但是能够双向同步。也就是父组件的变化会同步到子组件，而子组件的变化也会同步到父组件。

● 父组件
@Entry
@Component
struct Parent{
  @State count: number = 1;
  build(){
    Column(){
      Child({ count: $count });
    }
  }
}
● 子组件
@Component
export struct Child{
  @Link count: number;
  build(){
    Text('link.count: ' + this.count);
  }
}
需要注意的是：@Link装饰的变量不允许本地初始化，只能由父组件通过传参进行初始化，并且父组件必须使用$变量名的方式传参，以表示传递的是变量的引用。
@Provide 与 @Consume
@Provide和@Consume用于跨层级传递状态信息，其中@Provide用于装饰祖先组件的状态变量，@Consume用于装饰后代组件的状态变量。可以理解为祖先组件提供（Provide）状态信息供后代组件消费（Consume），并且祖先和后代的状态信息可以实现双向同步。

注意:
● @Provide装饰变量必须本地初始化，而@Consume装饰的变量不允许本地初始化。
● @Provide & @Consume处理的状态数据是双向同步的
● 祖先组件
@Entry
@Component
struct GrandParent {
    @Provide count: number = 1;
    @Provide('msg') message: string = 'atguigu';
    build() {
        Column() {
            ...
        }
    }
}
● 后代组件
@Entry
@Component
export struct Child {
  	@Consume count: number;
    @Consume('msg') childMsg: string;
  
    build() {
        Column() {
            Text('Consume.count: ' + this.count);
          	Text('Consume.childMsg: ' + this.childMsg);
        }
    }
}
@Watch
● 用来监视状态数据的变化，包括：@State、@Prop、@Link、@Provide、@Consume
● 一旦状态数据变化，监视的回调就会调用
● 我们可以在监视的回调中执行应用需要的特定逻辑
● 以@State为例编码
@State @Watch('onCountChange') count: number = 0

/**
 * 一旦count变化，此回调函数就会自动调用
 * @param name  被监视的状态属性名
 */
onCountChange (name) {
  // 可以在此做特定处理
}
状态管理深入
技术点
1. 各个状态都支持哪些数据类型
2. 各个状态数据的哪些更新操作能监视，哪些不能监视
3. 解决不能监视的更新操作的问题
@State
允许装饰的类型
● 基本类型：string、number、boolean、enum
● 对象类型：json对象、class的实例对象、
● 数组类型：上面所有类型的数组
能够观察到的变化
注意:
● 并不是状态变量的所有更改都会引起UI的刷新
● 只有可以被框架观察到的修改才会引起UI刷新
● 属性本身的改变都可以 （无论什么类型）
● 对象：能监视对象的直接属性变化，不能监视嵌套属性的改变
● 数组：能监视数组中元素的变化，不能监视元素对象内部的变化
编码测试
● 定义对象和数组的状态和显示数据
@State @Watch('onChange')obj: {a: {b: number}} = {a: {b: 1}}
@State @Watch('onChange2')arr: {a: number}[] = [{a: 1}]

Text('state.obj' + JSON.stringify(this.obj)).fontSize(18)
Text('state.arr' + JSON.stringify(this.arr)).fontSize(18)
● 修改属性对象
this.obj = {a: {b: 2}}   // 修改属性本身 => 能监视

this.obj.a = {b: 3}  // 修改属性对象的直接属性 =》 能监视

this.obj.a.b = 4   // 修改属性对象的嵌套属性 =》 不能监视到
● 修改属性数组
this.arr = [] // 修改属性本身 => 能监视

this.arr[0] = {a: 2} // 修改属性数组的元素 => 能监视

this.arr.push({a: 3}) // 修改属性数组的元素 => 能监视

this.arr[0].a = 4 // 修改属性数组的元素对象内部属性 =》 不能监视
@Prop
允许装饰的类型
● 官方文档：允许任何类型
能够观察到的变化
● 与@State一致
@Link
允许装饰的类型
● 与@State一致
框架能够观察到的变化
● 与@State一致
@Provide 和 @Consume
允许装饰的类型
● 与@State一致
能够观察到的变化
● 与@State一致

编码测试

@Component
export default struct Child1 {

  @Prop obj1: {a: {b: number}}
  @Prop arr1: {a: number}[]

  update() {
    // this.obj1 = {a: {b: 2}}   // 修改属性本身 => 能监视
    // this.obj1.a = {b: 5}  // 修改属性对象的直接属性 =》 能监视
    // setTimeout(() => {
    //   this.obj1.a.b = 6   // 修改属性对象的嵌套属性 =》 不能监视到 报错(且会报错，导致程序退出)
    // }, 1000)

    // this.arr1 = [] // 修改属性本身 => 能监视
    // this.arr1[0] = {a: 2} // 修改属性数组的元素 => 能监视
    this.arr1.push({a: 3}) // 修改属性数组的元素 => 能监视
    setTimeout(() => {
      this.arr1[0].a = 4 // 修改属性数组的元素对象内部属性 =》 不能监视(且会报错，导致程序退出)
    }, 1000)
  }

  build() {
    Column({space: 10}) {
      Text('prop.obj' + JSON.stringify(this.obj1)).fontSize(18)
      Text('prop.arr' + JSON.stringify(this.arr1)).fontSize(18)
      Button('更新 prop').onClick(() => this.update())
    }
    .width('100%')
    .padding(20)
    .border({width: 1, color: Color.Gray})
  }
}

@Component
export default struct Child2 {

  @Link obj2: {a: {b: number}}
  @Link arr2: {a: number}[]

  update () {
    // this.obj1 = {a: {b: 2}}   // 修改属性本身 => 能监视
    // this.obj2.a = {b: 7}  // 修改属性对象的直接属性 =》 能监视
    // setTimeout(() => {
    //   this.obj2.a.b = 8   // 修改属性对象的嵌套属性 =》 不能监视到
    // })

    // this.arr2 = [] // 修改属性本身 => 能监视
    // this.arr2[0] = {a: 2} // 修改属性数组的元素 => 能监视
    this.arr2.push({a: 3}) // 修改属性数组的元素 => 能监视
    setTimeout(() => {
      this.arr2[0].a = 4 // 修改属性数组的元素对象内部属性 =》 不能监视
    })
  }

  build() {
    Column({space: 10}) {
      Text('link.obj2' + JSON.stringify(this.obj2)).fontSize(18)
      Text('link.arr2' + JSON.stringify(this.arr2)).fontSize(18)

      Button('更新 link').onClick(() => this.update())
    }
    .width('100%')
    .padding(20)
    .border({width: 1, color: Color.Gray})
  }
}

import Child1 from './Child1'
import Child2 from './Child2'

@Entry
@Component
struct StateTest {

  @State obj: {a: {b: number}} = {a: {b: 1}}
  @State arr: {a: number}[] = [{a: 1}]

  update() {
    // this.obj = {a: {b: 2}}   // 修改属性本身 => 能监视
    // this.obj.a = {b: 3}  // 修改属性对象的直接属性 =》 能监视
    // setTimeout(() => {
    //   this.obj.a.b = 4   // 修改属性对象的嵌套属性 =》 不能监视到
    // }, 1000)

    // this.arr = [] // 修改属性本身 => 能监视
    // this.arr[0] = {a: 2} // 修改属性数组的元素 => 能监视
    this.arr.push({a: 3}) // 修改属性数组的元素 => 能监视
    setTimeout(() => {
      this.arr[0].a = 4 // 修改属性数组的元素对象内部属性 =》 不能监视
    }, 1000)
  }

  build() {
    Column({space: 10}) {
      Text('state.obj' + JSON.stringify(this.obj)).fontSize(18)
      Text('state.arr' + JSON.stringify(this.arr)).fontSize(18)

      Button('更新2 state').onClick(() => this.update())

      Child1({obj1: this.obj, arr1: this.arr})

      Child2({obj2: $obj, arr2: $arr})
    }
    .width('100%')
    .padding(20)
  }
}
@ObjectLink 和 @Observed
前面的问题：
● 属性对象中的嵌套对象的属性修改不能监视到，也就不会自动更新UI
● 属性数组中的元素对象的属性修改不能监视到，也就不会自动更新UI
● @Props与@Link声明接收的属性，必须是@State的属性，而不能是@State属性对象中嵌套的属性
解决办法
● 将嵌套对象的类型用class定义， 并使用@Observed来装饰
● 子组件中定义的嵌套对象的属性， 使用@ObjectLink来装饰

编码测试

@Observed
class Person2 {
  id: number;
  name: string;
  age: number;

  constructor(id, name, age) {
    this.id = id
    this.name = name
    this.age = age
  }
}

@Component
struct PersonItem {
  // @Prop person: Person
  // @Link person: Person
  @ObjectLink person: Person2

  build() {
    Row() {
      Text(JSON.stringify(this.person))
        .fontSize(20)
      Button('更新年龄')
        .onClick(() => this.person.age += 2)
    }
    .border({width: 1, color: Color.Gray})
    .padding(10)
  }
}

@Entry
@Component
struct PersonList {
  @State persons: Person2[] = [
    new Person2(1, 'Tom', 12),
    new Person2(2, 'Jack', 13),
  ]

  build() {
    Column({space: 10}){
      Button('更新嵌套对象的属性：一个人的年龄')
        .onClick(() => {
          this.persons[0].age++
        })
      List() {
        ForEach(this.persons, (item: Person2, index: number) => {
          ListItem(){
            PersonItem({person: item})
          }
        })
      }
    }
    .padding(20)
  }
}

ForEach列表更新问题
ForEach(arr, itemGenerator, keyGenerator)
● 参数1： 遍历的数组数据
● 参数2：遍历数组元素用于显示对应行视图ListItem的函数   
  ○ （item, index）=> {ListItem()}
● 参数3：用来返回决定当前行界面是否需要重新构建的函数,返回值是一个唯一的key
  ○ 类型： (item, index) => string
  ○ 默认值：(item, index) => index + JSON.stringfy(item)	
  ○ 如果新的返回值key在原有所有key就能找到相同的key，则复用对应的item视图
  ○ 如果没有找到相同的key, 则重新构建新的Item视图，也就是会更新item界面
● ForEach经常用于遍历数组显示列表
● 数组中的元素很可能是对象，包含id以及其它多个业务属性数据
● 在动态显示后，可能会更新某个人的业务属性数据
● 下面以人员列表为例，编码如下（ForEach不指定第三个参数）
interface Person {
  id: number;
  name: string
}

@Entry
@Component
struct ForEachTest {
  @State persons: Person[] = [
    {id: 1, name: 'tom'},
    {id: 2, name: 'Jack'},
    {id: 3, name: 'Bob'},

  ]

  update () {
    this.persons[1] = {id: 2, name: 'Jack---'}
  }

  update2 () {
    this.persons = [this.persons[1], this.persons[0], this.persons[2]]
  }

  build() {
    Column({space: 10}) {
      Button('更新(内部属性)').onClick(() => this.update())
      Button('更新(顺序)').onClick(() => this.update2())

      List({space: 10}){
        ForEach(this.persons, (item: Person) => {
          ListItem() {
            Row({space: 10}){
              Text('--' + Date.now()) // 如果它变化了， 说明item视图更新显示了，否则说明复用了
              Text(item.name)
            }
          }
        }, (item, index) => index +JSON.stringify(item))
      }
    }
  }
}
● 更新(内部属性)：只更新对应行UI, 其它行都是复用的
● 更新（顺序）：顺序改变的行都更新了(没有复用)
  ○ 有问题：顺序改变的行也应该复用
  ○ 解决：指定第三个参数为 (item, index) => JSON.stringify(item)
ForEach(
  this.persons,
  (item: Person) => {
    ListItem(){
      Row({space: 10}){
        Text('--' + Date.now()) // 如果它变化了， 说明item视图更新显示了，否则说明复用了
        Text(item.name)
      }
    }
  },
  (item, index) => JSON.stringify(item)   // 指定返回item的JSON
)
● 更新(内部属性)：只更新对应行UI, 其它行都是复用的
● 更新（顺序）：顺序改变的行复用了，只是改了显示顺序

ForEach(
  this.persons,
  (item: Person, index) => {
    ListItem(){
      Row({space: 10}){
        Text('--' + Date.now()) // 如果它变化了， 说明item视图更新显示了，否则说明复用了
        Text(index + '--' + item.name)
      }
    }
  },
  (item, index) => JSON.stringify(item)   // 指定返回item的JSON
)
● 问题：如果item显示带了下标index，更新顺序时显示有问题（下标不更新）
● 解决：指定第三个参数为 (item, index) =>index + JSON.stringfy(item), 或不指定参数
ForEach(
  this.persons,
  (item: Person, index) => {
    ListItem(){
      Row({space: 10}){
        Text('--' + Date.now()) // 如果它变化了， 说明item视图更新显示了，否则说明复用了
        Text(index + '--' + item.name)
      }
    }
  }
)
ForEach总结
● 对于存在数组内部更新的列表
  ○ 显示时使用了下标: 不传递第三个参数，或指定(item, index) => index + JSON.stringfy(item)
  ○ 显示时没使用下标：传递第三个参数为：item => JSON.stringfy(item)
● 对于不存在数组内部更新的列表
  ○ 传递item => item.id 效率会高一些（不需要做item转JSON的操作）
状态管理实战
该案例要实现的是一个通讯录（联系人列表），需要支持添加联系人、批量删除联系人、收藏联系人等功能，具体效果如下


页面路由与组件导航
页面路由
理解
● 页面路由：路径与页面组件的映射对
● 页面路由组件需要使用@Entry装饰，并在resources/base/profile/main_pages.json中定义对应路径	
● 我们可以跳转到不同路径来显示不同的路由组件界面
相关API
● 说明：HarmonyOS提供了@ohos.router模块来控制路由跳转
● router.pushUrl()：push模式跳转到指定路由
● router.replaceUrl()：replace模式跳转到指定路由
● router.back(): 返回到上一个路由页面
● router.params： 读取跳转路由携带的参数
编码测试
                                  
import router from '@ohos.router';
@Entry
@Component
struct First {
  build() {
    Column({ space: 10 }) {
      Text('第一个页面').fontSize(30);
      Button('push').onClick(() => {
        router.pushUrl({ url: 'pages/Second' })
      })
      Button('replace').onClick(() => {
        router.replaceUrl({ url: 'pages/Second' })
      });
      Button('params').onClick(() => {
        router.pushUrl({ url: 'pages/Second',params:{a:1} })
      });

    }
    .width('100%');
  }
}
import router from '@ohos.router';
@Entry
@Component
struct Second {
  build() {
    Column({ space: 10 }) {
      Text('第二个页面：params: ' + JSON.stringify(router.getParams()));
      Button('back').onClick(() => {
        router.back();
      })
    }
    .width('100%')
  }
}

组件导航
这里主要复用Tabs组件实现界面局部切换显示
相关API
  ○ Tabs组件
  ○ TabsController  用于控制Tabs跳转页面的控制器类
编码测试1: 简单使用

@Entry
@Component
struct TabsSimple {
  private controller: TabsController = new TabsController();
  private tabList = ['测试', '圈子', "我的"]

  build() {
    Column() {
      Tabs({barPosition: BarPosition.End, controller: this.controller}) {
        TabContent() {
          Text('测试界面').fontSize(30)
        }
        .tabBar(this.tabList[0])

        TabContent() {
          Text('圈子界面').fontSize(30)
        }
        .tabBar(this.tabList[1])

        TabContent() {
          Text('我的界面（点击去圈子）').fontSize(30)
            .onClick(() => this.controller.changeIndex(1))
        }
        .tabBar(this.tabList[2])
      }
    }
      .height('100%')
  }
}
编码测试2: 自定义Tab


const tabList = [
  {
    id: 1,
    icon: $r('app.media.ic_tab_test'),
    icon_selected: $r('app.media.ic_tab_test_select'),
    text: '测试',
    color: '#959595',
    color_selected: '#000000'
  },
  {
    id: 2,
    icon: $r('app.media.ic_tab_group'),
    icon_selected: $r('app.media.ic_tab_group_select'),
    text: '圈子',
    color: '#959595',
    color_selected: '#000000'
  },
  {
    id: 3,
    icon: $r('app.media.ic_tab_mine'),
    icon_selected: $r('app.media.ic_tab_mine_select'),
    text: '我的',
    color: '#959595',
    color_selected: '#000000'
  },
]

@Entry
@Component
struct TabsCustom {
  private controller: TabsController = new TabsController();

  @State currentIndex: number = 0


  aboutToAppear() {
    setTimeout(() => {
      this.controller.changeIndex(2)
    }, 2000)
  }

  @Builder tabBuilder (index) {
    Column() {
      Image(index === this.currentIndex ? tabList[index].icon_selected : tabList[index].icon)
        .width(40)
        .height(40)
        .objectFit(ImageFit.Contain);

      Text(tabList[index].text)
        .fontSize(14)
        .fontWeight(FontWeight.Medium)
        .fontColor(this.currentIndex === index ? tabList[index].color_selected : tabList[index].color)
    }
  }

  build() {
    Column() {
      Tabs({barPosition: BarPosition.End, controller: this.controller}) {
        TabContent() {
          Text('测试的界面').fontSize(30)
        }
        .tabBar(this.tabBuilder(0))

        TabContent() {
          Text('圈子的界面').fontSize(30)
        }
        .tabBar(this.tabBuilder(1))

        TabContent() {
          Text('个人的界面').fontSize(30)
        }
        .tabBar(this.tabBuilder(2))
      }
        .onChange(index => this.currentIndex = index)
    }
      .height('100%')
      .padding({bottom: 5})
  }
}
动画
概述
动画可以在UI界面发生变化时，提供渐变过渡效果，提升用户体验。
动画的实现原理是通过在一段时间内连续播放一系列静止画面（帧），从而产生流畅的视觉效果。

ArkUI 提供了多种动画接口，例如：显式动画、属性动画、转场动画等，来实现各种动画效果。
显式动画(页面内)
● animateTo()是ArkUI 提供的一个全局的动画函数，调用此函数实现的动画称为显式动画
animateTo(value: AnimateParam, event: () => void): void
● 该函数共有两个参数，分别是
  ○ 动画参数，用于设置动画时长、属性值变化曲线等等。
  ○ 匿名函数，用于设置属性值的终点值，在该函数中设置的属性值，系统均会按照前边设置的动画参数，驱动属性值从其初始值平滑的过渡到终点值，从而实现动画效果。
● 编码测试

@Entry
@Component
struct AnimationTest1 {
  @State marginLeft: number|string = 0;
  @State opacityNumber: number = 1;

  @State rotateAngle: number = 0
  @State scaleX: number = 1
  @State scaleY: number = 1

  build() {
    Column({space: 30}) {
      Text('显式动画')
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .width('100%')
        .textAlign(TextAlign.Center)
        .margin({left: this.marginLeft})
        .opacity(this.opacityNumber)

      Text('显式动画2')
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .width('100%')
        .textAlign(TextAlign.Center)
        .scale({x: this.scaleX, y: this.scaleY})
        .rotate({angle: this.rotateAngle})
        .opacity(this.opacityNumber)

      Blank()

      Button('切换显示')
        .onClick(() => {
          animateTo({ duration: 2000, curve: Curve.Linear }, () => {
            if (this.marginLeft===0) {
              this.marginLeft = '-100%'
              this.opacityNumber = 0
            } else {
              this.marginLeft = 0
              this.opacityNumber = 1
            }

            if (this.rotateAngle===0) {
              this.rotateAngle = 360
              this.scaleX = 0
              this.scaleY = 0
            } else {
              this.rotateAngle = 0
              this.scaleX = 1
              this.scaleY = 1
            }
          })
        })
    }
    .padding({ top: 200, bottom: 200 })
    .width('100%')
    .height('100%')
  }
}
属性动画(页面内)
● animation()是ArkUI提供的组件的属性方法，调用此函数实现的动画称为属性动画
animation(value: AnimateParam)
● 该方法和其他属性方法的语法完全相同，在目标组件后边直接调用即可。
● 注意：产生属性动画的属性须在animation之前声明，其后声明的将不会产生属性动画。
● 编码测试

@Entry
@Component
struct AnimationTest2 {
  @State marginLeft: number|string = '0';
  @State opacityNumber: number = 1;

  @State rotateAngle: number = 0
  @State scaleX: number = 1
  @State scaleY: number = 1

  build() {
    Column({space: 30}) {
      Text('属性动画')
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .width('100%')
        .textAlign(TextAlign.Center)
        .margin({left: this.marginLeft})
        .opacity(this.opacityNumber)
        .animation({duration: 2000, curve: Curve.Linear})

      Text('属性动画2')
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .width('100%')
        .textAlign(TextAlign.Center)
        .scale({x: this.scaleX, y: this.scaleY})
        .rotate({angle: this.rotateAngle})
        .opacity(this.opacityNumber)
        .animation({duration: 2000, curve: Curve.Linear})

      Blank()

      Button('切换显示')
        .onClick(() => {
          if (this.opacityNumber===0) {
            this.marginLeft = 0;
            this.opacityNumber = 1;
          } else {
            this.marginLeft = '-100%';
            this.opacityNumber = 0;
          }

          if (this.rotateAngle===0) {
            this.rotateAngle = 360
            this.scaleX = 0
            this.scaleY = 0
          } else {
            this.rotateAngle = 0
            this.scaleX = 1
            this.scaleY = 1
          }
        })
    }
    .padding({ top: 200, bottom: 200 })
    .width('100%')
    .height('100%')
  }
}
转场动画(页面内)
● 转场动画是指组件出现或消失时的过渡动画。ArkUI 专门提供了transition接口来配置转场动画效果，可以定义平移、透明度、旋转、缩放这几种转场样式的单个或者组合的转场效果。
transition(value: TransitionOptions)
● TransitionOptions的定义如下
参数名称	参数类型	必填	参数描述
type	TransitionType	否	默认包括组件新增和删除。
默认值：TransitionType.All
说明：
不指定Type时说明插入删除使用同一种效果。
opacity	number	否	设置组件转场时的透明度效果，为插入时起点和删除时终点的值。
默认值：1
取值范围： [0, 1]
说明：
设置小于0或大于1的非法值时，按1处理。
translate	{
x? : number | string,
y? : number | string,
z? : number | string
}	否	设置组件转场时的平移效果，为插入时起点和删除时终点的值。
-x：横向的平移距离。
-y：纵向的平移距离。
-z：竖向的平移距离。
scale	{
x? : number,
y? : number,
z? : number,
cx? : number | string,
cy? : number | string
}	否	设置组件转场时的缩放效果，为插入时起点和删除时终点的值。
-x：横向放大倍数（或缩小比例）。
-y：纵向放大倍数（或缩小比例）。
-z：竖向放大倍数（或缩小比例）。
- cx、cy指缩放中心点，cx和cy默认是"50%"。
- 中心点为0时，默认的是组件的左上角。
rotate	{
x?: number,
y?: number,
z?: number,
angle: number | string,
cx?: number | string,
cy?: number | string
}	否	设置组件转场时的旋转效果，为插入时起点和删除时终点的值。
-x：横向的旋转向量。
-y：纵向的旋转向量。
-z：竖向的旋转向量。
- cx,cy指旋转中心点，cx和cy默认值是"50%"。
- 中心点为（0，0）时，默认的是组件的左上角。
● 编码测试

@Entry
@Component
struct AnimationTest3 {
  @State flag: boolean = true;

  build() {
    Column({space: 30}) {
      if (this.flag) {
        Text('转场动画')
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
          .width('100%')
          .textAlign(TextAlign.Center)
          .transition({ type: TransitionType.Insert, opacity: 0, translate: {x: '-100%'} })  // 插入的起始样式
          .transition({ type: TransitionType.Delete, opacity: 0, translate: {x: '-100%'} }) // 删除后的结束样式


        Text('转场动画2')
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
          .width('100%')
          .textAlign(TextAlign.Center)
          .transition({ type: TransitionType.Insert, scale: { x: 0, y: 0 }, rotate: { angle: 360 } })  // 插入的起始样式
          .transition({ type: TransitionType.Delete, scale: { x: 0, y: 0 }, rotate: { angle: 360 } }) // 删除后的结束样式
      }

      Blank()

      Button('切换显示')
        .onClick(() => {
          animateTo({ duration: 2000 }, () => {
            this.flag = !this.flag;
          })
        })
    }
    .padding({ top: 200, bottom: 200 })
    .width('100%')
    .height('100%')
  }
}
转场动画(页面间)
● 除了页面内的动画，我们还可以实现页面间转场动画
● 在push跳转路由及返回上一个路由页面时，默认就有转场动画
● HarmonyOS也提供了自定义的页面间的转场动画语法
// 用来配置页面间过渡效果的回调函数
pageTransition() {
  // 配置进入的动画
  PageTransitionEnter({type?: RouteType,duration?: number,curve?: Curve | string,delay?: number})

  // 配置离开的动画
  PageTransitionExit({type?: RouteType,duration?: number,curve?: Curve | string,delay?: number})
}
● 编码测试
import router from '@ohos.router'
@Entry
@Component
struct AnimationTest4 {
  @State message: string = '第一个页面'

  // 用来配置页面间过渡效果的回调函数
  pageTransition() {
    // push离开，持续1S，向底部
    PageTransitionExit({type: RouteType.Push,duration: 1000,curve: Curve.EaseInOut})
      .slide(SlideEffect.Bottom)

    // push/pop进入，持续2S，从右侧
    PageTransitionEnter({type: RouteType.None,duration: 2000,curve: Curve.EaseInOut})
      .slide(SlideEffect.Right)
  }

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)

        Button('跳转去页面二')
          .onClick(() => {
            router.pushUrl({url: 'pages/animation/SecondPage'})
          })
      }
      .width('100%')
    }
    .height('100%')
  }
}

@Entry
@Component
struct SecondPage {
  @State message: string = '第二个页面'

  // 用来配置页面间过渡效果的回调函数
  pageTransition() {
    // 从上面进入，持续1S
    PageTransitionEnter({type: RouteType.None,duration: 1000,curve: Curve.Linear})
      .slide(SlideEffect.Top)
  }

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
状态数据共享
● 疑问1：如何实现一个页面中所有组件的数据共享？
  ○ 解决：使用LocalStorage技术
● 疑问2：如何实现整个应用中所有页面的所有组件的数据共享？
  ○ 解决：使用AppStorage技术
● 疑问3：如何实现退出应用后状态数据还存在？
  ○ 解决：使用PersistentStorage技术
LocalStorage
● 页面级状态内存存储
  ○ 只能在一个页面中的所有组件中共享
  ○ 退出应用不存在
● 相关API
  ○ LocalStorage({name, value})：构造函数
  ○ @Entry(storage): 将storage绑定到页面根组件
  ○ @LocalStorageLink(name)：实现组件状态与LocalStorage的双向同步
  ○ @LocalStorageProp(name)：实现LocalStorage到组件状态的单向同步
AppStorage
● 应用级状态内存存储
  ○ 在所有页面中的所有组件中共享
  ○ 退出应用不存在
● 相关API
  ○ AppStorage.SetOrCreate(name, value)：初始化一个存储数据
  ○ @StorageLink(name): 实现组件状态与AppStorage的双向同步
  ○ @StorageProp装饰器(name)：实现AppStorage到组件状态的单向同步
PersistentStorage
● AppStorage数据的持久化
  ○ 退出应用后数据还存在，再次启动后，还能操作到AppStorage中的数据
● 相关API
  ○ PersistentStorage.PersistProp<T>(name: string, value: T): 初始化数据
  ○ @StorageLink/@StorageProp装饰器：获取同步数据
● 注意
  ○ 持久化的number类型数据，在应用退出后，再读取得到的string类型
编码测试
   
// 创建新实例并使用给定对象初始化
import router from '@ohos.router';
import Child1 from './componets/Child1'

const storage = new LocalStorage({ 'count1': 11 });

AppStorage.SetOrCreate('count2', 22) // 初始化g一个存储数据
// PersistentStorage.PersistProp<number>('count2', 222); // 初始化存储数据并持久化

@Entry(storage)
@Component
struct Test1 {
  @LocalStorageLink('count1') c1: number = 2
  @StorageLink('count2') c2: number = 3

  build() {
    Column({space: 10}) {
      Text(`localStorage count1: ${this.c1}`)

      Text(`AppStorage count2: ${this.c2}`)

      Button('更新LocalStorage count1')
        .onClick(() => {
          this.c1 += 2
        })
      Button('更新AppStorage count2')
        .onClick(() => {
          this.c2 = +this.c2 + 2
        })

      Child1()

      Button('跳转到Test2页面')
        .onClick(() => router.pushUrl({url: 'pages/storage/test2'}))
    }
  }
}

@Component
export default struct Child1 {
  @LocalStorageProp('count1') c1: number = 3
  @StorageProp('count2') c2: number = 4

  build() {
    Column({space: 10}) {
      Text(`LocalStorage count1: ${this.c1}`)

      Text(`AppStorage count2: ${this.c2}`)

      Button('更新LocalStorage count1')
        .onClick(() => {
          this.c1 += 1
        })
      Button('更新AppStorage count2')
        .onClick(() => {
          this.c2 += 2
        })
    }
      .width('100%')
      .backgroundColor(Color.Gray)
      .padding(10)
  }
}

@Entry
@Component
struct Test2 {
  @LocalStorageProp('count1') c1: number = -1
  @StorageProp('count2') c2: number = -1

  build() {
    Column() {
      // 得不到另一个路由页面的localStorage数据
      Text(`localStorage count1：${this.c1}`).fontSize(20)
      // 能得到另一个跌幅页面创建的AppStorage数据
      Text(`appStorage count2：${this.c2}`).fontSize(20)
    }.padding(20)
  }
}

网络请求
搭建本地测试服务器
https://www.yuque.com/zhangxiaofei-x0p8x/rlpomz/nr25d1shglhli3m7?singleDoc#
接口文档
操作	URL	请求方式	请求体
查询所有学生	http://电脑网络IP:7070/students	GET	无
查询所有男学生	http://电脑网络IP:7070/students?gender=男	GET	无
添加一个学生	http://电脑网络IP:7070/students	POST	name/age/gender的对象
更新一个学生	http://电脑网络IP:7070/students/{id}	PUT	name/age/gender的对象
删除一个学生	http://电脑网络IP:7070/students/{id} 	DELETE	无
原生Ajax请求
● 相关API
  ○ 主要使用@ohos.net.http模块提供的API
  ○ http.createHttp(): 创建能发送HTTP请求的请求对象
  ○ request(url: string, options: HttpRequestOptions, callback: AsyncCallback<HttpResponse>): void 发送HTTP请求
    ■ url: 请求的地址
    ■ options：相关配置
      ● method: 请求方式
      ● extraData： 请求体参数
      ● header: 请求头
      ● expectDataType：指定响应数据的类型, 默认是字符串，也可以指定为对象
    ■ callback: 请求成功或失败的回调函数
  ○ request(url: string, options?: HttpRequestOptions): Promise<HttpResponse>;
    ■ 与上面的方法相比，主要是不指定回调，而返回包含响应的Promise对象
● 注意：
  ○ 需要在module.json5中注册网络使用权限
{"name": "ohos.permission.INTERNET"},
● 测试编码

/*
使用内置原生http模块
 */

import http from '@ohos.net.http';

const httpRequest = http.createHttp()

interface Student {
  id: number;
  name: string;
  age: number;
  gender: string;
}

const baseURL = 'http://172.17.0.105:7070' // 需要指定为电脑的网络ip地址

@Entry
@Component
struct Index {
  @State studentList: Student[] = []
  @State inputId: string = '1'

  query1 =  () => {
    httpRequest.request(baseURL + '/students', {
      method: http.RequestMethod.GET
    }, (error, response) => {
      if (error) {
        console.error(JSON.stringify(error))
      } else {
        console.log("result", response.result)
        this.studentList = JSON.parse(response.result as string).data
      }
    })
  }

  query2 = async  () => {
    try {
      const response = await httpRequest.request(baseURL + '/students?gender=男', {
        method: http.RequestMethod.GET,
        expectDataType: http.HttpDataType.OBJECT
      })
      console.log('result2', JSON.stringify(response.result))
      const list = (response.result as any).data
      this.studentList = list
    } catch (error) {
      console.error(JSON.stringify(error))
    }
  }

  save = async () => {
    try {
      const response = await httpRequest.request(baseURL + '/students', {
        method: http.RequestMethod.POST,
        expectDataType: http.HttpDataType.OBJECT,
        extraData: {
          name: 'Marry',
          age: 13,
          gender: Date.now()%2===1 ? '男' : '女'
        }
      })
      console.log('result2', JSON.stringify(response.result))
      this.query1()
    } catch (error) {
      console.error(JSON.stringify(error))
    }
  }

  update = async () => {
    try {
      const response = await httpRequest.request(baseURL + `/students/${this.inputId}`, {
        method: http.RequestMethod.PUT,
        expectDataType: http.HttpDataType.OBJECT,
        extraData: {
          name: 'xxx',
          age: 32,
          gender: '女'
        }
      })
      console.log('更新成功', JSON.stringify(response.result))
      this.query1()
    } catch (error) {
      console.error(JSON.stringify(error))
    }
  }

  remove = async () => {
    console.log('----', `/students/${this.inputId}}`)
    try {
      const response = await httpRequest.request(baseURL + `/students/${this.inputId}`, {
        method: http.RequestMethod.DELETE,
        expectDataType: http.HttpDataType.OBJECT,
      })
      console.log('删除成功', JSON.stringify(response.result))
      this.query1()
    } catch (error) {
      console.error(error)
    }
  }

  build() {
    Column({space: 10}) {
      TextInput({text: this.inputId})
        .width(50)
        .type(InputType.Number)
        .onChange(val => this.inputId = val)

      Button('查询所有学生（GET）')
        .onClick(this.query1)
      Button('查询所有男学生（GET）')
        .onClick(this.query2)
      Button('添加一个学生（POST）')
        .onClick(this.save)
      Button('更新一个学生（PUT）')
        .onClick(this.update)
      Button('删除一个学生（DELETE）')
        .onClick(this.remove)

      Divider()

      List() {
        ForEach(this.studentList, (item) => {
          ListItem(){
            Text(JSON.stringify(item))
          }
        })
      }
    }
    .width('100%')
  }
}

第三方工具包axios
● 下载
  ○ ohpm i @ohos/axios
● 相关API
  ○ axios(url): Promise  发GET请求
  ○ axios(options): Promise  发送GET/POST/PUT/DELETE请求
  ○ axios.get(url, options): Promise  发GET请求
  ○ axios.delete(url, options): Promise  发DELETE请求
  ○ axios.post(url, data, options): Promise  发POST请求
  ○ axios.put(url, data, options): Promise  发PUT请求
● 编码测试
/*
使用axios发送请求
 */

import axios from '@ohos/axios'
import Prompt from '@system.prompt'

interface Student {
  id: number;
  name: string;
  age: number;
  sex: string;
}

const baseURL = 'http://172.17.0.105:7070'

@Entry
@Component
struct Index {
  @State studentList: Student[] = []
  @State inputId: string = '1'

  query1 =  () => {
    axios.get(baseURL + '/students')
      .then(
        response => this.studentList = response.data.data,
        error => console.error(error.message)
      )
  }

  query2 = async  () => {
    try {
      const response = await axios.get(baseURL + '/students', {params: {gender: '男'}})
      this.studentList = response.data.data
    } catch (error) {
      console.error(error.message)
    }
  }

  save = async () => {

    try {
      const response = await axios.post(baseURL + '/students', {
        name: 'Petter33',
        age: 13,
        gender: Date.now()%2===1 ? '男' : '女'
      })
      console.log(JSON.stringify(response.data))
      Prompt.showToast({message: '保存成功'})
      this.query1()
    } catch (error) {
      console.error(error.message)
    }
  }

  update = async () => {
    try {
      await axios.put(baseURL + `/students/${this.inputId}`, {
        name: 'yyyyy',
        age: 22,
        gender: '女'
      })
      Prompt.showToast({message: '更新成功'})
      this.query1()
    } catch (error) {
      console.error(error.message)
    }
  }

  remove = async () => {
    try {
      const response = await axios.delete(baseURL + `/students/${this.inputId}`)
      console.log(JSON.stringify(response.data))
      Prompt.showToast({message: '删除成功'})
      this.query1()
    } catch (error) {
      console.error(error.message)
    }
  }

  build() {
    Column({space: 10}) {
      TextInput({text: this.inputId})
        .type(InputType.Number)
        .width(50)
        .onChange(val => this.inputId = val)

      Button('查询所有学生（GET）')
        .onClick(this.query1)
      Button('查询所有男学生（GET）')
        .onClick(this.query2)
      Button('添加一个学生（POST）')
        .onClick(this.save)
      Button('更新一个学生（PUT）')
        .onClick(this.update)
      Button('删除一个学生（DELETE）')
        .onClick(this.remove)

      Divider()

      List() {
        ForEach(this.studentList, (item) => {
          ListItem(){
            Text(JSON.stringify(item))
          }
        })
      }
    }
      .width('100%')
  }
}

axios二次封装
● 封装的技术点
  ○ 指定基础路径
  ○ 指定超时时间
  ○ 指定请求成功返回不再是response， 而是需要处理的结果数据
  ○ 指定请求失败时的统一提示
● 相关API
  ○ create(config?: CreateAxiosDefaults): AxiosInstance   创建一个新的axios
  ○ axios.interceptors.request.use(onResolved)  注册请求拦截器
  ○ axios.interceptors.response.use(onResolved, onRejected)  注册响应拦截器
● 编码
import axios from '@ohos/axios'
import Prompt from '@system.prompt'

const service = axios.create({
  baseURL: 'http://192.168.1.105:7070', // ip得是电脑的网络ip
  timeout: 20000
})

service.interceptors.request.use(config => {
  // 暂时不需要做处理，后续会在此携带用户登陆的token
  return config
})

service.interceptors.response.use(
  response => {
    const result = response.data
    console.log('--res', JSON.stringify(result))
    if (result.code===200) {
      return result.data
    } else {
      Prompt.showToast(result.message || '网络请求出错')
      return Promise.reject(new Error(result.message))
    }
  },
  error => {
    console.log('++res', JSON.stringify(error))
    Prompt.showToast(error.message || '网络请求出错')
    throw error
  }
)

export default service

/*
使用封装好的axios发请求
 */

import request from './api/request'
import Prompt from '@system.prompt'

interface Student {
  id: number;
  name: string;
  age: number;
  gender: string;
}

@Entry
@Component
struct Index {
  @State studentList: Student[] = []
  @State inputId: string = '1'

  query1 =  () => {
    request.get<any, Student[]>('/students')
      .then(
        data => this.studentList = data,
        error => console.error(error.message)
      )
  }

  query2 = async  () => {
    try {
      const data = await request.get<any, Student[]>('/students', {params: {gender: '男'}})
      this.studentList = data
    } catch (error) {
      console.error(error.message)
    }
  }

  save = async () => {

    try {
      await request.post('/students', {
        name: 'Petter2',
        age: 13,
        gender: '女',
      })
      Prompt.showToast({message: '保存成功'})
      this.query1()
    } catch (error) {
      console.error(error.message)
    }
  }

  update = async () => {
    try {
      await request.put(`/students/${this.inputId}`, {
        name: 'zzzz',
        age: 23,
        gender: '女'
      })
      Prompt.showToast({message: '更新成功'})
      this.query1()
    } catch (error) {
      console.error(error.message)
    }
  }

  remove = async () => {
    try {
      await request.delete(`/students/${this.inputId}`)
      Prompt.showToast({message: '删除成功'})
      this.query1()
    } catch (error) {
      console.error(error.message)
    }
  }

  build() {
    Column({space: 10}) {
      TextInput({text: this.inputId})
        .type(InputType.Number)
        .width(50)
        .onChange(val => this.inputId = val)

      Button('查询所有学生（GET）')
        .onClick(this.query1)
      Button('查询所有男学生（GET）')
        .onClick(this.query2)
      Button('添加一个学生（POST）')
        .onClick(this.save)
      Button('更新一个学生（PUT）')
        .onClick(this.update)
      Button('删除一个学生（DELETE）')
        .onClick(this.remove)

      Divider()

      List() {
        ForEach(this.studentList, (item) => {
          ListItem(){
            Text(JSON.stringify(item))
          }
        })
      }
    }
      .width('100%')
  }
}

接口请求函数封装
● 在axios二次封装的基础上，针对不同接口定义不同的请求函数，来简化请求调用
export interface Student {
  id?: number;
  name: string;
  age: number;
  gender: string;
}

import request from './request'
import { Student } from './types'

export const reqGetStudents = (params = {}) => request.get<any, Student[]>('/students', {params})

export const reqAddStudent = (student: Student) => request.post('/students', student)

export const reqUpdateStudent = (student: Student) => request.put('/students/'+student.id, student)

export const reqDeleteStudent = (id: number) => request.delete('/students/'+id)


/**
 * 使用封装好的接口请求函数发送请求
 */

import Prompt from '@system.prompt'
import { Student } from './api/types'
import { reqAddStudent, reqDeleteStudent, reqGetStudents, reqUpdateStudent } from './api'

@Entry
@Component
struct Test4 {
  @State studentList: Student[] = []
  @State inputId: string = '1'

  query1 =  async () => {
    const data = await reqGetStudents()
    this.studentList = data
  }

  query2 = async  () => {
    const data = await reqGetStudents({gender: '男'})
    this.studentList = data
  }

  save = async () => {
    await reqAddStudent({
      name: 'Petter',
      age: 13,
      gender: '女'
    })
    Prompt.showToast({message: '保存成功'})
    this.query1()
  }

  update = async () => {
    await reqUpdateStudent({"id": +this.inputId,"name":"Petter111","gender":"男","age":21})
    Prompt.showToast({message: '更新成功'})
    this.query1()
  }

  remove = async () => {
    await reqDeleteStudent(+this.inputId)
    Prompt.showToast({message: '删除成功'})
    this.query1()
  }

  build() {
    Column({space: 10}) {
      TextInput({text: this.inputId})
        .type(InputType.Number)
        .width(50)
        .onChange(val => this.inputId = val)

      Button('查询所有学生（GET）')
        .onClick(this.query1)
      Button('查询所有男学生（GET）')
        .onClick(this.query2)
      Button('添加一个学生（POST）')
        .onClick(this.save)
      Button('更新一个学生（PUT）')
        .onClick(this.update)
      Button('删除一个学生（DELETE）')
        .onClick(this.remove)

      Divider()

      List() {
        ForEach(this.studentList, (item) => {
          ListItem(){
            Text(JSON.stringify(item))
          }
        })
      }
    }
      .width('100%')
  }
}

实现常用CRUD功能

/*
 * 人员列表
 * */
import { Student, StudentArr } from './api/types'
import { reqAddStudent, reqGetStudents, reqUpdateStudent } from './api'
import promptAction from '@ohos.promptAction'
import { reqDeleteStudent } from './api'

@Entry
@Component
struct StudentsPage {

  @State students: StudentArr = []
  @State student: Student = {id: 0, name: '', age: 0, gender: '女'} // 添加和更新收集的学生

  dialogController: CustomDialogController = new CustomDialogController({
    builder: CustomDialogExample({
      cancel: this.onCancel,
      confirm: this.onAccept.bind(this),
      student: $student
    }),
    alignment: DialogAlignment.Default,  // 可设置dialog的对齐方式，设定显示在底部或中间等，默认为底部显示
  })
  onCancel() {
    console.info('Callback when the first button is clicked')
  }
  async onAccept() {
    if (this.student.id) {
      await reqUpdateStudent(this.student)
      promptAction.showToast({message: '更新学生成功'})
    } else {
      await reqAddStudent(this.student)
      promptAction.showToast({message: '添加学生成功'})
    }
    this.getStudents()
  }

  async getStudents () {
    const list = await reqGetStudents()
    this.students = list
  }

  aboutToAppear() {
    this.getStudents()
  }

  async deleteStudent (s: Student) {
    // 显示删除的确认框
    const {index} = await promptAction.showDialog({
      title: '警告',
      message: `确认删除${s.name}吗?`,
      buttons: [
        {text: '取消', color: 'black'},
        {text: '确定', color: 'black'},
      ]
    })
    if (index===1) {
      await reqDeleteStudent(s.id)
      promptAction.showToast({message: '删除成功'})
      this.getStudents()
    }
  }

  addStudent () {
    this.student = {id: 0, name: '', age: 0, gender: '女'}
    // 显示添加的对话框
    this.dialogController.open()
  }

  updateStudent (s: Student) {
    this.student = {...s}
    // 显示删除的对话框
    this.dialogController.open()
  }

  @Builder
  ItemBuilder (s: Student) {
    Row(){
      Text(s.name).fontSize(20).width(100)
      Text(s.age + '').fontSize(20)
      Text(s.gender).fontSize(20)
      Button('更新').onClick(() => this.updateStudent(s))
      Button('删除').backgroundColor(Color.Red)
        .onClick(() => this.deleteStudent(s))
    }
    .width('100%')
    .height(40)
    .justifyContent(FlexAlign.SpaceBetween)
  }

  build() {
    Column({space: 10}) {
      Row() {
        Text('学生管理').fontSize(30)
        Blank()
        Button('+').fontSize(30).onClick(() => this.addStudent())
      }
        .width('100%')
        .height(50)
        .border({width: {bottom: 1}, color: Color.Gray})

      List({space: 10}) {
        ForEach(this.students, (item: Student) => {
          ListItem() {
            this.ItemBuilder(item)
          }
        })
      }
    }
      .width('100%')
      .height('100%')
      .padding(20)
  }
}

@CustomDialog
struct CustomDialogExample {
  @Link student: Student
  controller: CustomDialogController
  cancel: () => void
  confirm: () => void

  @Styles
  inputStyles () {
    .layoutWeight(1)
    .borderRadius(0)
    .backgroundColor(Color.White)
    .padding({left: 0})
    .border({width: {bottom: 1}, color: Color.Gray})
  }

  build() {
    Column({space: 10}) {
      Text(this.student.id ?'更新学生':'添加学生').fontSize(25)

      Row(){
        Text('姓名').margin({right: 20})
        TextInput({text: this.student.name, placeholder: '请输入姓名'})
          .inputStyles()
          .onChange(val => this.student.name = val)
      }.width('100%').height(40)

      Row(){
        Text('年龄').margin({right: 20})
        TextInput({text: this.student.age + '', placeholder: '请输入年龄'})
          .inputStyles()
          .type(InputType.PhoneNumber)
          .onChange(val => this.student.age = +val)
      }.width('100%').height(40)

      Row(){
        Text('性别').margin({right: 20})
        Select([{value: '男'}, {value: '女'}])
          .value(this.student.gender)
          .width(50)
          .onSelect((index, val) => this.student.gender = val)
      }.width('100%').height(40)


      Flex({ justifyContent: FlexAlign.SpaceAround }) {
        Button('取消')
          .onClick(() => {
            this.controller.close()
            this.cancel()
          }).backgroundColor(Color.Gray)
        Button('确定')
          .onClick(() => {
            this.controller.close()
            this.confirm()
          }).backgroundColor(Color.Blue)
      }
    }.width('100%').padding(20)
  }
}
其它功能
多线程
1. 介绍
任务池（taskpool）作用是为应用程序提供一个多线程的运行环境
2. 注意事项
● 实现任务的函数需要使用装饰器@Concurrent标注，且仅支持在.ets文件中使用。
● 任务函数在TaskPool工作线程的执行耗时不能超过3分钟（不包含Promise和async/await异步调用的耗时，例如网络下载、文件读写等I/O任务的耗时），否则会被强制退出。
● 序列化传输的数据量大小限制为16MB。
● 只支持在模拟器或真机调试。
3. 使用
// 定义分线程要执行的任务函数
@Concurrent
function add(a: number, b: number): number {
  return a + b;
}

// 创建分线程并执行任务
import { taskpool } from '@kit.ArkTS';
const task = new taskpool.Task(add, 1, 3);
const result = await taskpool.execute(task);

// 另外一种方式
const result = await taskpool.execute(add, 1, 3);
Web组件
● 疑问1：在应用中如何展现一个Web网页？
  ○ 解答：使用Web组件
● 疑问2：如何实现应用端与Web网页的相互通信
  ○ 解答：应用组件调用网页中的JS函数 & 网页JS中调用应用组件的函数
加载页面
● 相关API
  ○ WebviewController: @ohos.web.webview模块提供的webview浏览器的控制器
    ■ loadUrl(url): 加载指定url的网页
  ○ Web组件：显示网页
    ■ src: 要加载的网页地址，远程或本地
    ■ controller: WebviewController的实例
● 编码测试
/*
加载远程网页
 */
import webview from '@ohos.web.webview';

@Entry
@Component
struct WebTest1 {
  webviewController: webview.WebviewController = new webview.WebviewController();

  build() {
    Column() {
      Button('去尚硅谷学习')
        .onClick(() => {
          try {
            // 点击按钮时，通过loadUrl，跳转到www.atguigu.com/harmonyos/
            this.webviewController.loadUrl('http://m.atguigu.com/harmonyos/');
          } catch (error) {
            console.error(`ErrorCode: ${error.code},  Message: ${error.message}`);
          }
        })
      // 组件创建时，加载www.atguigu.com
      Web({ src: 'https://developer.huawei.com/consumer/cn', controller: this.webviewController})
    }
  }
}

/*
加载本地页面
需要先在resources/rawfile下创建2个不同内容的网页test1.html和test2.html
 */
import webview from '@ohos.web.webview';

@Entry
@Component
struct WebTest2 {
  webviewController: webview.WebviewController = new webview.WebviewController();

  build() {
    Column() {
      Button('加载另一个本地页面')
        .onClick(() => {
          try {
            // 点击按钮时，通过loadUrl，跳转到local1.html
            this.webviewController.loadUrl($rawfile("test1.html"));
          } catch (error) {
            console.error(`ErrorCode: ${error.code},  Message: ${error.message}`);
          }
        })
      // 组件创建时，通过$rawfile加载本地文件local.html
      Web({ src: $rawfile("test2.html"), controller: this.webviewController })
    }
  }
}
相互通信
● 相关API
  ○ runJavaScript(script: string): Promise<string>   应用端调用web端JS函数
    ■ script：函数调用的JS代码，可以指定实参传递数据给web端
    ■ 返回值：函数返回值的Promise对象
  ○ registerJavaScriptProxy(object: object, name: string, methodList: Array<string>)   注册应用端的函数供网页端调用
    ■ object: 饱含多个方法的对象
    ■ name: 指定web端访问对象的名称
    ■ methodList: 指定对象中可以访问的方法名
● 编码测试
/*
应用端调用web页面端函数
*/
import webview from '@ohos.web.webview';

@Entry
@Component
struct WebTest3 {
  webviewController: webview.WebviewController = new webview.WebviewController();

  @State content: string = 'HarmonyOS'
  
  onPageShow() {
    const obj = {
      fn1: (val) => {
        this.content += val
      },

      fn2: (val) => {
        this.content += val
        return '应用端返回给web端的数据'
      },

      p1: 123,  // 注意：传递不了属性
    }
    // 注册给Web调用的函数
    this.webviewController.registerJavaScriptProxy(obj, 'atguigu', ['fn1', 'fn2'])
  }

  build() {
    Column() {
      Text(this.content)
      Button('调用web页中的JS函数')
        .onClick(async () => {
          // 调用web端的JS函数，得到函数的返回值
          const result = await this.webviewController.runJavaScript('htmlTest("应用端传递给web端的数据")');
          this.content = result
        })

      Web({ src: $rawfile('test3.html'), controller: this.webviewController})

    }
  }
}

<!DOCTYPE html>
<html>
  <body>
    <p style="margin-top: 50px" id="cotnent">Hello World</p>
    <br>
    <button id="btn">调用应用端的函数</button>

    <script>
      function htmlTest(msg) {
        document.getElementById('cotnent').innerHTML = msg.toUpperCase()
        return 'Web中的JS返回给应用端的数据'
      }

      document.getElementById('btn').addEventListener('click', function () {
        /*Web端调用应用端的函数*/
        atguigu.fn1('aaa')
        const result = atguigu.fn2('bbb')
        document.getElementById('cotnent').innerHTML = result
      })
    </script>
  </body>
</html>
视频播放
● 编码测试：先在resources/rawfile目录下保存一个视频文件：test.mp4
controller: VideoController = new VideoController()

Video({
  src: $rawfile('test.mp4'),
  previewUri: $r('app.media.startIcon'),
  controller: this.controller
})
  .width('100%')
  .height(200)
  .autoPlay(true)
  .controls(true)
应用国际化
● 相关操作
  ○ 常量字符串国际化
  ○ 动态数据国际化
● 相关API
  ○ $r(value: string, ...params: any[]): Resource   用于得到国际化静态字符串
  ○ Configuration.getLocale(): LocaleResponse   得到当前国家的本地对象，包含国家代码，语言代码等
    ■ language： 语言代码
    ■ countryOrRegion：国家或地区代码
  ○ Intl.DateTimeFormat   日期/时间格式化
  ○ Intl.NumberFormat  数字/货币格式化   

● 编码测试
{
  "name": "text_content",
  "value": "Hello Harmony---"
},

{
  "name": "text_content",
  "value": "Hello Harmony"
},

{
  "name": "text_content",
  "value": "你好 鸿蒙"
},

import Intl from '@ohos.intl';
import configuration from '@system.configuration';

/*
常量文本格式化
  en_US/zh_CN资源string
intl国际化
  日期时间格式化
  数字货币格式化
 */
@Entry
@Component
struct I18nPage {

  localeStr: string = '未知'

  aboutToAppear() {
    this.testLocale()
    this.formatDateTime()
    this.formatNumber()
  }

  testLocale () {
    const {language, countryOrRegion} = configuration.getLocale()
    console.log('lc', language, countryOrRegion)
    this.localeStr = language + '-' + countryOrRegion

    const locale = new Intl.Locale(this.localeStr)
    console.log("locale", locale.toString())
  }

  formatDateTime () {
    // 国际化日期时间
    // full long / medium / short
    const d1 = new Intl.DateTimeFormat('zh-CN', { dateStyle: 'long', timeStyle: "long", hourCycle: 'h24' }).format(new Date())
    const d2 = new Intl.DateTimeFormat('en-US', { dateStyle: 'long', timeStyle: "long", hourCycle: 'h24' }).format(new Date())
    console.log(d1)
    console.log(d2)

    const d3 = new Intl.DateTimeFormat('zh-CN', { dateStyle: 'medium', timeStyle: 'medium', hourCycle: 'h24' }).formatRange(new Date(Date.now() - 1000*60*60*60), new Date())
    console.log(d3)
  }

  formatNumber () {
    const number = 1234567.7895
    // 格式化数值
    const n1 = new Intl.NumberFormat('zh-CN', { maximumFractionDigits: 2 }).format(number)
    const n2 = new Intl.NumberFormat('en-US', { maximumFractionDigits: 2 }).format(number)
    console.log(n1, n2)
    // 格式化人民币
    const n3 = new Intl.NumberFormat('zh-CN', {style:'currency', currency: 'CNY', maximumFractionDigits: 1}).format(number)
    const n4 = new Intl.NumberFormat('en-US', {style:'currency', currency: 'USD', maximumFractionDigits: 1}).format(number)
    console.log(n3, n4)
  }

  build() {
    Column({space: 10}){

      Text($r('app.string.text_content'))
        .fontSize(20)

      Text(this.localeStr)
        .fontSize(20)
    }
    .width('100%')
    .padding(10)
  }
}
通知
● 相关操作
  ○ 发布通知
  ○ 点击通知响应跳转
● 相关API
  ○ function publish(request: NotificationRequest): Promise<void>  发布通知
  ○ cancel(id: number): Promise<void>   取消通知
● 编码测试
import { notificationManager } from '@kit.NotificationKit';
import { BusinessError } from '@kit.BasicServicesKit';

@Entry
@Component
struct NotifyPage {
  @State message: string = 'NotifyPage'

  build() {
    Column({space: 10}) {
      Button('发布通知')
        .width('100%')
        .onClick(() => {
          //publish回调
          let publishCallback = (err: BusinessError): void => {
            if (err) {
              console.error(`publish failed, code is ${err.code}, message is ${err.message}`);
            } else {
              console.info("publish success");
            }
          }
          //通知Request对象
          let notificationRequest: notificationManager.NotificationRequest = {
            id: 1,
            content: {
              notificationContentType: notificationManager.ContentType.NOTIFICATION_CONTENT_BASIC_TEXT,
              normal: {
                title: "test_title",
                text: "test_text",
                additionalText: "test_additionalText"
              }
            }
          };
          notificationManager.publish(notificationRequest, publishCallback);
          })
    }
    .width('100%')
    .padding(20)
  }
}
位置服务
● 相关操作
  ○ 获取当前位置
  ○ 根据经纬度得到地址
  ○ 根据地址得到对应的经纬度
● 相关API
  ○ 主要使用@ohos.geoLocationManager模块的API
  ○ manager.getLastLocation(): Location  获取当前位置
    ■ longitude 经度
    ■ latitude  纬度
  ○ manager.on(type: 'locationChange', request: LocationRequest, callback: Callback<Location>) 绑定位置改变监听，用于得到最新的位置
  ○ manager.getAddressesFromLocationName(request: GeoCodeRequest): Promise<Array<GeoAddress>>  获取指定地址对应的经纬度
  ○ manager.getAddressesFromLocation(request: ReverseGeoCodeRequest): Promise<Array<GeoAddress>>  获取指定经纬度对应的地址
● 编码测试
// 申请权限
{
  "name": "ohos.permission.APPROXIMATELY_LOCATION",
  "reason": "$string:app_name",
  "usedScene": {
    "when": "inuse"
  }
},
{
  "name": "ohos.permission.LOCATION",
  "reason": "$string:app_name",
  "usedScene": {
    "when": "inuse"
  }
}
import geoLocationManager from '@ohos.geoLocationManager';

import abilityAccessCtrl, { Permissions } from '@ohos.abilityAccessCtrl';
import common from '@ohos.app.ability.common';
import promptAction from '@ohos.promptAction';
import Prompt from '@system.prompt';

const permissions: Array<Permissions> = ['ohos.permission.LOCATION'];

let requestInfo = {
  'priority': geoLocationManager.LocationRequestPriority.ACCURACY,
  'timeInterval': 0,
  'distanceInterval': 0,
  'maxAccuracy': 0
};

@Entry
@Component
struct LocationPage {

  @State address: string = '未知地址'
  @State longitude: number = 0
  @State @Watch('onLatChange') latitude: number = 0

  async openPermissionsInSystemSettings() {
    let context = getContext(this) as common.UIAbilityContext;
    let wantInfo = {
      action: 'action.settings.app.info',
      parameters: {
        settingsParamBundleName: 'com.example.myapplication' // 打开指定应用的详情页面
      }
    }
    context.startAbility(wantInfo)
  }

  async isPerLocation (){
    let context = getContext(this) as common.UIAbilityContext;
    let atManager = abilityAccessCtrl.createAtManager();
    const data = await atManager.requestPermissionsFromUser(context, permissions)
    let grantStatus: Array<number> = data.authResults;
    const status = grantStatus[0]
    console.log('status', status, grantStatus.length);


    return status === 0
  }

  async reqPermissionsFromUser() {
    if (!await this.isPerLocation()) {
      // 用户拒绝授权，提示用户必须授权才能访问当前页面的功能，并引导用户到系统设置中打开相应的权限
      const response = await promptAction.showDialog({
        title: '警告',
        message: '还没有开启定位权限',
        buttons: [
          {
            text: '禁止',
            color: '#000000',
          },
          {
            text: '开启',
            color: '#000000',
          }
        ]
      })
      if (response.index===0) {
        Prompt.showToast({message: '当前页面无法定位'})
      } else {
        this.openPermissionsInSystemSettings()
      }
    }
  }

  async aboutToAppear() {
    await this.reqPermissionsFromUser()
  }

  async onPageShow() {
    console.log('onPageShow')
    if (await this.isPerLocation()) {
      geoLocationManager.on('locationChange', requestInfo, this.locationChange);
    }
  }

  onPageHide() {
    geoLocationManager.off('locationChange', this.locationChange)
  }

  locationChange = (location: geoLocationManager.Location) => {
    console.log('locationChanger: data: ' + JSON.stringify(location));
    const {latitude, longitude} = location
    this.longitude = longitude
    this.latitude = latitude
  };

  async onLatChange () {
    let reverseGeocodeRequest = {"latitude": this.latitude, "longitude": this.longitude, "maxItems": 1};
    try {
      const result = await geoLocationManager.getAddressesFromLocation(reverseGeocodeRequest);
      this.address = result[0].descriptions[0]
    } catch (err) {
      console.error("errCode:" + err.code + ",errMessage:" + err.message);
    }
  }

  build() {
    Column({space: 10}) {

      Text(this.latitude + '--' + this.longitude)

      Text(this.address)

      Button('获取当前位置')
        .width('100%')
        .onClick(() => {
          try {
            let location = geoLocationManager.getLastLocation();
            console.log('获取到位置', JSON.stringify(location))
            const {latitude, longitude} = location
            this.longitude = longitude
            this.latitude = latitude

          } catch (err) {
            console.error("errCode:" + err.code + ",errMessage:" + err.message);
          }
        })

      Button('得到【尚硅谷武汉基地】的经纬度')
        .width('100%')
        .onClick(async () => {
          let geocodeRequest = {"description": "尚硅谷武汉基地", "maxItems": 1};
          try {
            const result = await geoLocationManager.getAddressesFromLocationName(geocodeRequest);
            const {latitude, longitude} = result[0]

            this.latitude = latitude
            this.longitude = longitude
          } catch (error) {
            console.error('getAddressesFromLocationName err: ' + JSON.stringify(error));
          }
        })
    }
    .width('100%')
    .padding(20)
  }
}
电话服务
● 相关操作
  ○ 跳转拨号界面拨号
  ○ 获取信号信息
● 相关API
  ○ @ohos.telephony.call模块
    ■ call.makeCall(phoneNumber: string, callback: AsyncCallback<void>)  指定号码，跳转拨号界面
● 编码测试
import { call } from '@kit.TelephonyKit';

@Entry
@Component
struct PhonePage {

  build() {
    Column({space: 10}) {
      Button('呼13712341234')
        .width('100%')
        .onClick(() => {
          // 续跳转到拨号界面，并显示拨号的号码
          call.makeCall("13712341234", (err)=> {
            if (!err) {
              console.log("make call success.");
            } else {
              console.log("make call fail, err is:" + JSON.stringify(err));
            }
          });
        })
    }
    .width('100%')
    .padding(20)
  }
}
多窗口
