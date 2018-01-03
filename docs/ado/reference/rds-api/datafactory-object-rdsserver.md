---
title: DataFactory-Objekt (RDSServer) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: DataFactory object [ADO]
ms.assetid: e75240c2-b749-471e-b6ea-98cae232efbe
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3a29e823d4be1fdb878b709116ec5feea525f70f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="datafactory-object-rdsserver"></a>DataFactory-Objekt (RDSServer)
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Diese serverseitige Business-Standardobjekt implementiert Methoden, die Lese-/Schreibzugriff Datenzugriff mit angegebenen Datenquellen für clientseitige Anwendungen bereitstellen.  
  
 Die **RDSServer.DataFactory** Objekt dient als serverseitige Automatisierungsobjekt, der Clientanforderungen empfängt. In einer Internet-Implementierung befindet sich auf einem Webserver, und es wird von der Komponente ADISAPI instanziiert. Die **RDSServer.DataFactory** Objekt stellt Lesezugriff und Schreibzugriff auf die angegebenen Daten Datenquellen, aber enthält keine Validierung oder Regeln die Geschäftslogik.  
  
 Wenn Sie eine Methode verwenden, die sowohl in der **RDSServer.DataFactory** und [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekte aufweist, Remote Data Service verwendet die **RDS. DataControl** Version standardmäßig. Die Standardeinstellung wird angenommen, ein grundlegendes Programmiermodells Szenario, in dem die **RDSServer.DataFactory** dient als ein generischer serverseitige Geschäftsobjekt.  
  
 Wenn Sie Ihre Webanwendung aufgabenspezifischen serverseitige Verarbeitung behandeln möchten, können Sie ersetzen die **RDSServer.DataFactory** mit der ein benutzerdefiniertes Geschäftsobjekt.  
  
 Serverseitige Geschäftsobjekte, die aufgerufen werden können die **RDSServer.DataFactory** Methoden, wie z. B. [Abfrage](../../../ado/reference/rds-api/query-method-rds.md) und [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md). Dies ist hilfreich, wenn Sie Ihre Geschäftsobjekte Funktionalität hinzufügen, aber vorhandene Remote Data Service-Technologie nutzen möchten.  
  
 Die **DataFactory** Objekt ist nicht sicher für Skripts, die auf der Clientseite ausgeführt.  
  
 Die Klassen-ID für die **RDSServer.DataFactory** Objekt ist 9381D8F5-0288-11-D 0-9501-00AA00B911A5.  
  
 Dieser Abschnitt enthält das folgende Thema.  
  
-   [DataFactory-Objekt (RDSServer) – Eigenschaften, Methoden und Ereignisse](../../../ado/reference/rds-api/datafactory-object-rdsserver-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataFactory-Objekt, Abfragemethode und CreateObject-Methode – Beispiel (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


