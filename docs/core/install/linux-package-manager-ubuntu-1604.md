---
title: 在 Ubuntu 16.04 包管理器上安装 .NET Core - .NET Core
description: 使用包管理器在 Ubuntu 16.04 上安装 .NET Core SDK 和运行时。
author: thraka
ms.author: adegeo
ms.date: 12/04/2019
ms.openlocfilehash: 77033e327349e7543148dab27f7229c69de4aa1c
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2019
ms.locfileid: "74999055"
---
# <a name="ubuntu-1604-package-manager---install-net-core"></a><span data-ttu-id="b1d50-103">Ubuntu 16.04 包管理器 - 安装 .NET Core</span><span class="sxs-lookup"><span data-stu-id="b1d50-103">Ubuntu 16.04 Package Manager - Install .NET Core</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-switcher.md)]

<span data-ttu-id="b1d50-104">本文介绍如何使用包管理器在 Ubuntu 16.04 上安装 .NET Core。</span><span class="sxs-lookup"><span data-stu-id="b1d50-104">This article describes how to use a package manager to install .NET Core on Ubuntu 16.04.</span></span> <span data-ttu-id="b1d50-105">如果要安装该运行时，建议安装 [ASP.NET Core 运行时](#install-the-aspnet-core-runtime)，因为它同时包括 .NET Core 和 ASP.NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="b1d50-105">If you're installing the runtime, we suggest you install the [ASP.NET Core runtime](#install-the-aspnet-core-runtime), as it includes both .NET Core and ASP.NET Core runtimes.</span></span>

## <a name="register-microsoft-key-and-feed"></a><span data-ttu-id="b1d50-106">注册 Microsoft 密钥和源</span><span class="sxs-lookup"><span data-stu-id="b1d50-106">Register Microsoft key and feed</span></span>

<span data-ttu-id="b1d50-107">安装 .NET 之前，需要：</span><span class="sxs-lookup"><span data-stu-id="b1d50-107">Before installing .NET, you'll need to:</span></span>

- <span data-ttu-id="b1d50-108">注册 Microsoft 密钥</span><span class="sxs-lookup"><span data-stu-id="b1d50-108">Register the Microsoft key</span></span>
- <span data-ttu-id="b1d50-109">注册产品存储库</span><span class="sxs-lookup"><span data-stu-id="b1d50-109">register the product repository</span></span>
- <span data-ttu-id="b1d50-110">安装必需的依赖项</span><span class="sxs-lookup"><span data-stu-id="b1d50-110">Install required dependencies</span></span>

<span data-ttu-id="b1d50-111">每台计算机只需要执行一次此操作。</span><span class="sxs-lookup"><span data-stu-id="b1d50-111">This only needs to be done once per machine.</span></span>

<span data-ttu-id="b1d50-112">打开终端并运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="b1d50-112">Open a terminal and run the following commands.</span></span>

```bash
wget -q https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-core-sdk"></a><span data-ttu-id="b1d50-113">安装 .NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="b1d50-113">Install the .NET Core SDK</span></span>

<span data-ttu-id="b1d50-114">更新可供安装的产品，然后安装 .NET Core SDK。</span><span class="sxs-lookup"><span data-stu-id="b1d50-114">Update the products available for installation, then install the .NET Core SDK.</span></span> <span data-ttu-id="b1d50-115">在终端中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="b1d50-115">In your terminal, run the following commands.</span></span>

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-3.1
```

> [!IMPORTANT]
> <span data-ttu-id="b1d50-116">如果收到类似于“找不到包 dotnet-sdk-3.1”  的错误消息，请参阅[包管理器疑难解答](#troubleshoot-the-package-manager)部分。</span><span class="sxs-lookup"><span data-stu-id="b1d50-116">If you receive an error message similar to **Unable to locate package dotnet-sdk-3.1**, see the [Troubleshoot the package manager](#troubleshoot-the-package-manager) section.</span></span>

## <a name="install-the-aspnet-core-runtime"></a><span data-ttu-id="b1d50-117">安装 ASP.NET Core 运行时</span><span class="sxs-lookup"><span data-stu-id="b1d50-117">Install the ASP.NET Core runtime</span></span>

<span data-ttu-id="b1d50-118">更新可供安装的产品，然后安装 ASP.NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="b1d50-118">Update the products available for installation, then install the ASP.NET Core runtime.</span></span> <span data-ttu-id="b1d50-119">在终端中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="b1d50-119">In your terminal, run the following commands.</span></span>

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install aspnetcore-runtime-3.1
```

> [!IMPORTANT]
> <span data-ttu-id="b1d50-120">如果收到类似于“找不到包 aspnetcore-runtime-3.1”  的错误消息，请参阅[包管理器疑难解答](#troubleshoot-the-package-manager)部分。</span><span class="sxs-lookup"><span data-stu-id="b1d50-120">If you receive an error message similar to **Unable to locate package aspnetcore-runtime-3.1**, see the [Troubleshoot the package manager](#troubleshoot-the-package-manager) section.</span></span>

## <a name="install-the-net-core-runtime"></a><span data-ttu-id="b1d50-121">安装 .NET Core 运行时</span><span class="sxs-lookup"><span data-stu-id="b1d50-121">Install the .NET Core runtime</span></span>

<span data-ttu-id="b1d50-122">更新可供安装的产品，然后安装 .NET Core 运行时。</span><span class="sxs-lookup"><span data-stu-id="b1d50-122">Update the products available for installation, then install the .NET Core runtime.</span></span> <span data-ttu-id="b1d50-123">在终端中，运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="b1d50-123">In your terminal, run the following commands.</span></span>

```bash
sudo apt-get update
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-runtime-3.1
```

> [!IMPORTANT]
> <span data-ttu-id="b1d50-124">如果收到类似于“找不到包 dotnet-runtime-3.1”  的错误消息，请参阅[包管理器疑难解答](#troubleshoot-the-package-manager)部分。</span><span class="sxs-lookup"><span data-stu-id="b1d50-124">If you receive an error message similar to **Unable to locate package dotnet-runtime-3.1**, see the [Troubleshoot the package manager](#troubleshoot-the-package-manager) section.</span></span>

## <a name="how-to-install-other-versions"></a><span data-ttu-id="b1d50-125">如何安装其他版本</span><span class="sxs-lookup"><span data-stu-id="b1d50-125">How to install other versions</span></span>

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a><span data-ttu-id="b1d50-126">包管理器疑难解答</span><span class="sxs-lookup"><span data-stu-id="b1d50-126">Troubleshoot the package manager</span></span>

<span data-ttu-id="b1d50-127">如果收到类似于“找不到包 {.NET Core 包}”  的错误消息，请运行以下命令。</span><span class="sxs-lookup"><span data-stu-id="b1d50-127">If you receive an error message similar to **Unable to locate package {the .NET Core package}**, run the following commands.</span></span>

```bash
sudo dpkg --purge packages-microsoft-prod && sudo dpkg -i packages-microsoft-prod.deb
sudo apt-get update
sudo apt-get install {the .NET Core package}
```

<span data-ttu-id="b1d50-128">如果这不起作用，可使用以下命令运行手动安装。</span><span class="sxs-lookup"><span data-stu-id="b1d50-128">If that doesn't work, you can run a manual install with the following commands.</span></span>

```bash
sudo apt-get install -y gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget -q https://packages.microsoft.com/config/ubuntu/16.04/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
sudo apt-get install -y apt-transport-https
sudo apt-get update
sudo apt-get install {the .NET Core package}
```