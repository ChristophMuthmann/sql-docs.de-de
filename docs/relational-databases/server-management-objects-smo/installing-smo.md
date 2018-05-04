---
title: Installieren von SMO | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.prod_service: database-engine
ms.component: smo
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- installing SMO
- SMO [SQL Server], installing
- SQL Server Management Objects, installing
ms.assetid: 140e9971-4940-4866-89b9-5cec938e2a16
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 125712a02b362a49902c9f1e2422414f059864ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
#<a name="installing-smo"></a>Installieren von SMO

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Diese Seite enthält Informationen zum Installieren von SMO für die Verwendung von Anwendungen und die systemvoraussetzungen für SMO verwenden.

## <a name="smo-nuget-package"></a>SMO-NuGet-Paket

Beginnend mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 SMO wird als verteilt die [Microsoft.SqlServer.SqlManagementObjects](https://www.nuget.org/packages/Microsoft.SqlServer.SqlManagementObjects) NuGet-Paket, um Benutzern das Entwickeln von Anwendungen mit SMO ermöglichen.

Dies ist ein Ersatz für SharedManagementObjects.msi, die zuvor als Teil des SQL-Feature Pack für jede Version von SQL Server veröffentlicht wurde. Anwendungen, die SMO verwenden sollte aktualisiert werden, um stattdessen verwenden Sie das NuGet-Paket und ist zuständig für das sicherstellen, dass die Binärdateien installiert sind, mit der Anwendung entwickelt wird.

>>[!Important]
>>Wie erwähnt die [Dateien und Versionsnummern](files-and-version-numbers.md) Seite, Sie sollten nicht die SMO-Assemblys im globalen Assemblycache installieren. Auf diese Weise kann dazu führen, dass Probleme mit anderen Anwendungen, die auch diese Versionen von SMO verwenden (z. B. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio).

##<a name="installing-the-package"></a>Installieren des Pakets

Finden Sie unter [NuGet-Schnellstart - Verwenden eines Pakets](https://docs.microsoft.com/en-us/nuget/quickstart/use-a-package) Anweisungen und Beispiele der installieren und Verwenden von NuGet-Paket. 
  
## <a name="system-requirements"></a>Systemanforderungen
  
 SMO erfordert [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.0 ausgeführt wird, damit alle Anwendungen verwenden, sicherstellen, dass müssen Clientcomputer installiert haben, dass Version oder höher installiert.
  
