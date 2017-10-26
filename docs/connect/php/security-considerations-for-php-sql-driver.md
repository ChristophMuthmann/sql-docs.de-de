---
title: "Überlegungen zur Sicherheit für PHP SQL Driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security considerations
ms.assetid: a8c1a570-9204-454f-b94c-ba34f54d487c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2a7423bcfcfd28073840ad7f8c9ee2e7424507bc
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="security-considerations-for-php-sql-driver"></a>Überlegungen zur Sicherheit für den PHP-SQL-Treiber
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Dieses Thema beschreibt Sicherheitsüberlegungen speziell für die Entwicklung, die Bereitstellung und den Betrieb von Anwendungen, die [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]verwenden. Ausführlichere Informationen zum Thema SQL Server-Sicherheit finden Sie unter [Datensicherheit und -konformität](http://go.microsoft.com/fwlink/?LinkId=129225).  
  
## <a name="connect-using-windows-authentication"></a>Herstellen einer Verbindung mithilfe der Windows-Authentifizierung  
Aus folgenden Gründen sollte, wann immer möglich, die Windows-Authentifizierung für die Verbindung zu SQL Server verwendet werden:  
  
-   **Während der Authentifizierung werden keine Anmeldeinformationen über das Netzwerk übergeben.** Benutzernamen und Kennwörter werden nicht in die Verbindungszeichenfolge der Datenbank eingebettet. Dies bedeutet, dass böswillige Benutzer oder Angreifer die Anmeldeinformationen nicht durch Überwachen des Netzwerks oder durch Einsehen der Verbindungszeichenfolgen in Konfigurationsdateien erhalten können.  
  
-   **Die Benutzer werden über eine zentralisierte Kontoverwaltung verwaltet** Sicherheitsrichtlinien, wie z. B. Gültigkeitszeiträume für Passwörter, Vorgaben zur Mindestlänge von Passwörtern und die Sperrung von Konten nach mehreren ungültigen Anmeldeanfragen werden umgesetzt.  
  
Informationen zum Herstellen einer Verbindung mit einem Server mithilfe der Windows-Authentifizierung finden Sie unter [Vorgehensweise: Herstellen einer Verbindung mithilfe der Windows-Authentifizierung](../../connect/php/how-to-connect-using-windows-authentication.md).  
  
Wenn Sie eine Verbindung mithilfe der Windows-Authentifizierung herstellen, sollten Sie Ihre Umgebung so konfigurieren, dass SQL Server das Kerberos-Authentifizierungsprotokoll verwenden kann. Weitere Informationen finden Sie unter [Gewusst wie: Sicherstellen, dass Sie Kerberos-Authentifizierung verwenden, wenn Sie eine Remoteverbindung mit einer Instanz von SQL Server 2005 erstellen](http://go.microsoft.com/fwlink/?LinkId=121862) oder unter [Kerberos-Authentifizierung und SQL Server](http://go.microsoft.com/fwlink/?LinkId=129226).  
  
## <a name="use-encrypted-connections-when-transferring-sensitive-data"></a>Verwenden Sie verschlüsselte Verbindungen, wenn Sie sensible Daten übertragen.  
Sie sollten immer verschlüsselte Verbindungen verwenden, wenn der SQL Server sensible Daten empfangen/senden soll. Informationen zum Aktivieren verschlüsselter Verbindungen finden Sie unter [zum Aktivieren von verschlüsselten Verbindungen zum Datenbankmodul (SQL Server-Konfigurations-Manager)](http://go.microsoft.com/fwlink/?LinkId=121864). Zum Herstellen einer sicheren Verbindung mit dem [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], verwenden Sie das Attribut „Encrypt connection“ beim Verbinden mit dem Server. Weitere Informationen zu Verbindungsattributen finden Sie unter [Connection Options](../../connect/php/connection-options.md).  
  
## <a name="use-parameterized-queries"></a>Verwenden parametrisierter Abfragen  
Verwenden Sie parametrisierte Abfragen, um das Risiko von Angriffen durch Einschleusung von SQL-Befehlen zu senken. Beispiele für die Ausführung parametrisierter Abfragen finden Sie unter [How to: Perform Parameterized Queries](../../connect/php/how-to-perform-parameterized-queries.md).  
  
Weitere Informationen zu Angriffen durch Einschleusung von SQL-Befehlen und Sicherheitsüberlegungen dazu finden Sie unter [Einschleusen von SQL-Befehlen](http://go.microsoft.com/fwlink/?LinkId=104224).  
  
## <a name="do-not-accept-server-or-connection-string-information-from-end-users"></a>Akzeptieren Sie KEINE Server- oder Verbindungszeichenfolgeinformationen von Endbenutzern.  
Schreiben Sie Anwendungen so, dass Endbenutzer keine Server- oder Verbindungszeichenfolgeinformationen an die Anwendungen übermitteln können. Sie können die Angriffsfläche für böswillige Aktivitäten reduzieren, indem Sie strikte Kontrolle über die Server- und Verbindungszeichenfolgeinformationen behalten.  
  
## <a name="turn-warningsaserrors-on-during-application-development"></a>Aktivieren von „WarningsAsErrors“ während der Anwendungsentwicklung  
Legen Sie während der Anwendungsentwicklung für den Schalter „ **WarningsAsErrors** “ den Wert **true** fest, damit vom Treiber ausgegebenen Warnungen wie Fehler behandelt werden. Dadurch können Sie Warnungen angehen, bevor Sie Ihre Anwendung bereitstellen. Weitere Informationen finden Sie unter [Handling Errors and Warnings](../../connect/php/handling-errors-and-warnings.md).  
  
## <a name="secure-logs-for-deployed-application"></a>Sichere Protokolle für bereitgestellte Anwendungen  
Stellen Sie sicher, dass die Protokolle bereitgestellter Anwendungen an einem sicheren Ort gespeichert werden, oder dass die Protokollierung deaktiviert ist. Dies schützt gegen mögliche Zugriffe von Endbenutzern auf Informationen, die in die Protokolldateien geschrieben wurden. Weitere Informationen finden Sie unter [Logging Activity](../../connect/php/logging-activity.md).  
  
## <a name="see-also"></a>Siehe auch  
[Programmierhandbuch für den PHP-SQL-Treiber](../../connect/php/programming-guide-for-php-sql-driver.md)
  

