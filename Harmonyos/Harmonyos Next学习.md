# Harmonyos Next学习.md

# 一、基本语法

## 1、自定义组件

在ArkUI中，UI显示的内容均为组件，由框架接提供的称为系统组件，由开发者定义的称为自定义组件。在进行 UI 界面开发时，通常不是简单的将系统组件进行组合使用，而是需要考虑代码可复用性、业务逻辑与UI分离，后续版本演进等因素。因此，将UI和部分业务逻辑封装成自定义组件是不可或缺的能力。

自定义组件具有以下特点：

- 可组合：允许开发者组合使用系统组件、及其属性和方法。
- 可重用：自定义组件可以被其他组件重用，并作为不同的实例在不同的父组件或容器中使用。
- 数据驱动UI更新：通过状态变量的改变，来驱动UI的刷新。

### 自定义组件的基本用法

```js
@Component
struct HelloComponent {
  @State message: string = 'Hello, World!';

  build() {
    // HelloComponent自定义组件组合系统组件Row和Text
    Row() {
      Text(this.message)
        .onClick(() => {
          // 状态变量message的改变驱动UI刷新，UI从'Hello, World!'刷新为'Hello, ArkUI!'
          this.message = 'Hello, ArkUI!';
        })
    }
  } 
}
```

### 页面和自定义组件生命周期

在开始之前，我们先明确自定义组件和页面的关系：

- 自定义组件：@Component装饰的UI单元，可以组合多个系统组件实现UI的复用，可以调用组件的生命周期。
- 页面：即应用的UI页面。可以由一个或者多个自定义组件组成，[@Entry](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-create-custom-components-0000001580025742-V1#ZH-CN_TOPIC_0000001666547300__自定义组件的基本结构)装饰的自定义组件为页面的入口组件，即页面的根节点，一个页面有且仅能有一个@Entry。只有被@Entry装饰的组件才可以调用页面的生命周期。

页面生命周期，即被@Entry装饰的组件生命周期，提供以下生命周期接口：

- [onPageShow](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-custom-component-lifecycle-0000001579866590-V1#ZH-CN_TOPIC_0000001666547700__onpageshow)：页面每次显示时触发一次，包括路由过程、应用进入前台等场景。
- [onPageHide](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-custom-component-lifecycle-0000001579866590-V1#ZH-CN_TOPIC_0000001666547700__onpagehide)：页面每次隐藏时触发一次，包括路由过程、应用进入后台等场景。
- [onBackPress](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-custom-component-lifecycle-0000001579866590-V1#ZH-CN_TOPIC_0000001666547700__onbackpress)：当用户点击返回按钮时触发。

组件生命周期，即一般用@Component装饰的自定义组件的生命周期，提供以下生命周期接口：

- [aboutToAppear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-custom-component-lifecycle-0000001579866590-V1#ZH-CN_TOPIC_0000001666547700__abouttoappear)：组件即将出现时回调该接口，具体时机为在创建自定义组件的新实例后，在执行其build()函数之前执行。
- [aboutToDisappear](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-custom-component-lifecycle-0000001579866590-V1#ZH-CN_TOPIC_0000001666547700__abouttodisappear)：aboutToDisappear函数在自定义组件析构销毁之前执行。不允许在aboutToDisappear函数中改变状态变量，特别是@Link变量的修改可能会导致应用程序行为不稳定。

生命周期流程如下图所示，下图展示的是被@Entry装饰的组件（页面）生命周期。

![img](https://alliance-communityfile-drcn.dbankcdn.com/FileServer/getFile/cmtyPub/011/111/111/0000000000011111111.20240415145038.62586124932834396542583512272723:50001231000000:2800:514A40C841B97B4DAC337D4AA69BDD46524DCBCA8741E75A5FE4D36130DE7D7F.png?needInitFileName=true?needInitFileName=true)

根据上面的流程图，我们从自定义组件的初始创建、重新渲染和删除来详细解释。

## 2、@Builder装饰器：自定义构建函数

![9201715220851_.pic](https://gitee.com/LuHenChang/blog_pic/raw/master/9201715220851_.pic.jpg)

```kotlin
@Entry
@Component
struct Index {
  @Prop message: string = 'Hello World';

  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold).onClick((event: ClickEvent) => {
        this.message = "Hell ArcTs"
      })
    }
    .height('100%')
  }
}
```

### 全局自定义构建函数

为了让Index页面保持简洁，可以采用全局自定义构造函数，将其内部组件分装到外边。

> 必须分装为对象才可以更新全局@Builder内容，且参数必须唯一。如果在其他包需要export让外部可见，可调用。

```js
export class Tmp {
  paramA1: string = ''
}
```

[按引用传递](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-builder-0000001579865938-V1#ZH-CN_TOPIC_0000001666548016__按引用传递参数)

```js
import { Tmp } from '../data/model/Tmp'

//引用传递，会更新
@Builder
export function MyGlobalTextBuilderFunction(
  params: Tmp) {
  Text(`${params.paramA1}`)
    .fontSize(50)
    .fontWeight(FontWeight.Bold)
}

//按值传递参数
@Builder
export function MyGlobalTextBuilderFunction1(
  params: string) {
  Text(`${params}`)
    .fontSize(50)
    .fontWeight(FontWeight.Bold)
}
```

所以@Builder方式构建需要进行按应用传参

```typescript
@Entry
@Component
struct Index {
  @Prop message: string = 'Hello World';

  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .onClick((event: ClickEvent) => {
          this.message = "Hell ArcTs"
        })
      //全局，必须是将参数进行对象分装进行引用才可以。按引用传递
      MyGlobalTextBuilderFunction({ paramA1: this.message })
      //这样是无法更新UI的
      MyGlobalTextBuilderFunction1(this.message)

    }
    .height('100%')
  }
}
```

### 局部自定义构建函数

> 局部自定义构造函数只是不需要加function、使用时this.进行引用即可。

```typescript
@Entry
@Component
struct Index {
  @Prop message: string = 'Hello World';

  @Builder
  LocalTextBuilderFunction(
    params: Tmp) {
    Text(`${params.paramA1}`)
      .fontSize(50)
      .fontWeight(FontWeight.Bold)
  }

  build() {
    Column() {
      Text(this.message)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
        .onClick((event: ClickEvent) => {
          this.message = "Hell ArcTs"
        })
      //局部方法
      this.LocalTextBuilderFunction({ paramA1: this.message })
    }
    .height('100%')
  }
}
```

### @BuilderParam装饰器：引用@Builder函数

@BuilderParam装饰的方法可以是有参数和无参数的两种形式，需与指向的@Builder方法类型匹配。@BuilderParam装饰的方法类型需要和@Builder方法类型一致。

```js
class Tmp{
  label:string = ''
}
@Builder function overBuilder($$ : Tmp) {
  Text($$.label)
    .width(400)
    .height(50)
    .backgroundColor(Color.Green)
}

@Component
struct Child {
  label: string = 'Child'
  @Builder customBuilder() {}
  // 无参数类型，指向的componentBuilder也是无参数类型
  @BuilderParam customBuilderParam: () => void = this.customBuilder;
  // 有参数类型，指向的overBuilder也是有参数类型的方法
  @BuilderParam customOverBuilderParam: ($$ : Tmp) => void = overBuilder;

  build() {
    Column() {
      this.customBuilderParam()
      this.customOverBuilderParam({label: 'global Builder label' } )
    }
  }
}

@Entry
@Component
struct Parent {
  label: string = 'Parent'

  @Builder componentBuilder() {
    Text(`${this.label}`)
  }

  build() {
    Column() {
      this.componentBuilder()
      Child({ customBuilderParam: this.componentBuilder, customOverBuilderParam: overBuilder })
    }
  }
}
```

## 3、自定义装饰器

### @Styles装饰器：定义组件重用样式

- 当前@Styles仅支持[通用属性](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-universal-attributes-size-0000001580026314-V1)和[通用事件](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V1/ts-universal-events-click-0000001580345638-V1)。

- @Styles方法不支持参数，反例如下。

  ```typescript
  // 反例： @Styles不支持参数
  @Styles function globalFancy (value: number) { .width(value)}
  ```

- @Styles可以定义在组件内或全局，在全局定义时需在方法名前面添加function关键字，组件内定义时则不需要添加function关键字。

说明：只能在当前文件内使用，不支持export

```javascript
// 全局
@Styles function functionName() { ... }

// 在组件内
@Component
struct FancyUse {
  @Styles fancy() {
    .height(100)
  }
}
```

- 定义在组件内的@Styles可以通过this访问组件的常量和状态变量，并可以在@Styles里通过事件来改变状态变量的值，示例如下：

  ```typescript
  @Component
  struct FancyUse {
    @State heightValue: number = 100 
    @Styles fancy() {   
      .height(this.heightValue)   
       .backgroundColor(Color.Yellow)
       .onClick(() => { 
        this.heightValue = 200  
        })
    }
  }
  ```

- 组件内@Styles的优先级高于全局@Styles。

  框架优先找当前组件内的@Styles，如果找不到，则会全局查找。

### @Extend装饰器：定义扩展组件样式

**使用规则**

- 和@Styles不同，@Extend仅支持在全局定义，不支持在组件内部定义。

  > 说明：只能在当前文件内使用，不支持export

- 和@Styles不同，@Extend支持封装指定的组件的私有属性和私有事件，以及预定义相同组件的@Extend的方法。

  ```typescript
  // @Extend(Text)可以支持Text的私有属性
  fontColor@Extend(Text) function fancy () {
    .fontColor(Color.Red)
  }
  // superFancyText可以调用预定义的fancy
  @Extend(Text) function superFancyText(size:number) {  
    .fontSize(size).fancy()
  }
  ```
  
  @Styles不同，@Extend装饰的方法支持参数，开发者可以在调用时传递参数，调用遵循TS方法传值调用。
  
  ```typescript
  // xxx.ets
  @Extend(Text) function fancy (fontSize: number) { 
    .fontColor(Color.Red).fontSize(fontSize)
  }
  @Entry
  @Component
  struct FancyUse { 
    build() {   
      Row({ space: 10 }) {  
        Text('Fancy').fancy(16)    
        Text('Fancy').fancy(24)  
       }
    }
  }
  ```
  
  @Extend装饰的方法的参数可以为function，作为Event事件的句柄。
  
  ```typescript
  @Extend(Text) function makeMeClick(onClick: () => void) {
    .backgroundColor(Color.Blue)
    .onClick(onClick)
  }
  
  @Entry
  @Component
  struct FancyUse {
    @State label: string = 'Hello World';
  
    onClickHandler() {
      this.label = 'Hello ArkUI';
    }
  
    build() {
      Row({ space: 10 }) {
        Text(`${this.label}`)
          .makeMeClick(() => {this.onClickHandler()})
      }
    }
  }
  ```
  
  @Extend的参数可以为[状态变量](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-state-management-overview-0000001580025746-V1)，当状态变量改变时，UI可以正常的被刷新渲染。
  
  ```typescript
  @Extend(Text) function fancy (fontSize: number) {
    .fontColor(Color.Red)
    .fontSize(fontSize)
  }
  
  @Entry
  @Component
  struct FancyUse {
    @State fontSizeValue: number = 20
    build() {
      Row({ space: 10 }) {
        Text('Fancy')
          .fancy(this.fontSizeValue)
          .onClick(() => {
            this.fontSizeValue = 30
          })
      }
    }
  }
  ```

# 二、状态管理

自定义组件拥有变量，变量必须被装饰器装饰才可以成为状态变量，状态变量的改变会引起UI的渲染刷新。如果不使用状态变量，UI只能在初始化时渲染，后续将不会再刷新。 下图展示了State和View（UI）之间的关系。

![image-20240514110342575](https://gitee.com/LuHenChang/blog_pic/raw/master/image-20240514110342575.png)

- View(UI)：UI渲染，指将build方法内的UI描述和@Builder装饰的方法内的UI描述映射到界面。
- State：状态，指驱动UI更新的数据。用户通过触发组件的事件方法，改变状态数据。状态数据的改变，引起UI的重新渲染。

状态变量：被状态装饰器装饰的变量。

[管理组件拥有的状态](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-state-0000001579865942-V1)，即图中Components级别的状态管理：

![image-20240514111251478](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240514111251478.png)

- [@State](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-state-0000001579865942-V1)：@State装饰的变量拥有其所属组件的状态，可以作为其子组件单向和双向同步的数据源。当其数值改变时，会引起相关组件的渲染刷新。
- [@Prop](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-prop-0000001580185150-V1)：@Prop装饰的变量可以和父组件建立单向同步关系，@Prop装饰的变量是可变的，但修改不会同步回父组件。
- [@Link](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-link-0000001630145733-V1)：@Link装饰的变量和父组件构建双向同步关系的状态变量，父组件会接受来自@Link装饰的变量的修改的同步，父组件的更新也会同步给@Link装饰的变量。
- [@Provide/@Consume](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-provide-and-consume-0000001580345078-V1)：@Provide/@Consume装饰的变量用于跨组件层级（多层组件）同步状态变量，可以不需要通过参数命名机制传递，通过alias（别名）或者属性名绑定。
- [@Observed](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-observed-and-objectlink-0000001630425061-V1)：@Observed装饰class，需要观察多层嵌套场景的class需要被@Observed装饰。单独使用@Observed没有任何作用，需要和@ObjectLink、@Prop连用。
- [@ObjectLink](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V1/arkts-observed-and-objectlink-0000001630425061-V1)：@ObjectLink装饰的变量接收@Observed装饰的class的实例，应用于观察多层嵌套场景，和父组件的数据源构建双向同步。

### 使用箭头函数改变状态变量未生效

```js
class TitleModel {
  title: string = ''
  name: string = ''
  sub: string = ''

  constructor(title: string, name: string, sub: string) {
    this.title = title
    this.name = name
    this.sub = sub
  }

  //箭头函数需要注意
  changeTitle = (vm: TitleModel) => {
    //这样是错误的 this.title这里的this指向了当前类TitleModel，而非装饰器修饰的状态变量。
    this.title = "Hello ArkTs"
    vm.title = "Hello ArkTs"
  }

  changeName(): void {
    this.name = "王飞"
  }

  changeSub(): void {
    this.name = "SubSecond"
  }
}

@Entry
@Component
struct StateStudyPage {
  @State titleModel: TitleModel = new TitleModel("Hello World", "王菲", "sub");

  build() {
    Row() {
      Column() {
        Text(this.titleModel.title)
          .fontSize(50)
          .fontWeight(FontWeight.Bold).onClick(() => {
          let self = this.titleModel
          this.titleModel.changeTitle(self)
          //为啥不能更新呢？
          //编译之后：this.titleModel.changeTitle(ObservedObject.GetRawObject(this.titleModel));
          //编译之后发现会被ObservedObject.GetRawObject包裹。所以引用非titleModel对象了。
          //this.titleModel.changeTitle(this.titleModel)
        })

        Text(this.titleModel.name)
          .fontSize(50)
          .fontWeight(FontWeight.Bold).onClick(() => {
          this.titleModel.changeName()
        })

        Text(this.titleModel.name)
          .fontSize(50)
          .fontWeight(FontWeight.Bold).onClick(() => {
          this.titleModel.changeSub()
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

### 状态变量的修改放在构造函数内未生效

在状态管理中，类会被一层“代理”进行包装。当在组件中改变该类的成员变量时，会被该代理进行拦截，在更改数据源中值的同时，也会将变化通知给绑定的组件，从而实现观测变化与触发刷新。当开发者把状态变量的修改放在构造函数里时，此修改不会经过代理（因为是直接对数据源中的值进行修改），即使修改成功执行，也无法观测UI的刷新。【反例】

```javascript
@Entry
@Component
struct Index {
  @State viewModel: TestModel = new TestModel();

  build() {
    Row() {
      Column() {
        Text(this.viewModel.isSuccess ? 'success' : 'failed')
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
          .onClick(() => {
            this.viewModel.query()
          })
      }.width('100%')
    }.height('100%')
  }
}

export class TestModel {
  isSuccess: boolean = false
  model: Model

  constructor() {
    this.model = new Model(() => {
      this.isSuccess = true
      console.log(`this.isSuccess: ${this.isSuccess}`)
    })
  }

  query() {
    this.model.query()
  }
}

export class Model {
  callback: () => void

  constructor(cb: () => void) {
    this.callback = cb
  }

  query() {
    this.callback()
  }
}
```

【正例】

```javascript
@Entry
@Component
struct Index {
  @State viewModel: TestModel = new TestModel();

  build() {
    Row() {
      Column() {
        Text(this.viewModel.isSuccess ? 'success' : 'failed')
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
          .onClick(() => {
            this.viewModel.query()
          })
      }.width('100%')
    }.height('100%')
  }
}

export class TestModel {
  isSuccess: boolean = false
  model: Model = new Model(() => {
  })

  query() {
    this.model = new Model(() => {
      this.isSuccess = true
    })
    this.model.query()
  }
}

export class Model {
  callback: () => void

  constructor(cb: () => void) {
    this.callback = cb
  }

  query() {
    this.callback()
  }
}
```



















