---
title: "Erweiterte Konfigurationsoptionen für Machine Learning-Dienste | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 872acf107d72989b4623a9d5f4ccb85c44d1f2f9
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>Erweiterte Konfigurationsoptionen für Machine Learning-Webdienste

Dieser Artikel beschreibt die Änderungen, die Sie zum Ändern der Konfiguration des R-Laufzeitmoduls und andere Dienste, die für Machine Learning in der SQL Server nach der Installation vornehmen können.

Gilt für: SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

##  <a name="bkmk_Provisioning"></a>Für die Bereitstellung von Benutzerkonten für Computer lernen

Externes Skript-Prozessen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Kontext des lokalen Benutzerkonten mit einer geringen ausgeführt. Diese Prozesse in einzelnen Konten, die mit eingeschränkten Berechtigungen ausgeführt, hat die folgenden Vorteile:

+ Reduziert die Berechtigungen des externen Skripts-laufzeitprozesse auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer
+ Eine Isolation zwischen Sitzungen aus einer externen z. B. R oder Python.

Als Teil der Installation einer neuen Windows *benutzerkontenpool* erstellt wird, enthält die lokalen Benutzerkonten zum Ausführen von R-Laufzeitprozess erforderlich sind. Falls nötig können Sie die Anzahl von Benutzer zur Unterstützung von R anpassen. Der Administrator Ihrer Datenbank muss dieser Gruppe außerdem die Erlaubnis erteilen, eine Verbindung mit jeder Instanz herstellen zu können, auf der R Services aktiviert ist. Weitere Informationen finden Sie unter [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)zugeordnet sind.

Sie können allerdings eine Zugriffssteuerungliste (ACL) für sensible Ressourcen auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definieren, um den Zugriff auf diese Gruppe zu verhindern, damit der R-Laufzeitprozess keinen Zugriff auf die Ressourcen erhält.

+ Der Benutzerkontenpool ist mit einer bestimmten Instanz verknüpft.  Für jede Instanz, auf der R-Skript aktiviert wurde, wird ein separater Pool aus Workerkonten erstellt. Konten können nicht zwischen Instanzen freigegeben werden.

+ Benutzerkontonamen im Pool weisen das Format „SQLInstanzname*nn*zugeordnet sind. Wenn Sie z. B. die Standardinstanz als R-Server verwenden, unterstützt der Benutzerkontenpool Kontonamen wie MSSQLSERVER01, MSSQLSERVER02 usw.

+ Die Größe des Benutzerkontenpools ist statisch und der Standardwert ist 20. Die Anzahl der R-Laufzeitsitzungen, die gleichzeitig gestartet werden können, ist durch die Größe dieses Benutzerkontenpools beschränkt. Diese Einschränkung kann allerdings von einem Administrator mithilfe von SQL Server Configuration Manager angepasst werden.

Weitere Informationen zum Ändern des Benutzerkontenpools finden Sie unter [Modify the User Account Pool for SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a>Verwalten von externen Skriptprozesse belegter Arbeitsspeicher

Die [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] zugeordneten R-Laufzeitprozesse sind standardmäßig auf die Verwendung von nicht mehr als 20 % des gesamten Arbeitsspeichers beschränkt. Dieser Grenzwert kann jedoch bei Bedarf vom Administrator erhöht werden.

Dieser Wert ist im Allgemeinen für schwerwiegende R-Aufgaben nicht ausreichend; zu schwerwiegenden Aufgaben zählen z.B. Trainingsmodelle oder das Vorhersagen von vielen Datenzeilen. Möglicherweise müssen Sie den für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (oder für andere Dienste) reservierten Speicherplatz reduzieren und Resource Governor verwenden, um einen externen Ressourcenpool bzw. -pools zu definieren und zuzuweisen. Weitere Informationen finden Sie unter [Ressourcenkontrolle für R](../../advanced-analytics/r/resource-governance-for-r-services.md).

##  <a name="bkmk_ChangingConfig"></a>Erweiterte Dienstoptionen mithilfe der Konfigurationsdatei ändern

Sie können einige erweiterte Einstellungen von [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] durch Bearbeiten der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]-Konfigurationsdatei steuern. Diese Datei wird während des Setups von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eingerichtet und standardmäßig am folgenden Speicherort als Nur-Text-Datei gespeichert:

`<instance path>\binn\rlauncher.config`

Sie müssen Administrator auf dem Computer sein, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, um diese Datei ändern zu können. Für die Bearbeitung der Datei wird empfohlen, dass Sie eine Sicherungskopie erstellen, bevor Sie Änderungen speichern.

Z. B. um Editor beim Öffnen der Konfigurationsdatei für die Standardinstanz verwenden, würde Sie eine Eingabeaufforderung als Administrator öffnen, und geben Sie den folgenden Befehl:

```
C:\>Notepad.exe "%programfiles%\Microsoft SQL Server\MSSQL13.MSSQLSERVER\mssql\binn\rlauncher.config"  
```

##  <a name="bkmk_properties"></a>Bearbeiten der Konfigurationseigenschaften

Die folgende Tabelle führt jede für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] unterstützte Einstellung mit den zulässigen Werten auf.

Alle Einstellungen haben die Form eines Schlüssel-Wert-Paars, bei dem jede Einstellung in einer separaten Zeile enthalten ist. Diese Eigenschaft gibt z. B. die Ablaufverfolgungsebene für RLauncher:

Standard: TRACE_LEVEL=4


|**Einstellungsname**|**Werttyp**|**Standardwert**|**Beschreibung**|
|------------------|----------------|-------------|-----------------|
|JOB_CLEANUP_ON_EXIT|Integer<br /><br /> 0 = Deaktiviert<br /><br /> 1 = Aktiviert|1<br /><br /> Protokolldateien werden beim Beenden entfernt.|Gibt an, ob der für jede R-Sitzung erstellte temporäre Arbeitsordner nach Abschluss der R-Sitzung bereinigt werden soll. Diese Einstellung ist beim Debuggen nützlich.<br /><br /> Hinweis: Dies ist eine interne Einstellung – ändern Sie diesen Wert nicht.|
|TRACE_LEVEL|Integer<br /><br /> 1 = Fehler<br /><br /> 2 = Leistung<br /><br /> 3 = Warnung<br /><br /> 4 = Information|1<br /><br /> Nur schwerwiegende Warnungen ausgeben|Konfiguriert den Ausführlichkeitsgrad der Ablaufverfolgung für das R-Startprogramm (MSSQLLAUNCHPAD) zu Debugzwecken. Diese Einstellung wirkt sich auf den Ausführlichkeitsgrad der Ablaufverfolgungen aus, die in den folgenden Ablaufverfolgungsdateien gespeichert werden, die sich beide in dem Pfad befinden, der durch die Einstellung LOG_DIRECTORY angegeben wird:<br /><br /> **rlauncher.log**: Die Ablaufverfolgungsdatei, die für R-Sitzungen generiert wurde, die von T-SQL-Abfragen gestartet wurden.<br /><br /> |

## <a name="bkmk_Launchpad"></a>Ändern Sie das Launchpad-Dienstkonto

Eine Separate [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst erstellt und für jede Instanz auf dem Sie Machine learning Services konfiguriert haben.

Launchpad ist standardmäßig so konfiguriert, dass es mit dem Konto „NT Service\MSSQLLaunchpad“ ausgeführt wird, das mit allen erforderlichen Berechtigungen für das Ausführen von R-Skript bereitgestellt wird. Jedoch, wenn Sie dieses Konto ändern, das Launchpad möglicherweise nicht gestartet oder Zugriff auf die SQL Server-Instanz, auf dem externen Skripts ausgeführt werden soll.

Wenn Sie das Dienstkonto ändern, achten Sie darauf, dass Sie die Anwendung **Local Security Policy** (Lokale Sicherheitsrichtlinie) verwenden und die Berechtigungen in jedem Dienstkonto aktualisieren, sodass sie folgende Berechtigungen enthalten:

+ Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)
+ Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)
+ Anmelden als Dienst (SeServiceLogonRight)
+ Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)

Weitere Informationen zu erforderlichen Berechtigungen für das Ausführen von SQL Server-Diensten finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

## <a name="see-also"></a>Siehe auch

[Überlegungen zur Sicherheit](security-considerations-for-the-r-runtime-in-sql-server.md)
