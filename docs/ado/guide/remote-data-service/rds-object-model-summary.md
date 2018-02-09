---
title: Zusammenfassung der RDS-Objekt | Microsoft Docs
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
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9423b2f6072f142336e1f36f02785b69f9efdae6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="rds-object-model-summary"></a>Zusammenfassung für RDS-Objekt
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Objekt|Description|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|Dieses Objekt enthält eine Methode zum Abrufen eines Proxys für Server. Der Proxy möglicherweise der Standard- oder ein benutzerdefiniertes Serverprogramm (Business-Objekt). Des Programms werden von einem lokalen Dynamic Link Library oder auf das Internet, Intranet, ein lokales Netzwerk initiiert werden kann.<br /><br /> Die **DataSpace** Objekt für die Skripterstellung sicher ist.|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Dieses Objekt stellt das Standardprogramm für den Server dar. Dadurch wird das RDS Daten abrufen und aktualisieren Standardverhalten ausgeführt.<br /><br /> Die **DataFactory** Objekt ist nicht sicher für Skripting.|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Dieses Objekt kann automatisch Aufrufen der **RDS. DataSpace** und **RDSServer.DataFactory** Objekte.<br /><br /> Verwenden Sie dieses Objekt, um die standardmäßige Verhalten von RDS-Daten abrufen "oder" Update aufzurufen.<br /><br /> Dieses Objekt stellt auch die notwendigen Mittel zum visuelle Steuerelemente auf das zurückgegebene **Recordset** Objekt.<br /><br /> Die **DataControl** Objekt für die Skripterstellung sicher ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [RDS-Grundlagen](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [RDS-Szenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Verwendung und Sicherheit von RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


