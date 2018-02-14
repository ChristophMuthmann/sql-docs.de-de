---
title: "Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e1dbd4fe6152e7318da0267d25c5900ec10c4814
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/13/2018
---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>Verwalten und Überwachen der Volltextsuche auf einer Serverinstanz
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Die Volltextverwaltung für eine Serverinstanz enthält Folgendes:  
  
-   Die Systemverwaltungsaufgaben wie z. B. das Verwalten des FDHOST-Startprogrammdiensts (MSSQLFDLauncher), das Neustarten des Filterdaemonhost-Prozesses nach dem Ändern der Dienstkontoinformationen, das Konfigurieren der serverweiten Volltexteigenschaften und das Sichern des Volltextkatalogs. Auf der Serverebene können Sie beispielsweise eine Standardvolltextsprache festlegen, die sich vollständig von der Standardsprache der Serverinstanz unterscheidet.  
  
-   Konfigurieren von linguistischen Volltextkomponenten (Wörtertrennung, Stammerkennung, Thesaurusdatei, Stoppwörter und Stoplisten).  
  
-   Konfigurieren einer Benutzerdatenbank für die Volltextsuche. Dies beinhaltet das Erstellen von Volltextkatalogen für die Datenbank und die Definition eines Volltextindexes für jede Tabelle oder indizierte Sicht, für die Volltextabfragen ausgeführt werden sollen.  
  
##  <a name="props"></a> Anzeigen oder Ändern von Servereigenschaften für die Volltextsuche  
 Sie können die Eigenschaften für die Volltextsuche einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen.  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>So zeigen Sie Servereigenschaften für die Volltextsuche an und ändern diese  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf einen Server, und klicken Sie dann auf **Eigenschaften**.  
  
2.  Klicken Sie im Dialogfeld **Servereigenschaften** auf die Seite **Erweitert** , um Serverinformationen zur Volltextsuche anzuzeigen. Hierbei handelt es sich um die folgenden Eigenschaften:  
  
    -   **Volltext-Standardsprache**  
  
         Gibt eine Standardsprache für Spalten mit Volltextindex an. Linguistische Analysen von Daten mit Volltextindex werden von der Sprache der Daten bestimmt. Der Standardwert für diese Option ist die Sprache des Servers. Informationen zu der Sprache, die der angezeigten Einstellung entspricht, finden Sie unter [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
    -   **Volltextupgrade-Option**  
  
         Mit dieser Servereigenschaft wird gesteuert, wie Volltextindizes migriert werden, wenn Sie eine Datenbank von [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] zu einer höheren Version migrieren. Diese Eigenschaft ist für die folgenden Aktionen gültig: Upgrade durch Anfügen einer Datenbank, Wiederherstellen einer Datenbanksicherung, Wiederherstellen einer Dateisicherung oder Kopieren der Datenbank mit dem Assistenten zum Kopieren von Datenbanken.  
  
         Die Alternativen lauten folgendermaßen:  
  
         **Importieren**  
         Volltextkataloge werden importiert. Normalerweise ist der Import bedeutend schneller als eine Neuerstellung. Wenn Sie zum Beispiel nur eine CPU verwenden, läuft ein Import etwa zehnmal schneller ab als eine Neuerstellung. Ein importierter Volltextkatalog verwendet jedoch nicht die neuen mit [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]eingeführten Wörtertrennungen. Aus diesem Grund sollten Sie zu einem späteren Zeitpunkt eine Neuerstellung der Volltextkataloge durchführen.  
  
        > [!NOTE]  
        >  Sie können die Neuerstellung im Multithreadmodus ausführen. Wenn mehr als 10 CPUs verfügbar sind, ist die Neuerstellung ggf. schneller als der Import, falls dabei alle CPUs genutzt werden können.  
  
         Wenn ein Volltextkatalog nicht verfügbar ist, werden die zugehörigen Volltextindizes neu erstellt. Diese Option ist nur für [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] -Datenbanken verfügbar.  
  
         **Neu erstellen**  
         Volltextkataloge werden mithilfe der neuen und verbesserten Worttrennmodule neu erstellt. Das Neuerstellen von Indizes kann einige Zeit dauern, und nach dem Upgrade ist ggf. eine beträchtliche Menge an CPU-Leistung und Arbeitsspeicherkapazität erforderlich.  
  
         **Zurücksetzen**  
         Volltextkataloge werden zurückgesetzt. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Volltextkatalogdateien werden entfernt. Die Metadaten für die Volltextkataloge und die Volltextindizes bleiben jedoch erhalten. Nach der Upgrade wird die Änderungsnachverfolgung für alle Volltextindizes deaktiviert, und Durchforstungen werden nicht automatisch gestartet. Der Katalog bleibt leer, bis Sie ihn nach Beendigung des Upgrades manuell vollständig auffüllen.  
  
         Informationen zum Auswählen einer Option für das Volltextupgrade finden Sie unter[Upgrade der Volltextsuche](../../relational-databases/search/upgrade-full-text-search.md).  
  
        > [!NOTE]  
        >  Die Option für das Volltextupgrade kann auch mit der [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)**upgrade_option** -Aktion festgelegt werden.  
  
##  <a name="metadata"></a> Anzeigen zusätzlicher Volltextservereigenschaften  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktionen können verwendet werden, um die Werte verschiedener Eigenschaften der Volltextsuche auf Serverebene abzurufen. Diese Informationen sind für die Verwaltung und Problembehandlung der Volltextsuche hilfreich.  
  
 In der folgenden Tabelle werden die Volltexteigenschaften einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Serverinstanz und die zugehörigen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Funktionen aufgeführt.  
  
|Eigenschaft|Description|Funktion|  
|--------------|-----------------|--------------|  
|**IsFullTextInstalled**|Gibt an, ob die Volltextkomponente mit der aktuellen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]installiert wurde.|[FULLTEXTSERVICEPROPERTY](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)<br /><br /> [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)|  
||||  
|**LoadOSResources**|Gibt an, ob Wörtertrennungen und Filter des Betriebssystems mit dieser Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]registriert und verwendet werden.|FULLTEXTSERVICEPROPERTY|  
|**VerifySignature**|Gibt an, ob ausschließlich signierte Binärdateien vom Volltextmodul geladen werden.|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> Überwachen der Volltextsuchaktivität  
 Verschiedene dynamische Verwaltungssichten und -funktionen eignen sich für die Überwachung von Volltextsuchaktivitäten auf einer Serverinstanz.  
  
 **So zeigen Sie Informationen über Volltextkataloge mit Auffüllungsaktivitäten an**  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
 **So zeigen Sie die aktuelle Aktivität eines Filterdaemon-Hostprozesses an**  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
 **So zeigen Sie Informationen über aktive Indexauffüllungen an**  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
 **So zeigen Sie die Speicherpuffer in einem Speicherpool an, die für eine Durchforstung oder Durchforstungsbereich verwendet werden**  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
 **So zeigen Sie Informationen zu den Shared Memory-Pools an, die für die Volltext-Gatherer-Komponente für einen Volltext-Crawl-Vorgang oder einen Volltext-Crawl-Bereich zur Verfügung stehen**  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
 **So zeigen Sie Informationen zu den einzelnen Volltextindizierungs-Batches an**  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
 **So zeigen Sie Informationen über die spezifischen Bereiche einer aktiven Auffüllung an**  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  
