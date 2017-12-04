---
title: Versionsanmerkungen zu SQL Server 2016|Microsoft-Dokumente
ms.date: 10/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
caps.latest.revision: "276"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 688c1607028a6792a128cef04128c494ade15d93
ms.sourcegitcommit: 284a64817d5641b5245bc70ddebef2dc51d2e558
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2017
---
# <a name="sql-server-2016-release-notes"></a>Versionsanmerkungen zu SQL Server 2016
  In den folgenden Artikeln werden Einschränkungen und Probleme mit Releases von SQL Server 2016 beschrieben.    
    
 **Probieren Sie es aus:**    
   
[![Download aus dem Evaluation Center](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) Laden Sie SQL Server 2016 aus dem **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)** herunter.    
    
[![Azure Virtual Machine (klein)](../includes/media/azure-vm.png)](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/) Haben Sie ein Azure-Konto?  Wechseln Sie anschließend **[hierhin](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** , um einen virtuellen Computer zu starten, auf dem SQL Server 2016 SP1 bereits installiert ist.
    
[![SSMS herunterladen](../includes/media/download2.png)**SSMS:** Laden Sie die neueste Version von SQL Server Management Studio hier herunter: **[Download SQL Server Management Studio (SSMS) (Herunterladen von SQL Server Management Studio (SSMS))](../ssms/download-sql-server-management-studio-ssms.md)**.   
    
 Informationen zu Neuerungen finden Sie unter [Neues im Berichts-Generator für SQL Server 2016](http://msdn.microsoft.com/library/8223c19b-4b0d-4b1d-a042-9a726c18e708).
    
##  <a name="bkmk_top"></a> Abschnitte in diesem Artikel:    

-   [SQL Server 2016 Service Pack 1 (SP1) verfügbar](#bkmk_2016sp1)    
-   [SQL Server 2016 Allgemeine Verfügbarkeit (GA, General Availability)](#bkmk_2016_ga) 
-   [SQL Server 2016 Release Candidate 3 (RC3)](#bkmk_2016_rc3)     

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1) verfügbar
![info_tip](../sql-server/media/info-tip.png) Mit SQL Server 2016 SP1 werden alle Editionen und Dienstebenen von SQL Server 2016 auf SQL Server 2016 SP1 aktualisiert. Neben den Fehlerbehebungen, die in diesem Artikel aufgeführt sind, enthält SQL Server 2016 SP1 Hotfixes, die in SQL Server 2016 CU1 (kumulatives Update 1) bis SQL Server 2016 CU3 enthalten waren.
    
- [Downloadseite für SQL Server 2016 SP1](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1-Versionsinformationen](https://support.microsoft.com/kb/3182545) Enthält die einzelnen Fehlernummern und Probleme, die in SP1 korrigiert oder geändert wurden.
 - ![info_tip](../sql-server/media/info-tip.png) Links und Informationen zu allen unterstützten Versionen, einschließlich Service Packs, von [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] finden Sie im [Update Center für Microsoft SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) 
    
    
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