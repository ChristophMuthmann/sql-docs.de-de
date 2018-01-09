---
title: "Programmierung für SQL Server Native Client | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLNCLI, about SQL Server Native Client
- SQL Server Native Client, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
- data access [SQL Server Native Client]
- SQL Server Native Client
- SQLNCLI
- native data access [SQL Server Native Client]
ms.assetid: 14ba2cb1-a424-4e4d-b224-0bf1015ab801
caps.latest.revision: "66"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a60ee91484043192ee6998266b04f9b73b9f5424
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="sql-server-native-client-programming"></a>Programmierung für SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ist eine eigenständige Datenzugriffs-API (Application Programming Interface), die sowohl für OLE DB als auch für ODBC verwendet wird und in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführt wurde. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (SQL Native Client) ist eine DLL (Dynamic Link Library), die den SQL-OLE DB-Anbieter und den SQL-ODBC-Treiber enthält. Sie stellt auch neue Funktionen bereit, die weit über die von Windows Data Access Components (Windows DAC, früher Microsoft Data Access Components oder MDAC genannt) bereitgestellten Funktionalität hinausgehen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client kann zur Erstellung neuer Anwendungen oder zur Erweiterung vorhandener Anwendungen verwendet werden, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] neu eingeführte Funktionen nutzen müssen, wie Multiple Active Result Sets (MARS), benutzerdefinierte Datentypen (UDT), Abfragebenachrichtigungen, Momentaufnahmenisolation und Unterstützung für XML-Datentypen.  
  
> [!NOTE]  
>  Eine Liste der Unterschiede zwischen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client und Windows DAC sowie Informationen zu Problemen, Sie sollten vor dem Aktualisieren einer Windows DAC-Anwendung auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client finden Sie unter [Aktualisieren einer Anwendung mit SQL Server Native Client von MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
 Der ODBC-Treiber von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client wird stets in Verbindung mit dem ODBC-Treiber-Manager verwendet, der zum Lieferumfang von Windows DAC gehört. Der OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client kann in Verbindung mit den OLE DB-Basisdiensten von Windows DAC verwendet werden, dies wird jedoch nicht vorausgesetzt. Ob die Basisdienste verwendet werden oder nicht, hängt von den Anforderungen der jeweiligen Anwendung ab (beispielsweise wenn Verbindungspooling erforderlich ist).  
  
 ActiveX Data Object (ADO)-Anwendungen können die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB-Anbieter, aber es wird empfohlen, ADO in Verbindung mit der **DataTypeCompatibility** Schlüsselwort für Verbindungszeichenfolgen (oder seiner entsprechenden  **DataSource** Eigenschaft). Beim Einsatz des OLE DB-Anbieters von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client können ADO-Anwendungen die neuen Funktionen nutzen, die in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] eingeführt wurden und für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client über die Verbindungszeichenfolgen-Schlüsselwörter oder OLE DB-Eigenschaften oder [!INCLUDE[tsql](../../includes/tsql-md.md)] verfügbar sind. Weitere Informationen zur Verwendung dieser Funktionen mit ADO finden Sie unter [mithilfe von ADO mit SQL Server Native Client](../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client wurde entwickelt, um eine einfache Methode für den systemeigenen Datenzugriff auf SQL Server über OLE DB oder ODBC zur Verfügung zu stellen. Er ist einfach, weil OLE DB- und ODBC-Technologien in einer Bibliothek integriert sind, und er bietet eine Möglichkeit, Datenzugriffsfunktionen zu optimieren und weiterzuentwickeln, ohne die aktuellen Windows DAC-Komponenten zu ändern, die jetzt Teil der Microsoft Windows-Plattform sind.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client verwendet zwar Komponenten von Windows DAC, ist jedoch nicht ausdrücklich von einer bestimmten Version von Windows DAC abhängig. Sie können [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client mit der Version von Windows DAC verwenden, die zusammen mit dem von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützten Betriebssystem installiert wird.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client.md)  
 Listet wichtige neue [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Funktionen auf.  
  
 [Einsatzbedingungen für SQL Server Native Client](../../relational-databases/native-client/when-to-use-sql-server-native-client.md)  
 Erläutert, welche Rolle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unter den Datenzugriffstechnologien von Microsoft spielt und welche Unterschiede gegenüber Windows DAC und ADO.NET bestehen, und bietet Entscheidungshilfen für die Auswahl einer Datenzugriffstechnologie.  
  
 [SQL Server Native Client-Features](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
 Beschreibt die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client unterstützten Funktionen.  
  
 [Erstellen von Anwendungen mit SQL Server Native Client](../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
 Bietet einen Überblick über die Entwicklung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sowie die Unterschiede gegenüber Windows DAC, die verwendeten Komponenten und darüber, wie ADO in Verbindung damit verwendet werden kann.  
  
 In diesem Abschnitt wird außerdem die Installation und Bereitstellung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client einschließlich der Weiterverteilung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client-Bibliothek erläutert.  
  
 [Systemanforderungen für SQL Server Native Client](../../relational-databases/native-client/system-requirements-for-sql-server-native-client.md)  
 Erläutert die zur Nutzung von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client erforderlichen Systemressourcen.  
  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
 Bietet Informationen zur Verwendung des OLE DB-Anbieter von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [SQL Server Native Client &#40; ODBC &#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 Bietet Informationen zur Verwendung des ODBC-Treibers von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 [Finden weiterer SQL Server Native Client-Informationen](../../relational-databases/native-client/finding-more-sql-server-native-client-information.md)  
 Stellt zusätzliche Ressourcen über [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client bereit, einschließlich Links zu externen Ressourcen und zum Abrufen weiterer Hilfe.  
  
 [Fehler bei SQL Server Native Client](http://msdn.microsoft.com/library/ebd0e9a8-5fe5-4b15-9a44-2f131a13c186)  
 Enthält Themen zu Laufzeitfehlern, die dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client zugeordnet sind.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Aktualisieren einer Anwendung von SQL Server 2005 Native Client](../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)   
 [Vorgehensweisen zu ODBC](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Vorgehensweisen für OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
