---
title: 'Internet-Serverfehler: Zugriff verweigert. | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad54a40b51084bbf17c754521d914e08222408bb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="internet-server-error-access-denied"></a>Internet-Serverfehler: Zugriff verweigert
Wenn Sie diesen Fehler erhalten, bedeutet dies normalerweise, dass Microsoft Internet Information Services (IIS) die folgenden Status zurückgegeben:  
  
 HTTP_STATUS_DENIED 401  
  
 Stellen Sie sicher, dass die erforderlichen Berechtigungen verfügen, die Verzeichnisse, die von IIS zugegriffen. RDS mit IIS-Webserver ausgeführt wird, in einem der drei Modi Kennwortauthentifizierung kommunizieren kann: anonym, Basic oder NT Challenge/Response (integrierte Windows-Authentifizierung in Windows 2000 genannt). Darüber hinaus benötigt der Webserver auf dem Quellcomputer Daten Berechtigungen ist ein Computer unter Windows NT, Windows 2000.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)




