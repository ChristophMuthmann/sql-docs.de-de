---
title: OLE DB-Treiber für SQL Server-Programmierung | Microsoft Docs
description: OLE DB-Treiber für SQL Server-Programmierung
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1a3d642eb3cef1f9f01accd8b50f571f5e4903ac
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server-programming"></a>OLE DB-Treiber für SQL Server-Programmierung
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB-Treiber für SQL Server ist eine eigenständige Zugriff Anwendungsprogrammierschnittstelle (API), verwendet für OLE DB, das in eingeführte [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. OLE DB-Treiber für SQL Server bietet die SQL OLE DB-Treiber in einer Dynamic Link Library (DLL). Sie stellt auch neue Funktionen bereit, die weit über die von Windows Data Access Components (Windows DAC, früher Microsoft Data Access Components oder MDAC genannt) bereitgestellten Funktionalität hinausgehen. OLE DB-Treiber für SQL Server kann verwendet werden, um die Erstellung neuer Anwendungen oder zur Verbesserung vorhandener Anwendungen, die in eingeführte Funktionen nutzen müssen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], z. B. mehrere aktive Resultsets (MARS), benutzerdefinierte Datentypen (UDT), Abfrage Unterstützung von Benachrichtigungen, Snapshot-Isolation und XML-Datentyp.  
  
> [!NOTE]  
>  Eine Übersicht über die Unterschiede zwischen OLE DB-Treiber für SQL Server und Windows DAC sowie Informationen zu Problemen, berücksichtigen Sie vor dem Aktualisieren einer Windows DAC-Anwendung in OLE DB-Treiber für SQL Server finden Sie unter [Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQL Server von MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 Der OLE DB-Treiber für SQL Server kann in Verbindung mit OLE DB-Basisdiensten von Windows DAC verwendet werden, aber dies ist nicht erforderlich; die Entscheidung, Basisdienste oder nicht verwenden, hängt von den Anforderungen der jeweiligen Anwendung ab (z. B., wenn Verbindungspooling erforderlich ist).  
  
 ActiveX Data Object (ADO)-Anwendungen können den OLE DB-Treiber für SQL Server verwenden, aber es wird empfohlen, das Verwenden von ADO in Verbindung mit der **DataTypeCompatibility** Schlüsselwort für Verbindungszeichenfolgen (bzw. der zugehörigen  **DataSource** Eigenschaft). Wenn der OLE DB-Treiber für SQL Server verwenden, ADO-Anwendungen nutzen, die diese neuen Funktionen in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , die über den OLE DB-Treiber für SQL Server über Verbindungszeichenfolgen-Schlüsselwörter oder OLE DB-Eigenschaften verfügbar sind oder [!INCLUDE[tsql](../../includes/tsql-md.md)]. Weitere Informationen zur Verwendung dieser Funktionen mit ADO finden Sie unter [mithilfe von ADO mit OLE DB-Treiber für SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 OLE DB-Treiber für SQL Server wurde entwickelt, um eine einfache Methode für den systemeigenen Datenzugriff auf SQL Server mithilfe von OLE DB-bereitzustellen. Es bietet eine Möglichkeit, Innovationsbereitschaft optimieren und weiterzuentwickeln Datenzugriffsfunktionen ohne Änderung der aktuellen Windows DAC-Komponenten, die jetzt Teil der Microsoft Windows-Plattform sind.  
  
 Während der OLE DB-Treiber für SQL Server-Komponenten in Windows DAC verwendet wird, ist es nicht explizit auf eine bestimmte Version von Windows DAC abhängig. Sie können den OLE DB-Treiber für SQL Server mit der Version von Windows DAC verwenden, die mit der vom OLE DB-Treiber für SQL Server unterstützten Betriebssystem installiert ist.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [OLE DB-Treiber für SQLServer](../oledb/oledb-driver-for-sql-server.md)  
 Listet die bedeutende neue OLE DB-Treiber für SQL Server-Funktionen.  
  
 [Verwendung von OLE DB-Treiber für SQLServer](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server mit Microsoft Data Access Technologies, harmoniert wie es gegenüber Windows DAC und ADO.NET bestehen, und bietet Entscheidungshilfen für die Entscheidung der Datenzugriff Technologie zu verwenden.  
  
 [OLE DB-Treiber für SQL Server-Funktionen](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Beschreibt die Funktionen von OLE DB-Treiber für SQL Server unterstützt.  
  
 [Erstellen von Anwendungen mit OLE DB-Treiber für SQLServer](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Bietet einen Überblick über die OLE DB-Treiber für SQL Server-Anwendungsentwicklung, einschließlich, wie sie gegenüber Windows DAC, die Komponenten unterscheiden, die verwendet werden, und mit ihm ADO verwendet werden kann.  
  
 Dieser Abschnitt beschreibt auch die OLE DB-Treiber für SQL Server-Installation und Bereitstellung, einschließlich der weiterverteilung der OLE DB-Treiber für SQL Server-Bibliothek.  
  
 [Systemanforderungen für OLE DB-Treiber für SQLServer](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Erläutert, die die Systemressourcen für die Verwendung von OLE DB-Treiber für SQL Server erforderlich.  
  
 [OLE DB-Treiber für SQLServer &#40;OLE DB&#41;](../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
 Enthält Informationen zur Verwendung von OLE DB-Treiber für SQL Server.  
  
 [Suchen von Weitere OLE DB-Treiber für SQL Server-Informationen](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Stellt zusätzliche Ressourcen zum OLE DB-Treiber für SQL Server, einschließlich Links zu externen Ressourcen und Weitere Informationsquellen bereit.  
  
  
## <a name="see-also"></a>Siehe auch  
 [Aktualisieren einer Anwendung von SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB-Themen zur Vorgehensweise](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
