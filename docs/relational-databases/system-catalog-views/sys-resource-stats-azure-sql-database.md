---
title: Sys. resource_stats (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: 
ms.date: 05/23/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
caps.latest.revision: "28"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dad039b91c30e4c8d89168dd90d549ec6507c750
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt die CPU-Nutzung und Speicherdaten für eine Azure SQL-Datenbank zurück. Die Daten werden in Intervallen von fünf Minuten gesammelt und aggregiert. Für jede Benutzerdatenbank wird eine Zeile für jedes fünfminütige Berichtsfenster erstellt, in dem sich der Ressourcenverbrauch ändert. Dies schließt die CPU-Auslastung, Änderung der Speichergröße und Datenbank-SKU-Änderungen ein. Datenbanken im Leerlauf ohne Änderungen enthalten u. U. nicht für jedes Intervall von fünf Minuten eine Zeile. Verlaufsdaten werden ungefähr 14 Tage lang beibehalten.  
  
 Die **Sys. resource_stats** Ansicht verfügt über andere Definitionen abhängig von der Version der Azure SQL-Datenbankservers her, die die Datenbank zugeordnet ist. Berücksichtigen Sie diese Unterschiede und alle Änderungen, die Ihre Anwendung erfordert, beim Upgrade auf eine neue Serverversion.  
  
 Die folgende Tabelle beschreibt die verfügbaren Spalten bei einem Server mit der Version 12:  
  
|Spalten (Server mit der Version 12)|Datentyp|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC-Zeit, die den Anfang des 5-minütigen Berichtsintervalls angibt.|  
|end_time|**datetime**|UTC-Zeit, die das Ende des fünfminütigen Berichtsintervalls angibt.|  
|database_name|**varchar**|Name der Benutzerdatenbank.|  
|sku|**varchar**|Dienstebene der Datenbank. Folgende Werte sind möglich:<br /><br /> Standard<br /><br /> Standard<br /><br /> Premium|  
|storage_in_megabytes|**float**|Die maximale Speichergröße für den Zeitraum in MB, einschließlich Datenbankdaten, Indizes, gespeicherte Prozeduren und Metadaten.|  
|avg_cpu_percent|**numeric**|Die durchschnittliche Servernutzung als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|avg_data_io_percent|**numeric**|Die durchschnittliche E/A-Nutzung als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|avg_log_write_percent|**numeric**|Die durchschnittliche Nutzung von Schreibressourcen als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|max_worker_percent|**decimal(5,2) wird**|Maximale gleichzeitige Arbeitsthreads (Anforderungen) in Prozent basierend auf den Grenzwert der Dienstebene der Datenbank.<br /><br /> Maximale wird derzeit für das basierend auf den zweiten 15 Beispielen Anzahl gleichzeitiger Arbeitsthreads 5-Minuten-Intervall berechnet.|  
|max_session_percent|**decimal(5,2) wird**|Maximaler gleichzeitiger Sitzungen in Prozent basierend auf den Grenzwert der Dienstebene der Datenbank.<br /><br /> Maximale wird derzeit für das 5-Minuten-Intervall basierend auf den zweiten 15 Beispielen der Anzahl gleichzeitiger Sitzungen Anzahlen berechnet.|  
|dtu_limit|**int**|Aktuelle maximale DTU datenbankeinstellung für diese Datenbank während dieses Intervalls.|  
  
> [!TIP]  
>  Mehr Kontext zu diesen Grenzwerten und Dienstebenen finden Sie unter den Themen [Dienstebenen](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/) und [-Service-Tier-Funktionen und Beschränkungen](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/).  
  
 Die folgende Tabelle beschreibt die verfügbaren Spalten bei einem Server mit der Version 11:  
  
|Spalten (Server mit der Version 11)|Datentyp|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC-Zeit, die den Anfang des 5-minütigen Berichtsintervalls angibt.|  
|end_time|**datetime**|UTC-Zeit, die das Ende des fünfminütigen Berichtsintervalls angibt.|  
|database_name|**nvarchar**|Der Name der Datenbank.|  
|sku|**nvarchar**|Dienstebene der Datenbank. Folgende Werte sind möglich:<br /><br /> Web<br /><br /> Business<br /><br /> Standard<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|*Hinweis: Diese Spalte ist für v11 veraltet, und sein Wert immer auf 0 festgelegt wird.*<br /><br /> Die verwendete CPU-Zeit seit Durchführung der letzten Messung.<br /><br /> Für die CPU-Messung, wir empfehlen die Verwendung der **Avg_cpu_cores_used** -Spalte anstelle dieser Spalte.|  
|storage_in_megabytes|**decimal**|Die maximale Speichergröße für den Zeitraum in MB, einschließlich Datenbankdaten, Indizes, gespeicherte Prozeduren und Metadaten.|  
|avg_cpu_cores_used|**decimal**|*Hinweis: Diese Spalte ist für v11 veraltet, und sein Wert immer auf 0 festgelegt wird.*<br /><br /> Durchschnittliche CPU-Kerne, die in diesem Intervall verwendet wurden.|  
|avg_physical_read_iops|**decimal**|*Hinweis: Diese Spalte ist für v11 veraltet, und sein Wert immer auf 0 festgelegt wird.*<br /><br /> Durchschnittliche Lese-IOPS in diesem Intervall.|  
|avg_physical_write_iops|**decimal**|*Hinweis: Diese Spalte ist für v11 veraltet, und sein Wert immer auf 0 festgelegt wird.*<br /><br /> Durchschnittliche Schreib-IOPS in diesem Intervall.|  
|active_memory_used_kb|**bigint**|*Hinweis: Diese Spalte ist für v11 veraltet, und sein Wert immer auf 0 festgelegt wird.*<br /><br /> Die am Ende dieses Intervalls verwendete aktive Arbeitsspeicherkapazität.|  
|active_session_count|**int**|Die Anzahl der aktiven Sitzungen am Ende dieses Intervalls.|  
|active_worker_count|**int**|Die Anzahl der aktiven Arbeitsthreads am Ende dieses Intervalls.|  
|avg_cpu_percent|**decimal**|Die durchschnittliche Servernutzung als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|avg_physical_data_read_percent|**decimal**|Die durchschnittliche E/A-Nutzung als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|avg_log_write_percent|**decimal**|Die durchschnittliche Nutzung von Schreibressourcen als Prozentwert der maximalen Kapazität für die Dienstebene.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="remarks"></a>Hinweise  
 Die zurückgegebene Daten **Sys. resource_stats** wird angegeben als Prozentsatz des maximal zulässigen dtu-Grenzwerte für den Dienst/Leistungsebene, die Sie für Basic, Standard und Premium-Datenbanken ausgeführt werden.  Für die Web- und Businessebenen geben diese Zahlen den Prozentsatz in Bezug auf die Standard S2-Leistungsebene an.  Wenn zum Beispiel beim Ausführen mit einer Webdatenbank avg_cpu_percent den Wert 70% zurückgibt, weist dies auf 70% des S2-Ebenenhöchstwerts hin. Darüber hinaus kann für Web- und Businessebenen der Prozentsatz eine Zahl über 100% zurückgeben, was ebenfalls auf dem S2-Ebenenhöchstwert basiert.  
  
 Wenn eine Datenbank einem elastischen Pool angehört, Ressourcenstatistiken als Prozentangaben, dargestellt als den Prozentsatz der maximalen DTU-Grenzwerts für die Datenbanken als Gruppe in der Konfiguration des elastischen Pools ausgedrückt.  
  
 Verwenden Sie für eine genauere Ansicht dieser Daten, **dm_db_resource_stats** -verwaltungssicht in einer Benutzerdatenbank. Diese Sicht erfasst die Daten jede 15 Sekunden und behält die Verlaufsdaten eine Stunde bei.  Weitere Informationen finden Sie unter [dm_db_resource_stats &#40; Azure SQL-Datenbank &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Datenbanken zurückgegeben, die in der letzten Woche mindestens 80 % der Serverkapazität genutzt haben.  
  
```  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
  
 Mit dem folgenden Beispiel wird der durchschnittliche DTU-Verbrauch in Prozent für die angegebene Datenbank berechnet. (Diese Abfrage funktioniert nur für einen Server mit der Version 11.)  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
   FROM (VALUES (avg_cpu_percent), (avg_physical_data_read_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.resource_stats   
WHERE database_name = '<your db name>'   
ORDER BY end_time DESC;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Dienstebenen](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Dienst-Tier-Funktionen und Beschränkungen](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
