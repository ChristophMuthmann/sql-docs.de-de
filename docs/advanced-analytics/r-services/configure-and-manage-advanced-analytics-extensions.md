---
title: "Konfigurieren und Verwalten von Advanced Analytics-Erweiterungen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# Konfigurieren und Verwalten von Advanced Analytics-Erweiterungen
  Nach der Installation [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], können Sie kleinere Änderungen vornehmen, in der Konfiguration der R-Laufzeit und anderen Diensten zugeordnet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] .  
  
  
 **In diesem Thema**  
  
-   [Bereitstellen von Benutzerkonten für SQL Server R Services](#bkmk_Provisioning)  
  
-   [Verwalten der Speicherplatzverwendung durch R-Prozesse](#bkmk_ManagingMemory)  
  
-   [Ändern der Dienststandardwerte mithilfe der Konfigurationsdatei](#bkmk_ChangingConfig) 

-   [Ändern das Launchpad-Dienstkonto](#bkmk_Launchpad) 
  
##  <a name="bkmk_Provisioning"></a> Bereitstellen von Benutzerkonten für SQL Server R Services  
 R-Laufzeit verarbeitet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Kontext des lokalen Benutzerkonten mit einer geringen ausgeführt. Die Ausführung von R-Laufzeitprozessen in einzelnen Konten mit geringen Rechten weist folgende Vorteile auf:  
  
-   Reduzieren Sie die Berechtigungen des R-Laufzeit die aktiven Prozesse auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer  
  
-   Bereitstellung der Isolation zwischen den R-Laufzeitsitzungen.  
  
 Als Teil des Installationsvorgangs in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], einen neuen Windows *Konto Benutzerpool* erstellt wird, enthält die lokale Benutzerkonten, die zum Ausführen der R-Laufzeitprozess erforderlich sind. Sie können die Anzahl der Benutzer ändern, bei Bedarf zur Unterstützung von R. Der Datenbankadministrator muss auch erteilen dieser Gruppe die Berechtigung zur Verbindung mit einer beliebigen Instanz, in denen R Services aktiviert wurde. Weitere Informationen finden Sie unter [Ändern Sie den Benutzer-Konto-Pool für SQL Server-R-Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
 Allerdings kann eine Zugriffssteuerungsliste (ACL) für vertrauliche Ressourcen definiert werden, auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Zugriff auf diese Gruppe, um zu verhindern, dass der R-Laufzeitprozess erhalten Zugriff auf die Ressourcen zu verweigern.  
  
-   Pool-Konto Benutzer ist einer bestimmten Instanz verknüpft.  Für jede Instanz, auf die R-Skript aktiviert wurde, einen separaten Pool von Arbeitsthreads werden Konten erstellt. Konten können nicht zwischen Instanzen freigegeben werden.
  
-   Benutzernamen im Pool werden im Format SQLInstanceName*Nn*. Wenn Sie z. B. die Standardinstanz als R-Server verwenden, unterstützt der Benutzerkontenpool Kontonamen wie MSSQLSERVER01, MSSQLSERVER02 usw.  
  
-   Die Größe des Benutzerkontenpools ist statisch und der Standardwert ist 20. Die Anzahl der R-Laufzeitsitzungen, die gleichzeitig gestartet werden können, ist durch die Größe dieses Benutzerkontenpools beschränkt. Allerdings kann dieses Limit mithilfe von SQL Server-Konfigurations-Manager von einem Administrator geändert werden.  
  
  
 Weitere Informationen zum Konto Benutzerpool ändern, finden Sie unter [Ändern Sie den Benutzer-Konto-Pool für SQL Server-R-Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).  
  
##  <a name="bkmk_ManagingMemory"></a> Verwalten der Speicherplatzverwendung durch R-Prozesse  
 In der Standardeinstellung die R-Laufzeitprozessen zugeordnet [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] sind auf die Verwendung von nicht mehr als 20 % der Gesamtanzahl der Computer Arbeitsspeicher beschränkt. Dieser Grenzwert kann jedoch bei Bedarf vom Administrator erhöht werden.  
  
 Dieser Betrag wird in der Regel für schwerwiegende R-Aufgaben wie das Modell trainieren oder Vorhersagen auf viele Zeilen mit Daten unzureichend ist. Möglicherweise müssen Sie die für reservierten Speicher reduzieren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (oder andere Dienste) und Verwenden der Ressourcenkontrolle zum Definieren einer externen oder Ressourcenpools und zuordnen. Weitere Informationen finden Sie unter [Ressourcenkontrolle für R Services](../../advanced-analytics/r-services/resource-governance-for-r-services.md).  
  
##  <a name="bkmk_ChangingConfig"></a> Erweiterte Service-Optionen mithilfe der Konfigurationsdatei ändern  
 
Sie können einige erweiterte Eigenschaften steuern [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] durch Bearbeiten der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Konfigurationsdatei. Diese Datei wird erstellt, während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einrichten und in der Standardeinstellung als nur-Text-Datei am folgenden Speicherort gespeichert:  
 
```  
<instance path>\binn\rlauncher.config  
```  
  
 Sie müssen ein Administrator auf dem Computer, auf dem ausgeführt wird, wird sein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um diese Datei zu ändern. Für die Bearbeitung der Datei wird empfohlen, dass Sie eine Sicherungskopie erstellen, bevor Sie Änderungen speichern.  
  
 Wenn Sie die Konfigurationsdatei für die Standardinstanz (MSSQLSERVER) z. B. im Editor öffnen möchten, würden Sie eine Eingabeaufforderung als Administrator öffnen und folgenden Befehl eingeben:  
  
```  
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
  
```  
  
###  <a name="bkmk_properties"></a> Konfigurationseigenschaften  
 Alle Einstellungen haben die Form eines Schlüssel-Wert-Paars, bei dem jede Einstellung in einer separaten Zeile enthalten ist. Diese Eigenschaft gibt z. B. an, dass nicht mehr als 20 Prozent des Systemspeichers von R-Prozessen verwendet werden dürfen:  
  
 Standardwert: `MEMORY_LIMIT_PERCENT=20`  
  
 Die folgende Tabelle enthält jede der Einstellungen für unterstützt [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], mit die zulässigen Werte.  
  
|Einstellungsname|Werttyp|Standardwert|Beschreibung|  
|------------------|----------------|-------------|-----------------|  
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = Deaktiviert<br /><br /> 1 = Aktiviert|1<br /><br /> Protokolldateien werden beim Beenden entfernt.|Gibt an, ob der für jede R-Sitzung erstellte temporäre Arbeitsordner nach Abschluss der R-Sitzung bereinigt werden soll. Diese Einstellung ist beim Debuggen nützlich.<br /><br /> Hinweis: Dies ist eine interne Einstellung – ändern Sie diesen Wert nicht.|  
|TRACE_LEVEL|Integer<br /><br /> 1 = Fehler<br /><br /> 2 = Leistung<br /><br /> 3 = Warnung<br /><br /> 4 = Informationen|1<br /><br /> Nur schwerwiegende Warnungen ausgeben|Konfiguriert den Ausführlichkeitsgrad der Ablaufverfolgung für das R-Startprogramm (MSSQLLAUNCHPAD) zu Debugzwecken. Diese Einstellung wirkt sich auf den Ausführlichkeitsgrad der Ablaufverfolgungen aus, die in den folgenden Ablaufverfolgungsdateien gespeichert werden, die sich beide in dem Pfad befinden, der durch die Einstellung LOG_DIRECTORY angegeben wird:<br /><br /> **rlauncher.log**: die Ablaufverfolgungsdatei für R-Sitzung gestartet, indem Sie T-SQL-Abfragen generiert.<br /><br /> Weitere Informationen hierzu finden Sie unter [Durchsuchen von Daten und Predictive Modellierung mit R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).|  

## <a name="bkmk_Launchpad"></a>Ändern das Launchpad-Dienstkonto

Eine Separate [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst erstellt und für jede Instanz, auf dem Sie konfiguriert haben [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. 

Standardmäßig ist das Launchpad konfiguriert ausführen, verwenden das Konto NT-Service\MSSQLLaunchpad, die mit allen erforderlichen Berechtigungen zum Ausführen von R-Skripts bereitgestellt wird. Aber wenn Sie dieses Konto ändern, das Launchpad möglicherweise nicht starten oder Zugriff auf die SQL Server-Instanz dem R-Skripts ausgeführt werden soll.
 
  Wenn Sie das Dienstkonto ändern, müssen Sie verwenden die **Lokale Sicherheitsrichtlinie** Anwendung und aktualisieren die Berechtigungen für jeden Dienst das Konto zum Beispiel:
  + Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)
  + Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)
  + Anmelden als Dienst (SeServiceLogonRight)
  + Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)

Weitere Informationen über die erforderlichen Berechtigungen zum Ausführen von SQL Server-Dienste finden Sie unter [Windows-Dienstkonten konfigurieren und Berechtigungen](https://msdn.microsoft.com/library/ms143504.aspx#Windows).
   
## Siehe auch  
 [Erste Schritte mit SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  