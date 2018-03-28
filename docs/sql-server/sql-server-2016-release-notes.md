---
title: Versionsanmerkungen zu SQL Server 2016|Microsoft-Dokumente
ms.date: 03/14/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
caps.latest.revision: ''
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1a6d422098fdacb3a7bc6392b99fe63bb25c2c36
ms.sourcegitcommit: 6e16d1616985d65484c72f5e0f34fb2973f828f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2018
---
# <a name="sql-server-2016-release-notes"></a>Versionsanmerkungen zu SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  Im folgenden Artikel werden Einschränkungen und Probleme mit Releases von SQL Server 2016, Service Packs inbegriffen, beschrieben. Informationen zu Neuerungen finden Sie unter [Neues im Berichts-Generator für SQL Server 2016](https://docs.microsoft.com/en-us/sql/sql-server/what-s-new-in-sql-server-2016).

> [![Download aus dem Evaluation Center](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) Laden Sie SQL Server 2016 aus dem **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** herunter.
>
> [![Azure Virtual Machine (klein)](../includes/media/azure-vm.png)](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/) Haben Sie ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** , um einen virtuellen Computer zu starten, auf dem SQL Server 2016 SP1 bereits installiert ist.
>
> [![SSMS herunterladen](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) Wechseln Sie zu **[Herunterladen von SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)**, um die neueste Version von SQL Server Management Studio (SSMS) abzurufen.

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1 umfasst alle Problembehebungen bis zu SQL Server 2016 RTM CU3 Security einschließlich des Sicherheitsupdates MS16-136. Es enthält ein Rollup der in den kumulativen Updates von SQL Server 2016 bereitgestellten Lösungen und umfasst das aktuelle kumulative Update CU3 sowie das Sicherheitsupdate MS16-136 mit Veröffentlichungsdatum am 8. November 2016. 

Die folgenden Features sind in der Standard, Web, Express und Local DB Edition von SQL Server SP1 verfügbar (sofern nicht anders angegeben):
- Always Encrypted
- Geänderte Datenerfassung (in Express nicht verfügbar)
- columnstore
- Komprimierung
- Dynamische Datenmaskierung
- Differenzierte Überwachung
- In-Memory OLTP (in Local DB nicht verfügbar)
- Mehrere FileStream-Container (in Local DB nicht verfügbar)
- Partitionierung
- Polybase
- Sicherheit auf Zeilenebene

In der folgenden Tabelle werden wichtige Verbesserungen in SQL Server 2016 SP1 zusammengefasst.

|Funktion|Description|Weitere Informationen finden Sie unter|
|---|---|---|
|Masseneinfügung in Heaps mit automatischem TABLOCK unter TF 715| Das Ablaufverfolgungsflag 715 aktiviert Tabellensperren für Massenladevorgänge in einen Heap ohne nicht gruppierte Indizes.|[Migrating SAP workloads to SQL Server just got 2.5x faster (Beschleunigung der Migration von SAP-Workloads zu SQL Server um das 2,5-fache)](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE OR ALTER|Bereitstellen von Objekten wie gespeicherten Prozeduren, Triggern, benutzerdefinierten Funktionen und Ansichten.|[Blog der SQL Server-Datenbank-Engine](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|DROP TABLE-Unterstützung für die Replikation|DROP TABLE DDL-Unterstützung für die Replikation zum Löschen von Replikationsartikeln.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Signieren des FileStream RsFx-Treibers|Der Filestream RsFx-Treiber wird im Windows Hardware Developer Center Dashboard-Portal (Dev-Portal) signiert und zertifiziert. Dadurch kann der Filestream RsFx-Treiber von SQL Server 2016 SP1 problemlos unter Windows Server 2016/Windows 10 installiert werden.|[Migrating SAP workloads to SQL Server just got 2.5x faster (Beschleunigung der Migration von SAP-Workloads zu SQL Server um das 2,5-fache)](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|LPIM für SQL-Dienstkonto – programmgesteuerte Identifikation|Ermöglicht DBAs die programmgesteuerte Identifikation, wenn die Berechtigung zum Sperren von Seiten im Speicher (Lock Pages in Memory, LPIM) zur Startzeit des Service besteht.|[Developers Choice: Programmatically identify LPIM and IFI privileges in SQL Server (Wahl für Entwickler: LPIM- und IFI-Berechtigungen zur programmgesteuerten Identifikation in SQL Server)](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|Manuelles Bereinigen der Änderungsnachverfolgung|Die neue gespeicherte Prozedur löscht die interne Tabelle der Änderungsnachverfolgung bedarfsgesteuert.| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|Parallele INSERT..SELECT-Änderungen in lokalen temporären Tabellen|Neue parallele INSERT in INSERT..SELECT-Vorgänge.|[SQL Server-Kundenberatungsteam](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|Erweiterte Diagnose einschließlich einer aktivierten Zuweisungswarnung und eines aktivierten maximalen Arbeitsspeichers für eine Abfrage, aktivierter Ablaufverfolgungsflags und Oberflächen für andere Diagnoseinformationen. | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|Speicherklassenspeicher|Steigern Sie mit dem Speicherklassenspeicher in Windows Server 2016 die Transaktionsverarbeitung, wodurch die Commitzeiten für Transaktionen nach Größenordnungen beschleunigt werden können.|[Blog der SQL Server-Datenbank-Engine](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|Verwenden Sie die Abfrageoption `OPTION(USE HINT('<option>'))`, um das Verhalten des Abfrageoptimierers mit unterstützten Hinweisen auf Abfrageebene zu ändern. Anders als bei der Option QUERYTRACEON sind bei der Option USE HINT keine Systemadministratorberechtigungen erforderlich.|[Developers Choice: USE HINT query hints (Wahl der Entwickler: USE HINT-Abfragehinweise)](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|XEvent-Ergänzungen|Neue XEvents- und Perfmon-Diagnosefunktionen bewirken eine Optimierung der Wartezeit bei der Problembehandlung.|[Erweiterte Ereignisse](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

Zudem sollten Sie folgende Problembehandlungen beachten:
- Basierend auf Feedback von DBAs und der SQL-Community werden die Hekaton-Protokollierungsnachrichten ab SQL 2016 SP1 auf ein Minimum reduziert.
- Überprüfen neuer [Ablaufverfolgungsflags](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).
- Die vollständigen Versionen der WideWorldImporters-Beispieldatenbanken können jetzt beginnend mit SQL Server 2016 SP1 mit der Standard Edition und der Express Edition ausgeführt werden und sind auf [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) verfügbar. Im Beispiel müssen keine Änderungen vorgenommen werden. Die Datenbanksicherungen, die zum RTM der Enterprise Edition erstellt wurden, werden in SP1 von der Standard und der Express Edition unterstützt. 

Für die Installation von SQL Server 2016 SP1 ist nach der Installation möglicherweise ein Neustart erforderlich. Als bewährte Methode wird empfohlen, nach der Installation von SQL Server 2016 SP1 einen Neustart zu planen und durchzuführen.

### <a name="download-pages-and-more-information"></a>Downloadseiten und weitere Informationen

- [Service Pack 1 für Microsoft SQL Server 2016 herunterladen](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1 (SP1) freigegeben](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [Releaseinformationen zu SQL Server 2016 Service Pack 1](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) Links und Informationen zu allen unterstützten Versionen finden Sie unter [SQL Server-Update Center](https://msdn.microsoft.com/library/ff803383.aspx). Dort finden Sie auch Informationen zu Service Packs von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 

##  <a name="bkmk_2016_ga"></a> SQL Server 2016 Release - General Availability (GA)
-   [Datenbankmodul (GA)](#bkmk_ga_instalpatch) 
-   [Stretch Database (GA)](#bkmk_ga_stretch)
-   [Abfragespeicher (GA)](#bkmk_ga_query_store)
-   [Produktdokumentation (GA)](#bkmk_ga_docs)
 
### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA) 
**Problem und Kundenbeeinträchtigung:** Microsoft hat ein Problem erkannt, das die Microsoft VC++ 2013 Runtime-Binarys betrifft, die von SQL Server 2016 als erforderliche Komponente installiert werden. Ein Update ist verfügbar, um dieses Problem zu beheben. Wenn dieses Update an den VC++ Runtime-Binarys nicht installiert wird, können bei SQL Server 2016 in bestimmten Szenarien Stabilitätsprobleme auftreten. Bevor Sie SQL Server 2016 installieren, überprüfen Sie, ob der Computer das in [KB 3164398](http://support.microsoft.com/kb/3164398)beschriebenen Patch benötigt. Der Patch ist auch im [Kumulativen Updatepaket 1 (CU1) für SQL Server 2016 RTM](https://www.microsoft.com/download/details.aspx?id=53338) enthalten. 

**Lösung:** Greifen Sie auf eine der folgenden Lösungen zurück:

- Installieren Sie [KB 3138367 – Update für Visual C++ 2013 und Visual C++ Redistributable Package](http://support.microsoft.com/kb/3138367). Der KB-Hotfix ist die bevorzugte Lösung. Sie können dies vor oder nach der Installation von SQL Server 2016 installieren. 

    Wenn SQL Server 2016 bereits installiert ist, führen Sie nacheinander die folgenden Schritte aus:

    1.  Laden Sie die passende *vcredist_\*exe* herunter.
    1.  Beenden Sie den SQL Server-Dienst für alle Instanzen des Datenbankmoduls.
    1.  Installieren Sie **KB 3138367**.
    1.  Starten Sie den Computer neu.
 

 - Installieren Sie  [KB 3164398 – kritisches Update für erforderliche MSVCRT-Komponenten für SQL Server 2016](http://support.microsoft.com/kb/3164398).  
 
    Wenn Sie **KB 3164398**verwenden, können Sie während der Installation von SQL Server über Microsoft Update oder Microsoft Download Center installieren. 

    - **Während der Installation von SQL Server 2016:** Wenn der Computer, auf dem Sie SQL Server einrichten, Zugang zum Internet hat, überprüft das SQL Server-Setup im Rahmen der gesamten SQL Server-Installation, ob das Update vorhanden ist. Wenn Sie das Update akzeptieren, lädt das Setupprogramm die Binärdateien im Rahmen der Installation herunter und aktualisiert sie.

    - **Microsoft Update:** Das Update ist bei Microsoft Update als wichtiges, nicht sicherheitsrelevantes Update für SQL Server 2016 verfügbar. Installation über Microsoft Update, nachdem SQL Server 2016 nach dem Update den Neustart des Servers fordert. 

    - **Download Center:** Das Update steht im Microsoft Download Center zur Verfügung. Sie können die Software für das Update herunterladen und nach der Installation von SQL Server 2016 auf Servern installieren. 


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>Problem mit einem bestimmten Zeichen in einem Datenbank- oder Tabellennamen

**Problem und Beeinträchtigung des Kunden:** Beim Versuch, Stretch Database auf einer Datenbank oder in einer Tabelle zu aktivieren, ist ein Fehler aufgetreten. Das Problem tritt auf, wenn der Name des Objekts ein Zeichen enthält, das beim Konvertieren von Klein- und Großschreibung als ein anderes Zeichen behandelt wird. Ein Beispiel für ein Zeichen, das dieses Problem auslöst, ist das Zeichen „ƒ“ (durch Drücken von ALT+159 erstellt).

**Lösung:** Wenn Sie Stretch Database in einer Datenbank oder Tabelle aktivieren möchten, ist die einzige Option, das Objekt umzubenennen und das Problemzeichen zu entfernen.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>Problem mit einem Index, der das Schlüsselwort INCLUDE verwendet

**Problem und Kundenbeeinträchtigung:** Der Versuch, Stretch Database in einer Tabelle zu aktivieren, die über einen Index verfügt, der das INCLUDE-Schlüsselwort verwendet, um zusätzliche Spalten in den Index einzubeziehen, resultiert in einem Fehler.

**Lösung:** Löschen Sie den Index, der das INCLUDE-Schlüsselwort verwendet, aktivieren Sie Stretch Database in der Tabelle, und erstellen Sie den Index neu. Wenn Sie dies tun, achten Sie darauf, die Wartungsmethoden und Richtlinien Ihrer Organisation einzuhalten, um sicherzustellen, dass für Benutzer der betreffenden Tabelle höchstens minimale Auswirkungen entstehen.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Problem mit automatischer Datenbereinigung bei anderen Editionen als Enterprise und Developer

 **Problem und Kundenbeeinträchtigung:** Fehler bei automatischer Datenbereinigung bei anderen Editionen als Enterprise und Developer. In Folge dessen wächst der vom Abfragespeicher verwendete Speicherplatz mit der Zeit, bis das konfigurierte Limit erreicht ist, wenn Daten nicht manuell gelöscht werden. Wenn dieses Problem nicht beseitigt wird, wird auch der Speicherplatz aufgefüllt, der den Fehlerprotokollen zugeordnet ist, da jeder Bereinigungsversuch eine Dumpdatei erzeugt. Der Aktivierungszeitraum für die Bereinigung hängt von der Häufigkeit der Arbeitsauslastung ab, ist aber nicht länger als 15 Minuten.

 **Lösung:** Wenn Sie den Abfragespeicher bei anderen Editionen als Enterprise und Developer verwenden möchten, müssen Sie explizit die Bereinigungsrichtlinien deaktivieren. Dies kann über SQL Server Management Studio (Seite „Datenbankeigenschaften“) oder über das Transact-SQL-Skript erfolgen:

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

Darüber hinaus sollten Sie manuelle Bereinigungsoptionen erwägen, um zu verhindern, dass der Abfragespeicher in den schreibgeschützten Modus übergeht. Führen Sie z.B. die folgende Abfrage zum Bereinigen des gesamten Datenbereichs in regelmäßigen Abständen aus:

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

Führen Sie außerdem die folgenden gespeicherten Prozeduren des Abfragespeichers regelmäßig aus, um Laufzeitstatistik, bestimmte Abfragen oder Plänen zu bereinigen:

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> Produktdokumentation (GA) 
 **Problem und Kundenbeeinträchtigung:** Eine herunterladbare Version der Dokumentation zu SQL Server 2016 ist noch nicht verfügbar. Wenn Sie den Hilfebibliotheks-Manager verwenden, um zu versuchen, **Inhalt vom Onlinespeicherort zu installieren**, wird Ihnen die Dokumentationen zu SQL Server 2012 und SQL Server 2014 angezeigt. Allerdings gibt es keine Optionen zum Anzeigen der SQL Server 2016-Dokumentation.    
    
 **Problemumgehung:** Sie können eine der folgenden Problemumgehungen verwenden:    
    
 ![Verwalten der Hilfeeinstellungen für SQL Server](../sql-server/media/docs-sql2016-managehelpsettings.png "Verwalten der Hilfeeinstellungen für SQL Server")    
    
-   Verwenden Sie die Option **Onlinehilfe oder lokale Hilfe auswählen** , und konfigurieren Sie die Hilfe für „Ich möchte Onlinehilfe verwenden“.    
    
-   Verwenden Sie die Option **Inhalt von Onlinespeicherort installieren** , und laden Sie den Inhalt von SQL Server 2014 herunter.    
    
 **F1-Hilfe:** Beim Drücken von F1 in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] wird standardmäßig die Onlineversion des F1-Hilfeartikels im Browser angezeigt. Für die Probleme wird browserbasierte Hilfe angeboten, auch wenn Sie die lokale Hilfe konfiguriert und installiert haben. 
     
**Aktualisieren von Inhalten:**    
In SQL Server Management Studio und Visual Studio kann die Anwendung Help Viewer während des Hinzufügens der Dokumentation einfrieren (hängenbleiben). Führen Sie zur Lösung des Problems folgende Schritte aus. Weitere Informationen zu diesem Problem finden Sie unter [Visual Studio Help Viewer friert beim Begrüßungsbildschirm ein](https://msdn.microsoft.com/library/mt654096.aspx).    
    
* Öffnen Sie die Datei „%LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings“ | „HlpViewer_VisualStudio14_en-US.settings“ im Editor, und ändern Sie das Datum im folgenden Code in einen Zeitpunkt in der Zukunft.    
    
     
```    
     Cache LastRefreshed="12/31/2017 00:00:00"    
``` 

## <a name="additional-information"></a>Zusätzliche Informationen
+ [SQL Server 2016-Installation](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [SQL Server-Update Center – Links und Informationen zu allen unterstützten Versionen](https://msdn.microsoft.com/library/ff803383.aspx)


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]    

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")    
