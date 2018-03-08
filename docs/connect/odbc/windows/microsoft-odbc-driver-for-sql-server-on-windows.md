---
title: Microsoft ODBC Driver for SQLServer on Windows | Microsoft Docs
ms.custom: 
ms.date: 02/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 990665bcb7091b61bc8579a1a33e30c3cc56874e
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Der Microsoft ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] sind eigenständige ODBC-Treiber die eine Anwendungsprogrammierschnittstelle (API), der Implementieren der ODBC-Standardschnittstellen für Microsoft bereitstellen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].

Der Microsoft ODBC-Treiber für SQL Server kann verwendet werden, um neue Anwendungen zu erstellen. Sie können auch Ihre älteren Anwendungen aktualisieren, die zurzeit einen älteren ODBC-Treiber verwenden. Der ODBC-Treiber für SQL Server unterstützt Verbindungen mit Azure SQL-Datenbank, Azure SQL Data Warehouse, SQL Server-2017, SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008 und SQL Server 2005.  

## <a name="summary"></a>Zusammenfassung

| Version       | Unterstützte Funktionen      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 für SQLServer | <ul><li>Always Encrypted-Unterstützung für BCP-API</li><li>Neues Verbindungszeichenfolgen-Attribut UseFMTONLY bewirkt, dass Treiber ältere Metadaten in besonderen Fällen, dass temporäre Tabellen verwendet werden.</li>
| Microsoft ODBC Driver 13.1 for SQLServer     | <ul><li>Always Encrypted</li><li>Azure AD-Authentifizierung</li><li>Always On-Verfügbarkeitsgruppen (Availability Groups, AG)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQLServer      | <ul><li>Internationaler Domänenname (IDN)</li></ul> |
| Microsoft ODBC Driver 11 for SQL Server | <ul><li>Treiberfähiges Verbindungspooling</li><li>Verbindungsstabilität</li><li>Asynchrone Ausführung (Abruf-Methode)</li></ul> |    

## <a name="documentation"></a>Dokumentation  
Diese Dokumentation für den Microsoft ODBC Driver für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] enthält:  
  
-   [Versionsanmerkungen](../../../connect/odbc/windows/release-notes.md)  
-   [Funktionen von Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Systemanforderungen, Installation und Treiberdateien](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Treiberfähiges Verbindungspooling im ODBC-Treiber für SQL Server.](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Beispiel für asynchrone Ausführung &#40;Benachrichtigungsmethode&#41;](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Verbindungsresilienz im Windows ODBC-Treiber](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Mit "immer verschlüsselt" mit dem ODBC-Treiber](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [Mithilfe von Azure Active Directory mit dem ODBC-Treiber](../../../connect/odbc/using-azure-active-directory.md) 
-   [Mithilfe des transparenten Netzwerk-IP-Auflösung](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Community  
- [Microsoft ODBC Driver for SQL Server Teamblog](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server-Datenzugriffsforum](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Siehe auch  
- [Informationen zu SQL Server Native Client](https://msdn.microsoft.com/sqlserver/ff658532.aspx)   
- [Erstellen von Anwendungen mit SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [FAQ zu SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937707.aspx)   
- [ODBC-Programmierreferenz](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
