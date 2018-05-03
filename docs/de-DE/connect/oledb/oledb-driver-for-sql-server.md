---
title: OLE DB-Treiber für SQLServer | Microsoft Docs
description: OLE DB-Treiber für SQLServer
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
manager: craigg
ms.openlocfilehash: 30ca6b7e894482aa2a94c778cc44bfcbba2a759e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQLServer
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB-Treiber für SQL Server ist eine eigenständige Zugriff Anwendungsprogrammierschnittstelle (API), verwendet für OLE DB, das in eingeführte [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. OLE DB-Treiber für SQL Server bietet die SQL OLE DB-Treiber in einer Dynamic Link Library (DLL). Sie stellt auch neue Funktionen bereit, die weit über die von Windows Data Access Components (Windows DAC, früher Microsoft Data Access Components oder MDAC genannt) bereitgestellten Funktionalität hinausgehen. OLE DB-Treiber für SQL Server kann verwendet werden, um die Erstellung neuer Anwendungen oder zur Verbesserung vorhandener Anwendungen, die in eingeführte Funktionen nutzen müssen [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], z. B. mehrere aktive Resultsets (MARS), benutzerdefinierte Datentypen (UDT), Abfrage Unterstützung von Benachrichtigungen, Snapshot-Isolation und XML-Datentyp.  
  
> [!NOTE]  
>  Eine Übersicht über die Unterschiede zwischen OLE DB-Treiber für SQL Server und Windows DAC sowie Informationen zu Problemen, berücksichtigen Sie vor dem Aktualisieren einer Windows DAC-Anwendung in OLE DB-Treiber für SQL Server finden Sie unter [Aktualisieren von einer Anwendung auf OLE DB-Treiber für SQL Server von MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 Der OLE DB-Treiber für SQL Server kann in Verbindung mit OLE DB-Basisdiensten von Windows DAC verwendet werden, aber dies ist nicht erforderlich; die Entscheidung, Basisdienste oder nicht verwenden, hängt von den Anforderungen der jeweiligen Anwendung ab (z. B., wenn Verbindungspooling erforderlich ist).  
  
 ActiveX Data Object (ADO)-Anwendungen können den OLE DB-Treiber für SQL Server verwenden, aber es wird empfohlen, das Verwenden von ADO in Verbindung mit der **DataTypeCompatibility** Schlüsselwort für Verbindungszeichenfolgen (bzw. der zugehörigen  **DataSource** Eigenschaft). Wenn der OLE DB-Treiber für SQL Server verwenden, ADO-Anwendungen nutzen, die diese neuen Funktionen in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , die über den OLE DB-Treiber für SQL Server über Verbindungszeichenfolgen-Schlüsselwörter oder OLE DB-Eigenschaften verfügbar sind oder [!INCLUDE[tsql](../../includes/tsql-md.md)]. Weitere Informationen zur Verwendung dieser Funktionen mit ADO finden Sie unter [mithilfe von ADO mit OLE DB-Treiber für SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 OLE DB-Treiber für SQL Server wurde entwickelt, um eine einfache Methode für den systemeigenen Datenzugriff auf SQL Server mithilfe von OLE DB-bereitzustellen. Es bietet eine Möglichkeit, Innovationsbereitschaft optimieren und weiterzuentwickeln Datenzugriffsfunktionen ohne Änderung der aktuellen Windows DAC-Komponenten, die jetzt Teil der Microsoft Windows-Plattform sind.  
  
 Während der OLE DB-Treiber für SQL Server-Komponenten in Windows DAC verwendet wird, ist es nicht explizit auf eine bestimmte Version von Windows DAC abhängig. Sie können den OLE DB-Treiber für SQL Server mit der Version von Windows DAC verwenden, die mit der vom OLE DB-Treiber für SQL Server unterstützten Betriebssystem installiert ist.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Verschiedene Generationen von OLE DB-Treiber

Es gibt drei verschiedene Generationen von Microsoft OLE DB-Anbieter für SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Microsoft OLE DB-Anbieter für SQLServer (SQLOLEDB)
Die [Microsoft OLE DB-Anbieter für SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) noch geliefert wird, im Rahmen des [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). Sie wird nicht mehr verwaltet, und es wird nicht empfohlen, diesen Treiber für neue Entwicklungen verwenden.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) enthält eine OLE DB-Provider-Schnittstelle (SQLNCLI) und ist der OLE DB-Anbieter, die im Lieferumfang [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] über [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Es wurde [angekündigt, sobald in 2011 veraltet](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) und es wird nicht empfohlen, diesen Treiber für neue Entwicklungen verwenden. Weitere Informationen zu den SNAC-Lebenszyklus und die verfügbaren Downloads, finden Sie unter [SNAC-Lebenszyklus erklärt](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Microsoft OLE DB-Treiber für SQLServer (MSOLEDBSQL)
Wurde von OLE DB- [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) und in 2018 veröffentlicht wurden.

Die neue OLE DB-Anbieter wird der Microsoft OLE DB-Treiber für SQL Server (MSOLEDBSQL) aufgerufen. Der neue Anbieter wird mit den neuesten Server-Funktionen, die zukünftig aktualisiert werden.

> [!NOTE]
> Um die neue Microsoft OLE DB-Treiber für SQL Server in vorhandene Anwendungen zu verwenden, sollten Sie planen, die Verbindungszeichenfolgen von SQLOLEDB oder SQLNCLI, in MSOLEDBSQL zu konvertieren.
  
## <a name="in-this-section"></a>In diesem Abschnitt  
[Verwendung des OLE DB-Treibers für SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Erläutert, wie OLE DB-Treiber für SQL Server mit Microsoft Data Access Technologies, harmoniert wie es gegenüber Windows DAC und ADO.NET bestehen, und bietet Entscheidungshilfen für die Entscheidung der Datenzugriff Technologie zu verwenden.  
  
 [OLE DB-Treiber für SQL Server-Features](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Beschreibt die Funktionen von OLE DB-Treiber für SQL Server unterstützt.  
  
 [Erstellen von Anwendungen mit dem OLE DB-Treiber für SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Bietet einen Überblick über die OLE DB-Treiber für SQL Server-Anwendungsentwicklung, einschließlich, wie sie gegenüber Windows DAC, die Komponenten unterscheiden, die verwendet werden, und mit ihm ADO verwendet werden kann.  
  
 Dieser Abschnitt beschreibt auch die OLE DB-Treiber für SQL Server-Installation und Bereitstellung, einschließlich der weiterverteilung der OLE DB-Treiber für SQL Server-Bibliothek.  
  
 [Systemanforderungen für den OLE DB-Treiber für SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Erläutert, die die Systemressourcen für die Verwendung von OLE DB-Treiber für SQL Server erforderlich.  
  
 [OLE DB-Treiber für SQL Server-Programmierung](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Enthält Informationen zur Verwendung von OLE DB-Treiber für SQL Server.  
  
 [Weitere Informationen zum OLE DB-Treiber für SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Stellt zusätzliche Ressourcen zum OLE DB-Treiber für SQL Server, einschließlich Links zu externen Ressourcen und Weitere Informationsquellen bereit.  
  
  
## <a name="see-also"></a>Siehe auch  
 [Aktualisieren einer Anwendung von SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB-Themen zur Vorgehensweise](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
