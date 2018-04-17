---
title: Befehlszeilen-Installation von SQL Server-Machine Learning-Komponenten | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1bc0cda53059b715a04d6e9a350e40d3a265d5e0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="install-sql-server-machine-learning-components-from-the-command-line"></a>Installieren von SQL Server-Machine Learning-Komponenten über die Befehlszeile
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel enthält Anweisungen zum Installieren SQL Server-Machine learning-Komponenten über die Befehlszeile:

+ [In der Datenbank-Instanz](#indb)
+ [Fügen Sie zu einer vorhandenen Datenbank-Engine-Instanz hinzu](#add-existing)
+ [Automatische Installation](#silent)
+ [Eigenständiger Server](#shared-feature)

Sie können automatische, Standard- oder vollständige Interaktion mit der Setup-Benutzeroberfläche angeben. In diesem Artikel stellt eine Ergänzung [Installieren von SQL Server von der Befehlszeile aus](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), behandelt die Parameter, die nur für R und Python Machine Learning-Komponenten.

## <a name="pre-install-checklist"></a>Prüfliste vor der Installation

+ Führen Sie Befehle von einer Eingabeaufforderung mit erhöhten Rechten. 

+ Eine Datenbank-Modulinstanz wird für die Installation in der Datenbank erforderlich. Sie können nicht nur R oder Python-Features installieren, obwohl Sie können [inkrementell zu einer vorhandenen Instanz hinzufügen](#add-existing). Wenn Sie nur die R und Python ohne das Datenbankmodul möchten Installieren der [eigenständiger Server](#shared-feature).

+ Nicht auf einem Failovercluster installieren. Zum Isolieren von R und Python-Prozesse Sicherheitsmechanismus ist nicht kompatibel mit einer Windows Server Failover Cluster-Umgebung.

+ Nicht auf einem Domänencontroller installieren. Der Machine Learning-Dienste Teil von Setup schlägt fehl.

+ Vermeiden Sie die eigenständige und Instanzen in der Datenbank auf demselben Computer installieren. Ein eigenständiger Server wird für die gleichen Ressourcen, während Sie die Leistung der beiden Installationen untergraben konkurrieren.


## <a name="command-line-arguments"></a>Befehlszeilenargumente

Das Argument Funktionen ist es erforderlich, Begriff Vereinbarungen Lizenzierung sind. 

Wenn Sie über die Eingabeaufforderung installieren, unterstützt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe des /Q-Parameters den vollständigen stillen Modus oder mithilfe des /QS-Parameters den einfachen stillen Modus. Mithilfe des /QS-Schalters wird nur der Fortschritt angezeigt, es sind jedoch keine Eingaben möglich. Außerdem werden beim Auftreten von Fehlern keine Fehlermeldungen angezeigt. Der /QS-Parameter wird nur unterstützt, wenn /Action=install angegeben wurde.

| Argumente | Description |
|-----------|-------------|
| / FEATURES = AdvancedAnalytics | Installiert die Datenbankversion: SQL Server 2017 Machine Learning Services (Datenbankintern) oder SQL Server 2016 R Services (Datenbankintern).  |
| /FEATURES = SQL_INST_MR | Gilt nur für SQLServer 2017. Kombinieren Sie dies mit AdvancedAnalytics. Installiert die (In-Database) R-Funktion, einschließlich Microsoft R Open und proprietäre R-Pakete. Die SQL Server 2016-R-Services-Funktion ist R-nur, damit es keinen Parameter für diese Version zugreifen gibt.|
| / FEATURES = SQL_INST_MPY | Gilt nur für SQLServer 2017. Kombinieren Sie dies mit AdvancedAnalytics. Installiert die (In-Database) Python-Funktion, einschließlich Anaconda und proprietäre Python-Pakete. |
| /FEATURES = SQL_SHARED_MR | Installiert die R-Funktion für die eigenständige Version: SQL Server 2017 Machine Learning-Server (eigenständig) oder SQL Server 2016 R Server (eigenständig). Ein eigenständiger Server ist eine "freigegebene Funktion" nicht auf eine Datenbankmodulinstanz gebunden.|
| / FEATURES = SQL_SHARED_MPY | Gilt nur für SQLServer 2017. Installiert die Python-Funktion für die eigenständige Version: SQL Server 2017 Machine Learning-Server (eigenständig). Ein eigenständiger Server ist eine "freigegebene Funktion" nicht auf eine Datenbankmodulinstanz gebunden.|
| /IACCEPTROPENLICENSETERMS  | Gibt an, dass Sie die Lizenzbedingungen für die Verwendung der open-Source-R-Komponenten akzeptiert haben. |
| / IACCEPTPYTHONLICENSETERMS | Gibt an, dass Sie die Lizenzbedingungen für die Verwendung der Python-Komponenten akzeptiert haben. |
| /IACCEPTSQLSERVERLICENSETERMS | Gibt an, dass Sie die Lizenzbedingungen für die Verwendung von SQL Server akzeptiert haben.|
| / MRCACHEDIRECTORY | Für offline-Setup legt den Ordner mit der R-Komponente CAB-Dateien. |
| /MPYCACHEDIRECTORY | Für offline-Setup legt den Ordner mit den Python-Komponente CAB-Dateien. |


## <a name="indb"></a> Instanz-Installationen in der Datenbank

In der Datenbank Analytics stehen für datenbankmodulinstanzen, die erforderlich sind, zum Hinzufügen der **AdvancedAnalytics** Funktion zu Ihrer Installation. Sie können eine Datenbank-Modulinstanz mit erweiterten Analysen installieren oder [zu einer vorhandenen Instanz hinzufügen](#add-existing). 

Um Statusinformationen ohne die interaktive auf dem Bildschirm eingabeaufforderungen anzuzeigen, verwenden Sie den/QS-Argument.

> [!Important]
> Bleiben zwei zusätzliche Konfigurationsschritte nach der Installation. Integration ist nicht abgeschlossen, bevor diese Tasks ausgeführt werden. Finden Sie unter [Aufgaben nach der Installation](#post-install) Anweisungen.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQLServer 2017: Datenbankmodul, Erweiterte Analysen mit Python und R

Geben Sie für eine gleichzeitige Installation von der Instanz des Datenbankmoduls den Instanznamen und administratoranmeldung (Windows) aus. Enthalten Sie Features für die Installation von Core und Sprachkomponenten sowie die Annahme der Lizenzbedingungen für alle.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

Diese denselben Befehl jedoch mit einer SQL Server-Anmeldung für einen Datenbank-Engine mithilfe gemischte Authentifizierung.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

In diesem Beispiel wird Python nur anzeigt, dass Sie eine Sprache hinzufügen können, indem Sie eine Funktion auslassen.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQLServer 2016: Datenbankmodul und erweiterte Analysen mit R

Dieser Befehl ist identisch zu SQL Server-2017, jedoch ohne die Python-Elemente, nicht verfügbar sind in SQL Server 2016-Setup.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> (Erforderlich) Konfiguration nach der Installation

Gilt für in-Installationen nur Database.

Wenn Setup abgeschlossen ist, müssen Sie eine Datenbank-Modulinstanz mit R und Python Microsoft R und Python-Pakete, Microsoft R Open, Anaconda, Tools, Beispiele und Skripts, die Teil der Verteilung sind. 

Zwei weitere Aufgaben sind erforderlich, um die Installation abzuschließen:

1. Starten Sie den Datenbank-Engine-Dienst neu.

1. Aktivieren Sie externer Skripts, bevor Sie das Feature verwenden können. Befolgen Sie die Anweisungen in [installieren Sie SQL Server 2017 Machine Learning Services (Datenbankintern)](sql-machine-learning-services-windows-install.md) im nächsten Schritt. 

Für SQL Server 2016, verwenden Sie diesen Artikel stattdessen [installieren Sie SQL Server 2016 R Services (Datenbankintern)](sql-r-services-windows-install.md).

## <a name="add-existing"></a> Erweiterte Analysen zu einer vorhandenen Datenbank-Engine-Instanz hinzufügen

Wenn Sie erweiterte Analysen in der Datenbank zu einer vorhandenen Datenbank-Engine-Instanz hinzufügen, geben Sie den Instanznamen an. Z. B. Wenn Sie zuvor eine 2017 von SQL Server-Datenbankmodul und Python installiert, können mit diesem Befehl Sie r hinzufügen

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> Automatische Installation

Eine automatische Installation unterdrückt die Prüfung auf Speicherorte der CAB-Datei. Aus diesem Grund müssen Sie den Speicherort angeben, in dem CAB-Dateien werden entpackt werden. Sie können das temp-Verzeichnis für diese.
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> Eigenständige Serverinstallationen

Ein eigenständiger Server ist eine "freigegebene Funktion" nicht auf eine Datenbankmodulinstanz gebunden. Die folgenden Beispiele zeigen gültigen Syntax für beide Versionen.

SQL Server-2017 unterstützt Python und R auf einem eigenständigen Server:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016 ist nur für R:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

Wenn Setup abgeschlossen ist, müssen Sie einen Server, Microsoft-Pakete, Open Source-Verteilung von R und Python-Tools, Beispiele und Skripts, die Teil der Verteilung sind. 

So öffnen Sie ein R-Konsolenfenster, wechseln Sie zu \Programme\Microsoft SQL Server\140 (oder 130) \R_SERVER\bin\x64, und doppelklicken Sie auf **RGui.exe**. Haben Sie noch keine Erfahrung mit R? Wiederholen Sie dieses Lernprogramm: [grundlegende R-Befehle und RevoScaleR-Funktionen: 25 gängige Beispiele](https://docs.microsoft.com/en-us/machine-learning-server/r/tutorial-r-to-revoscaler).

Um eine Python-Befehl zu öffnen, wechseln Sie zu \Programme\Microsoft SQL Server\140\PYTHON_SERVER\bin\x64, und doppelklicken Sie auf **python.exe**.

## <a name="get-help"></a>Abrufen von Hilfe

Benötigen Sie Hilfe bei der Installation oder Aktualisierung? Antworten auf häufig gestellte Fragen und bekannte Probleme finden Sie im folgenden Artikel:

* [Upgrade und Installation häufig gestellte Fragen – Machine Learning-Dienste](../r/upgrade-and-installation-faq-sql-server-r-services.md)

Überprüfen Sie den Installationsstatus der Instanz, und beheben Probleme, wiederholen Sie dann diese benutzerdefinierten Berichte.

* [Benutzerdefinierte Berichte für SQL Server R Services](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>Nächste Schritte

R-Entwickler können mit einigen einfachen Beispielen beginnen und die Grundlagen der Funktionsweise von R mit SQL Server. Im nächsten Schritt finden Sie unter den folgenden Links:

+ [Lernprogramm: Ausführen von R in T-SQL](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [Lernprogramm: In-Database-Analyse für R-Entwickler](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python-Entwickler können zum Verwenden von Python mit SQL Server gemäß diesen Lernprogrammen erfahren:

+ [Lernprogramm: Ausführen von Python in T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Lernprogramm: In-Database-Analyse für Python-Entwickler](../tutorials/sqldev-in-database-python-for-sql-developers.md)

Beispiele für Machine Learning, reale Szenarien basieren, finden Sie unter [Machine learning-Lernprogramme](../tutorials/machine-learning-services-tutorials.md).