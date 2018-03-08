---
title: Funktionen von Microsoft ODBC Driver for SQLServer on Windows | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 204b8ba3c81bae77c6a663e93f2b541c8aca0727
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/18/2017
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Funktionen von Microsoft ODBC Driver for SQL Server on Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Microsoft ODBC Driver 13.1 for SQLServer on Windows

Der ODBC Driver 13.1 for SQL Server enthält die gesamte Funktionalität der vorherigen Version (11) und bietet Unterstützung für Always Encrypted und Azure Active Directory-Authentifizierung, wenn in Verbindung mit Microsoft SQL Server 2016 verwendet.  
  
„Immer verschlüsselt“ ermöglicht es Clients, sensible Daten in Clientanwendungen zu verschlüsseln und die Verschlüsselungsschlüssel niemals an SQL Server weiterzugeben. Ein auf dem Clientcomputer installierter Treiber, bei dem „Immer verschlüsselt“ aktiviert ist, erreicht dies durch die automatische Ver- und Entschlüsselung von sensiblen Daten in der SQL Server-Clientanwendung. Der Treiber verschlüsselt die Daten in vertraulichen Spalten, bevor er sie an SQL Server weitergibt, und schreibt Abfragen automatisch neu, sodass die Semantik der Anwendung beibehalten wird. Auf ähnliche Weise entschlüsselt der Treiber transparent Daten in verschlüsselten Datenbankspalten, die in Abfrageergebnissen enthalten sind. Weitere Informationen finden Sie unter [Using Always Encrypted mit dem ODBC-Treiber](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md).
 
Azure Active Directory sind Benutzer, DBAs und Anwendungsprogrammierer als Mechanismus für die der Verbindung mit Microsoft Azure SQL-Datenbank und Microsoft SQL Server 2016 Identitäten in Azure Active Directory (Azure AD mit Azure Active Directory-Authentifizierung verwenden ). Weitere Informationen finden Sie unter [mithilfe von Azure Active Directory mit dem ODBC-Treiber](../../../connect/odbc/using-azure-active-directory.md), und [Herstellen einer Verbindung mit SQL-Datenbank oder SQL Data Warehouse durch Verwenden von Azure Active Directory-Authentifizierung](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/).   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Microsoft ODBC Driver 11 für SQL Server unter Windows  

Der ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] enthält die gesamte Funktionalität des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ODBC-Treibers, der im Lieferumfang von [!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]enthalten ist. Weitere Informationen finden Sie unter [SQL Server Native Client-Programmierung](http://msdn.microsoft.com/library/ms130892.aspx). Der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ODBC-Treiber basiert auf dem ODBC-Treiber, der im Lieferumfang des Betriebssystems von Windows enthalten ist. Weitere Informationen finden Sie unter [Windows Data Access Components SDK](http://msdn.microsoft.com/library/aa968814(VS.85).aspx).  
  
Diese Version des ODBC-Treibers für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] enthält die folgenden neuen Features:  
  
### <a name="bcpexe-l-option-for-specifying-a-login-timeout"></a>bcp.exe Option "– i" für die Angabe ein Anmeldungstimeout
 
Die Option "– i" gibt die Anzahl der Sekunden, bevor ein `bcp.exe` Anmeldung [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] ein Timeout eintritt, wenn Sie versuchen, eine Verbindung mit einem Server herstellen. Das Standardtimeout für die Anmeldung ist 15 Sekunden. Das Anmeldungstimeout muss eine Zahl zwischen 0 und 65534 sein. Wenn der angegebene Wert kein numerischer Wert ist oder außerhalb dieses Bereichs liegt, generiert `bcp.exe` eine Fehlermeldung. Der Wert 0 gibt ein unbegrenztes Timeout. Ein Anmeldungstimeout von weniger als (circa) 10 Sekunden ist nicht zuverlässig.  
  
### <a name="driver-aware-connection-pooling"></a>Treiberfähiges Verbindungspooling  
Der ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unterstützt [Treiberfähiges Verbindungspooling](http://msdn.microsoft.com/library/hh405031(VS.85).aspx). Weitere Informationen finden Sie unter [Driver-Aware Connection Pooling in the ODBC Driver for SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).  
  
### <a name="asynchronous-execution-notification-method"></a>Asynchrone Ausführung (Benachrichtigungsmethode)  
Der ODBC-Treiber für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] unterstützt [asynchrone Ausführung (Benachrichtigungsmethode)](http://msdn.microsoft.com/library/hh405038(VS.85).aspx). Ein Beispiel zur Verwendung finden Sie unter [asynchrone Ausführung &#40; Benachrichtigungsmethode &#41; Beispiel](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md).  
  
### <a name="connection-resiliency"></a>Verbindungsstabilität
Um sicherzustellen, dass die Anwendungen mit einer Microsoft Azure SQL-Datenbank verbunden sind, kann der ODBC-Treiber unter Windows Verbindungen im Leerlauf wiederherstellen. Weitere Informationen finden Sie unter [Connection Resiliency in the Windows ODBC Driver](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md).  
  
## <a name="behavior-changes"></a>Verhaltensänderungen

In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client die `-y0` option `sqlcmd.exe` verursacht die Ausgabe bei 1 MB abgeschnitten wird, wenn die Anzeigebreite 0 wurde.
  
Ab der ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], besteht keine Einschränkung hinsichtlich der Datenmenge, die in einer einzelnen Spalte abgerufen werden können beim `–y0` angegeben ist. `sqlcmd.exe`streamt jetzt Spalten bis zu 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Datentyp-Maximum).  
  
Ein weiterer Unterschied ist, dass die Angabe sowohl `-h` und `-y0` erzeugt nun einen Fehler meldet, dass die Optionen inkompatibel sind. `-h`, die gibt die Anzahl der Zeilen an, zwischen den Spaltenüberschriften gedruckt und war noch nie mit kompatibel `-y0`, wurde ignoriert, obwohl keine Überschriften gedruckt wurden.
  
Beachten Sie, dass `-y0` kann auf dem Server und das Netzwerk, abhängig von der Größe der zurückgegebenen Daten zu Leistungsproblemen führen.

## <a name="see-also"></a>Siehe auch  
[Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
