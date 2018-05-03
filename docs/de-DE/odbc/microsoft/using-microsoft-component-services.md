---
title: Mithilfe von Microsoft Komponentendienste | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c28df0cd6000a4ae0b2cb500a9521dc32facc6c9
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-microsoft-component-services"></a>Mithilfe der Microsoft Component Services
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Sie können eine Oracle-Datenbank mithilfe des transaktional Komponentendienste (oder MTS, bei Verwendung von Windows NT) unter Microsoft Windows NT/Windows 2000 und Microsoft Windows 95-und Windows 98. Zum Aktivieren einer Oracle-Datenbank mithilfe der Komponentendienste zu arbeiten, die Transaktionen unterstützen, sollten Systemadministratoren eine Sicht mit dem Namen V$ XATRANS$ erstellen. Um dieses Skript zu erstellen, müssen Sie ein Oracle bereitgestellte Skript ausführen. Weitere Informationen finden Sie in der Hilfe zu Component Services oder in der Oracle-Dokumentation.
