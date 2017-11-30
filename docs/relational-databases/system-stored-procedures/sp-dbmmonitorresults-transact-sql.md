---
title: Sp_dbmmonitorresults (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
caps.latest.revision: "46"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9dd87ba18696c5787c3ee2220846a3dde857b660
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spdbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Statuszeilen für eine überwachte Datenbank aus der Statustabelle zurück, in der der Verlauf des Datenbankspiegelungs-Monitors gespeichert ist. Dabei können Sie angeben, ob die Prozedur zuvor den letzten Status abrufen soll.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Gibt die Datenbank an, für die der Spiegelungsstatus zurückgegeben werden soll.  
  
 *rows_to_return*  
 Gibt die Menge der zurückgegebenen Zeilen an:  
  
 0 = Letzte Zeile  
  
 1 = Zeilen der letzten 2 Stunden  
  
 2 = Zeilen der letzten 4 Stunden  
  
 3 = Zeilen der letzten 8 Stunden  
  
 4 = Zeilen des letzten Tages  
  
 5 = Zeilen der letzten 2 Tage  
  
 6 = letzte 100 Zeilen  
  
 7 = letzte 500 Zeilen  
  
 8 = letzte 1.000 Zeilen  
  
 9 = Die letzten 1.000.000 Zeilen  
  
 *update_status*  
 Gibt das Verhalten der Prozedur vor dem Zurückgeben der Ergebnisse an:  
  
 0 = Der Status der Datenbank wird nicht aktualisiert. Die Ergebnisse werden nur aus den letzten beiden Zeilen berechnet, deren Alter vom Aktualisierungszeitpunkt der Statustabelle abhängt.  
  
 1 = der Status für die Datenbank aktualisiert, durch den Aufruf **Sp_dbmmonitorupdate** vor dem Berechnen der Ergebnisse. Jedoch, wenn es sich bei der Aktualisierung der Statustabelle innerhalb der vorhergehenden 15 Sekunden, oder der Benutzer ist kein Mitglied von der **Sysadmin** festen Serverrolle **Sp_dbmmonitorresults** ausgeführt wird, ohne den Status aktualisieren.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Gibt die angeforderte Anzahl von Zeilen aus dem Statusverlauf für die angegebene Datenbank zurück. Jede Zeile enthält die folgenden Informationen:  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Name einer gespiegelten Datenbank.|  
|**Rolle ""**|**int**|Aktuelle Spiegelungsrolle der Serverinstanz:<br /><br /> 1 = Prinzipal<br /><br /> 2 = Spiegel|  
|**mirroring_state**|**int**|Status der Datenbank:<br /><br /> 0 = angehalten<br /><br /> 1 = getrennt<br /><br /> 2 = Wird synchronisiert<br /><br /> 3 = Ausstehendes Failover<br /><br /> 4 = Synchronisiert|  
|**witness_status**|**int**|Verbindungsstatus des Zeugen in der Datenbank-Spiegelungssitzung der Datenbank:<br /><br /> 0 = Unbekannt<br /><br /> 1 = Verbunden<br /><br /> 2 = Getrennt|  
|**log_generation_rate**|**int**|Umfang des seit dem vorhergehenden Update des Spiegelungsstatus dieser Datenbank generierten Protokolls in KB/s.|  
|**unsent_log**|**int**|Größe des nicht gesendeten Protokolls in der Sendewarteschlange auf dem Prinzipal in KB.|  
|**send_rate**|**int**|Senderate des Protokolls vom Prinzipal zum Spiegel in KB/s.|  
|**unrestored_log**|**int**|Größe der Wiederholungswarteschlange auf dem Spiegel in KB.|  
|**recovery_rate**|**int**|Wiederholungsrate auf dem Spiegel in KB/s.|  
|**transaction_delay**|**int**|Gesamtverzögerung für alle Transaktionen in Millisekunden.|  
|**transactions_per_sec**|**int**|Anzahl der Transaktionen, die pro Sekunde in der Prinzipalserverinstanz auftreten.|  
|**average_delay**|**int**|Durchschnittliche Verzögerung in der Prinzipalserverinstanz für jede Transaktion aufgrund der Datenbankspiegelung. Im Modus für hohe Leistung (d. h., wenn die SAFETY-Eigenschaft auf OFF festgelegt ist), ist dieser im Allgemeinen 0.|  
|**time_recorded**|**datetime**|Zeit, zu der die Zeile vom Datenbankspiegelungs-Monitor aufgezeichnet wurde. Dies ist die Systemuhrzeit auf dem Prinzipal.|  
|**time_behind**|**datetime**|Ungefähre Systemuhrzeit des Prinzipals, auf deren Stand die Spiegelungsdatenbank derzeit gebracht wird. Der Wert ist nur in der Prinzipalserverinstanz sinnvoll.|  
|**local_time**|**datetime**|Systemuhrzeit in der lokalen Serverinstanz, zu der diese Zeile aktualisiert wurde.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_dbmmonitorresults** ausgeführt werden kann, nur im Rahmen der **Msdb** Datenbank.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **Sysadmin** feste Serverrolle oder in der **Dbm_monitor** festen Datenbankrolle "" in der **Msdb** Datenbank. Die **Dbm_monitor** -Rolle ermöglicht ihren Mitgliedern das Anzeigen von Datenbank-Spiegelungsstatus, aber nicht aktualisieren, jedoch nicht anzeigen oder Konfigurieren der datenbankspiegelung auftretende Ereignisse.  
  
> [!NOTE]  
>  Bei der erstmaligen **Sp_dbmmonitorupdate** ausgeführt wird, erstellt der **Dbm_monitor** festen Datenbankrolle "" in der **Msdb** Datenbank. Mitglieder der **Sysadmin** -Serverrolle sysadmin kann beliebige Benutzer hinzufügen die **Dbm_monitor** festen Datenbankrolle "".  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Zeilen, die in den letzten 2 Stunden aufgezeichnet wurden, zurückgegeben, ohne dass der Status der Datenbank aktualisiert wird.  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Sp_dbmmonitorchangemonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [Sp_dbmmonitoraddmonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [Sp_dbmmonitordropmonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [Sp_dbmmonitorhelpmonitoring &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
