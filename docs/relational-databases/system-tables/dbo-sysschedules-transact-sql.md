---
title: dbo.sysschedules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dbo.sysschedules_TSQL
- sysschedules
- sysschedules_TSQL
- dbo.sysschedules
dev_langs:
- TSQL
helpviewer_keywords:
- sysschedules system table
ms.assetid: 4cac9237-7a69-4035-bb3e-928b76aad698
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 15c683b263b8026503754e137d91d72e5ee7f0ce
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="dbosysschedules-transact-sql"></a>dbo.sysschedules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Enthält Informationen zu Auftragszeitplänen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents. Diese Tabelle wird in der **msdb** -Datenbank gespeichert.  
  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**schedule_id**|**int**|ID des Auftragszeitplans des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agents.|  
|**schedule_uid**|**uniqueidentifier**|Eindeutiger Bezeichner des Auftragszeitplans. Anhand dieses Wertes wird ein Zeitplan für verteilte Aufträge identifiziert.|  
|**originating_server_id**|**int**|ID des Masterservers, von dem der Auftragszeitplan stammt.|  
|**name**|**Sysname (nvarchar(128))**|Benutzerdefinierter Name für den Auftragszeitplan. Dieser Name muss innerhalb eines Auftrags eindeutig sein.|  
|**owner_sid**|**varbinary(85)**|Microsoft Windows *Security_identifier* des Benutzers oder der Gruppe, die den Auftragszeitplan besitzt.|  
|**Aktiviert**|**int**|Status des Auftragszeitplans:<br /><br /> **0** = nicht aktiviert.<br /><br /> **1** = Aktiviert.<br /><br /> Wenn der Zeitplan nicht aktiviert ist, werden keine Aufträge auf dem Zeitplan ausgeführt.|  
|**freq_type**|**int**|Häufigkeit der Ausführung eines Auftrags für diesen Zeitplan.<br /><br /> **1** = nur einmal<br /><br /> **4** = täglich<br /><br /> **8** = wöchentlich<br /><br /> **16** = monatlich<br /><br /> **32** = monatlich, relativ zum **Freq_interval**<br /><br /> **64** = wird ausgeführt, wenn der SQL Server-Agent-Dienst gestartet wird<br /><br /> **128** = wird ausgeführt, wenn der Computer im Leerlauf befindet.|  
|**freq_interval**|**int**|Tage, an denen der Auftrag ausgeführt wird. Hängt vom Wert der **Freq_type**. Der Standardwert ist **0**, gibt an, dass **Freq_interval** wird nicht verwendet. Finden Sie in der nachfolgenden Tabelle die möglichen Werte und deren Auswirkungen.|  
|**freq_subday_type**|**int**|Einheiten für die **Freq_subday_interval**. Im folgenden sind die möglichen Werte und deren Beschreibungen.<br /><br /> <br /><br /> **1** : zum angegebenen Zeitpunkt<br /><br /> **2** : Sekunden<br /><br /> **4** : Minuten<br /><br /> **8** : Stunden|  
|**freq_subday_interval**|**int**|Anzahl der **Freq_subday_type** -Perioden zwischen den einzelnen Ausführungen des Auftrags auftreten.|  
|**freq_relative_interval**|**int**|Wenn **Freq_interval** in jedem Monat tritt auf, wenn **Freq_interval** ist **32** (mit relativem Monatsintervall). Folgende Werte sind möglich:<br /><br /> **0** = **Freq_relative_interval** wird nicht verwendet<br /><br /> **1** = erster<br /><br /> **2** = Sekunde<br /><br /> **4** = Dritter<br /><br /> **8** = vierter<br /><br /> **16** = letzter|  
|**freq_recurrence_**<br /><br /> **factor**|**int**|Die Anzahl der Wochen oder Monate zwischen den geplanten Ausführungen eines Auftrags. **Freq_recurrence_factor** wird nur verwendet, wenn **Freq_type** ist **8**, **16**, oder **32**. Wenn diese Spalte enthält **0**, **Freq_recurrence_factor** wird nicht verwendet.|  
|**active_start_date**|**int**|Datum, an dem die Ausführung eines Auftrags beginnen kann. Das Datum wird das Format YYYYMMDD. NULL steht für das Datum des heutigen Tages.|  
|**active_end_date**|**int**|Datum, an dem die Ausführung eines Auftrags enden kann. Für das Datum wird das Format YYYYMMDD verwendet.|  
|**active_start_time**|**int**|Uhrzeit an einem beliebigen Tag zwischen **Active_start_date** und **Active_end_date** , das dem Auftrag mit der Ausführung beginnt. Die Zeit wird als HHMMSS im 24-Stunden-Format angegeben.|  
|**active_end_time**|**int**|Uhrzeit an einem beliebigen Tag zwischen **Active_start_date** und **Active_end_date** , das dem Auftrag wird beendet. Die Zeit wird als HHMMSS im 24-Stunden-Format angegeben.|  
|**date_created**|**datetime**|Datum und Uhrzeit des Zeitpunkts, an dem der Zeitplan erstellt wurde.|  
|**date_modified**|**datetime**|Datum und Uhrzeit der letzten Änderung des Zeitplans.|  
|**version_number**|**int**|Aktuelle Versionsnummer des Zeitplans. Wenn ein Zeitplan 10-Mal geändert wurde beispielsweise die **Version_number** ist 10.|  
  
|Wert von freq_type|Auswirkung auf freq_interval|  
|-------------------------|------------------------------|  
|**1** (einmal)|**Freq_interval** wird nicht verwendet (**0**)|  
|**4** (täglich)|Jede **Freq_interval** Tage|  
|**8** (wöchentlich)|**Freq_interval** kann einen oder mehrere der folgenden:<br /><br /> **1** = Sonntag<br /><br /> **2** = Montag<br /><br /> **4** = Dienstag<br /><br /> **8** = Mittwoch<br /><br /> **16** = Donnerstag<br /><br /> **32** = Freitag<br /><br /> **64** = Samstag|  
|**16** (monatlich)|Auf der **Freq_interval** Tag des Monats|  
|**32** (monatlich, relativ)|**Freq_interval** ist eines der folgenden:<br /><br /> **1** = Sonntag<br /><br /> **2** = Montag<br /><br /> **3** = Dienstag<br /><br /> **4** = Mittwoch<br /><br /> **5** = Donnerstag<br /><br /> **6** = Freitag<br /><br /> **7** = Samstag<br /><br /> **8** = Tag<br /><br /> **9** = Arbeitstag<br /><br /> **10** = Wochenendtag|  
|**64** (wird beim SQL Server-Agent-Dienst gestartet)|**Freq_interval** wird nicht verwendet (**0**)|  
|**128** (wird ausgeführt, wenn der Computer im Leerlauf befindet)|**Freq_interval** wird nicht verwendet (**0**)|  
  
## <a name="see-also"></a>Siehe auch  
 [dbo.sysjobschedules & #40; Transact-SQL & #41;](../../relational-databases/system-tables/dbo-sysjobschedules-transact-sql.md)  
  
  
