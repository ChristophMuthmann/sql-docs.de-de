---
title: Erstellen von Anwendungen mit SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], building applications
- SQLNCLI, building applications
- applications [SQL Server Native Client]
- SQL Server Native Client, building applications
ms.assetid: 254a2b48-f0e3-43b5-a48d-3d666c2a779f
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4f4cf78541c48739b4ddcf94cd879fc7a56fe18d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="building-applications-with-sql-server-native-client"></a>Erstellen von Anwendungen mit SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Bei der Entwicklung einer Anwendung, die die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Bibliothek verwendet, sind eine Reihe von Punkten zu berücksichtigen. Die Themen in diesem Abschnitt beschreiben viele dieser Punkte einschließlich Aktualisieren von MDAC auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, Verwenden der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Header- und Bibliotheksdateien sowie eines Überblicks über die verschiedenen Verbindungszeichenfolgen, die mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwendet werden können.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Installieren von SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 Erläutert die Installation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, die Speicherorte zur Installation der verschiedenen Komponenten und die Deinstallation von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 [Komponenten von SQL Server Native Client](../../../relational-databases/native-client/applications/components-of-sql-server-native-client.md)  
 Beschreibt die Komponenten, aus denen sich [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client einschließlich Bibliothek, Ressource, Hilfe und Headerdateien zusammensetzt.  
  
 [Verwenden von Schlüsselwörtern für Verbindungszeichenfolgen mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
 Erläutert die verschiedenen Verbindungszeichenfolgen, die beim Herstellen einer Verbindung zu einer Datenbank mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verwendet werden können.  
  
 [Mithilfe der SQL Server Native Client-Header und Bibliotheksdateien](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md)  
 Erläutert die Verwendung der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client-Header- und Bibliotheksdateien innerhalb einer Anwendung.  
  
 [Aktualisieren einer Anwendung von MDAC auf SQL Server Native Client](../../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)  
 Beschreibt die Unterschiede zwischen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client und MDAC sowie Aspekte, die beim Aktualisieren von MDAC auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client zu berücksichtigen sind.  
  
 [Aktualisieren einer Anwendung von SQL Server 2005 Native Client](../../../relational-databases/native-client/applications/updating-an-application-from-sql-server-2005-native-client.md)  
 Beschreibt Aspekte, die beim Upgrade von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] Native Client auf [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] zu berücksichtigen sind.  
  
 [Verwenden von ADO mit SQL Server Native Client](../../../relational-databases/native-client/applications/using-ado-with-sql-server-native-client.md)  
 Erläutert, wie ADO mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client auf die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Funktionen zugreifen und diese verwenden kann.  
  
 [Richtlinien zur Unterstützung für SQL Server Native Client](../../../relational-databases/native-client/applications/support-policies-for-sql-server-native-client.md)  
 Erklärt die Verwendung verschiedener Datenzugriffskomponenten mit verschiedenen Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 [Herstellen einer Verbindung mit einer Windows Azure SQL-Datenbank mithilfe von SQL Server Native Client](../../../relational-databases/native-client/applications/connecting-to-a-windows-azure-sql-database-using-sql-server-native-client.md)  
 Erläutert, wie mithilfe von [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hergestellt wird.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmierung für SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Vorgehensweisen zu ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB-Themen zur Vorgehensweise](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
