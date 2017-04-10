---
title: "Tools f&#252;r erweiterte Ereignisse | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
  - "xevents"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Erweiterte Ereignisse [SQL Server], verwenden"
  - "Erweiterte Ereignisse [SQL Server], Optionen für die Verwendung"
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
caps.latest.revision: 19
author: "MightyPen"
ms.author: "genemi"
manager: "jhubbard"
caps.handback.revision: 19
---
# Tools f&#252;r erweiterte Ereignisse
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Sie können die folgenden Tools verwenden, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sitzungen für erweiterte Ereignisse zu erstellen und zu verwalten:  
  
-   DDL-Anweisungen (Data Definition Language, Datendefinitionssprache) Damit können Sie eine Sitzung für erweiterte Ereignisse erstellen und ändern.  
  
-   Dynamische Verwaltungssichten, Katalogsichten und Systemtabellen Diese ermöglichen Ihnen das Abrufen von Sitzungsdaten und Metadaten mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen. Anhand der Systemtabellen können Sie die Entsprechungen für vorhandene erweitere Ereignisse für SQL-Ablaufverfolgungs-Ereignisklassen und -Spalten bestimmen.  
  
-   Der Knoten **Erweiterte Ereignisse** von Objekt-Explorer. Auf diese Weise können Sie eine Sitzung starten, beenden oder löschen oder Sitzungsvorlagen importieren und exportieren.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Anbieter. Dabei handelt es sich um ein leistungsstarkes Tool, mit dem Sie Sitzungen für erweiterte Ereignisse erstellen, ändern und verwalten können. Weitere Informationen finden Sie unter [Verwenden des PowerShell-Anbieters für erweiterte Ereignisse](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Damit können Sie die in den Themen zu erweiterten Ereignissen bereitgestellten Codebeispiele erstellen und ausführen. Weitere Informationen finden Sie unter [Objekt-Explorer](../../ssms/object/object-explorer.md).  
  
 Zusätzlich zu Sitzungen, die Sie erstellen, ist auf dem Server eine standardmäßige Systemintegritätssitzung vorhanden. In der Sitzung werden Systemdaten erfasst, mit deren Hilfe Sie Leistungsprobleme beheben können. Weitere Informationen finden Sie unter [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## DDL-Anweisungen  
 Verwenden Sie die folgenden DDL-Anweisungen, um eine Sitzung für erweiterte Ereignisse zu erstellen, zu ändern und zu löschen.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)|Erstellt ein Sitzungsobjekt für erweiterte Ereignisse, das die Quelle der Ereignisse, die Ereignissitzungsziele und die Ereignissitzungsparameter identifiziert.|  
|[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)|Startet oder beendet eine Ereignissitzung oder ändert die Konfiguration einer Ereignissitzung.|  
|[DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)|Löscht eine Ereignissitzung.|  
  
## Katalogsichten  
 Verwenden Sie die folgenden Katalogsichten, um die beim Erstellen einer Ereignissitzung erstellten Metadaten abzurufen.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)|Listet alle Ereignissitzungsdefinitionen auf.|  
|[sys.server_event_session_actions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql.md)|Gibt für jede Aktion jedes Ereignisses einer Ereignissitzung eine Zeile zurück.|  
|[sys.server_event_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql.md)|Gibt für jedes Ereignis in einer Ereignissitzung eine Zeile zurück.|  
|[sys.server_event_session_fields &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql.md)|Gibt eine Zeile für jede anpassbare Spalte zurück, die explizit für Ereignisse und Ziele festgelegt wurde.|  
|[sys.server_event_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql.md)|Gibt für eine Ereignissitzung eine Zeile für jedes Ereignisziel zurück.|  
  
## Dynamische Verwaltungssichten  
 Verwenden Sie die folgenden dynamischen Verwaltungssichten, um Sitzungsmetadaten und Sitzungsdaten abzurufen. Die Metadaten werden aus den Katalogsichten abgerufen, und die Sitzungsdaten werden erstellt, wenn Sie eine Ereignissitzung starten und ausführen.  
  
> [!NOTE]  
>  Diese Sichten weisen erst Sitzungsdaten auf, wenn eine Sitzung gestartet wird.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|Gibt Informationen zu Sitzungsverteilerpools zurück.|  
|[sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)|Gibt eine Zeile für jedes Objekt zurück, das von einem Ereignispaket verfügbar gemacht wird.|  
|[sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)|Gibt die Schemainformationen für alle Objekte zurück.|  
|[sys.dm_xe_packages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql.md)|Listet alle für das Modul für erweiterte Ereignisse registrierten Pakete auf.|  
|[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)|Gibt Informationen über eine aktive Sitzung mit erweiterten Ereignissen zurück.|  
|[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)|Gibt Informationen über Sitzungsziele zurück.|  
|[sys.dm_xe_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql.md)|Gibt Informationen zu Sitzungsereignissen zurück.|  
|[sys.dm_xe_session_event_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql.md)|Gibt Informationen zu Ereignissitzungsaktionen zurück.|  
|[sys.dm_xe_map_values &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql.md)|Stellt eine Zuordnung von internen numerischen Schlüsseln zu für den Benutzer lesbarem Text bereit.|  
|[sys.dm_xe_session_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql.md)|Zeigt die Konfigurationswerte für Objekte an, die an eine Sitzung gebunden sind.|  
  
## Systemtabellen  
 Verwenden Sie die folgenden Systemtabellen, um Informationen zu den Entsprechungen für erweiterte Ereignissen für SQL-Ablaufverfolgungs-Ereignisklassen und -Spalten abzurufen.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[trace_xe_event_map &#40;Transact-SQL&#41;](../Topic/trace_xe_event_map%20\(Transact-SQL\).md)|Enthält eine Zeile für jedes einer SQL-Ablaufverfolgungs-Ereignisklasse zugeordnete Ereignis für erweiterte Ereignisse.|  
|[trace_xe_action_map &#40;Transact-SQL&#41;](../Topic/trace_xe_action_map%20\(Transact-SQL\).md)|Enthält eine Zeile für jede Aktion für erweiterte Ereignisse, die der Spalten-ID für eine SQL-Ablaufverfolgung zugeordnet ist.|  
  
## Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](../Topic/Dynamic%20Management%20Views%20and%20Functions%20\(Transact-SQL\).md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Tabellen für erweiterte Ereignisse von SQL Server &#40;Transact-SQL&#41;](../Topic/SQL%20Server%20Extended%20Events%20Tables%20\(Transact-SQL\).md)   
 [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [Verwenden des PowerShell-Anbieters für erweiterte Ereignisse](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)  
  
  