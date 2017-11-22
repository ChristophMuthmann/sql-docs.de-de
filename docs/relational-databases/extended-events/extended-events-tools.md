---
title: "Tools für erweiterte Ereignisse | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: extended-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
- xevents
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 91fd4695d0b68aabf95f3ba43d2cb30c18595bb8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="extended-events-tools"></a>Tools für erweiterte Ereignisse
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Sie können die folgenden Tools verwenden, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sitzungen für erweiterte Ereignisse zu erstellen und zu verwalten:  
  
-   DDL-Anweisungen (Data Definition Language, Datendefinitionssprache) Damit können Sie eine Sitzung für erweiterte Ereignisse erstellen und ändern.  
  
-   Dynamische Verwaltungssichten, Katalogsichten und Systemtabellen Diese ermöglichen Ihnen das Abrufen von Sitzungsdaten und Metadaten mithilfe von [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen. Anhand der Systemtabellen können Sie die Entsprechungen für vorhandene erweitere Ereignisse für SQL-Ablaufverfolgungs-Ereignisklassen und -Spalten bestimmen.  
  
-   Der Knoten **Erweiterte Ereignisse** von Objekt-Explorer. Auf diese Weise können Sie eine Sitzung starten, beenden oder löschen oder Sitzungsvorlagen importieren und exportieren.  
  
-   Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell-Anbieter. Dabei handelt es sich um ein leistungsstarkes Tool, mit dem Sie Sitzungen für erweiterte Ereignisse erstellen, ändern und verwalten können. Weitere Informationen finden Sie unter [Verwenden des PowerShell-Anbieters für erweiterte Ereignisse](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md).  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Damit können Sie die in den Themen zu erweiterten Ereignissen bereitgestellten Codebeispiele erstellen und ausführen. Weitere Informationen finden Sie unter [Objekt-Explorer](http://msdn.microsoft.com/library/469ea8e2-79b9-44c8-bb6f-f0e1c5dbf0f2).  
  
 Zusätzlich zu Sitzungen, die Sie erstellen, ist auf dem Server eine standardmäßige Systemintegritätssitzung vorhanden. In der Sitzung werden Systemdaten erfasst, mit deren Hilfe Sie Leistungsprobleme beheben können. Weitere Informationen finden Sie unter [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md).  
  
## <a name="ddl-statements"></a>DDL-Anweisungen  
 Verwenden Sie die folgenden DDL-Anweisungen, um eine Sitzung für erweiterte Ereignisse zu erstellen, zu ändern und zu löschen.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)|Erstellt ein Sitzungsobjekt für erweiterte Ereignisse, das die Quelle der Ereignisse, die Ereignissitzungsziele und die Ereignissitzungsparameter identifiziert.|  
|[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)|Startet oder beendet eine Ereignissitzung oder ändert die Konfiguration einer Ereignissitzung.|  
|[DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)|Löscht eine Ereignissitzung.|  
  
## <a name="catalog-views"></a>Katalogsichten  
 Verwenden Sie die folgenden Katalogsichten, um die beim Erstellen einer Ereignissitzung erstellten Metadaten abzurufen.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)|Listet alle Ereignissitzungsdefinitionen auf.|  
|[sys.server_event_session_actions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql.md)|Gibt für jede Aktion jedes Ereignisses einer Ereignissitzung eine Zeile zurück.|  
|[sys.server_event_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql.md)|Gibt für jedes Ereignis in einer Ereignissitzung eine Zeile zurück.|  
|[sys.server_event_session_fields &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql.md)|Gibt eine Zeile für jede anpassbare Spalte zurück, die explizit für Ereignisse und Ziele festgelegt wurde.|  
|[sys.server_event_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql.md)|Gibt für eine Ereignissitzung eine Zeile für jedes Ereignisziel zurück.|  
  
## <a name="dynamic-management-views"></a>Dynamische Verwaltungssichten  
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
  
## <a name="system-tables"></a>Systemtabellen  
 Verwenden Sie die folgenden Systemtabellen, um Informationen zu den Entsprechungen für erweiterte Ereignissen für SQL-Ablaufverfolgungs-Ereignisklassen und -Spalten abzurufen.  
  
|Name|Beschreibung|  
|----------|-----------------|  
|[trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)|Enthält eine Zeile für jedes einer SQL-Ablaufverfolgungs-Ereignisklasse zugeordnete Ereignis für erweiterte Ereignisse.|  
|[trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)|Enthält eine Zeile für jede Aktion für erweiterte Ereignisse, die der Spalten-ID für eine SQL-Ablaufverfolgung zugeordnet ist.|  
  
## <a name="see-also"></a>Siehe auch  
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Tabellen für erweiterte Ereignisse von SQL Server &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/6d52ff03-f5aa-4f0f-8c98-9b49dc76f94e)   
 [Verwenden der system_health-Sitzung](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [Verwenden des PowerShell-Anbieters für erweiterte Ereignisse](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)  
  
  
