---
title: Mithilfe von Microsoft Komponentendienste | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc193620497eccd11c609d5bc4b9861b33576941
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="using-microsoft-component-services"></a>Mithilfe der Microsoft Component Services
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Sie können eine Oracle-Datenbank mithilfe des transaktional Komponentendienste (oder MTS, bei Verwendung von Windows NT) unter Microsoft Windows NT/Windows 2000 und Microsoft Windows 95-und Windows 98. Zum Aktivieren einer Oracle-Datenbank mithilfe der Komponentendienste zu arbeiten, die Transaktionen unterstützen, sollten Systemadministratoren eine Sicht mit dem Namen V$ XATRANS$ erstellen. Um dieses Skript zu erstellen, müssen Sie ein Oracle bereitgestellte Skript ausführen. Weitere Informationen finden Sie in der Hilfe zu Component Services oder in der Oracle-Dokumentation.
