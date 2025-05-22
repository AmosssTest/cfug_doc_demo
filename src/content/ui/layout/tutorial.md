---
# title: Build a Flutter layout
title: 构建 Flutter 布局
# short-title: Layout tutorial
short-title: [布局教程][Layout tutorial]
# description: Learn how to build a layout in Flutter.
description: 学习如何在 Flutter 中构建布局。
---

{% assign examples = site.repo.this | append: "/tree/" | append: site.branch | append: "/examples" -%}

<!-- :::secondary What you'll learn -->
:::secondary 你将学到什么

* How to lay out widgets next to each other.

  如何将 widget 并排放置。

* How to add space between widgets.

  如何在 widget 之间添加间距。

* How adding and nesting widgets results in a Flutter layout.

  添加和嵌套 widget 如何形成 Flutter 布局。

:::

This tutorial explains how to design and build layouts in Flutter.

本教程讲解如何在 Flutter 中设计和构建布局。

If you use the example code provided, you can build the following app.

如果你使用提供的示例代码，你可以构建以下应用。

{% render docs/app-figure.md, img-class:"site-mobile-screenshot border", image:"ui/layout/layout-demo-app.png", caption:"The finished app.", width:"50%" %}

<figcaption class="figure-caption">

Photo by [Dino Reichmuth][ch-photo] on [Unsplash][].
Text by [Switzerland Tourism][].

照片由 [Dino Reichmuth][ch-photo] 拍摄于 [Unsplash][]。
文本由 [Switzerland Tourism][] 提供。

</figcaption>

To get a better overview of the layout mechanism, start with
[Flutter's approach to layout][].

为了更好地了解布局机制，请从 [Flutter 的布局方法][Flutter's approach to layout] 开始。

[Switzerland Tourism]: https://www.myswitzerland.com/en-us/destinations/lake-oeschinen
[Flutter's approach to layout]: /ui/layout

## Diagram the layout

## 图解布局

In this section, consider what type of user experience you want for
your app users.

在本节中，考虑你希望你的应用用户获得什么样的用户体验。

Consider how to position the components of your user interface.
A layout consists of the total end result of these positionings.
Consider planning your layout to speed up your coding.
Using visual cues to know where something goes on screen can be a great help.

考虑如何定位用户界面的组件。
布局由这些定位的最终结果组成。
考虑规划你的布局以加快你的编码速度。
使用视觉提示来了解屏幕上的内容会很有帮助。

Use whichever method you prefer, like an interface design tool or a pencil
and a sheet of paper. Figure out where you want to place elements on your
screen before writing code. It's the programming version of the adage:
"Measure twice, cut once."

使用你喜欢的任何方法，比如界面设计工具或铅笔和纸。
在编写代码之前，弄清楚你想把元素放在屏幕上的什么位置。
这是编程版的格言：「三思而后行」。

<ol>
<li>

Ask these questions to break the layout down to its basic elements.

提出这些问题，将布局分解为基本元素。

* Can you identify the rows and columns?

  你能识别出行和列吗？

* Does the layout include a grid?

  布局是否包含网格？

* Are there overlapping elements?

  是否有重叠的元素？

* Does the UI need tabs?

  UI 是否需要选项卡？

* What do you need to align, pad, or border?

  你需要对齐、填充或边框什么？

</li>

<li>

Identify the larger elements. In this example, you arrange the image, title,
buttons, and description into a column.

识别较大的元素。在本例中，你将图像、标题、按钮和描述排列成一列。

{% render docs/app-figure.md, img-class:"site-mobile-screenshot border", image:"ui/layout/layout-sketch-intro.svg", caption:"Major elements in the layout: image, row, row, and text block", width:"50%" %}

</li>
<li>

Diagram each row.

图解每一行。

<ol type="a">

<li>

Row 1, the **Title** section, has three children:
a column of text, a star icon, and a number.
Its first child, the column, contains two lines of text.
That first column might need more space.

第 1 行，**标题**部分，有三个子项：一列文本、一个星标图标和一个数字。
它的第一个子项，即列，包含两行文本。
第一列可能需要更多空间。

{% render docs/app-figure.md, image:"ui/layout/layout-sketch-title-block.svg", caption:"Title section with text blocks and an icon" -%}

</li>

<li>

Row 2, the **Button** section, has three children: each child contains
a column which then contains an icon and text.

第 2 行，**按钮**部分，有三个子项：每个子项包含一列，然后包含一个图标和文本。

{% render docs/app-figure.md, image:"ui/layout/layout-sketch-button-block.svg", caption:"The Button section with three labeled buttons", width:"50%" %}

  </li>

</ol>

</li>
</ol>

After diagramming the layout, consider how you would code it.

在图解布局之后，考虑你将如何编写代码。

Would you write all the code in one class?
Or, would you create one class for each part of the layout?

你会在一个类中编写所有代码吗？
或者，你会为布局的每个部分创建一个类吗？

To follow Flutter best practices, create one class, or Widget,
to contain each part of your layout.
When Flutter needs to re-render part of a UI,
it updates the smallest part that changes.
This is why Flutter makes "everything a widget".
If only the text changes in a `Text` widget, Flutter redraws only that text.
Flutter changes the least amount of the UI possible in response to user input.

为了遵循 Flutter 的最佳实践，创建一个类或 widget，来包含布局的每个部分。
当 Flutter 需要重新渲染 UI 的一部分时，它会更新发生变化的最小部分。
这就是为什么 Flutter 会让「一切皆为 widget」。
如果只有 `Text` widget 中的文本发生变化，Flutter 只会重绘该文本。
Flutter 会根据用户输入，尽可能少地更改 UI。

For this tutorial, write each element you have identified as its own widget.

对于本教程，将你已识别的每个元素编写为它自己的 widget。

## Create the app base code

## 创建应用基本代码

In this section, shell out the basic Flutter app code to start your app.

在本节中，shell 输出基本的 Flutter 应用代码以启动你的应用。

<?code-excerpt path-base="layout/base"?>

1. [Set up your Flutter environment][].

   [设置你的 Flutter 环境][Set up your Flutter environment]。

1. [Create a new Flutter app][new-flutter-app].

   [创建一个新的 Flutter 应用][new-flutter-app]。

1. Replace the contents of `lib/main.dart` with the following code.
   This app uses a parameter for the app title and the title shown
   on the app's `appBar`. This decision simplifies the code.

   将 `lib/main.dart` 的内容替换为以下代码。
   这个应用使用一个参数作为应用标题和应用 `appBar` 上显示的标题。这个决定简化了代码。

   <?code-excerpt "lib/main.dart (all)"?>
   ```dart
   import 'package:flutter/material.dart';
   
   void main() => runApp(const MyApp());
   
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

[Set up your Flutter environment]: /get-started/install
[new-flutter-app]: /reference/create-new-app

## Add the Title section

## 添加标题部分

In this section, create a `TitleSection` widget that resembles
the following layout.

在本节中，创建一个类似于以下布局的 `TitleSection` widget。

<?code-excerpt path-base="layout/lakes"?>

{% render docs/app-figure.md, image:"ui/layout/layout-sketch-title-block-unlabeled.svg", caption:"The Title section as sketch and prototype UI" %}

### Add the `TitleSection` Widget

### 添加 `TitleSection` Widget

Add the following code after the `MyApp` class.

在 `MyApp` 类之后添加以下代码。

<?code-excerpt "step2/lib/main.dart (title-section)"?>
```dart
class TitleSection extends StatelessWidget {
  const TitleSection({super.key, required this.name, required this.location});

  final String name;
  final String location;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(32),
      child: Row(
        children: [
          Expanded(
            /*1*/
            child: Column(
              crossAxisAlignment: CrossAxisAlignment.start,
              children: [
                /*2*/
                Padding(
                  padding: const EdgeInsets.only(bottom: 8),
                  child: Text(
                    name,
                    style: const TextStyle(fontWeight: FontWeight.bold),
                  ),
                ),
                Text(location, style: TextStyle(color: Colors.grey[500])),
              ],
            ),
          ),
          /*3*/
          Icon(Icons.star, color: Colors.red[500]),
          const Text('41'),
        ],
      ),
    );
  }
}
```

{:.numbered-code-notes}

1. To use all remaining free space in the row, use the `Expanded` widget to
   stretch the `Column` widget.
   To place the column at the start of the row,
   set the `crossAxisAlignment` property to `CrossAxisAlignment.start`.

   要使用行中所有剩余的可用空间，请使用 `Expanded` widget 来拉伸 `Column` widget。
   要将列放置在行的开头，请将 `crossAxisAlignment` 属性设置为 `CrossAxisAlignment.start`。

2. To add space between the rows of text, put those rows in a `Padding` widget.

   要在文本行之间添加间距，请将这些行放在 `Padding` widget 中。

3. The title row ends with a red star icon and the text `41`.
    The entire row falls inside a `Padding` widget and pads each edge
    by 32 pixels.

   标题行以一个红色星标图标和文本 `41` 结尾。
   整个行都位于 `Padding` widget 内，并将每个边缘填充 32 像素。

### Change the app body to a scrolling view

### 将应用主体更改为滚动视图

In the `body` property, replace the `Center` widget with a
`SingleChildScrollView` widget.
Within the [`SingleChildScrollView`][] widget, replace the `Text` widget with a
`Column` widget.

在 `body` 属性中，将 `Center` widget 替换为 `SingleChildScrollView` widget。
在 [`SingleChildScrollView`][] widget 中，将 `Text` widget 替换为 `Column` widget。

```dart diff
- body: const Center(
-   child: Text('Hello World'),
+ body: const SingleChildScrollView(
+   child: Column(
+     children: [
```

These code updates change the app in the following ways.

这些代码更新以以下方式更改应用。

* A `SingleChildScrollView` widget can scroll.
  This allows elements that don't fit on the current screen to display.

  `SingleChildScrollView` widget 可以滚动。
  这允许显示不适合当前屏幕的元素。

* A `Column` widget displays any elements within its `children` property
  in the order listed.
  The first element listed in the `children` list displays at
  the top of the list. Elements in the `children` list display
  in array order on the screen from top to bottom.

  `Column` widget 按列出的顺序显示其 `children` 属性中的任何元素。
  `children` 列表中列出的第一个元素显示在列表的顶部。
  `children` 列表中的元素按数组顺序从上到下显示在屏幕上。

[`SingleChildScrollView`]: {{site.api}}/flutter/widgets/SingleChildScrollView-class.html

### Update the app to display the title section

### 更新应用以显示标题部分

Add the `TitleSection` widget as the first element in the `children` list.
This places it at the top of the screen.
Pass the provided name and location to the `TitleSection` constructor.

将 `TitleSection` widget 添加为 `children` 列表中的第一个元素。
这会将其放置在屏幕顶部。
将提供的名称和位置传递给 `TitleSection` 构造函数。

```dart diff
+ children: [
+   TitleSection(
+     name: 'Oeschinen Lake Campground',
+     location: 'Kandersteg, Switzerland',
+   ),
+ ],
```

:::tip

* When pasting code into your app, indentation can become skewed.
  To fix this in your Flutter editor, use [automatic reformatting support][].

  将代码粘贴到你的应用中时，缩进可能会倾斜。
  要在你的 Flutter 编辑器中修复此问题，请使用 [自动重新格式化支持][automatic reformatting support]。

* To accelerate your development, try Flutter's [hot reload][] feature.

  为了加速你的开发，请尝试 Flutter 的 [热重载][] 功能。

* If you have problems, compare your code to [`lib/main.dart`][].

  如果你遇到问题，请将你的代码与 [`lib/main.dart`][] 进行比较。

:::

[automatic reformatting support]: /tools/formatting
[hot reload]: /tools/hot-reload
[`lib/main.dart`]: {{examples}}/layout/lakes/step2/lib/main.dart

## Add the Button section

## 添加按钮部分

In this section, add the buttons that will add functionality to your app.

在本节中，添加将为你的应用添加功能的按钮。

<?code-excerpt path-base="layout/lakes/step3"?>

The **Button** section contains three columns that use the same layout:
an icon over a row of text.

**按钮**部分包含三个使用相同布局的列：一个图标位于一行文本之上。

{% render docs/app-figure.md, image:"ui/layout/layout-sketch-button-block-unlabeled.svg", caption:"The Button section as sketch and prototype UI" %}

Plan to distribute these columns in one row so each takes the same
amount of space. Paint all text and icons with the primary color.

计划将这些列分布在一行中，以便每个列占用相同的空间。
用主色绘制所有文本和图标。

### Add the `ButtonSection` widget

### 添加 `ButtonSection` widget

Add the following code after the `TitleSection` widget to contain the code
to build the row of buttons.

在 `TitleSection` widget 之后添加以下代码，以包含构建按钮行的代码。

<?code-excerpt "lib/main.dart (button-start)"?>
```dart
class ButtonSection extends StatelessWidget {
  const ButtonSection({super.key});

  @override
  Widget build(BuildContext context) {
    final Color color = Theme.of(context).primaryColor;
    // ···
  }

}
```

### Create a widget to make buttons

### 创建一个 widget 来制作按钮

As the code for each column could use the same syntax,
create a widget named `ButtonWithText`.
The widget's constructor accepts a color, icon data, and a label for the button.
Using these values, the widget builds a `Column` with an `Icon` and a stylized
`Text` widget as its children.
To help separate these children, a `Padding` widget the `Text` widget
is wrapped with a `Padding` widget.

由于每列的代码都可以使用相同的语法，因此创建一个名为 `ButtonWithText` 的 widget。
该 widget 的构造函数接受颜色、图标数据和按钮的标签。
使用这些值，该 widget 构建一个 `Column`，其中包含一个 `Icon` 和一个样式化的 `Text` widget 作为其子项。
为了帮助分隔这些子项，`Padding` widget 将 `Text` widget 包装在一个 `Padding` widget 中。

Add the following code after the `ButtonSection` class.

在 `ButtonSection` 类之后添加以下代码。

<?code-excerpt "lib/main.dart (button-with-text)"?>
```dart
class ButtonSection extends StatelessWidget {
  const ButtonSection({super.key});
  // ···
}

class ButtonWithText extends StatelessWidget {
  const ButtonWithText({
    super.key,
    required this.color,
    required this.icon,
    required this.label,
  });

  final Color color;
  final IconData icon;
  final String label;

  @override
  Widget build(BuildContext context) {
    return Column(
      mainAxisSize: MainAxisSize.min,
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
        Icon(icon, color: color),
        Padding(
          padding: const EdgeInsets.only(top: 8),
          child: Text(
            label,
            style: TextStyle(
              fontSize: 12,
              fontWeight: FontWeight.w400,
              color: color,
            ),
          ),
        ),
      ],
    );
  }
```

### Position the buttons with a `Row` widget

### 使用 `Row` widget 定位按钮

Add the following code into the `ButtonSection` widget.

将以下代码添加到 `ButtonSection` widget 中。

1. Add three instances of the `ButtonWithText` widget, once for each button.

   为每个按钮添加三个 `ButtonWithText` widget 的实例。

1. Pass the color, `Icon`, and text for that specific button.

   传递该特定按钮的颜色、`Icon` 和文本。

1. Align the columns along the main axis with the
   `MainAxisAlignment.spaceEvenly` value.
   The main axis for a `Row` widget is horizontal and the main axis for a
   `Column` widget is vertical.
   This value, then, tells Flutter to arrange the free space in equal amounts
   before, between, and after each column along the `Row`.

   使用 `MainAxisAlignment.spaceEvenly` 值沿主轴对齐列。
   `Row` widget 的主轴是水平的，而 `Column` widget 的主轴是垂直的。
   然后，此值告诉 Flutter 在 `Row` 沿线的每列之前、之间和之后以相等的量排列可用空间。

<?code-excerpt "lib/main.dart (button-section)"?>
```dart
class ButtonSection extends StatelessWidget {
  const ButtonSection({super.key});

  @override
  Widget build(BuildContext context) {
    final Color color = Theme.of(context).primaryColor;
    return SizedBox(
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: [
          ButtonWithText(color: color, icon: Icons.call, label: 'CALL'),
          ButtonWithText(color: color, icon: Icons.near_me, label: 'ROUTE'),
          ButtonWithText(color: color, icon: Icons.share, label: 'SHARE'),
        ],
      ),
    );
  }

}

class ButtonWithText extends StatelessWidget {
  const ButtonWithText({
    super.key,
    required this.color,
    required this.icon,
    required this.label,
  });

  final Color color;
  final IconData icon;
  final String label;

  @override
  Widget build(BuildContext context) {
    return Column(
      // ···
    );
  }

}
```

### Update the app to display the button section

### 更新应用以显示按钮部分

Add the button section to the `children` list.

将按钮部分添加到 `children` 列表。

<?code-excerpt path-base="layout/lakes"?>

```dart diff
    TitleSection(
      name: 'Oeschinen Lake Campground',
      location: 'Kandersteg, Switzerland',
    ),
+   ButtonSection(),
  ],
```

## Add the Text section

## 添加文本部分

In this section, add the text description to this app.

在本节中，将文本描述添加到此应用。

{% render docs/app-figure.md, image:"ui/layout/layout-sketch-add-text-block.svg", caption:"The text block as sketch and prototype UI" %}

<?code-excerpt path-base="layout/lakes"?>

### Add the `TextSection` widget

### 添加 `TextSection` widget

Add the following code as a separate widget after the `ButtonSection` widget.

在 `ButtonSection` widget 之后添加以下代码作为单独的 widget。

<?code-excerpt "step4/lib/main.dart (text-section)"?>
```dart
class TextSection extends StatelessWidget {
  const TextSection({super.key, required this.description});

  final String description;

  @override
  Widget build(BuildContext context) {
    return Padding(
      padding: const EdgeInsets.all(32),
      child: Text(description, softWrap: true),
    );
  }
}
```

By setting [`softWrap`][] to `true`, text lines fill the column width before
wrapping at a word boundary.

通过将 [`softWrap`][] 设置为 `true`，文本行在单词边界处换行之前会填充列宽。

[`softWrap`]: {{site.api}}/flutter/widgets/Text/softWrap.html

### Update the app to display the text section

### 更新应用以显示文本部分

Add a new `TextSection` widget as a child after the `ButtonSection`.
When adding the `TextSection` widget, set its `description` property to
the text of the location description.

在 `ButtonSection` 之后添加一个新的 `TextSection` widget 作为子项。
添加 `TextSection` widget 时，将其 `description` 属性设置为位置描述的文本。

```dart diff
      location: 'Kandersteg, Switzerland',
    ),
    ButtonSection(),
+   TextSection(
+     description:
+         'Lake Oeschinen lies at the foot of the Blüemlisalp in the '
+         'Bernese Alps. Situated 1,578 meters above sea level, it '
+         'is one of the larger Alpine Lakes. A gondola ride from '
+         'Kandersteg, followed by a half-hour walk through pastures '
+         'and pine forest, leads you to the lake, which warms to 20 '
+         'degrees Celsius in the summer. Activities enjoyed here '
+         'include rowing, and riding the summer toboggan run.',
+   ),
  ], 
```

## Add the Image section

## 添加图像部分

In this section, add the image file to complete your layout.

在本节中，添加图像文件以完成你的布局。

### Configure your app to use supplied images

### 配置你的应用以使用提供的图像

To configure your app to reference images, modify its `pubspec.yaml` file.

要配置你的应用以引用图像，请修改其 `pubspec.yaml` 文件。

1. Create an `images` directory at the top of the project.

   在项目顶部创建一个 `images` 目录。

1. Download the [`lake.jpg`][] image and add it to the new `images` directory.

   下载 [`lake.jpg`][] 图像并将其添加到新的 `images` 目录。

   :::note

   You can't use `wget` to save this binary file.
   You can download the [image][ch-photo] from [Unsplash][]
   under the Unsplash License. The small size comes in at 94.4 kB.

   你不能使用 `wget` 来保存此二进制文件。
   你可以从 [Unsplash][] 下载 [图像][ch-photo]，遵循 Unsplash 许可。小尺寸为 94.4 kB。

   :::

1. To include images, add an `assets` tag to the `pubspec.yaml` file
   at the root directory of your app.
   When you add `assets`, it serves as the set of pointers to the images
   available to your code.

   要包含图像，请将 `assets` 标签添加到应用根目录下的 `pubspec.yaml` 文件中。
   当你添加 `assets` 时，它会作为指向你的代码可用的图像的指针集。

   ```yaml title="pubspec.yaml" diff
     flutter:
       uses-material-design: true
   +   assets:
   +     - images/lake.jpg
   ```

:::tip

Text in the `pubspec.yaml` respects whitespace and text case.
Write the changes to the file as given in the previous example.

`pubspec.yaml` 中的文本遵循空格和文本大小写。
按照上一个示例中的说明编写对文件的更改。

This change might require you to restart the running program to
display the image.

此更改可能需要你重新启动正在运行的程序才能显示图像。

:::

[`lake.jpg`]: https://raw.githubusercontent.com/flutter/website/main/examples/layout/lakes/step5/images/lake.jpg

### Create the `ImageSection` widget

### 创建 `ImageSection` widget

Define the following `ImageSection` widget after the other declarations.

在其他声明之后定义以下 `ImageSection` widget。

<?code-excerpt "step5/lib/main.dart (image-section)"?>
```dart
class ImageSection extends StatelessWidget {
  const ImageSection({super.key, required this.image});

  final String image;

  @override
  Widget build(BuildContext context) {
    return Image.asset(image, width: 600, height: 240, fit: BoxFit.cover);
  }
}
```

The `BoxFit.cover` value tells Flutter to display the image with
two constraints. First, display the image as small as possible.
Second, cover all the space that the layout allotted, called the render box.

`BoxFit.cover` 值告诉 Flutter 使用两个约束显示图像。首先，尽可能小地显示图像。
其次，覆盖布局分配的所有空间，称为渲染框。

### Update the app to display the image section

### 更新应用以显示图像部分

Add an `ImageSection` widget as the first child in the `children` list.
Set the `image` property to the path of the image you added in
[Configure your app to use supplied images](#configure-your-app-to-use-supplied-images).

将 `ImageSection` widget 添加为 `children` 列表中的第一个子项。
将 `image` 属性设置为你在 [配置你的应用以使用提供的图像](#configure-your-app-to-use-supplied-images) 中添加的图像的路径。

```dart diff
  children: [
+   ImageSection(
+     image: 'images/lake.jpg',
+   ),
    TitleSection(
      name: 'Oeschinen Lake Campground',
      location: 'Kandersteg, Switzerland',
```

## Congratulations

## 恭喜

That's it! When you hot reload the app, your app should look like this.

就这样！当你热重载应用时，你的应用应该看起来像这样。

{% render docs/app-figure.md, img-class:"site-mobile-screenshot border", image:"ui/layout/layout-demo-app.png", caption:"The finished app", width:"50%" %}

## Resources

## 资源

You can access the resources used in this tutorial from these locations:

你可以从以下位置访问本教程中使用的资源：

**Dart code:** [`main.dart`][]<br>
**Image:** [ch-photo][]<br>
**Pubspec:** [`pubspec.yaml`][]<br>

**Dart 代码：** [`main.dart`][]<br>
**图像：** [ch-photo][]<br>
**Pubspec：** [`pubspec.yaml`][]<br>

[`main.dart`]: {{examples}}/layout/lakes/step6/lib/main.dart
[ch-photo]: https://unsplash.com/photos/red-and-gray-tents-in-grass-covered-mountain-5Rhl-kSRydQ
[`pubspec.yaml`]: {{examples}}/layout/lakes/step6/pubspec.yaml

## Next Steps

## 下一步

To add interactivity to this layout, follow the
[interactivity tutorial][].

要向此布局添加交互性，请按照 [交互性教程][interactivity tutorial] 进行操作。

[interactivity tutorial]: /ui/interactivity
[Unsplash]: https://unsplash.com
