---
title: OLE DB-Anbieter (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
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
ms.assetid: 6e0488c3-934d-4976-99dc-65c580dc7a3c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8ef1c85f55928c266fb88f1639d5ccd53450fe59
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ole-db-providers-ado"></a>OLE DB-Anbieter (ADO)
OLE DB definiert einen Satz von COM-Schnittstellen für Anwendungen mit einheitlichen Zugriff auf Daten bereitzustellen, die in verschiedenen Datenquellen gespeichert sind. Dieser Ansatz ermöglicht eine Datenquelle, die Daten über die Schnittstellen freizugeben, die Menge des DBMS-Funktionen, die die Datenquelle zu unterstützen. Programmbedingt die hohe Leistung Architektur von OLE DB Verwendungsmöglichkeiten eines Modells für flexible und komponentenbasierter Services basiert. Anstatt eine vorgegebene Anzahl von Zwischenkomponenten zwischen der Anwendung und die Daten erfordert OLE DB-nur, wenn viele Komponenten, wie die an eine bestimmte Aufgabe auszuführen.  
  
 Nehmen wir beispielsweise an, dass ein Benutzer möchte zum Ausführen einer Abfrage. Betrachten Sie die folgenden Szenarien:  
  
-   Die Daten befinden sich in einer relationalen Datenbank, die für die derzeit vorhanden ist, aber keine systemeigenen OLE DB-Anbieter einen ODBC-Treiber: die Anwendung verwendet ADO, um die Kommunikation mit der OLE DB-Anbieter für ODBC, der dann den entsprechenden ODBC-Treiber geladen. Der Treiber übergibt die SQL-Anweisung an das DBMS an, das die Daten abruft.  
  
-   Die Daten befinden sich im Microsoft SQL Server ein systemeigenen OLE DB-Anbieter vorhanden ist: die Anwendung verwendet ADO, um direkt mit der OLE DB-Anbieter für Microsoft SQL Server kommunizieren. Es sind keine Zwischenkomponenten erforderlich.  
  
-   Die Daten befinden sich im Microsoft Exchange-Server für die OLE DB-Anbieter vorhanden ist, aber ein Modul zum Verarbeiten von SQL-Abfragen nicht offen: die Anwendung verwendet ADO, um die Kommunikation mit der OLE DB-Anbieter für Microsoft Exchange und ruft bei einem OLE DB-Abfrageprozessor die Komponente zum Verarbeiten der Abfragen.  
  
-   Die Daten befinden sich im Microsoft-NTFS-Dateisystem in Form von Dokumenten: Daten erfolgt über einen systemeigenen OLE DB-Anbieter für Microsoft Indexdienst, der indiziert den Inhalt und die Eigenschaften von Dokumenten in das Dateisystem auf effiziente Inhalte zu ermöglichen sucht.  
  
 In den vorherigen Beispielen kann die Anwendung die Daten Abfragen. Der Benutzer-Anforderungen werden mit einer minimalen Anzahl von Komponenten erfüllt. In jedem Fall zusätzliche Komponenten werden verwendet, nur im Bedarfsfall, und nur die erforderlichen Komponenten werden aufgerufen. Diese bedarfsgesteuertes Laden von wiederverwendbaren und freigegeben Komponenten trägt erheblich zur hohe Leistung, wenn OLE DB verwendet wird.  
  
 Anbieter können zwei Kategorien zugeordnet: Bereitstellen von Daten und die Dienste bereitstellen. Ein Datenanbieter besitzt seine eigenen Daten und es in tabellarischer Form an Ihre Anwendung verfügbar gemacht. Ein Dienstanbieter kapselt einen Dienst durch erzeugen und Nutzen von Daten, Erweitern der Funktionen in den ADO-Anwendungen. Ein Dienstanbieter kann auch weiter als eine Dienstkomponente definiert, werden die in Verbindung mit anderen Dienstanbietern oder Komponenten arbeiten müssen.  
  
 ADO bietet eine einheitliche Schnittstelle auf die verschiedenen OLE DB-Anbieter hoher Ebene.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Datenanbieter](../../../ado/guide/data/data-providers.md)  
  
-   [Dienstanbieter und Komponenten](../../../ado/guide/data/service-providers-and-components.md)

