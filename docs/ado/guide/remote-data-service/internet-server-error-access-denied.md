---
title: 'Internet-Serverfehler: Zugriff verweigert. | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8d5dd778ab543b719f44334bc2d344a38964e05f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="internet-server-error-access-denied"></a>Internet-Serverfehler: Zugriff verweigert
Wenn Sie diesen Fehler erhalten, bedeutet dies normalerweise, dass Microsoft Internet Information Services (IIS) die folgenden Status zurückgegeben:  
  
 HTTP_STATUS_DENIED 401  
  
 Stellen Sie sicher, dass die erforderlichen Berechtigungen verfügen, die Verzeichnisse, die von IIS zugegriffen. RDS mit IIS-Webserver ausgeführt wird, in einem der drei Modi Kennwortauthentifizierung kommunizieren kann: anonym, Basic oder NT Challenge/Response (integrierte Windows-Authentifizierung in Windows 2000 genannt). Darüber hinaus benötigt der Webserver auf dem Quellcomputer Daten Berechtigungen ist ein Computer unter Windows NT, Windows 2000.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




