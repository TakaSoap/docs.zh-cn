---
ms.openlocfilehash: 0358450024607a985f38564ec9743ba964949e8f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2020
ms.locfileid: "67804435"
---
### <a name="clickonce-supports-sha-256-on-40-targeted-apps"></a>ClickOnce 支持面向 4.0 的应用上的 SHA-256

|   |   |
|---|---|
|详细信息|以前，如果 ClickOnce 应用具有使用 SHA-256 签名的证书，即使应用面向 4.0 版本，也需要 .NET Framework 4.5 或更高版本。 现在，即使使用 SHA-256 签名，面向 .NET Framework 4.0 的 ClickOnce 应用也可在 .NET Framework 4.0 上运行。|
|建议|此更改删除了该依赖项，允许将 SHA-256 证书用于为面向 .NET Framework 4 或更早版本的 ClickOnce 应用签名。|
|范围|次要|
|Version|4.6|
|类型|重定目标|
