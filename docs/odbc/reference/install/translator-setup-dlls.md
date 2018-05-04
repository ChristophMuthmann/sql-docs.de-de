---
title: Konvertierer Setup DLLs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2aabec831ba9b623a24f261551684e9bb259e24
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="translator-setup-dlls"></a>Konvertierer-Setup-DLLs
> [!NOTE]  
>  Ab Windows XP und Windows Server 2003, ist ODBC in der Windows-Betriebssystem enthalten. Sie sollten nur explizit ODBC in früheren Versionen von Windows installieren.  
  
 Das Konvertierungsprogramm-Setup-DLL enthält die **ConfigTranslator** Funktion, die die Standardoption für ein Konvertierungsprogramm zurückgibt. Falls erforderlich, wird diese Informationen vom Benutzer zur Eingabe aufgefordert. Eine vollständige Beschreibung dieser Funktion, finden Sie unter [Setup DLL-API-Referenz](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 Das Konvertierungsprogramm-Setup wird vom Entwickler Konvertierer DLL geschrieben. Teil des Konvertierungsprogramms möglich DLL oder eine separate DLL.
