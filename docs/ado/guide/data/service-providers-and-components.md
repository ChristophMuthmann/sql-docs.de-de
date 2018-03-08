---
title: Service-Anbieter und -Komponenten | Microsoft Docs
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
- OLE DB providers [ADO]
- ADO, OLE DB providers
- service providers [ADO]
ms.assetid: 1fd7a374-587b-4ca9-9204-3a4019b67a71
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97e738fb4f5bd4635a8a53a87d000b72736edc5d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="service-providers-and-components"></a>Dienstanbieter und Komponenten
Dienstanbieter sind Komponenten, die die Funktionalität von Datenanbietern erweitern, indem implementieren die erweiterten Schnittstellen, die vom Datenspeicher nicht systemeigen unterstützt werden.  
  
 Universal Data Access enthält ein *Komponentenarchitektur* einzelne, spezielle Komponenten zum Implementieren der separate Sätze von Datenbankfunktionen oder "Dienste", über weniger leistungsfähige speichert ermöglicht. Daher geben Sie Dienstkomponenten anstatt das Erzwingen eines jeden Datenspeicher, um eine eigene Implementierung der erweiterten Funktionen bereitzustellen, oder durch das Erzwingen des allgemeiner Anwendungen, die intern zu implementieren, eine verbreitete Implementierung, die jede Anwendung kann Verwenden Sie, wenn Sie einen beliebigen Datenspeicher zugreifen. Die Tatsache, dass einige Funktionen systemintern durch den Datenspeicher und durch allgemeine Komponenten implementiert wird, ist für die Anwendung transparent.  
  
 Angenommen, ein Cursor Modul, wie z. B. [des Cursordiensts für OLE DB-](http://msdn.microsoft.com/en-us/57638feb-4ecd-4051-becb-8f828d21cf44), ist eine Dienstkomponente, die Daten aus einem sequenziellen, Vorwärtscursor Datenspeicher bildlauffähige Daten erstellt nutzen kann. Andere häufig verwendete ADO Dienstanbieter umfassen die [Microsoft OLE DB-Anbieter für Persistenz (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md) (zum Speichern von Daten in eine Datei), die [Microsoft-Datenstrukturierungsdiensts für OLE DB (ADO-Dienstanbieter) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (für hierarchische **Recordsets**), und die [Microsoft OLE DB-Anbieter für Remoting (ADO-Dienstanbieter)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md) (zum Aufrufen von Datenanbieter auf einem Remotecomputer befindet).  
  
 Weitere Informationen zum Dienst und Datenanbieter finden Sie unter [Anhang A: Anbieter](../../../ado/guide/appendixes/appendix-a-providers.md).
