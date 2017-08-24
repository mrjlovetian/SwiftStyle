

# Swift 编码风格指南

## 背景

本文主要是对以下几个编码规范的整理：

*   [The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
*   [Github Swift style guide](https://github.com/github/swift-style-guide)

对其中少数规范，我根据自己的习惯做了修改。

这里有些关于编码风格 Apple 官方文档，如果有些东西没有提及，可以在以下文档来查找更多细节：

*   [The Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
*   [The Swift Programming Language](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/index.html)
*   [Using Swift with Cocoa and Objective-C](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/BuildingCocoaApps/index.html)
*   [Swift Standard Library Reference](https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/SwiftStandardLibraryReference/index.html)

## 命名

使用驼峰命名法为 `类`、`方法`、`变量` 等取一个描述性强的命名。`类`、`结构体`、`枚举`、`协议` 这些类型名应该首字母大写，而 `方法`、`变量` 则应该首字母小写。

**推荐：**

<div class="language-swift highlighter-rouge">

```
private let maximumWidgetCount = 100

class WidgetContainer {
	var widgetButton: UIButton
	let widgetHeightPercentage = 0.85
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let MAX_WIDGET_COUNT = 100

class app_widgetContainer {
	var wBut: UIButton
	let wHeightPct = 0.85
}

```

</div>

一般情况下，应该避免使用缩略词。遵循 [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/#follow-case-conventions) 的规范，当你使用常见的缩略词时，应该保持它们的大小写一致性，要么所有字母都大写，要么所有字母都小写。比如：

**推荐：**


```
let urlString: URLString
let userID: UserID

```


**不推荐：**

<div class="language-swift highlighter-rouge">

```
let uRLString: UrlString
let userId: UserId

```

</div>

对于函数和构造器，除非上下文已经很清晰，最好为所有参数添加局部参数名。如果可以的话，最好也添加外部参数名来让函数调用语句更易读。

<div class="language-swift highlighter-rouge">

```
func dateFromString(dateString: String) -> NSDate
func convertPointAt(column column: Int, row: Int) -> CGPoint
func timedAction(afterDelay delay: NSTimeInterval, perform action: SKAction) -> SKAction!

// would be called like this:
dateFromString("2014-03-14")
convertPointAt(column: 42, row: 13)
timedAction(afterDelay: 1.0, perform: someOtherAction)

```

</div>

对于类中的方法，请遵循苹果惯例，将方法名作为第一个参数的外部名：

<div class="language-swift highlighter-rouge">

```
class Counter {
	func combineWith(otherCounter: Counter, options: Dictionary?) { ... }
	func incrementBy(amount: Int) { ... }
}

```

</div>

### 协议

遵循苹果的 API 设计规范，当协议是用来「描述一个东西是什么」时，协议名应该是一个名词，比如：`Collection`、`WidgetFactory`。当协议是用来「描述一种能力」时，协议名应该以 `-ing`、`-able` 或 `-ible` 结尾，比如：`Equatable`、`Resizing`。

### 枚举

遵循苹果的 API 设计规范对 Swift 3 的要求，使用首字母小写的驼峰命名法来给枚举值命名。

<div class="language-swift highlighter-rouge">

```
enum Shape {
	case rectangle
	case square
	case rightTriangle
	case equilateralTriangle
}

```

</div>

### 文字描述

在所有提及到函数的文字中（包括教程、书、评论），请从调用者的视角进行考虑，将所有的必要参数名都包含进来，比如：

> Call `convertPointAt(column:row:)` from your own `init` implementation.
> 
> If you call `dateFromString(_:)` make sure that you provide a string with the format “yyyy-MM-dd”.
> 
> If you call `timedAction(afterDelay:perform:)` from `viewDidLoad()` remember to provide an adjusted delay value and an action to perform.
> 
> You shouldn’t call the data source method `tableView(_:cellForRowAtIndexPath:)` directly.

### 类名前缀

Swift 的类型会被自动包含到它所在模块的命名空间中，所以没有必要再给 Swift 的类型添加类似 `RW` 这样的前缀了。如果两个不同模块的存在相同的名字，你可以通过在它们前面添加模块名来避免冲突。当然，你应该只在必要的时候才添加模块名前缀。

<div class="language-swift highlighter-rouge">

```
import SomeModule

let myClass = MyModule.UsefulClass()

```

</div>

### 选择器

不要再用字符串来指定选择器，而应该使用新的语法方式，更安全。通常，你应该使用上下文来缩短选择器表达式。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let sel = #selector(viewDidLoad)

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let sel = #selector(ViewController.viewDidLoad)

```

</div>

### 泛型

泛型名应该有较好的阅读性，用首字母大写的驼峰式命名。当一个类型没有有意义的关系和角色，使用传统的 `T`、`U`、`V` 来替代。

**推荐：**

<div class="language-swift highlighter-rouge">

```
struct Stack<Element> { ... }
func writeTo<Target: OutputStream>(inout target: Target)
func max<T: Comparable>(x: T, _ y: T) -> T

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
struct Stack<T> { ... }
func writeTo<target: OutputStream>(inout t: target)
func max<Thing: Comparable>(x: Thing, _ y: Thing) -> Thing

```

</div>

### 语言

使用美式英语，这样更契合苹果的 API。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let color = "red"

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let colour = "red"

```

</div>

## 代码结构

使用 `// MARK: -` 根据「代码功能类别」、「protocol/delegate 方法实现」等依据对代码进行分块组织。代码的组织顺序从整体上尽量遵循我们的认知顺序。

### 协议实现

其中，当你为一个类实现某些协议时，推荐添加一个独立的 `extension` 来实现具体的协议方法，这样可以让协议相关的代码聚合在一起，从而保持代码结构的清晰性，比如：

**推荐：**

<div class="language-swift highlighter-rouge">

```
class MyViewcontroller: UIViewController {
	// class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewcontroller: UITableViewDataSource {
	// table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewcontroller: UIScrollViewDelegate {
	// scroll view delegate methods
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
class MyViewcontroller: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
	// all methods
}

```

</div>

由于编译器不允许在派生类重复声明对协议的实现，所以并不要求总是复制基类的 extension 组。尤其当这个派生类是一个终端类，只有少量的方法需要重载时。何时保留 extension 组，这个应该由作者自己决定。

对于 UIKit 的 ViewControllers，可以考虑将 Lifecycle、Custom Accessors、IBAction 放在独立的 extension 中实现。

### 无用代码

无用的代码，包括 Xcode 代码模板提供的默认代码，以及占位的评论，都应该被删掉。除非你是在写教程需要读者来阅读你注释的代码。

**不推荐：**

<div class="language-swift highlighter-rouge">

```
override func didReceiveMemoryWarning() {
	super.didReceiveMemoryWarning()
	// Dispose of any resources that can be recreated.
}

override func numberOfSectionsInTableView(tableView: UITableView) -> Int {
	// #warning Incomplete implementation, return the number of sections
	return 1
}

override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
	// #warning Incomplete implementation, return the number of rows
	return Database.contacts.count
}

```

</div>

**推荐：**

<div class="language-swift highlighter-rouge">

```
override func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
	return Database.contacts.count
}

```

</div>

### 最小引用

只 import 你需要的模块。比如，如果引用 `Foundation` 以及足够，就不要再引用 `UIKit` 了。

## 空白

*   使用 Tab 而非空格。

*   方法的大括号以及其他的大括号（`if`/`else`/`switch`/`while` 等）总是与关联的程序语句在同一行打开，而在新起的一行结束。

**推荐：**

<div class="language-swift highlighter-rouge">

```
if user.isHappy {
	// Do something
} else {
	// Do something else
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
if user.isHappy
{
	// Do something
}
else {
	// Do something else
}

```

</div>

*   方法之间应该保留一行空格来使得代码结构组织更清晰。在方法中，可以用空行来隔开功能块，但是当一个方法中存在太多功能块时，那就意味着你可能需要重构这个大方法为多个小方法了。

*   冒号的左边总是不空格，右边空 1 格。除了在三元运算符 `? :` 和空字典 `[:]` 中。

**推荐：**

<div class="language-swift highlighter-rouge">

```
class TestDatabase: Database {
	var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
class TestDatabase : Database {
	var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}

```

</div>

## 注释

只在需要的时候添加注释来解释一段代码的意义，注释要么保持与对应的代码一起更新，要不然就删掉。

避免使用在代码中使用块注释，代码应该是自解释的。除非你的注释是用来生成文档的。

## 类和结构体

### 使用哪个

结构体是`值类型`，使用结构体来表示那些没有区别性的事物。一个包含 [a, b, c] 元素的数组和另一个包含 [a, b, c] 元素的数组是完全可替换的，你用第一个数组和用第二个数组没有任何区别，因为它们代表着同样的东西。所以数组是结构体。

类是`引用类型`，使用类来表示那些有区别性的事物。你用类来表示「人」这个概念，是因为两个「人」的实例是两个不一样的事情。两个「人」的实例就算拥有相同的姓名、生日，也不代表他们是一样的。但是「人」的生日数据应该用结构体表示，因为一个 1950-03-03 和另一个 1950-03-03 是一回事，日期这个概念没有区别性。

有时候，一些概念本应是用结构体，但是由于历史原因被实现为类了，比如 NSDate、NSSet。

### 类定义示例

以下是一个设计较好的类定义示例：

<div class="language-swift highlighter-rouge">

```
class Circle: Shape {
	var x: Int, y: Int
	var radius: Double
	var diameter: Double {
		get {
			return radius * 2
		}
		set {
			radius = newValue / 2
		}
	}

	init(x: Int, y: Int, radius: Double) {
		self.x = x
		self.y = y
		self.radius = radius
	}

	convenience init(x: Int, y: Int, diameter: Double) {
		self.init(x: x, y: y, radius: diameter / 2)
	}

	func describe() -> String {
		return "I am a circle at \(centerString()) with an area of \(computeArea())"
	}

	override func computeArea() -> Double {
		return M_PI * radius * radius
	}

	private func centerString() -> String {
		return "(\(x),\(y))"
	}
}

```

</div>

### 使用 Self

为了简洁，能不用 `self` 的地方就不用，因为 Swift 不需要用它来访问属性或调用方法。

Use `self` when required to differentiate between property names and arguments in initializers, and when referencing properties in closure expressions (as required by the compiler):

在下面情况中，你需要使用 `self`：

*   在构造器中，为了区别传入的参数和属性。
*   在闭包中访问属性，编译器要求用 `self`。

<div class="language-swift highlighter-rouge">

```
class BoardLocation {
	let row: Int, column: Int

	init(row: Int, column: Int) {
		self.row = row
		self.column = column

		let closure = {
			print(self.row)
		}
	}
}

```

</div>

### 计算属性

为了简洁，如果计算属性是只读的，那么就省略 `get`。只有当同时写了 `set` 语句时，才写 `get` 语句。

**推荐：**

<div class="language-swift highlighter-rouge">

```
var diameter: Double {
	return radius * 2
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
var diameter: Double {
	get {
		return radius * 2
	}
}

```

</div>

### Final

如果类不会被继承，那么将它设为 `final` 的。比如：

<div class="language-swift highlighter-rouge">

```
// Turn any generic type into a reference type using this Box class.
final class Box<T> {
	let value: T 
	init(_ value: T) {
		self.value = value
	}
}

```

</div>

## 函数声明

对于较短的函数声明，包括括号，在一行完成。

<div class="language-swift highlighter-rouge">

```
func reticulateSplines(spline: [Double]) -> Bool {
	// reticulate code goes here
}

```

</div>

对于较长的函数声明，在合适的地方换行，并在新起的一行加缩进。

<div class="language-swift highlighter-rouge">

```
func reticulateSplines(spline: [Double], adjustmentFactor: Double,
    translateConstant: Int, comment: String) -> Bool {
	// reticulate code goes here
}

```

</div>

## 闭包表达式

如果参数列表只有最后一个参数是闭包类型，则尽可能使用尾闭包语法。在所有情况下给闭包参数一个描述性强的命名。

**推荐：**

<div class="language-swift highlighter-rouge">

```
UIView.animateWithDuration(1.0) {
	self.myView.alpha = 0
}

UIView.animateWithDuration(1.0,
	animations: {
		self.myView.alpha = 0
	},
	completion: { finished in
		self.myView.removeFromSuperview()
	}
)

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
UIView.animateWithDuration(1.0, animations: {
	self.myView.alpha = 0
})

UIView.animateWithDuration(1.0,
	animations: {
		self.myView.alpha = 0
	}) { f in
		self.myView.removeFromSuperview()
}

```

</div>

对于上下文清晰的单表达式闭包，使用隐式的返回值：

<div class="language-swift highlighter-rouge">

```
attendeeList.sort { a, b in
	a > b
}

```

</div>

在链式方法调用中使用尾闭包语法时，需要确保上下文清晰可读。对于是否空行以及是否使用匿名参数等，则留给作者自行决定。例如：

<div class="language-swift highlighter-rouge">

```
let value = numbers.map { $0 * 2 }.filter { $0 % 3 == 0 }.indexOf(90)

let value = numbers
	.map {$0 * 2}
	.filter {$0 > 50}
	.map {$0 + 10}

```

</div>

## 类型

如果可以的话，总是优先使用 Swift 提供的原生类型。Swift 提供了对 Objective-C 的桥接，所以你可以使用所有需要的方法。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let width = 120.0 // Double
let widthString = (width as NSNumber).stringValue // String

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let width: NSNumber = 120.0 // NSNumber
let widthString: NSString = width.stringValue // NSString

```

</div>

在 Sprite Kit 代码中，使用 `CGFloat` 来避免过多的转换从而使代码更简练。

### 常量

用 `let` 关键字来定义常量，使用 `var` 关键字来定义变量。如果变量不需要被修改，则应该总是选择使用 `let`。

一个建议是：总是使用 `let` 除非编译器报警告诉你需要使用 `var`。

使用类型而非实例属性来定义常量。最好也别用全局常量，这样能更好区分常量和实例属性。如下：

**推荐：**

<div class="language-swift highlighter-rouge">

```
enum Math {
	static let e = 2.718281828459045235360287
	static let pi = 3.141592653589793238462643
}

radius * Math.pi * 2 // circumference

```

</div>

使用 case-less 枚举的优势在于它不会被意外初始化，而仅仅作为一个 namespace 来用。

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let e = 2.718281828459045235360287 // pollutes global namespace
let pi = 3.141592653589793238462643

radius * pi * 2 // is pi instance data or a global constant?

```

</div>

### 静态方法和静态类型属性

静态方法和静态类型属性与全局方法和全局变量类似，应该尽量少用。

### Optional

当一个变量或函数返回值可以为 nil 时，用 `?` 将其声明为 Optional 的。

对于在使用前一定会被初始化的实例变量，用 `!` 将其声明为隐式解包类型（Implicitly Unwrapped Types）。

在访问一个 Optional 值时，如果该值只被访问一次，或者之后需要连续访问多个 Optional 值，请使用链式 Optional 语法：

<div class="language-swift highlighter-rouge">

```
self.textContainer?.textLabel?.setNeedsDisplay()

```

</div>

对于需要将 Optional 值解开一次，多处使用的情况，使用 Optional 绑定更为方便：

<div class="language-swift highlighter-rouge">

```
if let textContainer = self.textContainer {
	// do many things with textContainer
}

```

</div>

不要使用类似 `optionalString`、`maybeView` 这种名字来命名 Optional 的变量或属性，因为这层意思以及明显的体现在他们的类型声明上了。

对于 Optional 绑定，推荐直接用同样的名字，不要用 `unwrappedView`、`actualLabel` 这种命名。

**推荐：**

<div class="language-swift highlighter-rouge">

```
var subview: UIView?
var volume: Double?

// later on...
if let subview = subview, volume = volume {
	// do something with unwrapped subview and volume
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
var optionalSubview: UIView?
var volume: Double?

if let unwrappedSubview = optionalSubview {
  if let realVolume = volume {
    // do something with unwrappedSubview and realVolume
  }
}

```

</div>

### 结构体构造器

使用 Swift 原生的结构体构造器。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let bounds = CGRect(x: 40, y: 20, width: 120, height: 80)
let centerPoint = CGPoint(x: 96, y: 42)

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let bounds = CGRectMake(40, 20, 120, 80)
let centerPoint = CGPointMake(96, 42)

```

</div>

推荐像 `CGRect.infinite`、`CGRect.null` 这样使用带命名空间约束的结构体常量，不推荐像 `CGRectInfinite`、`CGRectNull` 这样使用全局的结构体常量。对于已经存在的结构体类型变量，你可以使用类似 `.zero` 这样的缩写。

### 懒加载

使用懒加载机制来在对象的生命周期中实现更细粒度的内存和逻辑控制。尤其是 `UIViewController`，在加载其 views 时，尽量采用懒加载方式。可以使用 `<span class="p">{</span> <span class="w"></span> <span class="p">}</span><span class="err">()</span>` 这种闭包的方式或者私有工厂的方式来实现懒加载。比如：

<div class="language-swift highlighter-rouge">

```
lazy var locationManager: CLLocationManager = self.makeLocationManager()

private func makeLocationManager() -> CLLocationManager {
  let manager = CLLocationManager()
  manager.desiredAccuracy = kCLLocationAccuracyBest
  manager.delegate = self
  manager.requestAlwaysAuthorization()
  return manager
}

```

</div>

**注意：**

*   这里不需要 `[unowned self]`，因为这里没有引起循环引用。
*   CLLocationManager 有一个副作用，会唤起向用户申请权限的 UI 界面，所以在这里使用懒加载机制可以达到更细粒度的内存和逻辑控制。

### 类型推导

为了代码紧凑，推荐尽量使用 Swift 的类型推导。不过，对于 `CGFloat`、`Int16` 这种，推荐尽量指定明确的类型。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
let names = [String]()

```

</div>

**注意：** 遵循这条规范意味着选用一个描述性强的命名，比之前更重要了。

#### 类型标注

对于空的数组和字典，使用类型标注。

**推荐：**

<div class="language-swift highlighter-rouge">

```
var names: [String] = []
var lookup: [String: Int] = [:]

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
var names = [String]()
var lookup = [String: Int]()

```

</div>

### 语法糖

推荐使用简短的声明。

**推荐：**

<div class="language-swift highlighter-rouge">

```
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>

```

</div>

## 函数和方法

自由函数不属于任何一个类或类型，应该尽量少用。可以的话，尽量使用方法而非自由函数。这样可读性更好，也更易查找。

最适合使用自由函数的场景是这个函数功能与任何特定的类或类型都没有关联关系。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let sorted = items.mergeSort() // easily discoverable
rocket.launch() // clearly acts on the model

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let sorted = mergeSort(items) // hard to discover
launch(&rocket)

```

</div>

**自由函数示例**

<div class="language-swift highlighter-rouge">

```
let tuples = zip(a, b)  // feels natural as a free function (symmetry)
let value = max(x,y,z)  // another free function that feels natural

```

</div>

## 内存管理

在编码中应该避免循环引用。对于会产生循环应用的地方，使用 `weak` 和 `unowned` 来解决。此外，还可以使用类型（`struct`、`enum`）来避免循环引用。

### 延伸对象生命周期

可以通过 `[weak self]`、`guard let strongSelf = self else { return }` 来延伸对象的生命周期。

相对于 `[unowned self]`，这里更推荐使用 `[weak self]`。`[unowned self]` 在其作用的对象被释放后，会造成野指针，而 `[weak self]` 则会将对应的引用置为 nil。

相对于 Optional 拆包，更推荐明确的延长生命周期。

**推荐：**

<div class="language-swift highlighter-rouge">

```
resource.request().onComplete { [weak self] response in
	guard let strongSelf = self else { return }
	let model = strongSelf.updateModel(response)
	strongSelf.updateUI(model)
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
// might crash if self is released before response returns
resource.request().onComplete { [unowned self] response in
	let model = self.updateModel(response)
	self.updateUI(model)
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
// deallocate could happen between updating the model and updating UI
resource.request().onComplete { [weak self] response in
	let model = self?.updateModel(response)
	self?.updateUI(model)
}

```

</div>

## 访问控制

开发的访问级别不需要把 `public` 写出来，但对于 `private`，则最好写出。

除了 `static`、`@IBAction`、`@IBOutlet`，一般情况下，总是把访问控制修饰符 `private` 放在属性修饰符的第一位。

**推荐：**

<div class="language-swift highlighter-rouge">

```
class TimeMachine {  
	private dynamic lazy var fluxCapacitor = FluxCapacitor()
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
class TimeMachine {  
	lazy dynamic private var fluxCapacitor = FluxCapacitor()
}

```

</div>

## 控制流

相对于 `while-condition-increment`，更推荐使用 `for-in`。

**推荐：**

<div class="language-swift highlighter-rouge">

```
for _ in 0..<3 {
	print("Hello three times")
}

for (index, person) in attendeeList.enumerate() {
	print("\(person) is at position #\(index)")
}

for index in 0.stride(to: items.count, by: 2) {
	print(index)
}

for index in (0...3).reverse() {
	print(index)
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
var i = 0
while i < 3 {
	print("Hello three times")
	i += 1
}

var i = 0
while i < attendeeList.count {
	let person = attendeeList[i]
	print("\(person) is at position #\(i)")
	i += 1
}

```

</div>

## 黄金路径

尽早 return 或 break。当使用条件语句编写逻辑时，左手的代码应该是 「golden」 或 「happy」 路径。也就是说，不要嵌套多个 if 语句，即使写多个 return 语句也是 OK 的。`guard` 就是用来做这事的。

**推荐：**

<div class="language-swift highlighter-rouge">

```
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

	guard let context = context else { throw FFTError.noContext }
	guard let inputData = inputData else { throw FFTError.noInputData }

	// use context and input to compute the frequencies

	return frequencies
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

	if let context = context {
		if let inputData = inputData {
			// use context and input to compute the frequencies

			return frequencies
		}
		else {
			throw FFTError.noInputData
		}
	}
	else {
		throw FFTError.noContext
	}
}

```

</div>

当多个 Optional 使用 `guard` 或 `if let` 拆包，推荐最小化嵌套。比如：

**推荐：**

<div class="language-swift highlighter-rouge">

```
guard let number1 = number1, number2 = number2, number3 = number3 else { fatalError("impossible") }
// do something with numbers

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
if let number1 = number1 {
	if let number2 = number2 {
		if let number3 = number3 {
			// do something with numbers
		}
		else {
			fatalError("impossible")
		}
	}
	else {
		fatalError("impossible")
	}
}
else {
	fatalError("impossible")
}

```

</div>

### 失败的 Guard

`guard` 语句一般都需要以某种方式退出执行。一般来说使用 `return`、`throw`、`break`、`continue`、`fatalError()` 即可。应该避免在退出时写大段的代码，如果确实需要在不同的退出点上编写退出清理逻辑，可以考虑使用 `defer` 来避免重复。

## 分号

Swift 不需要在一行代码结束时使用分号。只有当你想把多行代码放在一行写时，才需要用分号隔开它们，但是一般不推荐这样做。只有在使用 `for-conditional-increment` 时用到分号是例外，当然我们更推荐使用 `for-in`。

**推荐：**

<div class="language-swift highlighter-rouge">

```
let swift = "not a scripting language"

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
let swift = "not a scripting language";

```

</div>

## 圆括号

条件判断语句外的圆括号不是必须的，推荐省略它们。

**推荐：**

<div class="language-swift highlighter-rouge">

```
if name == "Hello" {
	print("World")
}

```

</div>

**不推荐：**

<div class="language-swift highlighter-rouge">

```
if (name == "Hello") {
	print("World")
}

```

</div>


