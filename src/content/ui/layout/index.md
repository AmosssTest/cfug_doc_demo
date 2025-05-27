---
# title: Layouts in Flutter
title: Flutter 中的布局
# short-title: Layout
short-title: 布局
# description: >-
#   Learn how Flutter's layout mechanism works and how to build your app's layout.
description: 了解 Flutter 的布局机制如何工作，以及如何构建你的 App 布局。
---

:::note
本篇文档由 AI 翻译。
:::

{% assign api = site.api | append: '/flutter' -%}
{% capture examples -%} {{site.repo.this}}/tree/{{site.branch}}/examples {%- endcapture -%}

<?code-excerpt path-base=""?>

## Overview

## 概览

<!-- :::secondary What's the point? -->
:::secondary 要点是什么？

* Layouts in Flutter are built with widgets.

  Flutter 中的布局是使用 widget 构建的。

* Widgets are classes used to build UIs.

  Widget 是用于构建 UI 的类。

* Widgets are also used to build UI elements.

  Widget 也用于构建 UI 元素。

* Compose simple widgets to build complex widgets.

  组合简单的 widget 以构建复杂的 widget。

:::

The core of Flutter's layout mechanism is widgets.
In Flutter, almost everything is a widget&mdash;even
layout models are widgets. The images, icons,
and text that you see in a Flutter app are all widgets.
But things you don't see are also widgets,
such as the rows, columns, and grids that arrange,
constrain, and align the visible widgets.
You create a layout by composing widgets to build more
complex widgets.

Flutter 布局机制的核心是 widget。
在 Flutter 中，几乎所有东西都是 widget——甚至
布局模型也是 widget。你在 Flutter App 中看到的图像、图标
和文本都是 widget。但你没看到的东西也是 widget，
例如排列、约束和对齐可见 widget 的行、列和网格。
你可以通过组合 widget 来创建布局，以构建更复杂的 widget。

## Conceptual example

## 概念示例

In the following example, the first screenshot displays
three icons with labels and the second screenshot includes
the visual layout for rows and columns. In the second
screenshot, `debugPaintSizeEnabled` is set to `true` so you
can see the visual layout.

在以下示例中，第一张屏幕截图显示了三个带有标签的图标，
第二张屏幕截图包括行和列的可视化布局。在第二张
屏幕截图中，`debugPaintSizeEnabled` 设置为 `true`，因此你
可以看到可视化布局。

<div class="side-by-side">
  <div class="centered-rows">
    <img src='/assets/images/docs/ui/layout/lakes-icons.png' alt="Sample layout">
  </div>
  <div class="centered-rows">
    <img src='/assets/images/docs/ui/layout/lakes-icons-visual.png' alt="Sample layout with visual debugging">
  </div>
</div>

Here's a diagram of the widget tree for the previous
example:

这是前一个示例的 widget 树的图示：

<img src='/assets/images/docs/ui/layout/sample-flutter-layout.png' class="text-center diagram-wrap" alt="Node tree">

Most of this should look as you might expect, but you might be wondering
about the containers (shown in pink). [`Container`][] is a widget class
that allows you to customize its child widget. Use a `Container` when
you want to add padding, margins, borders, or background color,
to name some of its capabilities.

大多数内容应该看起来和你预期的一样，但你可能想知道
容器（显示为粉红色）的信息。[`Container`][] 是一个 widget 类，
允许你自定义其子 widget。当你想要添加填充、边距、边框或背景颜色时，
可以使用 `Container`，这只是它的一些功能。

Each [`Text`][] widget is placed in a `Container`
to add margins. The entire [`Row`][] is also placed in a
`Container` to add padding around the row.

每个 [`Text`][] widget 都放置在 `Container` 中
以添加边距。整个 [`Row`][] 也放置在
`Container` 中，以在行周围添加填充。

The rest of the UI is controlled by properties.
Set an [`Icon`][]'s color using its `color` property.
Use the `Text.style` property to set the font, its color, weight, and so on.
Columns and rows have properties that allow you to specify how their
children are aligned vertically or horizontally, and how much space
the children should occupy.

UI 的其余部分由属性控制。
使用 [`Icon`][] 的 `color` 属性设置其颜色。
使用 `Text.style` 属性设置字体、其颜色、粗细等。
列和行具有允许你指定其子项如何垂直或水平对齐，
以及子项应占用多少空间的属性。

:::note

Most of the screenshots in this tutorial are displayed with
`debugPaintSizeEnabled` set to `true` so you can see the
visual layout. For more information, see
[Debugging layout issues visually][].

本教程中的大多数屏幕截图都以
`debugPaintSizeEnabled` 设置为 `true` 的方式显示，因此你可以看到
可视化布局。有关更多信息，请参见
[以可视化方式调试布局问题][Debugging layout issues visually]。

:::

[`Container`]: {{api}}/widgets/Container-class.html
[Debugging layout issues visually]: /tools/devtools/inspector#debugging-layout-issues-visually
[`Icon`]: {{api}}/material/Icons-class.html
[`Row`]: {{api}}/widgets/Row-class.html
[`Text`]: {{api}}/widgets/Text-class.html

## Lay out a widget

## 布局一个 widget

How do you lay out a single widget in Flutter? This section
shows you how to create and display a simple widget.
It also shows the entire code for a simple Hello World app.

如何在 Flutter 中布局单个 widget？本节
向你展示如何创建和显示一个简单的 widget。
它还展示了一个简单的 Hello World App 的完整代码。

In Flutter, it takes only a few steps to put text, an icon,
or an image on the screen.

在 Flutter 中，只需几个步骤即可将文本、图标
或图像放在屏幕上。

### 1. Select a layout widget

### 1. 选择一个布局 widget

Choose from a variety of [layout widgets][] based
on how you want to align or constrain a visible widget,
as these characteristics are typically passed on to the
contained widget.

根据你想要如何对齐或约束可见 widget，
从各种 [布局 widget][layout widgets] 中进行选择，
因为这些特征通常会传递给包含的 widget。

For example, you could use the
[`Center`][] layout widget to center a visible widget
horizontally and vertically:

例如，你可以使用 [`Center`][] 布局 widget
水平和垂直居中一个可见 widget：

```dart
Center(
  // Content to be centered here.
)
```

[`Center`]: {{api}}/widgets/Center-class.html
[layout widgets]: /ui/widgets/layout

### 2. Create a visible widget

### 2. 创建一个可见 widget

Choose a [visible widget][] for your app to contain
visible elements, such as [text][], [images][], or
[icons][].

为你的 App 选择一个 [可见 widget][visible widget]，以包含
可见元素，例如 [文本][text]、[图像][images] 或
[图标][icons]。

For example, you could use the [`Text`][] widget display
some text:

例如，你可以使用 [`Text`][] widget 显示
一些文本：

```dart
Text('Hello World')
```

[icons]: {{api}}/material/Icons-class.html
[images]: {{api}}/widgets/Image-class.html
[text]: {{api}}/widgets/Text-class.html
[`Text`]: {{api}}/widgets/Text-class.html
[visible widget]: /ui/widgets

### 3. Add the visible widget to the layout widget

### 3. 将可见 widget 添加到布局 widget

<?code-excerpt path-base="layout/base"?>

All layout widgets have either of the following:

所有布局 widget 都具有以下任一项：

* A `child` property if they take a single child&mdash;for example,
  `Center` or `Container`

  一个 `child` 属性，如果它们采用单个子项——例如，
  `Center` 或 `Container`

* A `children` property if they take a list of widgets&mdash;for example,
  `Row`, `Column`, `ListView`, or `Stack`.

  一个 `children` 属性，如果它们采用 widget 列表——例如，
  `Row`、`Column`、`ListView` 或 `Stack`。

Add the `Text` widget to the `Center` widget:

将 `Text` widget 添加到 `Center` widget：

<?code-excerpt "lib/main.dart (centered-text)" replace="/body: //g"?>
```dart
const Center(
  child: Text('Hello World'),
),
```

### 4. Add the layout widget to the page

### 4. 将布局 widget 添加到页面

A Flutter app is itself a widget, and most widgets have a [`build()`][]
method. Instantiating and returning a widget in the app's `build()` method
displays the widget.

Flutter App 本身就是一个 widget，并且大多数 widget 都有一个 [`build()`][] 方法。
在 App 的 `build()` 方法中实例化并返回一个 widget 将显示该 widget。

<a id="non-material-apps" aria-hidden="true"></a>
<a id="material-apps" aria-hidden="true"></a>
<a id="cupertino-apps" aria-hidden="true"></a>

{% tabs "app-type-tabs", true %}

<!-- {% tab "Standard apps" %} -->
{% tab "标准 App" %}

For a general app, you can add the `Container` widget to
the app's `build()` method:

对于通用 App，你可以将 `Container` widget 添加到
App 的 `build()` 方法中：

<?code-excerpt path-base="layout/non_material"?>
<?code-excerpt "lib/main.dart (my-app)"?>
```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return Container(
      decoration: const BoxDecoration(color: Colors.white),
      child: const Center(
        child: Text(
          'Hello World',
          textDirection: TextDirection.ltr,
          style: TextStyle(fontSize: 32, color: Colors.black87),
        ),
      ),
    );
  }
}
```

By default, a general app doesn't include an `AppBar`,
title, or background color. If you want these features in a
general app, you have to build them yourself. This app
changes the background color to white and the text to
dark grey to mimic a Material app.

默认情况下，通用 App 不包括 `AppBar`、
标题或背景颜色。如果你希望在通用 App 中使用这些功能，
则必须自己构建它们。此 App
将背景颜色更改为白色，并将文本更改为
深灰色以模仿 Material App。

{% endtab %}

<!-- {% tab "Material apps" %} -->
{% tab "Material App" %}

For a `Material` app, you can use a [`Scaffold`][] widget;
it provides a default banner, background color,
and has API for adding drawers, snack bars, and bottom sheets.
Then you can add the `Center` widget directly to the `body`
property for the home page.

对于 `Material` App，你可以使用 [`Scaffold`][] widget；
它提供了一个默认的横幅、背景颜色，
并且具有用于添加抽屉、SnackBar 和底部sheet 的 API。
然后，你可以将 `Center` widget 直接添加到主页的 `body` 属性中。

<?code-excerpt path-base="layout/base"?>
<?code-excerpt "lib/main.dart (my-app)"?>
```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    const String appTitle = 'Flutter layout demo';
    return MaterialApp(
      title: appTitle,
      home: Scaffold(
        appBar: AppBar(title: const Text(appTitle)),
        body: const Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

:::note

The [Material library][] implements widgets that follow [Material
Design][] principles. When designing your UI, you can exclusively use
widgets from the standard [widgets library][], or you can use
widgets from the Material library. You can mix widgets from both
libraries, you can customize existing widgets,
or you can build your own set of custom widgets.

[Material 库][Material library] 实现了遵循 [Material
设计][Material Design] 原则的 widget。在设计 UI 时，你可以专门使用
标准 [widget 库][widgets library] 中的 widget，或者你可以使用
Material 库中的 widget。你可以混合使用来自两个
库的 widget，你可以自定义现有 widget，
或者你可以构建自己的一组自定义 widget。

:::

{% endtab %}

<!-- {% tab "Cupertino apps" %} -->
{% tab "Cupertino App" %}

To create a `Cupertino` app,
use the `CupertinoApp` and [`CupertinoPageScaffold`][] widgets.

要创建一个 `Cupertino` App，
请使用 `CupertinoApp` 和 [`CupertinoPageScaffold`][] widget。

Unlike `Material`, it doesn't provide a default banner or background color.
You need to set these yourself.

与 `Material` 不同，它不提供默认的横幅或背景颜色。
你需要自己设置这些。

* To set default colors, pass in a configured [`CupertinoThemeData`][]
  to your app's `theme` property.

  要设置默认颜色，请将配置好的 [`CupertinoThemeData`][] 传递到
  App 的 `theme` 属性。

* To add an iOS-styled navigation bar to the top of your app, add a
  [`CupertinoNavigationBar`][] widget to the `navigationBar`
  property of your scaffold.
  You can use the colors that [`CupertinoColors`][] provides to
  configure your widgets to match iOS design.

  要将 iOS 样式的导航栏添加到 App 的顶部，请将
  [`CupertinoNavigationBar`][] widget 添加到 scaffold 的 `navigationBar`
  属性。
  你可以使用 [`CupertinoColors`][] 提供的颜色来
  配置你的 widget 以匹配 iOS 设计。

* To lay out the body of your app, set the `child` property of your scaffold
  with the desired widget as its value, like `Center` or `Column`.

  要布局 App 的主体，请使用所需的 widget（如 `Center` 或 `Column`）
  将 scaffold 的 `child` 属性设置为其值。

To learn what other UI components you can add, check out the
[Cupertino library][].

要了解你可以添加哪些其他 UI 组件，请查看
[Cupertino 库][Cupertino library]。

<?code-excerpt "lib/cupertino.dart (my-app)"?>
```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const CupertinoApp(
      title: 'Flutter layout demo',
      theme: CupertinoThemeData(
        brightness: Brightness.light,
        primaryColor: CupertinoColors.systemBlue,
      ),
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          backgroundColor: CupertinoColors.systemGrey,
          middle: Text('Flutter layout demo'),
        ),
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [Text('Hello World')],
          ),
        ),
      ),
    );
  }
}
```

:::note

The [Cupertino library][] implements widgets that follow
[Apple's Human Interface Guidelines for iOS][].
When designing your UI, you can use
widgets from the standard [widgets library][] or the Cupertino library.
You can mix widgets from both libraries, you can customize existing widgets,
or you can build your own set of custom widgets.

[Cupertino 库][Cupertino library] 实现了遵循
[Apple 的 iOS 人机界面指南][Apple's Human Interface Guidelines for iOS] 的 widget。
在设计 UI 时，你可以使用标准 [widget 库][widgets library] 或 Cupertino 库中的 widget。
你可以混合使用来自两个库的 widget，你可以自定义现有 widget，
或者你可以构建自己的一组自定义 widget。

:::

{% endtab %}

{% endtabs %}

[`CupertinoColors`]: {{api}}/cupertino/CupertinoColors-class.html
[`CupertinoPageScaffold`]: {{api}}/cupertino/CupertinoPageScaffold-class.html
[`CupertinoThemeData`]: {{api}}/cupertino/CupertinoThemeData-class.html
[`CupertinoNavigationBar`]: {{api}}/cupertino/CupertinoNavigationBar-class.html
[Cupertino library]: {{api}}/cupertino/cupertino-library.html
[Apple's Human Interface Guidelines for iOS]: {{site.apple-dev}}/design/human-interface-guidelines/designing-for-ios
[`build()`]: {{api}}/widgets/StatelessWidget/build.html
[Material library]: {{api}}/material/material-library.html
[`Scaffold`]: {{api}}/material/Scaffold-class.html
[widgets library]: {{api}}/widgets/widgets-library.html

### 5. Run your app

### 5. 运行你的 App

<div class="side-by-side">
<div>

After you've added your widgets, run your app. When you run
the app, you should see _Hello World_.

添加 widget 后，运行你的 App。当你运行
App 时，你应该会看到 _Hello World_。

App source code:

App 源代码：

* [Material app]({{examples}}/layout/base)

  [Material App]({{examples}}/layout/base)

* [Non-Material app]({{examples}}/layout/non_material)

  [非 Material App]({{examples}}/layout/non_material)

</div>
{% render docs/app-figure.md, image:"ui/layout/hello-world.png", alt:"Screenshot of app displaying Hello World", img-style:"max-height: 400px;"  %}
</div>
<hr>

## Lay out multiple widgets vertically and horizontally

## 垂直和水平布局多个 widget

<?code-excerpt path-base=""?>

One of the most common layout patterns is to arrange
widgets vertically or horizontally. You can use a
`Row` widget to arrange widgets horizontally,
and a `Column` widget to arrange widgets vertically.

最常见的布局模式之一是垂直或水平排列
widget。你可以使用 `Row` widget 水平排列 widget，
并使用 `Column` widget 垂直排列 widget。

<!-- :::secondary What's the point? -->
:::secondary 要点是什么？

* `Row` and `Column` are two of the most commonly used layout patterns.

  `Row` 和 `Column` 是最常用的两种布局模式。

* `Row` and `Column` each take a list of child widgets.

  `Row` 和 `Column` 各自采用一个子 widget 列表。

* A child widget can itself be a `Row`, `Column`,
    or other complex widget.

  子 widget 本身可以是 `Row`、`Column`
  或其他复杂 widget。

* You can specify how a `Row` or `Column` aligns its children,
    both vertically and horizontally.

  你可以指定 `Row` 或 `Column` 如何对齐其子项，
  包括垂直和水平方向。

* You can stretch or constrain specific child widgets.

  你可以拉伸或约束特定的子 widget。

* You can specify how child widgets use the `Row`'s or
    `Column`'s available space.

  你可以指定子 widget 如何使用 `Row` 或
  `Column` 的可用空间。

:::

To create a row or column in Flutter, you add a list of children
widgets to a [`Row`][] or [`Column`][] widget. In turn,
each child can itself be a row or column, and so on.
The following example shows how it is possible to nest rows or
columns inside of rows or columns.

要在 Flutter 中创建行或列，你可以将子
widget 列表添加到 [`Row`][] 或 [`Column`][] widget。反过来，
每个子项本身可以是行或列，依此类推。
以下示例展示了如何在行或列内部嵌套行或列。

This layout is organized as a `Row`. The row contains two children:
a column on the left, and an image on the right:

此布局组织为 `Row`。该行包含两个子项：
左侧的一列和右侧的图像：

<img src='/assets/images/docs/ui/layout/pavlova-diagram.png' class="diagram-wrap" alt="Screenshot with callouts showing the row containing two children">

The left column's widget tree nests rows and columns.

左侧列的 widget 树嵌套了行和列。

<img src='/assets/images/docs/ui/layout/pavlova-left-column-diagram.png' class="diagram-wrap" alt="Diagram showing a left column broken down to its sub-rows and sub-columns">

You'll implement some of Pavlova's layout code in
[Nesting rows and columns](#nesting-rows-and-columns).

你将在 [嵌套行和列](#nesting-rows-and-columns) 中实现 Pavlova 的一些布局代码。

:::note

`Row` and `Column` are basic primitive widgets for horizontal
and vertical layouts&mdash;these low-level widgets allow for maximum
customization. Flutter also offers specialized, higher-level widgets
that might be sufficient for your needs. For example,
instead of `Row` you might prefer [`ListTile`][],
an easy-to-use widget with properties for leading and trailing icons,
and up to 3 lines of text.  Instead of Column, you might prefer
[`ListView`][], a column-like layout that automatically scrolls
if its content is too long to fit the available space.
For more information, see [Common layout widgets][].

`Row` 和 `Column` 是用于水平和垂直布局的基本原始 widget——这些底层 widget 允许最大限度的自定义。Flutter 还提供了专门的、更高级别的 widget，这些 widget 可能足以满足你的需求。例如，
你可以选择使用 [`ListTile`][] 而不是 `Row`，
这是一个易于使用的 widget，具有用于前置和后置图标以及最多 3 行文本的属性。你可以选择使用 [`ListView`][] 而不是 Column，
这是一个类似列的布局，如果其内容太长而无法适应可用空间，则会自动滚动。
有关更多信息，请参见 [常用布局 widget][Common layout widgets]。

:::

[Common layout widgets]: #common-layout-widgets
[`Column`]: {{api}}/widgets/Column-class.html
[`ListTile`]: {{api}}/material/ListTile-class.html
[`ListView`]: {{api}}/widgets/ListView-class.html
[`Row`]: {{api}}/widgets/Row-class.html

### Aligning widgets

### 对齐 widget

You control how a row or column aligns its children using the
`mainAxisAlignment` and `crossAxisAlignment` properties.
For a row, the main axis runs horizontally and the cross axis runs
vertically. For a column, the main axis runs vertically and the cross
axis runs horizontally.

你可以使用 `mainAxisAlignment` 和 `crossAxisAlignment` 属性控制行或列如何对齐其子项。
对于行，主轴水平运行，横轴垂直运行。对于列，主轴垂直运行，横轴水平运行。

<div class="side-by-side">
  <div class="centered-rows">
    <img src='/assets/images/docs/ui/layout/row-diagram.png' class="diagram-wrap" alt="Diagram showing the main axis and cross axis for a row">
  </div>
  <div class="centered-rows">
    <img src='/assets/images/docs/ui/layout/column-diagram.png' class="diagram-wrap" alt="Diagram showing the main axis and cross axis for a column">
  </div>
</div>

The [`MainAxisAlignment`][] and [`CrossAxisAlignment`][]
enums offer a variety of constants for controlling alignment.

[`MainAxisAlignment`][] 和 [`CrossAxisAlignment`][] 枚举提供了各种用于控制对齐方式的常量。

:::note

When you add images to your project,
you need to update the `pubspec.yaml` file to access
them&mdash;this example uses `Image.asset` to display
the images.  For more information, see this example's
[`pubspec.yaml` file][] or [Adding assets and images][].
You don't need to do this if you're referencing online
images using `Image.network`.

当你将图像添加到你的项目时，
你需要更新 `pubspec.yaml` 文件才能访问
它们——此示例使用 `Image.asset` 来显示
图像。有关更多信息，请参见此示例的
[`pubspec.yaml` file][] 或 [添加资源和图像][Adding assets and images]。
如果你使用 `Image.network` 引用在线图像，则无需执行此操作。

:::

In the following example, each of the 3 images is 100 pixels wide.
The render box (in this case, the entire screen)
is more than 300 pixels wide, so setting the main axis
alignment to `spaceEvenly` divides the free horizontal
space evenly between, before, and after each image.

在以下示例中，3 个图像中的每一个都是 100 像素宽。
渲染框（在本例中为整个屏幕）
的宽度超过 300 像素，因此将主轴
对齐方式设置为 `spaceEvenly` 会平均分配每个图像之间、之前和之后的可用水平空间。

<div class="code-and-content">
<div>

<?code-excerpt "layout/row_column/lib/main.dart (row)" replace="/Row/[!$&!]/g"?>
```dart
[!Row!](
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    Image.asset('images/pic1.jpg'),
    Image.asset('images/pic2.jpg'),
    Image.asset('images/pic3.jpg'),
  ],
);
```

</div>
<div>
  <img src='/assets/images/docs/ui/layout/row-spaceevenly-visual.png' class="small-diagram-wrap" alt="Row with 3 evenly spaced images">

  **App source:** [row_column]({{examples}}/layout/row_column)

  **App 源代码：** [row_column]({{examples}}/layout/row_column)

</div>
</div>

Columns work the same way as rows. The following example shows a column
of 3 images, each is 100 pixels high. The height of the render box
(in this case, the entire screen) is more than 300 pixels, so
setting the main axis alignment to `spaceEvenly` divides the free vertical
space evenly between, above, and below each image.

列的工作方式与行相同。以下示例显示了 3 个图像的列，每个图像高 100 像素。渲染框的
高度（在本例中为整个屏幕）超过 300 像素，因此
将主轴对齐方式设置为 `spaceEvenly` 会平均分配每个图像之间、上方和下方的可用垂直空间。

<div class="code-and-content">
<div>

  <?code-excerpt "layout/row_column/lib/main.dart (column)" replace="/Column/[!$&!]/g"?>
  ```dart
  [!Column!](
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: [
      Image.asset('images/pic1.jpg'),
      Image.asset('images/pic2.jpg'),
      Image.asset('images/pic3.jpg'),
    ],
  );
  ```

</div>
<div class="text-center">
  <img src='/assets/images/docs/ui/layout/column-visual.png' height="250px" class="small-diagram-wrap" alt="Column showing 3 images spaced evenly">

  **App source:** [row_column]({{examples}}/layout/row_column)

  **App 源代码：** [row_column]({{examples}}/layout/row_column)

</div>
</div>

[`CrossAxisAlignment`]: {{api}}/rendering/CrossAxisAlignment.html
[`MainAxisAlignment`]: {{api}}/rendering/MainAxisAlignment.html
[`pubspec.yaml` file]: {{examples}}/layout/row_column/pubspec.yaml

### Sizing widgets

### 调整 widget 大小

When a layout is too large to fit a device, a yellow
and black striped pattern appears along the affected edge.
Here is an [example][sizing] of a row that is too wide:

当布局太大而无法适应设备时，受影响的边缘会出现黄色
和黑色条纹图案。这是一个行太宽的 [示例][sizing]：

<img src='/assets/images/docs/ui/layout/layout-too-large.png' class="text-center" style="max-height: 15rem;" alt="Overly-wide row">

Widgets can be sized to fit within a row or column by using the
[`Expanded`][] widget. To fix the previous example where the
row of images is too wide for its render box,
wrap each image with an `Expanded` widget.

可以使用 [`Expanded`][] widget 调整 widget 的大小以适应行或列。
要修复前面的示例，其中图像行对于其渲染框来说太宽，
请使用 `Expanded` widget 包装每个图像。

<div class="code-and-content">
<div>

  <?code-excerpt "layout/sizing/lib/main.dart (expanded-images)" replace="/Expanded/[!$&!]/g"?>
  ```dart
  Row(
    crossAxisAlignment: CrossAxisAlignment.center,
    children: [
      [!Expanded!](child: Image.asset('images/pic1.jpg')),
      [!Expanded!](child: Image.asset('images/pic2.jpg')),
      [!Expanded!](child: Image.asset('images/pic3.jpg')),
    ],
  );
  ```

</div>
<div>
  <img src='/assets/images/docs/ui/layout/row-expanded-2-visual.png' class="small-diagram-wrap" alt="Row of 3 images that are too wide, but each is constrained to take only 1/3 of the space">

  **App source:** [sizing]({{examples}}/layout/sizing)

  **App 源代码：** [sizing]({{examples}}/layout/sizing)

</div>
</div>

Perhaps you want a widget to occupy twice as much space as its
siblings. For this, use the `Expanded` widget `flex` property,
an integer that determines the flex factor for a widget.
The default flex factor is 1. The following code sets
the flex factor of the middle image to 2:

也许你希望一个 widget 占用的空间是其同级 widget 的两倍。为此，请使用 `Expanded` widget 的 `flex` 属性，
这是一个整数，用于确定 widget 的 flex 因子。
默认的 flex 因子为 1。以下代码将中间图像的 flex 因子设置为 2：

<div class="code-and-content">
<div>

  <?code-excerpt "layout/sizing/lib/main.dart (expanded-images-with-flex)" replace="/flex.*/[!$&!]/g"?>
  ```dart
  Row(
    crossAxisAlignment: CrossAxisAlignment.center,
    children: [
      Expanded(child: Image.asset('images/pic1.jpg')),
      Expanded([!flex: 2, child: Image.asset('images/pic2.jpg')),!]
      Expanded(child: Image.asset('images/pic3.jpg')),
    ],
  );
  ```

</div>
<div>
  <img src='/assets/images/docs/ui/layout/row-expanded-visual.png' class="small-diagram-wrap" alt="Row of 3 images with the middle image twice as wide as the others">

  **App source:** [sizing]({{examples}}/layout/sizing)

  **App 源代码：** [sizing]({{examples}}/layout/sizing)

</div>
</div>

[`Expanded`]: {{api}}/widgets/Expanded-class.html
[sizing]: {{examples}}/layout/sizing

### Packing widgets

### 打包 widget

By default, a row or column occupies as much space along its main axis
as possible, but if you want to pack the children closely together,
set its `mainAxisSize` to `MainAxisSize.min`. The following example
uses this property to pack the star icons together.

默认情况下，行或列会沿其主轴占用尽可能多的空间，但如果你想将子项紧密地打包在一起，
请将其 `mainAxisSize` 设置为 `MainAxisSize.min`。以下示例
使用此属性将星形图标打包在一起。

<div class="code-and-content">
<div>

  <?code-excerpt "layout/pavlova/lib/main.dart (stars)" replace="/mainAxisSize.*/[!$&!]/g; /\w+ \w+ = //g; /;//g"?>
  ```dart
  Row(
    [!mainAxisSize: MainAxisSize.min,!]
    children: [
      Icon(Icons.star, color: Colors.green[500]),
      Icon(Icons.star, color: Colors.green[500]),
      Icon(Icons.star, color: Colors.green[500]),
      const Icon(Icons.star, color: Colors.black),
      const Icon(Icons.star, color: Colors.black),
    ],
  )
  ```

</div>
<div>
  <img src='/assets/images/docs/ui/layout/packed.png' class="small-diagram-wrap" alt="Row of 5 stars, packed together in the middle of the row">

  **App source:** [pavlova]({{examples}}/layout/pavlova)

  **App 源代码：** [pavlova]({{examples}}/layout/pavlova)

</div>
</div>

### Nesting rows and columns

### 嵌套行和列

The layout framework allows you to nest rows and columns
inside of rows and columns as deeply as you need.
Let's look at the code for the outlined
section of the following layout:

布局框架允许你根据需要在行和列内部嵌套行和列。
让我们看一下以下布局的轮廓
部分的代码：

<img src='/assets/images/docs/ui/layout/pavlova-large-annotated.png' class="border text-center" alt="Screenshot of the pavlova app, with the ratings and icon rows outlined in red">

The outlined section is implemented as two rows. The ratings row contains
five stars and the number of reviews. The icons row contains three
columns of icons and text.

轮廓部分实现为两行。评分行包含
五个星形和评论数。图标行包含三个
图标和文本列。

The widget tree for the ratings row:

评分行的 widget 树：

<img src='/assets/images/docs/ui/layout/widget-tree-pavlova-rating-row.png' class="text-center diagram-wrap" alt="Ratings row widget tree">

The `ratings` variable creates a row containing a smaller row
of 5-star icons, and text:

`ratings` 变量创建一个行，其中包含一个较小的 5 星图标行和文本：

<?code-excerpt "layout/pavlova/lib/main.dart (ratings)" replace="/ratings/[!$&!]/g"?>
```dart
final stars = Row(
  mainAxisSize: MainAxisSize.min,
  children: [
    Icon(Icons.star, color: Colors.green[500]),
    Icon(Icons.star, color: Colors.green[500]),
    Icon(Icons.star, color: Colors.green[500]),
    const Icon(Icons.star, color: Colors.black),
    const Icon(Icons.star, color: Colors.black),
  ],
);

final [!ratings!] = Container(
  padding: const EdgeInsets.all(20),
  child: Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: [
      stars,
      const Text(
        '170 Reviews',
        style: TextStyle(
          color: Colors.black,
          fontWeight: FontWeight.w800,
          fontFamily: 'Roboto',
          letterSpacing: 0.5,
          fontSize: 20,
        ),
      ),
    ],
  ),
);
```

:::tip

To minimize the visual confusion that can result from
heavily nested layout code, implement pieces of the UI
in variables and functions.

为了最大限度地减少因大量嵌套布局代码而可能造成的视觉混乱，请在变量和函数中实现 UI 的各个部分。

:::

The icons row, below the ratings row, contains 3 columns;
each column contains an icon and two lines of text,
as you can see in its widget tree:

评分行下方的图标行包含 3 列；
每列包含一个图标和两行文本，
你可以在其 widget 树中看到：

<img src='/assets/images/docs/ui/layout/widget-tree-pavlova-icon-row.png' class="text-center diagram-wrap" alt="Icon widget tree">

The `iconList` variable defines the icons row:

`iconList` 变量定义了图标行：

<?code-excerpt "layout/pavlova/lib/main.dart (icon-list)" replace="/iconList/[!$&!]/g"?>
```dart
const descTextStyle = TextStyle(
  color: Colors.black,
  fontWeight: FontWeight.w800,
  fontFamily: 'Roboto',
  letterSpacing: 0.5,
  fontSize: 18,
  height: 2,
);

// DefaultTextStyle.merge() allows you to create a default text
// style that is inherited by its child and all subsequent children.
final [!iconList!] = DefaultTextStyle.merge(
  style: descTextStyle,
  child: Container(
    padding: const EdgeInsets.all(20),
    child: Row(
      mainAxisAlignment: MainAxisAlignment.spaceEvenly,
      children: [
        Column(
          children: [
            Icon(Icons.kitchen, color: Colors.green[500]),
            const Text('PREP:'),
            const Text('25 min'),
          ],
        ),
        Column(
          children: [
            Icon(Icons.timer, color: Colors.green[500]),
            const Text('COOK:'),
            const Text('1 hr'),
          ],
        ),
        Column(
          children: [
            Icon(Icons.restaurant, color: Colors.green[500]),
            const Text('FEEDS:'),
            const Text('4-6'),
          ],
        ),
      ],
    ),
  ),
);
```

The `leftColumn` variable contains the ratings and icons rows,
as well as the title and text that describes the Pavlova:

`leftColumn` 变量包含评分行和图标行，
以及描述 Pavlova 的标题和文本：

<?code-excerpt "layout/pavlova/lib/main.dart (left-column)" replace="/leftColumn/[!$&!]/g"?>
```dart
final [!leftColumn!] = Container(
  padding: const EdgeInsets.fromLTRB(20, 30, 20, 20),
  child: Column(children: [titleText, subTitle, ratings, iconList]),
);
```

The left column is placed in a `SizedBox` to constrain its width.
Finally, the UI is constructed with the entire row (containing the
left column and the image) inside a `Card`.

左列放置在 `SizedBox` 中以约束其宽度。
最后，UI 是使用整个行（包含
左列和图像）在 `Card` 内部构建的。

The [Pavlova image][] is from [Pixabay][].
You can embed an image from the net using `Image.network()` but,
for this example, the image is saved to an images directory in the project,
added to the [pubspec file][], and accessed using `Images.asset()`.
For more information, see [Adding assets and images][].

[Pavlova 图像][Pavlova image] 来自 [Pixabay][]。
你可以使用 `Image.network()` 嵌入来自网络的图像，但
对于此示例，该图像已保存到项目中的 images 目录中，
已添加到 [pubspec 文件][]，并使用 `Images.asset()` 访问。
有关更多信息，请参见 [添加资源和图像][Adding assets and images]。

<?code-excerpt "layout/pavlova/lib/main.dart (body)"?>
```dart
body: Center(
  child: Container(
    margin: const EdgeInsets.fromLTRB(0, 40, 0, 30),
    height: 600,
    child: Card(
      child: Row(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [SizedBox(width: 440, child: leftColumn), mainImage],
      ),
    ),
  ),
),
```

:::tip

The Pavlova example runs best horizontally on a wide device,
such as a tablet.  If you are running this example in the iOS simulator,
you can select a different device using the **Hardware > Device** menu.
For this example, we recommend the iPad Pro.
You can change its orientation to landscape mode using
**Hardware > Rotate**. You can also change the size of the
simulator window (without changing the number of logical pixels)
using **Window > Scale**.

Pavlova 示例在平板电脑等宽设备上水平运行时效果最佳。
如果你在 iOS 模拟器中运行此示例，
你可以使用 **硬件 > 设备** 菜单选择其他设备。
对于此示例，我们建议使用 iPad Pro。
你可以使用 **硬件 > 旋转** 将其方向更改为横向模式。
你还可以使用 **窗口 > 缩放** 更改
模拟器窗口的大小（而不更改逻辑像素的数量）。

:::

**App source:** [pavlova]({{examples}}/layout/pavlova)

**App 源代码：** [pavlova]({{examples}}/layout/pavlova)

<hr>

[Pavlova image]: https://pixabay.com/en/photos/pavlova
[Pixabay]: https://pixabay.com/en/photos/pavlova
[pubspec file]: {{examples}}/layout/pavlova/pubspec.yaml

## Common layout widgets

## 常用布局 widget

Flutter has a rich library of layout widgets.
Here are a few of those most commonly used.
The intent is to get you up and running as quickly as possible,
rather than overwhelm you with a complete list.
For information on other available widgets,
refer to the [Widget catalog][],
or use the Search box in the [API reference docs][].
Also, the widget pages in the API docs often make suggestions
about similar widgets that might better suit your needs.

Flutter 拥有丰富的布局 widget 库。
以下是一些最常用的 widget。
目的是让你尽快启动并运行，
而不是用完整的列表让你不知所措。
有关其他可用 widget 的信息，
请参阅 [Widget 目录][]，
或使用 [API 参考文档][] 中的搜索框。
此外，API 文档中的 widget 页面通常会提供有关
可能更适合你需求的类似 widget 的建议。

The following widgets fall into two categories: standard widgets
from the [widgets library][], and specialized widgets from the
[Material library][]. Any app can use the widgets library but
only Material apps can use the Material Components library.

以下 widget 分为两类：来自 [widget 库][] 的标准 widget，
以及来自 [Material 库][] 的专用 widget。
任何 App 都可以使用 widget 库，但只有 Material App 才能使用 Material Components 库。

<a id="standard-widgets" aria-hidden="true"></a>
<a id="materials-widgets" aria-hidden="true"></a>

{% tabs "widget-types-tabs", true %}

<!-- {% tab "Standard widgets" %} -->
{% tab "标准 widget" %}

[`Container`](#container)
<br> Adds padding, margins, borders,
  background color, or other decorations to a widget.

[`Container`](#container)
<br> 向 widget 添加填充、边距、边框、
背景颜色或其他装饰。

[`GridView`](#gridview)
<br> Lays widgets out as a scrollable grid.

[`GridView`](#gridview)
<br> 将 widget 布局为可滚动网格。

[`ListView`](#listview)
<br> Lays widgets out as a scrollable list.

[`ListView`](#listview)
<br> 将 widget 布局为可滚动列表。

[`Stack`](#stack)
<br> Overlaps a widget on top of another.

[`Stack`](#stack)
<br> 将一个 widget 叠加在另一个 widget 之上。

{% endtab %}

<!-- {% tab "Material widgets" %} -->
{% tab "Material widget" %}

[`Scaffold`][]
<br> Provides a structured layout framework
  with slots for common Material Design app elements.

[`Scaffold`][]
<br> 提供了一个结构化的布局框架，
其中包含用于常见 Material Design App 元素的插槽。

[`AppBar`][]
<br> Creates a horizontal bar that's typically
  displayed at the top of a screen.

[`AppBar`][]
<br> 创建一个通常显示在屏幕顶部的水平栏。

[`Card`](#card)
<br> Organizes related info into a box with
  rounded corners and a drop shadow.

[`Card`](#card)
<br> 将相关信息组织到一个带有圆角和阴影的框中。

[`ListTile`](#listtile)
<br> Organizes up to 3 lines of text,
  and optional leading and trailing icons, into a row.

[`ListTile`](#listtile)
<br> 将最多 3 行文本以及可选的前置和后置图标组织到一行中。

{% endtab %}

<!-- {% tab "Cupertino widgets" %} -->
{% tab "Cupertino widget" %}

[`CupertinoPageScaffold`][]
<br> Provides the basic layout structure for an iOS-style page.

[`CupertinoPageScaffold`][]
<br> 为 iOS 风格的页面提供基本的布局结构。

[`CupertinoNavigationBar`][]
<br> Creates an iOS-style  navigation bar at the top of the screen.

[`CupertinoNavigationBar`][]
<br> 在屏幕顶部创建一个 iOS 风格的导航栏。

[`CupertinoSegmentedControl`][]
<br> Creates a segmented control for selecting.

[`CupertinoSegmentedControl`][]
<br> 创建一个用于选择的分段控件。

[`CupertinoTabBar`][] and [`CupertinoTabScaffold`][]
<br> Creates the characteristic iOS bottom tab bar.

[`CupertinoTabBar`][] 和 [`CupertinoTabScaffold`][]
<br> 创建具有 iOS 特征的底部选项栏。

{% endtab %}

{% endtabs %}

[`Scaffold`]: {{api}}/material/Scaffold-class.html
[`AppBar`]: {{api}}/material/AppBar-class.html
[`Container`]: {{api}}/widgets/Container-class.html
[`CupertinoPageScaffold`]: {{api}}/cupertino/CupertinoPageScaffold-class.html
[`CupertinoNavigationBar`]: {{api}}/cupertino/CupertinoNavigationBar-class.html
[`CupertinoSegmentedControl`]: {{api}}/cupertino/CupertinoSegmentedControl-class.html
[`CupertinoTabBar`]: {{api}}/cupertino/CupertinoTabBar-class.html
[`CupertinoTabScaffold`]: {{api}}/cupertino/CupertinoTabScaffold-class.html
[`GridView`]: {{api}}/widgets/GridView-class.html
[`ListTile`]: {{api}}/material/ListTile-class.html
[`ListView`]: {{api}}/widgets/ListView-class.html
[Material library]: {{api}}/material/material-library.html
[widgets library]: {{api}}/widgets/widgets-library.html

### Container

### Container

Many layouts make liberal use of [`Container`][]s to separate
widgets using padding, or to add borders or margins.
You can change the device's background by placing the
entire layout into a `Container` and changing its background
color or image.

许多布局都大量使用 [`Container`][] 来使用填充分隔
widget，或添加边框或边距。
你可以通过将整个布局放入 `Container` 中并更改其背景颜色或图像来更改设备的背景。

<div class="side-by-side">
<div>

[`Container`]: {{api}}/widgets/Container-class.html

#### Summary (Container)

#### 摘要 (Container)

* Add padding, margins, borders

  添加填充、边距、边框

* Change background color or image

  更改背景颜色或图像

* Contains a single child widget, but that child can be a `Row`,
  `Column`, or even the root of a widget tree

  包含单个子 widget，但该子项可以是 `Row`、`Column`，甚至可以是 widget 树的根

</div>
<div class="text-center">
  <img src='/assets/images/docs/ui/layout/margin-padding-border.png' class="diagram-wrap" alt="Diagram showing: margin, border, padding, and content">
</div>
</div>

#### Examples (Container)

#### 示例 (Container)

This layout consists of a column with two rows, each containing
2 images. A [`Container`][] is used to change the background color
of the column to a lighter grey.

此布局由一个包含两行的列组成，每行包含 2 个图像。
[`Container`][] 用于将列的背景颜色更改为较浅的灰色。

<div class="code-and-content">
<div>

  <?code-excerpt "layout/container/lib/main.dart (column)" replace="/\bContainer/[!$&!]/g;"?>
  ```dart
  Widget _buildImageColumn() {
    return [!Container!](
      decoration: const BoxDecoration(color: Colors.black26),
      child: Column(children: [_buildImageRow(1), _buildImageRow(3)]),
    );
  }
  ```

</div>
<div class="text-center">
  <img src='/assets/images/docs/ui/layout/container.png' class="mb-4" width="230px" alt="Screenshot showing 2 rows, each containing 2 images">
</div>
</div>

A `Container` is also used to add a rounded border and margins
to each image:

`Container` 还用于向每个图像添加圆角边框和边距：

<?code-excerpt "layout/container/lib/main.dart (row)" replace="/\bContainer/[!$&!]/g;"?>
```dart
Widget _buildDecoratedImage(int imageIndex) => Expanded(
  child: [!Container!](
    decoration: BoxDecoration(
      border: Border.all(width: 10, color: Colors.black38),
      borderRadius: const BorderRadius.all(Radius.circular(8)),
    ),
    margin: const EdgeInsets.all(4),
    child: Image.asset('images/pic$imageIndex.jpg'),
  ),
);

Widget _buildImageRow(int imageIndex) => Row(
  children: [
    _buildDecoratedImage(imageIndex),
    _buildDecoratedImage(imageIndex + 1),
  ],
);
```

You can find more `Container` examples in the [tutorial][].

你可以在 [教程][] 中找到更多 `Container` 示例。

**App source:** [container]({{examples}}/layout/container)

**App 源代码：** [container]({{examples}}/layout/container)

<hr>

[`Container`]: {{api}}/widgets/Container-class.html
[tutorial]: /ui/layout/tutorial

### GridView

### GridView

Use [`GridView`][] to lay widgets out as a two-dimensional
list. `GridView` provides two pre-fabricated lists,
or you can build your own custom grid. When a `GridView`
detects that its contents are too long to fit the render box,
it automatically scrolls.

使用 [`GridView`][] 将 widget 布局为二维列表。
`GridView` 提供了两个预制的列表，
或者你可以构建自己的自定义网格。当 `GridView` 检测到其内容太长而无法适应渲染框时，它会自动滚动。

[`GridView`]: {{api}}/widgets/GridView-class.html

#### Summary (GridView)

#### 摘要 (GridView)

* Lays widgets out in a grid

  以网格形式布局 widget

* Detects when the column content exceeds the render box
  and automatically provides scrolling

  检测列内容何时超过渲染框，并自动提供滚动

* Build your own custom grid, or use one of the provided grids:

  构建你自己的自定义网格，或使用提供的网格之一：

  * `GridView.count` allows you to specify the number of columns

    `GridView.count` 允许你指定列数

  * `GridView.extent` allows you to specify the maximum pixel
  width of a tile

    `GridView.extent` 允许你指定图块的最大像素宽度

{% comment %}

* Use `MediaQuery.of(context).orientation` to create a grid
  that changes its layout depending on whether the device
  is in landscape or portrait mode.

  使用 `MediaQuery.of(context).orientation` 创建一个网格，
  该网格会根据设备是处于横向模式还是纵向模式来更改其布局。

{% endcomment %}

:::note

When displaying a two-dimensional list where it's important which
row and column a cell occupies (for example,
it's the entry in the "calorie" column for the "avocado" row), use
[`Table`][] or [`DataTable`][].

当显示二维列表时，单元格占据的行和列很重要（例如，
它是“鳄梨”行的“卡路里”列中的条目），请使用 [`Table`][] 或 [`DataTable`][]。

:::

[`DataTable`]: {{api}}/material/DataTable-class.html
[`Table`]: {{api}}/widgets/Table-class.html

#### Examples (GridView)

#### 示例 (GridView)

<div class="side-by-side">
<div>
  <img src='/assets/images/docs/ui/layout/gridview-extent.png' class="text-center" alt="A 3-column grid of photos" height="440px">

  Uses `GridView.extent` to create a grid with tiles a maximum
  150 pixels wide.

  使用 `GridView.extent` 创建一个最大宽度为 150 像素的图块网格。

  **App source:** [grid_and_list]({{examples}}/layout/grid_and_list)

  **App 源代码：** [grid_and_list]({{examples}}/layout/grid_and_list)

</div>
<div>
  <img src='/assets/images/docs/ui/layout/gridview-count-flutter-gallery.png' class="text-center" alt="A 2 column grid with footers" height="440px">

  Uses `GridView.count` to create a grid that's 2 tiles
  wide in portrait mode, and 3 tiles wide in landscape mode.
  The titles are created by setting the `footer` property for
  each [`GridTile`][].

  使用 `GridView.count` 创建一个在纵向模式下为 2 个图块宽，在横向模式下为 3 个图块宽的网格。
  这些标题是通过为每个 [`GridTile`][] 设置 `footer` 属性来创建的。

  **Dart code:**
  [`grid_list_demo.dart`]({{examples}}/layout/gallery/lib/grid_list_demo.dart)

  **Dart 代码：**
  [`grid_list_demo.dart`]({{examples}}/layout/gallery/lib/grid_list_demo.dart)

</div>
</div>

<?code-excerpt "layout/grid_and_list/lib/main.dart (grid)" replace="/\GridView/[!$&!]/g;"?>
```dart
Widget _buildGrid() => [!GridView!].extent(
  maxCrossAxisExtent: 150,
  padding: const EdgeInsets.all(4),
  mainAxisSpacing: 4,
  crossAxisSpacing: 4,
  children: _buildGridTileList(30),
);

// The images are saved with names pic0.jpg, pic1.jpg...pic29.jpg.
// The List.generate() constructor allows an easy way to create
// a list when objects have a predictable naming pattern.
List<Widget> _buildGridTileList(int count) =>
    List.generate(count, (i) => Image.asset('images/pic$i.jpg'));
```

<hr>

[`GridTile`]: {{api}}/material/GridTile-class.html

### ListView

### ListView

[`ListView`][], a column-like widget, automatically
provides scrolling when its content is too long for
its render box.

[`ListView`][] 是一个类似列的 widget，当其内容对于其渲染框来说太长时，会自动提供滚动。

[`ListView`]: {{api}}/widgets/ListView-class.html

#### Summary (ListView)

#### 摘要 (ListView)

* A specialized [`Column`][] for organizing a list of boxes

  一个专门的 [`Column`][]，用于组织框列表

* Can be laid out horizontally or vertically

  可以水平或垂直布局

* Detects when its content won't fit and provides scrolling

  检测到其内容无法适应并提供滚动

* Less configurable than `Column`, but easier to use and
  supports scrolling

  比 `Column` 的可配置性差，但更易于使用并且支持滚动

[`Column`]: {{api}}/widgets/Column-class.html

#### Examples (ListView)

#### 示例 (ListView)

<div class="side-by-side">
<div>
  <img src='/assets/images/docs/ui/layout/listview.png' height="400px" class="simple-border text-center" alt="ListView containing movie theaters and restaurants">

  Uses `ListView` to display a list of businesses using
  `ListTile`s. A `Divider` separates the theaters from
  the restaurants.

  使用 `ListView` 通过 `ListTile` 显示商家列表。
  `Divider` 将剧院与餐厅分开。

  **App source:** [grid_and_list]({{examples}}/layout/grid_and_list)

  **App 源代码：** [grid_and_list]({{examples}}/layout/grid_and_list)

</div>
<div>
  <img src='/assets/images/docs/ui/layout/listview-color-gallery.png' height="400px" class="simple-border text-center" alt="ListView containing shades of blue">

  Uses `ListView` to display the [`Colors`][] from
  the [Material 2 Design palette][]
  for a particular color family.

  使用 `ListView` 显示来自 [Material 2 Design palette][] 的 [`Colors`][]，用于特定的颜色系列。

  **Dart code:**
  [`colors_demo.dart`]({{examples}}/layout/gallery/lib/colors_demo.dart)

  **Dart 代码：**
  [`colors_demo.dart`]({{examples}}/layout/gallery/lib/colors_demo.dart)

</div>
</div>

<?code-excerpt "layout/grid_and_list/lib/main.dart (list)" replace="/\ListView/[!$&!]/g;"?>
```dart
Widget _buildList() {
  return [!ListView!](
    children: [
      _tile('CineArts at the Empire', '85 W Portal Ave', Icons.theaters),
      _tile('The Castro Theater', '429 Castro St', Icons.theaters),
      _tile('Alamo Drafthouse Cinema', '2550 Mission St', Icons.theaters),
      _tile('Roxie Theater', '3117 16th St', Icons.theaters),
      _tile(
        'United Artists Stonestown Twin',
        '501 Buckingham Way',
        Icons.theaters,
      ),
      _tile('AMC Metreon 16', '135 4th St #3000', Icons.theaters),
      const Divider(),
      _tile('K\'s Kitchen', '757 Monterey Blvd', Icons.restaurant),
      _tile('Emmy\'s Restaurant', '1923 Ocean Ave', Icons.restaurant),
      _tile('Chaiya Thai Restaurant', '272 Claremont Blvd', Icons.restaurant),
      _tile('La Ciccia', '291 30th St', Icons.restaurant),
    ],
  );
}

ListTile _tile(String title, String subtitle, IconData icon) {
  return ListTile(
    title: Text(
      title,
      style: const TextStyle(fontWeight: FontWeight.w500, fontSize: 20),
    ),
    subtitle: Text(subtitle),
    leading: Icon(icon, color: Colors.blue[500]),
  );
}
```

<hr>

[`Colors`]: {{api}}/material/Colors-class.html
[Material 2 Design palette]: {{site.material2}}/design/color/the-color-system.html#tools-for-picking-colors

### Stack

### Stack

Use [`Stack`][] to arrange widgets on top of a base
widget&mdash;often an image. The widgets can completely
or partially overlap the base widget.

使用 [`Stack`][] 在基本 widget（通常是图像）之上排列 widget。这些 widget 可以完全或部分重叠基本 widget。

[`Stack`]: {{api}}/widgets/Stack-class.html

#### Summary (Stack)

#### 摘要 (Stack)

* Use for widgets that overlap another widget

  用于重叠另一个 widget 的 widget

* The first widget in the list of children is the base widget;
  subsequent children are overlaid on top of that base widget

  子项列表中的第一个 widget 是基本 widget；
  后续子项叠加在该基本 widget 之上

* A `Stack`'s content can't scroll

  `Stack` 的内容无法滚动

* You can choose to clip children that exceed the render box

  你可以选择裁剪超出渲染框的子项

#### Examples (Stack)

#### 示例 (Stack)

<div class="side-by-side">
<div>
  <img src='/assets/images/docs/ui/layout/stack.png' class="text-center" height="200px" alt="Circular avatar image with a label">

  Uses `Stack` to overlay a `Container`
  (that displays its `Text` on a translucent
  black background) on top of a `CircleAvatar`.
  The `Stack` offsets the text using the `alignment` property and
  `Alignment`s.

  使用 `Stack` 在 `CircleAvatar` 之上叠加一个 `Container`（在半透明黑色背景上显示其 `Text`）。
  `Stack` 使用 `alignment` 属性和 `Alignment` 偏移文本。

  **App source:** [card_and_stack]({{examples}}/layout/card_and_stack)

  **App 源代码：** [card_and_stack]({{examples}}/layout/card_and_stack)

</div>
<div>
  <img src='/assets/images/docs/ui/layout/stack-flutter-gallery.png' class="text-center" height="200px" alt="An image with a icon overlaid on top">

  Uses `Stack` to overlay an icon on top of an image.

  使用 `Stack` 在图像之上叠加一个图标。

  **Dart code:**
  [`bottom_navigation_demo.dart`]({{examples}}/layout/gallery/lib/bottom_navigation_demo.dart)

  **Dart 代码：**
  [`bottom_navigation_demo.dart`]({{examples}}/layout/gallery/lib/bottom_navigation_demo.dart)

</div>
</div>

<?code-excerpt "layout/card_and_stack/lib/main.dart (stack)" replace="/\bStack/[!$&!]/g;"?>
```dart
Widget _buildStack() {
  return [!Stack!](
    alignment: const Alignment(0.6, 0.6),
    children: [
      const CircleAvatar(
        backgroundImage: AssetImage('images/pic.jpg'),
        radius: 100,
      ),
      Container(
        decoration: const BoxDecoration(color: Colors.black45),
        child: const Text(
          'Mia B',
          style: TextStyle(
            fontSize: 20,
            fontWeight: FontWeight.bold,
            color: Colors.white,
          ),
        ),
      ),
    ],
  );
}
```

<hr>

### Card

### Card

A [`Card`][], from the [Material library][],
contains related nuggets of information and can
be composed of almost any widget, but is often used with
[`ListTile`][]. `Card` has a single child,
but its child can be a column, row, list, grid,
or other widget that supports multiple children.
By default, a `Card` shrinks its size to 0 by 0 pixels.
You can use [`SizedBox`][] to constrain the size of a card.

来自 [Material 库][] 的 [`Card`][] 包含相关的少量信息，并且可以由几乎任何 widget 组成，但通常与 [`ListTile`][] 一起使用。
`Card` 具有单个子项，但其子项可以是列、行、列表、网格或其他支持多个子项的 widget。
默认情况下，`Card` 会将其大小缩小到 0 x 0 像素。
你可以使用 [`SizedBox`][] 约束卡片的大小。

In Flutter, a `Card` features slightly rounded corners
and a drop shadow, giving it a 3D effect.
Changing a `Card`'s `elevation` property allows you to control
the drop shadow effect. Setting the elevation to 24,
for example, visually lifts the `Card` further from the
surface and causes the shadow to become more dispersed.
For a list of supported elevation values, see [Elevation][] in the
[Material guidelines][Material Design].
Specifying an unsupported value disables the drop shadow entirely.

在 Flutter 中，`Card` 具有略微圆角和阴影，使其具有 3D 效果。
更改 `Card` 的 `elevation` 属性允许你控制阴影效果。
例如，将 elevation 设置为 24 会在视觉上将 `Card` 从表面进一步抬起，并导致阴影更加分散。
有关支持的 elevation 值列表，请参见 [Material 指南][Material Design] 中的 [Elevation][]。
指定不支持的值将完全禁用阴影。

[`Card`]: {{api}}/material/Card-class.html
[Elevation]: {{site.material}}/styles/elevation
[`ListTile`]: {{api}}/material/ListTile-class.html
[Material Design]: {{site.material}}/styles
[`SizedBox`]: {{api}}/widgets/SizedBox-class.html
[Material library]: {{api}}/material/material-library.html

#### Summary (Card)

#### 摘要 (Card)

* Implements a [Material card][]

  实现 [Material card][]

* Used for presenting related nuggets of information

  用于呈现相关的少量信息

* Accepts a single child, but that child can be a `Row`,
  `Column`, or other widget that holds a list of children

  接受单个子项，但该子项可以是 `Row`、`Column` 或其他包含子项列表的 widget

* Displayed with rounded corners and a drop shadow

  以圆角和阴影显示

* A `Card`'s content can't scroll

  `Card` 的内容无法滚动

* From the [Material library][]

  来自 [Material 库][]

[Material card]: {{site.material}}/components/cards
[Material library]: {{api}}/material/material-library.html

#### Examples (Card)

#### 示例 (Card)

<div class="side-by-side">
<div>
  <img src='/assets/images/docs/ui/layout/card.png' height="200px" class="text-center" alt="Card containing 3 ListTiles">

  A `Card` containing 3 ListTiles and sized by wrapping
  it with a `SizedBox`. A `Divider` separates the first
  and second `ListTiles`.

  一个包含 3 个 ListTiles 的 `Card`，并通过使用 `SizedBox` 包装它来调整大小。
  `Divider` 分隔第一个和第二个 `ListTile`。

  **App source:** [card_and_stack]({{examples}}/layout/card_and_stack)

  **App 源代码：** [card_and_stack]({{examples}}/layout/card_and_stack)

</div>
<div>
  <img src='/assets/images/docs/ui/layout/card-flutter-gallery.png' height="200px" class="text-center" alt="Tappable card containing an image and multiple forms of text">

  A `Card` containing an image and text.

  一个包含图像和文本的 `Card`。

  **Dart code:**
  [`cards_demo.dart`]({{examples}}/layout/gallery/lib/cards_demo.dart)

  **Dart 代码：**
  [`cards_demo.dart`]({{examples}}/layout/gallery/lib/cards_demo.dart)

</div>
</div>

<?code-excerpt "layout/card_and_stack/lib/main.dart (card)" replace="/\bCard/[!$&!]/g;"?>
```dart
Widget _buildCard() {
  return SizedBox(
    height: 210,
    child: [!Card!](
      child: Column(
        children: [
          ListTile(
            title: const Text(
              '1625 Main Street',
              style: TextStyle(fontWeight: FontWeight.w500),
            ),
            subtitle: const Text('My City, CA 99984'),
            leading: Icon(Icons.restaurant_menu, color: Colors.blue[500]),
          ),
          const Divider(),
          ListTile(
            title: const Text(
              '(408) 555-1212',
              style: TextStyle(fontWeight: FontWeight.w500),
            ),
            leading: Icon(Icons.contact_phone, color: Colors.blue[500]),
          ),
          ListTile(
            title: const Text('costa@example.com'),
            leading: Icon(Icons.contact_mail, color: Colors.blue[500]),
          ),
        ],
      ),
    ),
  );
}
```

<hr>

### ListTile

### ListTile

Use [`ListTile`][], a specialized row widget from the
[Material library][], for an easy way to create a row
containing up to 3 lines of text and optional leading
and trailing icons. `ListTile` is most commonly used in
[`Card`][] or [`ListView`][], but can be used elsewhere.

使用来自 [Material 库][] 的专用行 widget [`ListTile`][]，可以轻松创建包含最多 3 行文本以及可选的前置和后置图标的行。
`ListTile` 最常用于 [`Card`][] 或 [`ListView`][] 中，但也可以在其他地方使用。

[`Card`]: {{api}}/material/Card-class.html
[`ListTile`]: {{api}}/material/ListTile-class.html
[`ListView`]: {{api}}/widgets/ListView-class.html
[Material library]: {{api}}/material/material-library.html

#### Summary (ListTile)

#### 摘要 (ListTile)

* A specialized row that contains up to 3 lines of text and
  optional icons

  一个专用行，包含最多 3 行文本和可选图标

* Less configurable than `Row`, but easier to use

  比 `Row` 的可配置性差，但更易于使用

* From the [Material library][]

  来自 [Material 库][]

[Material library]: {{api}}/material/material-library.html

#### Examples (ListTile)

#### 示例 (ListTile)

<div class="side-by-side">
<div>
  <img src='/assets/images/docs/ui/layout/card.png' class="text-center" alt="Card containing 3 ListTiles">

  A `Card` containing 3 `ListTile`s.

  一个包含 3 个 `ListTile` 的 `Card`。

  **App source:** [card_and_stack]({{examples}}/layout/card_and_stack)

  **App 源代码：** [card_and_stack]({{examples}}/layout/card_and_stack)

</div>
<div>
  <img src='/assets/images/docs/ui/layout/listtile-flutter-gallery.png' height="200px" class="simple-border text-center" alt="4 ListTiles, each containing a leading avatar">

  Uses `ListTile` with leading widgets.

  将 `ListTile` 与前置 widget 一起使用。

  **Dart code:**
  [`list_demo.dart`]({{examples}}/layout/gallery/lib/list_demo.dart)

  **Dart 代码：**
  [`list_demo.dart`]({{examples}}/layout/gallery/lib/list_demo.dart)

</div>
</div>

<hr>

## Constraints

## 约束

To fully understand Flutter's layout system, you need
to learn how Flutter positions and sizes
the components in a layout. For more information,
see [Understanding constraints][].

要完全理解 Flutter 的布局系统，你需要
了解 Flutter 如何定位和调整布局中的组件的大小。
有关更多信息，请参见 [理解约束][Understanding constraints]。

[Understanding constraints]: /ui/layout/constraints

## Videos

## 视频

The following videos, part of the
[Flutter in Focus][] series,
explain `Stateless` and `Stateful` widgets.

以下视频是 [Flutter in Focus][] 系列的一部分，
解释了 `Stateless` 和 `Stateful` widget。

{% ytEmbed 'wE7khGHVkYY', 'How to create stateless widgets' %}

{% ytEmbed 'AqCMFXEmf3w', 'How and when stateful widgets are best used' %}

[Flutter in Focus playlist]({{site.yt.playlist}}PLjxrf2q8roU2HdJQDjJzOeO6J3FoFLWr2)

[Flutter in Focus 播放列表]({{site.yt.playlist}}PLjxrf2q8roU2HdJQDjJzOeO6J3FoFLWr2)

---

Each episode of the [Widget of the Week series][] focuses on a widget.
Several of them include layout widgets.

[Widget of the Week series][] 的每一集都侧重于一个 widget。
其中一些包括布局 widget。

{% ytEmbed 'b_sQ9bMltGU', 'Introducing widget of the week' %}

[Flutter Widget of the Week playlist]({{site.yt.playlist}}PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG)

[Flutter Widget of the Week 播放列表]({{site.yt.playlist}}PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG)

[Widget of the Week series]: {{site.yt.playlist}}PLjxrf2q8roU23XGwz3Km7sQZFTdB996iG
[Flutter in Focus]: {{site.yt.watch}}?v=wgTBLj7rMPM&list=PLjxrf2q8roU2HdJQDjJzOeO6J3FoFLWr2

## Other resources

## 其他资源

The following resources might help when writing layout code.

以下资源可能有助于编写布局代码。

[Layout tutorial][]
<br> Learn how to build a layout.

[布局教程][Layout tutorial]
<br> 了解如何构建布局。

[Widget catalog][]
<br> Describes many of the widgets available in Flutter.

[核心 Widget 目录][Widget catalog]
<br> 描述了 Flutter 中可用的许多 widget。

[HTML/CSS Analogs in Flutter][]
<br> For those familiar with web programming,
  this page maps HTML/CSS functionality to Flutter features.

[Flutter 中的 HTML/CSS 对等物][HTML/CSS Analogs in Flutter]
<br> 对于那些熟悉 Web 编程的人，
此页面将 HTML/CSS 功能映射到 Flutter 功能。

[API reference docs][]
<br> Reference documentation for all of the Flutter libraries.

[API 参考文档][API reference docs]
<br> 所有 Flutter 库的参考文档。

[Adding assets and images][]
<br> Explains how to add images and other assets to your app's package.

[添加资源和图像][Adding assets and images]
<br> 解释了如何将图像和其他资源添加到 App 的 package 中。

[Zero to One with Flutter][]
<br> One person's experience writing their first Flutter app.

[Flutter 的从零到一][Zero to One with Flutter]
<br> 一个人编写他们的第一个 Flutter App 的经验。

[Layout tutorial]: /ui/layout/tutorial
[Widget catalog]: /ui/widgets
[HTML/CSS Analogs in Flutter]: /get-started/flutter-for/web-devs
[API reference docs]: {{api}}
[Adding assets and images]: /ui/assets/assets-and-images
[Zero to One with Flutter]: {{site.medium}}/@mravn/zero-to-one-with-flutter-43b13fd7b354
