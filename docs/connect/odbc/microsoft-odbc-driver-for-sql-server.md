---
title: Microsoft ODBC Driver for SQLServer | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: drivers
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9f2ae91b-06af-4c9a-9d24-062df7bc4662
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: a9e480bd8ab948c02be27aa82a8bcd8caa2d7015
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

![Download-nach-unten-Eingekreister](../../ssdt/media/download.png)[zum Herunterladen von ODBC-Treiber](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

ODBC ist die primäre native Datenzugriffs-API für Anwendungen, die für SQL Server in C und C++ geschrieben. Ein ODBC-Treiber für die meisten Datenquellen ist vorhanden. Andere Sprachen, die ODBC verwenden, können enthalten COBOL, Perl, PHP und Python. ODBC wird häufig in Datenintegration verwendet.

Der ODBC-Treiber stellt Tools wie z. B. [ **Sqlcmd** ](../../tools/sqlcmd-utility.md) und [ **Bcp**](../../tools/bcp-utility.md). Die **Sqlcmd** -Hilfsprogramm können Sie die Transact-SQL-Anweisungen, Systemprozeduren und SQL-Skripts ausgeführt werden. Die **Bcp** Hilfsprogramm per Massenvorgang kopiert Daten zwischen einer Instanz von Microsoft SQL Server und einer Datendatei in einem Format, das Sie auswählen. Sie können **Bcp** viele neue Zeilen in SQL Server-Tabellen importieren oder Daten aus Tabellen in Datendateien zu exportieren.  

## <a name="code-example-in-c"></a>Codebeispiel in C++

Wir haben eine kleine ZIP-Datei, die den Quellcode einem C++-Programm enthält, die ODBC verwendet:

- [C++-Codebeispiel zur Verwendung von ODBC](../../odbc/reference/sample-odbc-program.md)

## <a name="download"></a>Herunterladen

- ![Download-nach-unten-Eingekreister](../../ssdt/media/download.png)[zum Herunterladen von ODBC-Treiber](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

## <a name="documentation"></a>Dokumentation  

### <a name="features"></a>-Funktionen

- [Benutzerdefinierte-Schlüsselspeicher-Anbieter](../../connect/odbc/custom-keystore-providers.md)
- [DSN und Schlüsselwörter für Verbindungszeichenfolgen und Attribute](dsn-connection-string-attribute.md)
- [SQL Server Native Client](../../relational-databases/native-client/features/sql-server-native-client-features.md) (verfügbaren Funktionen auch anwenden, ohne die OLE DB, ODBC-Treiber für SQL Server)
- [Verwenden von immer verschlüsselte](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Mithilfe von Azure Active Directory](../../connect/odbc/using-azure-active-directory.md)
- [Mithilfe des transparenten Netzwerk-IP-Auflösung](../../connect/odbc/using-transparent-network-ip-resolution.md)

### <a name="linux-and-macos"></a>Linux und macOS

- [Installieren des Treibers](../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Connecting to SQL Server (Herstellen einer Verbindung mit SQL Server)](../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)
- [Herstellen einer Verbindung mit **Bcp**](../../connect/odbc/linux-mac/connecting-with-bcp.md)
- [Herstellen einer Verbindung mit **Sqlcmd**](../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)
- [Datenzugriffs-Ablaufverfolgung](../../connect/odbc/linux-mac/data-access-tracing-with-the-odbc-driver-on-linux.md)
- [Häufig gestellte Fragen](../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)
- [Installieren des Treiber-Managers](../../connect/odbc/linux-mac/installing-the-driver-manager.md)
- [Bekannte Probleme](../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)
- [Programmierrichtlinien](../../connect/odbc/linux-mac/programming-guidelines.md)
- [Anmerkungen zu dieser Version](../../connect/odbc/linux-mac/release-notes.md)
- [Unterstützung für hohe Verfügbarkeit und Wiederherstellung im Notfall](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
- [Mithilfe der integrierten Authentifizierung (Kerberos)](../../connect/odbc/linux-mac/using-integrated-authentication.md)

### <a name="windows"></a>Windows

- [Beispiel für asynchrone Ausführung (Benachrichtigungsmethode)](../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)
- [Verbindungsresilienz im Windows ODBC-Treiber](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)
- [Treiberfähiges Verbindungspooling](../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)
- [Features und Verhaltensänderungen](../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)
- [Anmerkungen zu dieser Version](../../connect/odbc/windows/release-notes.md)
- [Systemanforderungen, Installation und Treiberdateien](../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)



## <a name="community"></a>Community  
- [Microsoft ODBC Driver for SQL Server Teamblog](http://blogs.msdn.com/sqlnativeclient/default.aspx)  
- [SQL Server-Datenzugriffsforum](http://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
