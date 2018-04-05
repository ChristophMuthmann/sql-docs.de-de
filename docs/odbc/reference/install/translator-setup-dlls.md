---
title: Konvertierer Setup DLLs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3ce6961ec470bf0e0a7281a129d85f5cf69c9b80
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="translator-setup-dlls"></a>Konvertierer-Setup-DLLs
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Das Konvertierungsprogramm-Setup-DLL enthält die **ConfigTranslator** Funktion, die die Standardoption für ein Konvertierungsprogramm zurückgibt. Falls erforderlich, wird diese Informationen vom Benutzer zur Eingabe aufgefordert. Eine vollständige Beschreibung dieser Funktion, finden Sie unter [Setup DLL-API-Referenz](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 Das Konvertierungsprogramm-Setup wird vom Entwickler Konvertierer DLL geschrieben. Teil des Konvertierungsprogramms möglich DLL oder eine separate DLL.
