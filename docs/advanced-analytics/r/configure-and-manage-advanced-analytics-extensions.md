---
title: "Erweiterte Konfigurationsoptionen für Machine Learning-Dienste | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8d73fd98-0c61-4a62-94bb-75658195f2a6
caps.latest.revision: "21"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 369c630e249d7775e67508fc9b00e94447182012
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-configuration-options-for-machine-learning-services"></a>Erweiterte Konfigurationsoptionen für Machine Learning-Dienste

Dieser Artikel beschreibt die Änderungen, die Sie zum Ändern der Konfiguration der Runtime externes Skript und andere Dienste, die für Machine Learning in der SQL Server nach der Installation vornehmen können.

**Gilt für:** SQL Server 2016-R-Services, SqlServer 2017 Machine Learning-Dienste

##  <a name="bkmk_Provisioning"></a>Bereitstellen zusätzlicher-Benutzerkonten für den Computer lernen

Externes Skript-Prozessen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Kontext des lokalen Benutzerkonten mit einer geringen ausgeführt. Diese Prozesse in einzelnen Konten, die mit eingeschränkten Berechtigungen ausgeführt, hat die folgenden Vorteile:

+ Reduziert die Berechtigungen des externen Skripts-laufzeitprozesse auf die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Computer
+ Eine Isolation zwischen Sitzungen aus einer externen z. B. R oder Python.

Als Teil der Installation einer neuen Windows *benutzerkontenpool* erstellt wird, enthält die lokalen Benutzerkonten zum Ausführen von externen-Laufzeitprozessen, z. B. R oder Python erforderlich sind. Sie können die Anzahl der Benutzer ändern, wie zur Unterstützung von Machine Learning-Aufgaben erforderlich sind. 

Darüber hinaus erteilen Datenbankadministrator dieser Gruppe die Berechtigung zur Verbindung mit einer beliebigen Instanz, in denen Machine Learning aktiviert wurde. Weitere Informationen finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning-Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

Auf protext vertrauliche Ressourcen auf der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], können Sie eine Zugriffssteuerungsliste (ACL) für diese Gruppe definieren. Durch die Angabe von Ressourcen, denen die Gruppe Zugriff auf verweigert wird, können Sie den Zugriff von externen Prozessen wie R oder Python-Laufzeiten verhindern.

+ Der Benutzerkontenpool ist mit einer bestimmten Instanz verknüpft. Ein separater Pool von Worker-Konten wird für jede Instanz benötigt auf dem Machine Learning aktiviert wurde. Konten können nicht zwischen Instanzen freigegeben werden.

+ Benutzerkontonamen im Pool weisen das Format „SQLInstanzname*nn*zugeordnet sind. Z. B. bei Verwendung die Standardinstanz für den Machine learning unterstützt der benutzerkontenpool Kontonamen wie MSSQLSERVER01, MSSQLSERVER02 usw..

+ Die Größe des Benutzerkontenpools ist statisch und der Standardwert ist 20. Die Anzahl der externen-laufzeitsitzungen, die gleichzeitig gestartet werden kann, wird durch die Größe dieses benutzerkontenpools beschränkt. Zum Ändern dieses Limits, sollte ein Administrator SQL Server-Konfigurations-Manager verwenden.

Weitere Informationen zum Ändern des benutzerkontenpools finden Sie unter [Ändern des benutzerkontenpools für SQL Server-Machine Learning-Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

##  <a name="bkmk_ManagingMemory"></a>Verwalten von externen Skriptprozesse belegter Arbeitsspeicher

Standardmäßig sind die externen Skript Laufzeiten für Machine Learning auf nicht mehr als 20 % des gesamten Arbeitsspeichers beschränkt. Es hängt von Ihrem System, aber in der Regel stellen Sie möglicherweise dieses Limit nicht schwerwiegenden Machine Learning-Aufgaben wie z. B. Trainieren eines Modells oder Vorhersagen auf viele Zeilen mit Daten. 

Zur Unterstützung von Machine Learning kann ein Administrator dieses Limit zu erhöhen. Wenn Sie dies tun, müssen Sie möglicherweise verringern Sie die reservierten Umfang an Arbeitsspeicher für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder für andere Dienste. Außerdem sollten Sie die Verwendung der Ressourcenkontrolle können Sie einen externen Ressourcenpool und Pools definieren, damit bestimmte Ressourcenpools in R oder Python Aufträge zugewiesen werden kann.

Weitere Informationen finden Sie unter [Ressourcenkontrolle für Machine Learning](../../advanced-analytics/r/resource-governance-for-r-services.md).


## <a name="bkmk_Launchpad"></a>Ändern Sie das Launchpad-Dienstkonto

Eine Separate [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Dienst erstellt und für jede Instanz auf dem Sie Machine learning Services konfiguriert haben.

Launchpad ist standardmäßig so konfiguriert, dass es mit dem Konto „NT Service\MSSQLLaunchpad“ ausgeführt wird, das mit allen erforderlichen Berechtigungen für das Ausführen von R-Skript bereitgestellt wird. Jedoch, wenn Sie dieses Konto ändern, das Launchpad möglicherweise nicht gestartet oder Zugriff auf die SQL Server-Instanz, auf dem externen Skripts ausgeführt werden soll.

Wenn Sie das Dienstkonto ändern, achten Sie darauf, dass Sie die Anwendung **Local Security Policy** (Lokale Sicherheitsrichtlinie) verwenden und die Berechtigungen in jedem Dienstkonto aktualisieren, sodass sie folgende Berechtigungen enthalten:

+ Anpassen des Arbeitsspeicherkontingents für einen Prozess (SeIncreaseQuotaPrivilege)
+ Umgehen von durchsuchenden Prüfungen (SeChangeNotifyPrivilege)
+ Anmelden als Dienst (SeServiceLogonRight)
+ Ersetzen von Token auf Prozessebene (SeAssignPrimaryTokenPrivilege)

Weitere Informationen zu erforderlichen Berechtigungen für das Ausführen von SQL Server-Diensten finden Sie unter [Konfigurieren von Windows-Dienstkonten und -Berechtigungen](https://msdn.microsoft.com/library/ms143504.aspx#Windows).

##  <a name="bkmk_ChangingConfig"></a>Ändern der erweiterten Dienstoptionen

In frühen Versionen von SQL Server 2016 R Services können Sie einige Eigenschaften des Diensts ändern, indem Sie bearbeiten die [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Konfigurationsdatei. 

Diese Datei ist jedoch nicht mehr zum Ändern der Konfigurationen verwendet. Wir empfehlen die Verwendung von SQL Server-Konfigurations-Manager auf Auswirkungen Änderungen an der Dienstkonfiguration, wie das Dienstkonto und die Anzahl der Benutzer.

**Launchpad-Konfiguration ändern**

1. Öffnen Sie den [SQL Server-Konfigurations-Manager](../../relational-databases/sql-server-configuration-manager.md). 
2. SQL Server Launchpad Maustaste und wählen Sie **Eigenschaften**.

    + Um das Dienstkonto zu ändern, klicken Sie auf die **anmelden** Registerkarte.

    + Um die Anzahl von Benutzern zu erhöhen, klicken Sie auf die **erweitert** Registerkarte.


**So ändern Sie die Debugeinstellungen**

Einige Eigenschaften können nur geändert werden, mithilfe der Launchpad-Konfigurationsdatei, die sich in selteneren Fällen, z. B. das Debuggen von Nutzen sein kann. Die Konfigurationsdatei wird erstellt, während [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einrichten und wird standardmäßig als nur-Text-Datei am folgenden Speicherort gespeichert:`<instance path>\binn\rlauncher.config`

Sie müssen Administrator auf dem Computer sein, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird, um diese Datei ändern zu können. Für die Bearbeitung der Datei wird empfohlen, dass Sie eine Sicherungskopie erstellen, bevor Sie Änderungen speichern.

Die folgende Tabelle enthält die erweiterten Einstellungen für [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], mit den zulässigen Werten. 

|**Einstellungsname**|**Typ**|**Description**|
|----|----|----|
|AUFTRAG\_CLEANUP\_ON\_BEENDEN|Integer |Dies ist eine interne Einstellung – ändern Sie diesen Wert nicht. </br></br>Gibt an, ob die für jede externe Common Language Runtime-Sitzung erstellte temporäre Arbeitsordner bereinigt werden soll, nachdem die Sitzung abgeschlossen ist. Diese Einstellung ist beim Debuggen nützlich. </br></br>Unterstützte Werte sind **0** (deaktiviert) oder **1** (aktiviert). </br></br>Der Standard ist 1, Bedeutung Protokolldateien werden beim Beenden entfernt.|
|TRACE\_EBENE|Integer |Konfiguriert den Ausführlichkeitsgrad der Ablaufverfolgung des MSSQLLAUNCHPAD für Debugzwecke an. Dies wirkt sich auf Ablaufverfolgungsdateien im Pfad, durch die Einstellung LOG_DIRECTORY angegeben. </br></br>Unterstützte Werte sind: **1** (Fehler), **2** (Leistung), **3** (Warnung), **4** (Information). </br></br>Der Standard ist 1, d. h. die Ausgabe von Warnungen.|

Alle Einstellungen haben die Form eines Schlüssel-Wert-Paars, bei dem jede Einstellung in einer separaten Zeile enthalten ist. Klicken Sie z. B. um die Ablaufverfolgungsebene zu ändern, hinzufügen die Zeile `Default: TRACE_LEVEL=4`.

## <a name="see-also"></a>Siehe auch

[Überlegungen zur Sicherheit](security-considerations-for-the-r-runtime-in-sql-server.md)
