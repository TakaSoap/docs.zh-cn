---
title: 如何：更改过程自变量的值
ms.date: 07/20/2015
helpviewer_keywords:
- procedures [Visual Basic], arguments
- procedures [Visual Basic], parameters
- procedure arguments
- arguments [Visual Basic], passing by reference
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- arguments [Visual Basic], ByRef
- arguments [Visual Basic], changing value
ms.assetid: 6fad2368-5da7-4c07-8bf8-0f4e65a1be67
ms.openlocfilehash: deac87ca4690990a4d00f63d0ea9b843c3f9a9c4
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75344478"
---
# <a name="how-to-change-the-value-of-a-procedure-argument-visual-basic"></a>如何：更改过程参数的值 (Visual Basic)
调用过程时，提供的每个参数都对应于在过程中定义的参数之一。 在某些情况下，过程代码可以更改调用代码中的参数的基础值。 在其他情况下，该过程只能更改其参数的本地副本。  
  
 调用过程时，Visual Basic 将为每个传递了[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)的参数创建一个本地副本。 对于传递了[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)的每个参数，Visual Basic 为过程代码提供对调用代码中参数的基础编程元素的直接引用。  
  
 如果调用代码中的基础元素是可修改的元素，并且参数 `ByRef`传递，则过程代码可以使用直接引用更改调用代码中的元素值。  
  
## <a name="changing-the-underlying-value"></a>更改基础值  
  
#### <a name="to-change-the-underlying-value-of-a-procedure-argument-in-the-calling-code"></a>更改调用代码中过程参数的基础值  
  
1. 在过程声明中，为对应于参数的参数指定[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) 。  
  
2. 在调用代码中，将可修改的编程元素作为参数传递。  
  
3. 在调用代码中，不要将参数括在参数列表的括号中。  
  
4. 在过程代码中，使用参数名称将值分配给调用代码中的基础元素。  
  
 有关演示，请参阅进一步的示例。  
  
## <a name="changing-local-copies"></a>更改本地副本  
 如果调用代码中的基础元素是不可更改的元素，或者如果参数是 `ByVal`传递的，则该过程无法在调用代码中更改其值。 但是，该过程可以更改此类参数的本地副本。  
  
#### <a name="to-change-the-copy-of-a-procedure-argument-in-the-procedure-code"></a>更改过程代码中过程参数的副本  
  
1. 在过程声明中，为对应于参数的参数指定[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) 。  
  
     或  
  
     在调用代码中，将参数括在参数列表的括号中。 这会强制 Visual Basic 按值传递参数，即使相应的参数指定 `ByRef`也是如此。  
  
2. 在过程代码中，使用参数名称将值分配给参数的本地副本。 不会更改调用代码中的基础值。  
  
## <a name="example"></a>示例  
 下面的示例演示了两个过程，这些过程使用数组变量并对其元素进行操作。 `increase` 过程只是向每个元素添加一个。 `replace` 过程将新数组分配给参数 `a()` 然后向每个元素添加一个数组。  
  
 [!code-vb[VbVbcnProcedures#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#35)]  
  
 [!code-vb[VbVbcnProcedures#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#36)]  
  
 [!code-vb[VbVbcnProcedures#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnProcedures/VB/Class1.vb#37)]  
  
 第一个 `MsgBox` 调用显示 "增加（n）：11，21，31，41" 之后的 "。 由于数组 `n` 是引用类型，因此 `replace` 可以更改其成员，即使传递机制是 `ByVal`的。  
  
 第二个 `MsgBox` 调用显示 "replace （n）：101，201，301" 后的 "。 由于 `n` 传递 `ByRef`，`replace` 可以修改调用代码中的变量 `n` 并向其分配新数组。 由于 `n` 是引用类型，`replace` 也可以更改其成员。  
  
 您可以防止过程在调用代码中修改变量本身。 请参阅[如何：针对值更改保护过程参数](./how-to-protect-a-procedure-argument-against-value-changes.md)。  
  
## <a name="compile-the-code"></a>编译代码  
 通过引用传递变量时，必须使用 `ByRef` 关键字来指定此机制。  
  
 Visual Basic 中的默认值是按值传递参数。 但是，将[ByVal](../../../../visual-basic/language-reference/modifiers/byval.md)或[ByRef](../../../../visual-basic/language-reference/modifiers/byref.md)关键字用于每个声明的参数是一种好的编程做法。 这使代码更易于阅读。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 允许过程更改调用代码中参数的基础值始终存在潜在风险。 请确保此值已更改，并在使用之前对其进行检查以确保其有效性。  
  
## <a name="see-also"></a>另请参阅

- [过程](./index.md)
- [过程参数和自变量](./procedure-parameters-and-arguments.md)
- [如何：将自变量传递给过程](./how-to-pass-arguments-to-a-procedure.md)
- [按值和按引用传递自变量](./passing-arguments-by-value-and-by-reference.md)
- [可修改和不可修改自变量之间的差异](./differences-between-modifiable-and-nonmodifiable-arguments.md)
- [通过值传递自变量和通过引用传递自变量之间的差异](./differences-between-passing-an-argument-by-value-and-by-reference.md)
- [如何：防止过程自变量的值被更改](./how-to-protect-a-procedure-argument-against-value-changes.md)
- [如何：强制通过值传递自变量](./how-to-force-an-argument-to-be-passed-by-value.md)
- [按位置和按名称传递自变量](./passing-arguments-by-position-and-by-name.md)
- [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
