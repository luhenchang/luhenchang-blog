Android面试总结

1.动画类型？属性动画和补间动画的区别？

2.StringBuffer和StringBuilder区别？

3.jvm内存模型？

4.线程池7大核心参数及原理？

5.Android多进程方式有哪些？各自的优缺点？

6.Binder机制原理？

7.App启动流程？

8.Handler机制原理？

9.子线程可以更新ui吗？在Activity那个生命周期？

10.Activity生命周期？A跳转B执行生命周期？弹出Dialog时Activity生命周期？

11.屏幕旋转生命周期？

12.Activity启动模式及应用场景？A是singerTask,BC默认,DsingleTop，出栈顺序？

13.java中extends和super的区别？

14.String s1 = new String("abc") 创建了几个字符串对象？

15.Android中自定义view的流程以及onMeaure()方法调用时机？

16.什么时候调用View的onmeasure()方法?

17.为什么okhttp中核心线程数是0？

18.okhttp拦截器原理？

19.okhttp中 应用层拦截器和网络层拦截器区别？

20.synchronized关键字使用场景?

22.ThreadLocal原理？

23.jvm垃圾回收机制？回收算法？

24.RecyclerView缓存机制及原理？各自调用时机？

25.TV开发焦点问题？如何记忆焦点？

26.屏幕适配原理？

27.Android中内存优化？

28.什么是ANR？ANR类型及发生原因和解决办法？

29.内存泄漏是什么？发生原因？如何排查？解决方法？

30.ArrayList和LiskedList区别？

31.HashMap底层实现原理？扩容原理？

32.Android中开启多线程的方式？优缺点？

33.如何让多个线程按顺序执行？

34.OK HTTP使用了哪些设计模式及优缺点？

35.setContentView的绘制流程？

36.App打包流程？

37.Apk安装过程？

38.Android常用的设计模式有哪些？说说你的理解？

39.retrofit原理？

40.rxjava原理？如何切换线程？map操作符和flatmap区别？背压？

41.线程池核心参数有哪些？使用流程？拒绝策略？

42.jvm内存模型？

43.GC回收机制？如何判断一个对象是否能被回收？gc回收算法？

44.synchronized和volatile区别？

45.同步锁？重入锁？可重入锁？

46.java多线程用法？如何让多个线程按顺序执行？

47.LiveDate原理？使用过程中遇到的问题？解决方法？

48.viewmodel原理？

49.lifecycle原理？

50.协程原理？优缺点？

51.Java封装、多态、继承是什么？

52.Java中抽象和接口的区别？

53.Java中引用类型有哪些？概念？

54.Java中树结构和链表结构有啥区别？HashMap原理？ 55.Java中的线程模型？为啥i++=2？

56.Java中泛型的理解？

57.类的加载器，双亲机制，Android的类加载器

58.Java的虚拟机JVM的两个内存：栈内存和堆内存的区别是什么？

59.Android各大版本区别？如何适配？

60.Http和https的区别？

61.TCP三次握手和四次挥手过程？

62.TCP、UDP、Http、WebSocket区别？

63.对称加密和非对称加密？

64.组件化、模块化、插件化区别？

65.插件化原理？

66.Android中如何混淆以及要注意的问题？

67.Android中SDK开发如何加密及需要注意的问题？

68.Android中的保活方式有哪些？

69.Android多屏幕适配方案及原理？

70.Android中性能优化方式有哪些？

71.启动优化如何做？内存优化的方式？

72.自定义View的流程？3种测量模式区别？

73.Android中事件分发机制？

74.滑动冲突处理方式？

75.Android中线程通信方式有哪些？

76.服务两种启动方式生命周期如何执行？

77.断点续传原理？

78.Android中加密方式有哪些？如何进行加固处理？

79.Android签名机制v1、v2、v3的区别？

80.项目中遇到哪些问题？你是如何解决的？

81.蓝牙通信协议有哪些？数据格式？

82.音频编解码问题？PCM转aac?

83.视频播放器内核如何切换？

84.视频无缝播放如何实现？

85.视频列表跳转详情播放进度保存？

86.视频列表跳转详情播放状态同步？

87.视频边播边播如何实现？缓存实现？

88.播放时默认无声和按音量键调节声音的实现？

89.视频播放关键帧处理？

90.视频拖动时进度回弹处理？

91.视频小窗切换全屏实现？

92.视频播放在手机锁屏、退到后台和杀手app播放状态处理？

93.视频播放进度同步和清除进度处理？

94.视频播放卡顿处理？

95.视频全屏退到小窗进度、状态同步？

96.视频高宽不能全部充满屏幕，有黑边的问题？

97.在视频默认状态或暂停时从某个时间节点开始播放？

98.4g和WiFi切换流量提示？

99.串口通信协议有哪些？

100.常见的串口类型有哪些？

101.串口帧数据的组成

102.怎么排查数据收发问题，自发自收检测？

103.遇到不能发送数据，在接收数据后才能发送要怎么解决？

104.丢数据，数据被拆分要怎么解决?

105.串口无响应如何排查?

106.常见的数据检验方式，在数据比较多的情况，用啥方法转换能避免内存溢出问题?

107.串口设备主从通信方式?

108.串口广播组播的理解?

109.多个进程使用串口数据如何封装接口?

110.是否有wifi bt usb gps nfc 的串口调试经验?

111.scoket相关?tcp、udp、mqtt、websocket?

112.串口通信拆包、分包、丢包处理？ 113.线程池原理？

114.livedata和stateFlow原理？

115.flow、stateflow、sharedflow、livedata区别？实现原理？

116.ANR日志怎么抓取？问题查找？分析？解决方法？如何设计一个anr日志手机框架？

117.动画的实现方式？帧动画缺点？如何优化？

118.跨进程实现有哪几种方式？原理？如何实现？

119.kotlin高级函数有哪些？各种区别？原理？

120.kotlin协程是什么？原理？

121.kotlin优点？为啥使用？

122.kotlinobject函数是啥？有啥作用？

123.kotlin中apply、also、let、run区别与联系？应用场景？

124.kotlinz中如何实现懒加载？by lazy和lateinit区别？

125.viewmodel原理？

126.livedata优点？缺点？数据倒灌和粘性事件咋解决？ 127,请简述下什么是kotlin？它有什么特性？

128.Kotlin 中注解 @JvmOverloads 的作用？

129.Kotlin中的MutableList与List有什么区别？

130.kotlin实现单例的几种方式？

131.kotlin实现单例的几种方式？

132.什么是委托属性？简单说一下应用场景？

133.kotlin中Unit的应用以及和Java中void的区别？

134.Kotlin 中 infix 关键字的原理和使用场景?

135.Kotlin中的可见性修饰符有哪些？相比于 Java 有什么区别?

136.你觉得Kotlin与Java混合开发时需要注意哪些问题?

137.在Kotlin中，何为解构？该如何使用?

138.在Kotlin中，什么是内联函数？有什么作用?

139.谈谈kotlin中的构造方法？有哪些注意事项?

140.谈谈Kotlin中的Sequence，为什么它处理集合操作更加高效?

141.请谈谈Kotlin中的Coroutines，它与线程有什么区别？有哪些优点?

142.Kotlin中该如何安全地处理可空类型?

143.Kotlin中的?.然后后面调用方法如果为空的情况下是什么？如果是调用变量是什么情况?

144.说说 Kotlin中 的 Any 与Java中的 Object 有何异同?

145.Kotlin中的数据类型有隐式转换吗？为什么？

146.Kotlin 中集合遍历有哪几种方式？

147.为什么协程比线程要轻量?

148.协程Flow是什么，有哪些应用场景?

149.协程Flow的冷流和热流是什么?

150.协程中可能遇到哪些问题?

151.解释一下extension函数。?

152.kotlin中的null safety是什么意思?

153.kotlin中什么是并发?

154.对于Kotlin中的协程有什么理解？

155.协程比线程更高效的原因是什么？

156.协程框架中主要组成部分？

157.关于协程作用域CoroutineScope?

158.解释协程中的调度程序Dispatcher？

159.关于协程中的作业Job?

160.关于协程中的作业Job?

161.简单说说suspend挂起函数？

162.从另一个挂起函数调用一个挂起函数会发生什么？

163.关于协程中的挂起和阻塞有什么区别?

164.启动协程的launch() 和 async() 有什么区别？在某些情况下应该使用哪个？

165.区分 Kotlin 中的 launch / join 和 async / await

166.协程中的 GlobalScope 以及为什么要避免它？

167.如果协程内部抛出异常会怎么样?

168.CoroutineScope.async {} 中的异常如何工作？

169.平常使用协程时有碰到哪些错误？

170.使用 Kotlin 协程时有哪些好的做法可以遵循？ 171.Kotlin协程比Rxjava/RxKotlin好在哪里?

172.Kotlin中的数据类型有隐式转换吗？为什么？

173.Kotlin中集合遍历有哪几种方式？

174.谈谈kotlin中的构造方法？有哪些注意事项？

175.谈谈Kotlin中的Sequence，为什么它处理集合操作更加高效？

176.说说Kotlin中的Any与Java中的Object有何异同？

177.Kotlin中的数据类型有隐式转换吗？为什么？

178.理解线程间通信?

179.工作者线程（workerThread）与主线程（UI线程）的理解

180.通过Handler在线程间通信的原理

181.子线程发消息到主线程进行更新 UI，除了 handler 和 AsyncTask，还有什么？

182.子线程中能不能 new handler？为什么？

183.Handler、 Thread 和 HandlerThread 的差别

184.当Activity有多个Handler的时候，Message消息是否会混乱？怎么样区分当前消息由哪个Handler处理？

185.线程更新UI导致崩溃的原因？

186.ANR应用无响应

187.AsyncTask（异步任务）的工作原理

188.AsyncTask使用在哪些场景？它的缺陷是什么？如何解决？

189.Android中动画的类型：

190.理解Activity、View、Window三者之间的关系

191.Activity、Dialog、PopupWindow、Toast 与Window的关系

192.Android中Context详解：

193.讲解一下Context

194.Android常用的数据存储方式（5种）

195.SharedPreference跨进程使用会怎么样？如何保证跨进程使用安全？

196.数据库的操作类型有哪些，如何导入外部数据库？

197.SQLite支持事务吗? 添加删除如何提高性能?

198.Android垃圾回收机制和程序优化System.gc( )

199.为什么图片需要用软引用，MVP模式中的view接口用弱引用

200.Android平台的优势和不足

201.Android中任务栈的分配

202.Activity组件生命周期、四种启动模式

203.Activity的启动过程（不要回答生命周期）

204.保存Activity状态

205.如何修改 Activity 进入和退出动画

206.Service组件

207.什么是 IntentService？有何优点？

208.是否使用过 IntentService，作用是什么， AIDL 解决了什么问题？

209.BoradcastReceiver组件

210.配置文件静态注册和在代码中动态注册两种方式的区别

211.ContentProvider(内容提供者)组件

212.Fragment中add与replace的区别？

213.FragmentPagerAdapter 与 与 FragmentStatePagerAdapter 的区别与使用场景？

214.Activity静态添加Fragment

215.Activity动态加载Fragment

216.Intent

217.ViewPager

218.关于Fragment中的控件的事件的监听

219.使用View绘制视图

220.View的绘制流程

221.View，ViewGroup事件分发

222.Android的事件传递（分发）机制

223.Android中touch事件的传递机制是怎样的?

224.View的分发机制，滑动冲突

225.Android中跨进程通讯的几种方式

226.Android 线程间通信有哪几种方式（重要）

227.AIDL理解

228.AIDL 的全称是什么?如何工作?能处理哪些类型的数据？ 229.什么是 AIDL？如何使用？

230.Android中页面的横屏与竖屏操作

231.横竖屏切换的Activity 生命周期变化？

232.获取手机中屏幕的宽和高的方法

233.内存泄漏的相关原因

234.Android内存泄漏及管理

235.Android平台的虚拟机Dalvik

236.Android中的Binder机制

237.Android中的缓存机制

238.Android 中图片的三级缓存策略

239.Glide三级缓存

240.HybridApp WebView和JS交互

241.RecyclerView和ListView的区别

242.简述一下RecyclerView缓存机制？

243.recyclerView嵌套卡顿解决如何解决

244.Universal-ImageLoader，Picasso，Fresco，Glide对比

245.Xutils, OKhttp, Volley, Retrofit对比

246.请解释下 Android 程序运行时权限与文件系统权限的区别？

247.Framework 工作方式及原理，Activity 是如何生成一个 view 的，机制是什么？

248.Android 判断SD卡是否存在

249.Android与服务器交互的方式中的对称加密和非对称加密是什么?

250.SurfaceView和GLSurfaceView

251.说说JobScheduler

252.说说WorkManager

253.谈一谈startService和bindService的区别，生命周期以及使用场景？

254.Service如何进行保活？

255.热修复的原理

256.JNI

257.谈谈对Android NDK的理解

258.Android设计模式之MVC

259.mvc/mvp/mvvm

260.设计模式的六大原则

261.Android中的性能优化相关问题

262.Bitmap的使用及内存优化

263.性能优化（非常重要）

264.Android对HashMap做了优化后推出的新的容器类是什么？

264.谈谈你对安卓签名的理解

265.请解释安卓为啥要加签名机制?

266.权限管理系统（底层的权限是如何进行 grant 的）？

267.Kotlin 如何在 Android 上运行？

268.为什么要使用 Kotlin？

269.用var和val声明变量有什么区别？

270.用val和const声明变量有什么区别？

271.Kotlin 中如何保证 null 安全？

272.安全调用(?.)和空值检查(!!)有什么区别？

273.Kotlin 中是否有像 java 一样的三元运算符？

274.Kotlin 中的 Elvis 运算符是什么？

275.如何将 Kotlin 源文件转换为 Java 源文件？

276.你觉得Kotlin与Java混合开发时需要注意哪些问题？

277.@JvmStatic、@JvmOverloads、@JvmFiled 在 Kotlin 中有什么用？

278.Kotlin 中的数据类是什么？

279.Kotlin中的数据类型有隐式转换吗？为什么？

280.Kotlin中可以使用int、double、float等原始类型吗？

281.Kotlin 中的字符串插值是什么？

282.Kotlin 中的解构是什么意思？

283.在Kotlin中，何为解构？该如何使用？

284.如何检查一个lateinit变量是否已经初始化？

285.Kotlin 中的 lateinit 和 lazy 有什么区别？ 286.==操作符和===操作符有什么区别？

287.Kotlin 中的 forEach 是什么？

288.Kotlin 中的伴生对象是什么？

289.kotlin中Unit的应用以及和Java中void的区别？

290.Kotlin 中的 Java 静态方法等价物是什么？

291.Kotlin 中的 FlatMap 和 Map 有什么区别？

292.Kotlin中可以使用new关键字实例化一个类对象吗？

293.Kotlin 中的可见性修饰符是什么？

294.Kotlin中的可见性修饰符有哪些？相比于 Java 有什么区别？

295.如何在 Kotlin 中创建 Singleton 类？

296.Kotlin 中的初始化块是什么？

297.Kotlin 中的构造函数有哪些类型？

298.主构造函数和次构造函数之间有什么关系吗？

299.构造函数中使用的默认参数类型是什么？

300.谈谈kotlin中的构造方法？有哪些注意事项？

301.Kotlin 中的扩展函数是什么

302.kotlin基础： From Java To Kotlin

303.Kotlin 中什么时候使用 lateinit 关键字？

304.Kotlin 的延迟初始化: lateinit var 和 by lazy

305.Kotlin Tips:怎么用 Kotlin 去提高生产力（kotlin优势）

306.Kotlin数组和集合

307.Kotlin中的MutableList与List有什么区别？

308.Kotlin集合操作符

309.Kotlin 中集合遍历有哪几种方式？

310.说一下Kotlin的伴生对象(关键字companion)

311.Kotlin 顶层函数和属性

312.Kotlin 中的协程是什么？

313.Kotlin Coroutines 中的挂起函数是什么？

314.Kotlin Coroutines 中 Launch 和 Async 有什么区别？

315.Kotlin Coroutines 中的作用域是什么？

316.Kotlin Coroutines 中的异常处理是如何完成的？

317.在 Kotlin 中如何在 switch 和 when 之间进行选择？

318.Kotlin 中的 open 关键字是做什么用的？

319.什么是 lambdas 表达式？

320.Kotlin 中的高阶函数是什么？

321.Kotlin 中的扩展函数是什么？

322.Kotlin 中的中缀函数是什么？

323.Kotlin 中的内联函数是什么？

324.Kotlin 中的 noinline 是什么？

325.Kotlin 中的具体化类型是什么？

326.Kotlin 中的运算符重载是什么？

327.解释在 Kotlin 中 let、run、with 和 apply 的用例。

328.kotlin中with、run、apply、let函数的区别？一般用于什么场景？

329.Kotlin 中的 pair 和 Triple 是什么？

330.Kotlin 中的标签是什么？

331.使用密封类而不是枚举有什么好处？

332.协程是什么

333.kotlin中关键字data的理解？相对于普通的类有哪些特点？

334.谈谈Kotlin中的Sequence，为什么它处理集合操作更加高效？

335.说说 Kotlin中 的 Any 与Java中的 Object 有何异同？ Android面试总结

1.动画类型？属性动画和补间动画的区别？

2.StringBuffer和StringBuilder区别？

3.jvm内存模型？

4.线程池7大核心参数及原理？

5.Android多进程方式有哪些？各自的优缺点？

6.Binder机制原理？

7.App启动流程？

8.Handler机制原理？

9.子线程可以更新ui吗？在Activity那个生命周期？

10.Activity生命周期？A跳转B执行生命周期？弹出 Dialog时Activity生命周期？

11.屏幕旋转生命周期？

12.Activity启动模式及应用场景？A是 singerTask,BC默认,DsingleTop，出栈顺序？

13.java中extends和super的区别？

14.String s1 = new String("abc") 创建了几个字符 串对象？

15.Android中自定义view的流程以及onMeaure()方 法调用时机？ 16.什么时候调用View的onmeasure()方法?

17.为什么okhttp中核心线程数是0？

18.okhttp拦截器原理？

19.okhttp中 应用层拦截器和网络层拦截器区别？

20.synchronized关键字使用场景?

22.ThreadLocal原理？

23.jvm垃圾回收机制？回收算法？

24.RecyclerView缓存机制及原理？各自调用时机？

25.TV开发焦点问题？如何记忆焦点？

26.屏幕适配原理？

27.Android中内存优化？

28.什么是ANR？ANR类型及发生原因和解决办法？

29.内存泄漏是什么？发生原因？如何排查？解决方 法？

30.ArrayList和LiskedList区别？

31.HashMap底层实现原理？扩容原理？

32.Android中开启多线程的方式？优缺点？ 33.如何让多个线程按顺序执行？

34.OK HTTP使用了哪些设计模式及优缺点？

35.setContentView的绘制流程？

36.App打包流程？

37.Apk安装过程？

38.Android常用的设计模式有哪些？说说你的理解？

39.retrofit原理？

40.rxjava原理？如何切换线程？map操作符和 flatmap区别？背压？

41.线程池核心参数有哪些？使用流程？拒绝策略？

42.jvm内存模型？

43.GC回收机制？如何判断一个对象是否能被回收？ gc回收算法？

44.synchronized和volatile区别？

45.同步锁？重入锁？可重入锁？

46.java多线程用法？如何让多个线程按顺序执行？

47.LiveDate原理？使用过程中遇到的问题？解决方 法？

48.viewmodel原理？ 49.lifecycle原理？

50.协程原理？优缺点？

51.Java封装、多态、继承是什么？

52.Java中抽象和接口的区别？

53.Java中引用类型有哪些？概念？

54.Java中树结构和链表结构有啥区别？HashMap原 理？

55.Java中的线程模型？为啥i++=2？

56.Java中泛型的理解？

57.类的加载器，双亲机制，Android的类加载器

58.Java的虚拟机JVM的两个内存：栈内存和堆内存 的区别是什么？

59.Android各大版本区别？如何适配？

60.Http和https的区别？

61.TCP三次握手和四次挥手过程？

62.TCP、UDP、Http、WebSocket区别？

63.对称加密和非对称加密？

64.组件化、模块化、插件化区别？ 65.插件化原理？

66.Android中如何混淆以及要注意的问题？

67.Android中SDK开发如何加密及需要注意的问题？

68.Android中的保活方式有哪些？

69.Android多屏幕适配方案及原理？

70.Android中性能优化方式有哪些？

71.启动优化如何做？内存优化的方式？

72.自定义View的流程？3种测量模式区别？

73.Android中事件分发机制？

74.滑动冲突处理方式？

75.Android中线程通信方式有哪些？

76.服务两种启动方式生命周期如何执行？

77.断点续传原理？

78.Android中加密方式有哪些？如何进行加固处理？

79.Android签名机制v1、v2、v3的区别？

80.项目中遇到哪些问题？你是如何解决的？

81.蓝牙通信协议有哪些？数据格式？ 82.音频编解码问题？PCM转aac?

83.视频播放器内核如何切换？

84.视频无缝播放如何实现？

85.视频列表跳转详情播放进度保存？

86.视频列表跳转详情播放状态同步？

87.视频边播边播如何实现？缓存实现？

88.播放时默认无声和按音量键调节声音的实现？

89.视频播放关键帧处理？

90.视频拖动时进度回弹处理？

91.视频小窗切换全屏实现？

92.视频播放在手机锁屏、退到后台和杀手app播放状 态处理？

93.视频播放进度同步和清除进度处理？

94.视频播放卡顿处理？

95.视频全屏退到小窗进度、状态同步？

96.视频高宽不能全部充满屏幕，有黑边的问题？

97.在视频默认状态或暂停时从某个时间节点开始播 放？ 98.4g和WiFi切换流量提示？

99.串口通信协议有哪些？

100.常见的串口类型有哪些？

101.串口帧数据的组成

102.怎么排查数据收发问题，自发自收检测？

103.遇到不能发送数据，在接收数据后才能发送要怎 么解决？

104.丢数据，数据被拆分要怎么解决?

105.串口无响应如何排查?

106.常见的数据检验方式，在数据比较多的情况，用 啥方法转换能避免内存溢出问题?

107.串口设备主从通信方式?

108.串口广播组播的理解?

109.多个进程使用串口数据如何封装接口?

110.是否有wifi bt usb gps nfc 的串口调试经验?

111.scoket相关?tcp、udp、mqtt、websocket?

112.串口通信拆包、分包、丢包处理？

113.线程池原理？ 114.livedata和stateFlow原理？

115.flow、stateflow、sharedflow、livedata区别？ 实现原理？

116.ANR日志怎么抓取？问题查找？分析？解决方 法？如何设计一个anr日志手机框架？

117.动画的实现方式？帧动画缺点？如何优化？

118.跨进程实现有哪几种方式？原理？如何实现？

119.kotlin高级函数有哪些？各种区别？原理？

120.kotlin协程是什么？原理？

121.kotlin优点？为啥使用？

122.kotlinobject函数是啥？有啥作用？

123.kotlin中apply、also、let、run区别与联系？应 用场景？

124.kotlinz中如何实现懒加载？by lazy和lateinit区 别？

125.viewmodel原理？

126.livedata优点？缺点？数据倒灌和粘性事件咋解 决？ 127,请简述下什么是kotlin？它有什么特性？ 128.Kotlin 中注解 @JvmOverloads 的作用？

129.Kotlin中的MutableList与List有什么区别？

130.kotlin实现单例的几种方式？

131.kotlin实现单例的几种方式？

132.什么是委托属性？简单说一下应用场景？

133.kotlin中Unit的应用以及和Java中void的区别？

134.Kotlin 中 infix 关键字的原理和使用场景?

135.Kotlin中的可见性修饰符有哪些？相比于 Java 有什么区别?

136.你觉得Kotlin与Java混合开发时需要注意哪些问 题?

137.在Kotlin中，何为解构？该如何使用?

138.在Kotlin中，什么是内联函数？有什么作用?

139.谈谈kotlin中的构造方法？有哪些注意事项?

140.谈谈Kotlin中的Sequence，为什么它处理集合 操作更加高效?

141.请谈谈Kotlin中的Coroutines，它与线程有什么 区别？有哪些优点?

142.Kotlin中该如何安全地处理可空类型? 143.Kotlin中的?.然后后面调用方法如果为空的情况 下是什么？如果是调用变量是什么情况?

144.说说 Kotlin中 的 Any 与Java中的 Object 有何 异同?

145.Kotlin中的数据类型有隐式转换吗？为什么？

146.Kotlin 中集合遍历有哪几种方式？

147.为什么协程比线程要轻量?

148.协程Flow是什么，有哪些应用场景?

149.协程Flow的冷流和热流是什么?

150.协程中可能遇到哪些问题?

151.解释一下extension函数。?

152.kotlin中的null safety是什么意思?

153.kotlin中什么是并发?

154.对于Kotlin中的协程有什么理解？

155.协程比线程更高效的原因是什么？

156.协程框架中主要组成部分？

157.关于协程作用域CoroutineScope?

158.解释协程中的调度程序Dispatcher？ 159.关于协程中的作业Job?

160.关于协程中的作业Job?

161.简单说说suspend挂起函数？

162.从另一个挂起函数调用一个挂起函数会发生什 么？

163.关于协程中的挂起和阻塞有什么区别?

164.启动协程的launch() 和 async() 有什么区别？在 某些情况下应该使用哪个？

165.区分 Kotlin 中的 launch / join 和 async / await

166.协程中的 GlobalScope 以及为什么要避免它？

167.如果协程内部抛出异常会怎么样?

168.CoroutineScope.async {} 中的异常如何工作？

169.平常使用协程时有碰到哪些错误？

170.使用 Kotlin 协程时有哪些好的做法可以遵循？

171.Kotlin协程比Rxjava/RxKotlin好在哪里?

172.Kotlin中的数据类型有隐式转换吗？为什么？

173.Kotlin中集合遍历有哪几种方式？

174.谈谈kotlin中的构造方法？有哪些注意事项？ 175.谈谈Kotlin中的Sequence，为什么它处理集合 操作更加高效？

176.说说Kotlin中的Any与Java中的Object有何异 同？

177.Kotlin中的数据类型有隐式转换吗？为什么？

178.理解线程间通信?

179.工作者线程（workerThread）与主线程（UI线 程）的理解

180.通过Handler在线程间通信的原理

181.子线程发消息到主线程进行更新 UI，除了 handler 和 AsyncTask，还有什么？

182.子线程中能不能 new handler？为什么？

183.Handler、 Thread 和 HandlerThread 的差别

184.当Activity有多个Handler的时候，Message消 息是否会混乱？怎么样区分当前消息由哪个Handler 处理？

185.线程更新UI导致崩溃的原因？

186.ANR应用无响应

187.AsyncTask（异步任务）的工作原理 188.AsyncTask使用在哪些场景？它的缺陷是什么？ 如何解决？

189.Android中动画的类型：

190.理解Activity、View、Window三者之间的关系

191.Activity、Dialog、PopupWindow、Toast 与 Window的关系

192.Android中Context详解：

193.讲解一下Context

194.Android常用的数据存储方式（5种）

195.SharedPreference跨进程使用会怎么样？如何 保证跨进程使用安全？

196.数据库的操作类型有哪些，如何导入外部数据 库？

197.SQLite支持事务吗? 添加删除如何提高性能?

198.Android垃圾回收机制和程序优化System.gc( )

199.为什么图片需要用软引用，MVP模式中的view接 口用弱引用

200.Android平台的优势和不足

201.Android中任务栈的分配 202.Activity组件生命周期、四种启动模式

203.Activity的启动过程（不要回答生命周期）

204.保存Activity状态

205.如何修改 Activity 进入和退出动画

206.Service组件

207.什么是 IntentService？有何优点？

208.是否使用过 IntentService，作用是什么， AIDL 解决了什么问题？

209.BoradcastReceiver组件

210.配置文件静态注册和在代码中动态注册两种方式 的区别

211.ContentProvider(内容提供者)组件

212.Fragment中add与replace的区别？

213.FragmentPagerAdapter 与 与 FragmentStatePagerAdapter 的区别与使用场景？

214.Activity静态添加Fragment

215.Activity动态加载Fragment

216.Intent 217.ViewPager

218.关于Fragment中的控件的事件的监听

219.使用View绘制视图

220.View的绘制流程

221.View，ViewGroup事件分发

222.Android的事件传递（分发）机制

223.Android中touch事件的传递机制是怎样的?

224.View的分发机制，滑动冲突

225.Android中跨进程通讯的几种方式

226.Android 线程间通信有哪几种方式（重要）

227.AIDL理解

228.AIDL 的全称是什么?如何工作?能处理哪些类型 的数据？

229.什么是 AIDL？如何使用？

230.Android中页面的横屏与竖屏操作

231.横竖屏切换的Activity 生命周期变化？

232.获取手机中屏幕的宽和高的方法

233.内存泄漏的相关原因 234.Android内存泄漏及管理

235.Android平台的虚拟机Dalvik

236.Android中的Binder机制

237.Android中的缓存机制

238.Android 中图片的三级缓存策略

239.Glide三级缓存

240.HybridApp WebView和JS交互

241.RecyclerView和ListView的区别

242.简述一下RecyclerView缓存机制？

243.recyclerView嵌套卡顿解决如何解决

244.Universal-ImageLoader，Picasso，Fresco， Glide对比

245.Xutils, OKhttp, Volley, Retrofit对比

246.请解释下 Android 程序运行时权限与文件系统权 限的区别？

247.Framework 工作方式及原理，Activity 是如何 生成一个 view 的，机制是什么？

248.Android 判断SD卡是否存在

249.Android与服务器交互的方式中的对称加密和非 对称加密是什么? 250.SurfaceView和GLSurfaceView

251.说说JobScheduler

252.说说WorkManager

253.谈一谈startService和bindService的区别，生命 周期以及使用场景？

254.Service如何进行保活？

255.热修复的原理

256.JNI

257.谈谈对Android NDK的理解

258.Android设计模式之MVC

259.mvc/mvp/mvvm

260.设计模式的六大原则

261.Android中的性能优化相关问题

262.Bitmap的使用及内存优化 263.性能优化（非常重要）

264.Android对HashMap做了优化后推出的新的容器 类是什么？

264.谈谈你对安卓签名的理解

265.请解释安卓为啥要加签名机制?

266.权限管理系统（底层的权限是如何进行 grant 的）？

267.Kotlin 如何在 Android 上运行？

268.为什么要使用 Kotlin？

269.用var和val声明变量有什么区别？

270.用val和const声明变量有什么区别？

271.Kotlin 中如何保证 null 安全？

272.安全调用(?.)和空值检查(!!)有什么区别？

273.Kotlin 中是否有像 java 一样的三元运算符？

274.Kotlin 中的 Elvis 运算符是什么？

275.如何将 Kotlin 源文件转换为 Java 源文件？

276.你觉得Kotlin与Java混合开发时需要注意哪些问 题？

277.@JvmStatic、@JvmOverloads、@JvmFiled 在 Kotlin 中有什么用？ 278.Kotlin 中的数据类是什么？

279.Kotlin中的数据类型有隐式转换吗？为什么？

280.Kotlin中可以使用int、double、float等原始类型 吗？

281.Kotlin 中的字符串插值是什么？

282.Kotlin 中的解构是什么意思？

283.在Kotlin中，何为解构？该如何使用？

284.如何检查一个lateinit变量是否已经初始化？

285.Kotlin 中的 lateinit 和 lazy 有什么区别？

286.==操作符和===操作符有什么区别？

287.Kotlin 中的 forEach 是什么？

288.Kotlin 中的伴生对象是什么？

289.kotlin中Unit的应用以及和Java中void的区别？

290.Kotlin 中的 Java 静态方法等价物是什么？

291.Kotlin 中的 FlatMap 和 Map 有什么区别？

292.Kotlin中可以使用new关键字实例化一个类对象 吗？ 293.Kotlin 中的可见性修饰符是什么？

294.Kotlin中的可见性修饰符有哪些？相比于 Java 有什么区别？

295.如何在 Kotlin 中创建 Singleton 类？

296.Kotlin 中的初始化块是什么？

297.Kotlin 中的构造函数有哪些类型？

298.主构造函数和次构造函数之间有什么关系吗？

299.构造函数中使用的默认参数类型是什么？

300.谈谈kotlin中的构造方法？有哪些注意事项？

301.Kotlin 中的扩展函数是什么

302.kotlin基础： From Java To Kotlin

303.Kotlin 中什么时候使用 lateinit 关键字？

304.Kotlin 的延迟初始化: lateinit var 和 by lazy

305.Kotlin Tips:怎么用 Kotlin 去提高生产力 （kotlin优势）

306.Kotlin数组和集合

307.Kotlin中的MutableList与List有什么区别？

308.Kotlin集合操作符

309.Kotlin 中集合遍历有哪几种方式？ 310.说一下Kotlin的伴生对象(关键字companion)

311.Kotlin 顶层函数和属性

312.Kotlin 中的协程是什么？

313.Kotlin Coroutines 中的挂起函数是什么？

314.Kotlin Coroutines 中 Launch 和 Async 有什么 区别？

315.Kotlin Coroutines 中的作用域是什么？

316.Kotlin Coroutines 中的异常处理是如何完成 的？

317.在 Kotlin 中如何在 switch 和 when 之间进行选 择？

318.Kotlin 中的 open 关键字是做什么用的？

319.什么是 lambdas 表达式？

320.Kotlin 中的高阶函数是什么？

321.Kotlin 中的扩展函数是什么？

322.Kotlin 中的中缀函数是什么？

323.Kotlin 中的内联函数是什么？

324.Kotlin 中的 noinline 是什么？ 325.Kotlin 中的具体化类型是什么？

326.Kotlin 中的运算符重载是什么？

327.解释在 Kotlin 中 let、run、with 和 apply 的用 例。

328.kotlin中with、run、apply、let函数的区别？一 般用于什么场景？

329.Kotlin 中的 pair 和 Triple 是什么？

330.Kotlin 中的标签是什么？

331.使用密封类而不是枚举有什么好处？

332.协程是什么

333.kotlin中关键字data的理解？相对于普通的类有 哪些特点？

334.谈谈Kotlin中的Sequence，为什么它处理集合 操作更加高效？

335.说说 Kotlin中 的 Any 与Java中的 Object 有何 异同？





