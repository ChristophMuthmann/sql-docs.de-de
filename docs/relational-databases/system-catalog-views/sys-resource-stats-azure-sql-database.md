---
title: Sys. resource_stats (Azure SQL-Datenbank) | Microsoft Docs
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f1b2719813ecc58cc68477b47141a215f4880be
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2018
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Gibt die CPU-Nutzung und Speicherdaten für eine Azure SQL-Datenbank zurück. Die Daten werden in Intervallen von fünf Minuten gesammelt und aggregiert. Für jede Benutzerdatenbank wird eine Zeile für jedes fünfminütige Berichtsfenster erstellt, in dem sich der Ressourcenverbrauch ändert. Die zurückgegebenen Daten umfassen die CPU-Nutzung, Speichergröße oder Datenbank-SKU-Änderungen. Datenbanken im Leerlauf ohne Änderungen müssen Zeilen möglicherweise nicht für alle fünf-Minuten-Intervall. Verlaufsdaten werden ungefähr 14 Tage lang beibehalten.  
  
 Die **Sys. resource_stats** Ansicht verfügt über andere Definitionen abhängig von der Version der Azure SQL-Datenbankservers her, die die Datenbank zugeordnet ist. Berücksichtigen Sie diese Unterschiede und alle Änderungen, die Ihre Anwendung erfordert, beim Upgrade auf eine neue Serverversion.  
  
 Die folgende Tabelle beschreibt die verfügbaren Spalten bei einem Server mit der Version 12:  
  
|Spalten|Datentyp|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC-Zeit, der angibt, der des Anfang des Berichterstellungsintervalls fünf Minuten.|  
|end_time|**datetime**|UTC-Zeit, der angibt, des Ende des Berichterstellungsintervalls fünf Minuten.|  
|database_name|**varchar**|Name der Benutzerdatenbank.|  
|sku|**varchar**|Dienstebene der Datenbank. Folgende Werte sind möglich:<br /><br /> Standard<br /><br /> Standard<br /><br /> Premium<br /><br />Allgemeine Batchinstanzen<br /><br />Unternehmenswichtig|  
|storage_in_megabytes|**float**|Maximale Speichergröße in MB für den Zeitraum, einschließlich Datenbankdaten, Indizes, gespeicherte Prozeduren und Metadaten.|  
|avg_cpu_percent|**numeric**|Die durchschnittliche Servernutzung als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|avg_data_io_percent|**numeric**|Die durchschnittliche E/A-Nutzung als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|avg_log_write_percent|**numeric**|Die durchschnittliche Nutzung von Schreibressourcen als Prozentwert der maximalen Kapazität für die Dienstebene.|  
|max_worker_percent|**decimal(5,2)**|Maximale gleichzeitige Arbeitsthreads (Anforderungen) in Prozent basierend auf den Grenzwert der Dienstebene der Datenbank.<br /><br /> Maximale wird derzeit für das basierend auf den 15-Sekunden-Beispielen Anzahl gleichzeitiger Arbeitsthreads fünf-Minuten-Intervall berechnet.|  
|max_session_percent|**decimal(5,2)**|Maximaler gleichzeitiger Sitzungen in Prozent basierend auf den Grenzwert der Dienstebene der Datenbank.<br /><br /> Maximale wird derzeit für die fünf-Minuten-Intervall, das basierend auf den 15-Sekunden-Beispielen Anzahl gleichzeitiger Sitzungen berechnet.|  
|dtu_limit|**int**|Aktuelle maximale DTU datenbankeinstellung für diese Datenbank während dieses Intervalls. |  
  
> [!TIP]  
>  Mehr Kontext zu diesen Grenzwerten und Dienstebenen finden Sie unter den Themen [Dienstebenen](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/).  
    
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="remarks"></a>Hinweise  
 Die zurückgegebene Daten **Sys. resource_stats** wird angegeben als Prozentsatz des maximal zulässigen Grenzwerte für den Dienst/Leistungsebene, die Sie ausgeführt werden.  
  
 Wenn eine Datenbank einem elastischen Pool angehört, Ressourcenstatistiken als Prozentangaben, dargestellt als der prozentuale Anteil der maximale Grenzwert für die Datenbanken als Gruppe in der Konfiguration des elastischen Pools ausgedrückt.  
  
 Verwenden Sie für eine genauere Ansicht dieser Daten, **dm_db_resource_stats** -verwaltungssicht in einer Benutzerdatenbank. In dieser Ansicht werden Daten alle 15 Sekunden erfasst und verwaltet Daten zur Versionsgeschichte für 1 Stunde.  Weitere Informationen finden Sie unter [dm_db_resource_stats &#40;Azure SQL-Datenbank&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden alle Datenbanken zurückgegeben, die in der letzten Woche mindestens 80 % der Serverkapazität genutzt haben.  
  
```sql  
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
    
## <a name="see-also"></a>Siehe auch  
 [Dienstebenen](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [Dienst-Tier-Funktionen und Beschränkungen](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
