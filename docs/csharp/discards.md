---
title: 弃元 - C# 指南
description: 介绍 C# 对弃元的支持（弃元是未赋值的可丢弃变量），以及弃元的使用方式。
ms.technology: csharp-fundamentals
ms.date: 09/22/2020
ms.openlocfilehash: eefa81d3bd8d56c9296e01533aaf93c4725323a3
ms.sourcegitcommit: 42d436ebc2a7ee02fc1848c7742bc7d80e13fc2f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "102104947"
---
# <a name="discards---c-guide"></a>弃元 - C# 指南

从 C# 7.0 开始，C# 支持弃元，这是一种在应用程序代码中人为取消使用的占位符变量。 弃元相当于未赋值的变量；它们没有值。 弃元用于给编译器和其他阅读代码的用户传达一种意图：即你打算忽略表达式的结果。 你可能需要忽略表达式的结果、元组表达式的一个或多个成员、方法的 `out` 参数或模式匹配表达式的目标。

因为只有一个弃元变量，且该变量可能甚至不会被分配存储空间。 所以，弃元可以减少内存分配。 弃元使代码意图更加明确。 它们可以增强其可读性和可维护性。

通过将下划线 (`_`) 赋给一个变量作为其变量名，指示该变量为一个弃元变量。 例如，以下方法调用返回一个元组，其中第一个值和第二个值为弃元。 `area` 是以前声明的变量，设置为由 `GetCityInformation` 返回的第三个组件：

```csharp
(_, _, area) = city.GetCityInformation(cityName);
```

从 C# 9.0 开始，可以使用弃元指定 Lambda 表达式中不使用的输入参数。 有关详细信息，请参阅 [Lambda 表达式](language-reference/operators/lambda-expressions.md)一文中的 [Lambda 表达式的输入参数](language-reference/operators/lambda-expressions.md#input-parameters-of-a-lambda-expression)一节。

当 `_` 是有效弃元时，尝试检索其值或在赋值操作中使用它时会生成编译器错误 CS0301：“当前上下文中不存在名称 ‘\_’”。 出现此错误是因为 `_` 未赋值，甚至可能未分配存储位置。 如果它是一个实际变量，则不能像之前的示例那样对多个值使用弃元。

## <a name="tuple-and-object-deconstruction"></a>元组和对象析构

如果应用程序代码使用某些元组元素，但忽略其他元素，这时使用弃元来处理元组就会很有用。 例如，以下 `QueryCityDataForYears` 方法返回一个元组，包含城市名称、城市面积、一个年份、该年份的城市人口、另一个年份及该年份的城市人口。 该示例显示了两个年份之间人口的变化。 对于元组提供的数据，我们不关注城市面积，并在一开始就知道城市名称和两个日期。 因此，我们只关注存储在元组中的两个人口数量值，可将其余值作为弃元处理。  

:::code language="csharp" source="snippets/discards/discard-tuple.cs" ID="DiscardTupleMember" :::

有关使用弃元析构元组的详细信息，请参阅 [析构元组和其他类型](deconstruct.md#deconstructing-tuple-elements-with-discards)。

类、结构或接口的 `Deconstruct` 方法还允许从对象中检索和析构一组特定的数据。 如果想只使用析构值的一个子集，可使用弃元。 以下示例将 `Person` 对象析构为四个字符串（名字、姓氏、城市和省/市/自治区），但舍弃姓氏和省/市/自治区。

:::code language="csharp" source="snippets/discards/discard-class.cs" :::

有关使用弃元析构用户定义的类型的详细信息，请参阅 [析构元组和其他类型](deconstruct.md#deconstructing-a-user-defined-type-with-discards)。

## <a name="pattern-matching-with-switch"></a>利用 `switch` 的模式匹配

弃元模式可通过 [switch 表达式](language-reference/operators/switch-expression.md)用于模式匹配。 每个表达式（包括 `null`）都始终匹配弃元模式。

以下示例定义了一个 `ProvidesFormatInfo` 方法，它使用 `switch` 表达式来确定对象是否提供 <xref:System.IFormatProvider> 实现并测试对象是否为 `null`。 它还使用弃元模式来处理任何其他类型的非 null 对象。

:::code language="csharp" source="snippets/discards/discard-pattern2.cs" ID="DiscardSwitchExample" :::

## <a name="calls-to-methods-with-out-parameters"></a>对具有 `out` 参数的方法的调用

当调用 `Deconstruct` 方法来析构用户定义类型（类、结构或接口的实例）时，可使用弃元表示单个 `out` 参数的值。 但当使用 `out` 参数调用任何方法时，也可使用弃元表示 `out` 参数的值。

以下示例调用 [DateTime.TryParse(String, out DateTime)](<xref:System.DateTime.TryParse(System.String,System.DateTime@)>) 方法来确定日期的字符串表示形式在当前区域性中是否有效。 因为该示例侧重验证日期字符串，而不是解析它来提取日期，所以方法的 `out` 参数为弃元。

:::code language="csharp" source="snippets/discards/discard-out1.cs" ID="DiscardOutParameter" :::

## <a name="a-standalone-discard"></a>独立弃元

可使用独立弃元来指示要忽略的任何变量。 一种典型的用法是使用赋值来确保一个参数不为 null。 下面的代码使用弃元来强制赋值。 赋值的右侧使用 [Null 合并操作符](language-reference/operators/null-coalescing-operator.md)，用于在参数为 `null` 时引发 <xref:System.ArgumentNullException?displayProperty=nameWithType>。 此代码不需要赋值结果，因此将对其使用弃元。 该表达式强制执行 null 检查。 弃元说明你的意图：不需要或不使用赋值结果。

:::code language="csharp" source="snippets/discards/standalone-discard1.cs" ID="ArgNullCheck" :::

以下示例使用独立弃元来忽略异步操作返回的 <xref:System.Threading.Tasks.Task> 对象。 分配任务的效果等同于抑制操作即将完成时所引发的异常。 这使你的意图更加明确：你需要对 `Task` 使用弃元，并忽略该异步操作生成的任何错误。

:::code language="csharp" source="snippets/discards/standalone-discard1.cs" ID="SnippetDiscardTask" :::

如果不将任务分配给弃元，则以下代码会生成编译器警告：

:::code language="csharp" source="snippets/discards/standalone-discard1.cs" ID="SnippetNoDiscardTask" :::

> [!NOTE]
> 如果使用调试器运行前面两个示例中的任意一个，则在引发异常时，调试器将停止该程序。 在没有附加调试器的情况下，这两种情况下的异常都会被以静默方式忽略。

`_` 也是有效标识符。 当在支持的上下文之外使用时，`_` 不视为弃元，而视为有效变量。 如果名为 `_` 的标识符已在范围内，则使用 `_` 作为独立弃元可能导致：

- 将预期的弃元的值赋给范围内 `_` 变量，会导致该变量的值被意外修改。 例如：
   :::code language="csharp" source="snippets/discards/standalone-discard2.cs" ID="VariableIdentifier" :::
- 因违反类型安全而发生的编译器错误。 例如：
   :::code language="csharp" source="snippets/discards/standalone-discard2.cs" ID="VariableTypeInference" :::
- 编译器错误 CS0136：“无法在此范围中声明名为“\_”的局部变量或参数，因为该名称用于在封闭的局部范围中定义局部变量或参数”。 例如：
   :::code language="csharp" source="snippets/discards/standalone-discard2.cs" ID="CannotRedeclare" :::

## <a name="see-also"></a>另请参阅

- [析构元组和其他类型](deconstruct.md)
- [`is` 关键字](language-reference/keywords/is.md)
- [`switch` 关键字](language-reference/keywords/switch.md)
