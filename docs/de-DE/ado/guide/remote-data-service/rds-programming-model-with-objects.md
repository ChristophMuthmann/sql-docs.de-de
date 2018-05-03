---
title: RDS-Programmiermodell mit Objekten | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS programming model [ADO]
- RDS objects [ADO]
ms.assetid: 07ce0ef0-72f1-48f4-823d-1b65d28c0926
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a7e49e00e63ceb330f0da1779ad810516d6a78b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="rds-programming-model-with-objects"></a>RDS-Programmiermodell mit Objekten
Das Ziel von RDS ist, erhalten Zugriff auf und Aktualisieren von Datenquellen über einen Mittler wie z. B. IIS. Das Programmiermodell gibt die Abfolge von Aktivitäten, die zu diesem Zweck erforderlich. Das Objektmodell gibt die Objekte, deren Methoden und Eigenschaften über das Programmiermodell auswirken.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS bietet die Möglichkeit, die folgende Sequenz von Aktionen ausführen:  
  
-   Geben Sie das Programm, auf dem Server aufgerufen werden soll, und ermitteln Sie eine Möglichkeit (Proxy) vom Client darauf verweisen ([RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)).  
  
-   Rufen Sie die Server-Anwendung. Übergeben von Parametern an die Server-Anwendung, die die Datenquelle und den Befehl zum Ausstellen identifiziert (Proxy oder [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)).  
  
-   Die Server-Anwendung erhält einen [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekt aus der Datenquelle, in der Regel mithilfe von ADO. Optional, die **Recordset** Objekt wird auf dem Server verarbeitet ([RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)).  
  
-   Des Programms gibt den endgültigen **Recordset** Objekt an die Clientanwendung (Proxy).  
  
-   Auf dem Client die **Recordset** Objekt abgelegt eines Formulars, das einfach durch visuelle Steuerelemente verwendet werden kann (visual-Steuerelement und **RDS. DataControl**).  
  
-   Änderungen an der **Recordset** Objekt an den Server gesendet und zum Aktualisieren der Datenquelle verwendet werden (**RDS. DataControl** oder **RDSServer.DataFactory**).  
  
## <a name="see-also"></a>Siehe auch  
 [Zusammenfassung für RDS-Objekt](../../../ado/guide/remote-data-service/rds-object-model-summary.md)   
 [RDS (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)   
 [DataSpace-Objekt (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)   
 [RDS-Szenario](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [RDS-Lernprogramm](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Verwendung und Sicherheit von RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


