---
title: Sicherheitsüberlegungen für die Microsoft-Treiber für PHP für SQLServer | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b956d18a910772ae8a5633aaf88b61d69b44001
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="security-considerations-for-the-microsoft-drivers-for-php-for-sql-server"></a>Sicherheitsüberlegungen für die Microsoft-Treiber für PHP für SQLServer
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema beschreibt Sicherheitsüberlegungen speziell für die Entwicklung, die Bereitstellung und den Betrieb von Anwendungen, die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]verwenden. Ausführlichere Informationen zu SQL Server-Sicherheit finden Sie unter [Overview of SQL Server Security](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/overview-of-sql-server-security).  
  
## <a name="connect-using-windows-authentication"></a>Herstellen einer Verbindung mithilfe der Windows-Authentifizierung  
Aus folgenden Gründen sollte, wann immer möglich, die Windows-Authentifizierung für die Verbindung zu SQL Server verwendet werden:  
  
-   **Während der Authentifizierung werden keine Anmeldeinformationen über das Netzwerk übergeben.** Benutzernamen und Kennwörter werden nicht in die Verbindungszeichenfolge der Datenbank eingebettet. Aus diesem Grund können nicht böswillige Benutzer oder Angreifer die Anmeldeinformationen durch Überwachen des Netzwerks oder durch einsehen Verbindungszeichenfolgen in Konfigurationsdateien erhalten.  
  
-   **Die Benutzer werden über eine zentralisierte Kontoverwaltung verwaltet** Sicherheitsrichtlinien, wie z. B. Gültigkeitszeiträume für Passwörter, Vorgaben zur Mindestlänge von Passwörtern und die Sperrung von Konten nach mehreren ungültigen Anmeldeanfragen werden umgesetzt.  
  
Informationen zum Herstellen einer Verbindung mit einem Server mithilfe der Windows-Authentifizierung finden Sie unter [Vorgehensweise: Herstellen einer Verbindung mithilfe der Windows-Authentifizierung](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Wenn Sie eine Verbindung mithilfe der Windows-Authentifizierung herstellen, sollten Sie Ihre Umgebung so konfigurieren, dass SQL Server das Kerberos-Authentifizierungsprotokoll verwenden kann. Weitere Informationen finden Sie unter [Gewusst wie: sicherstellen, dass Sie Kerberos-Authentifizierung verwenden, wenn Sie eine Remoteverbindung mit einer Instanz von SQL Server 2005 erstellen](https://support.microsoft.com/en-ca/help/909801/how-to-make-sure-that-you-are-using-kerberos-authentication-when-you-c) oder [Kerberos-Authentifizierung und SQL Server](https://msdn.microsoft.com/library/cc280744.aspx).  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>Verwenden Sie verschlüsselte Verbindungen, wenn Sie sensible Daten übertragen.  
Sie sollten immer verschlüsselte Verbindungen verwenden, wenn der SQL Server sensible Daten empfangen/senden soll. Informationen zum Aktivieren verschlüsselter Verbindungen finden Sie unter [zum Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul (SQL Server-Konfigurations-Manager)](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md). Zum Herstellen einer sicheren Verbindung mit dem [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], verwenden Sie das Attribut „Encrypt connection“ beim Verbinden mit dem Server. Weitere Informationen zu Verbindungsattributen finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="use-parameterized-queries"></a>Verwenden parametrisierter Abfragen  
Verwenden Sie parametrisierte Abfragen, um das Risiko von Angriffen durch Einschleusung von SQL-Befehlen zu senken. Beispiele für die Ausführung parametrisierter Abfragen finden Sie unter [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md).  
  
Weitere Informationen zu SQL Injection-Angriffen und sicherheitsüberlegungen finden Sie unter [SQL Injection](https://msdn.microsoft.com/library/ms161953.aspx).  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>Akzeptieren Sie KEINE Server- oder Verbindungszeichenfolgeinformationen von Endbenutzern.  
Schreiben Sie Anwendungen so, dass Endbenutzer keine Server- oder Verbindungszeichenfolgeinformationen an die Anwendungen übermitteln können. Sie können die Angriffsfläche für böswillige Aktivitäten reduzieren, indem Sie strikte Kontrolle über die Server- und Verbindungszeichenfolgeinformationen behalten.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>Aktivieren von „WarningsAsErrors“ während der Anwendungsentwicklung  
Legen Sie während der Anwendungsentwicklung für den Schalter „ **WarningsAsErrors** “ den Wert **true** fest, damit vom Treiber ausgegebenen Warnungen wie Fehler behandelt werden. Dadurch können Sie Warnungen angehen, bevor Sie Ihre Anwendung bereitstellen. Weitere Informationen finden Sie unter [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="secure-logs-for-deployed-application"></a>Sichere Protokolle für bereitgestellte Anwendungen  
Stellen Sie sicher, dass die Protokolle bereitgestellter Anwendungen an einem sicheren Ort gespeichert werden, oder dass die Protokollierung deaktiviert ist. Dies schützt gegen mögliche Zugriffe von Endbenutzern auf Informationen, die in die Protokolldateien geschrieben wurden. Weitere Informationen finden Sie unter [Logging Activity](../../connect/php/logging-activity.md).  
  
## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den Microsoft-Treiber für PHP für SQLServer](../../connect/php/programming-guide-for-php-sql-driver.md)
  
