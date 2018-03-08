---
title: Dateien und Versionsnummern | Microsoft Docs
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: "34"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a23f5abd57fdf723382671b82d6078cbb2c7b8d5
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/12/2018
---
# <a name="files-and-version-numbers"></a>Dateien und Versionsnummern
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Alle erforderlichen Komponenten von SQL Server Management Object (SMO) in das Microsoft.SqlServer.SqlManagementObjects NuGet-Paket enthalten sind. SMO ist in mehreren verwalteten Assemblys implementiert. Sie können SMO-Anwendungen entweder auf einem Client oder auf einem Server entwickeln.  

>>[!Important]
Die Dateiversion der SMO-Assemblys wird als Hauptversion angezeigt. **0**. Build.Revision. Die eingebettete Assemblyversion ist Major jedoch. **100**. Build.Revision. Hierdurch wird die Version von SMO in jeder Anwendung verwendet werden, damit Updates auf einen keine Auswirkungen auf andere trennen.
>>
>>Aus diesem Grund sollten Sie **nicht** installieren Sie diese Versionen der Assemblys zum globalen Assemblycache (GAC). Auf diese Weise kann bewirken, dass andere Anwendungen, wie z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, unterbrochen. 
  
|File|Description|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Unterstützt das Herstellen von Verbindungen mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Unterstützt die Programmierung des [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Dies ist nur in Programmen erforderlich, die auf Service Broker zugreifen.|  
|Microsoft.SqlServer.Smo.dll|Enthält einen Großteil der SMO-Klassen.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Unterstützt die SMO-Klassen.|  
|Microsoft.SqlServer.WmiEnum.dll|Enthält die WMI-Anbieterklassen (Windows Management Instrumentation, Windows-Verwaltungsinstrumentation). Dies ist nur für Programme erforderlich, die die WMI-Anbieterklassen verwenden.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Enthält die Klassen, die den registrierten Server darstellen. Dies ist nur für Programme erforderlich, die die Klassen für den registrierten Server enthalten.|  
  
  
