---
title: Sp_dbmmonitorchangealert (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
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
- sp_dbmmonitorchangealert_TSQL
- sp_dbmmonitorchangealert
dev_langs: TSQL
helpviewer_keywords:
- sp_dbmmonitorchangealert
- database mirroring [SQL Server], monitoring
ms.assetid: 1b29f82b-9cf8-4539-8d5c-9a1024db8a50
caps.latest.revision: "42"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 276f3b3f6f3194a311874db3724f07bf8ab053d0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="spdbmmonitorchangealert-transact-sql"></a>sp_dbmmonitorchangealert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Mit dieser Prozedur können Warnungsschwellenwerte für eine bestimmte Spiegelungsleistungsmetrik hinzugefügt oder geändert werden.  

  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_dbmmonitorchangealert database_name   
    , alert_id   
    , alert_threshold   
    , enabled   
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Gibt die Datenbank an, für die der angegebene Warnschwellenwert hinzugefügt oder geändert wurde.  
  
 *alert_id*  
 Ein ganzzahliger Wert, der die hinzuzufügende oder zu ändernde Warnung identifiziert. Geben Sie einen der folgenden Werte an.  
  
|Wert|Leistungsmetrik|Schwellenwert für Warnung|  
|-----------|------------------------|-----------------------|  
|1|Älteste, nicht gesendete Transaktion|Gibt die Menge an Transaktionen (in Anzahl Minuten) an, die sich in der Sendewarteschlange ansammeln dürfen, bevor auf der Prinzipalserverinstanz eine Warnung generiert wird. Diese Warnung bietet die Möglichkeit, die Wahrscheinlichkeit eines Datenverlusts im Hinblick auf die Zeit zu messen. Sie ist besonders relevant für den Modus für hohe Leistung. Die Warnung ist aber auch für den Modus für hohe Sicherheit relevant, wenn die Spiegelung angehalten oder unterbrochen wird, weil die Verbindung zwischen den Partnern getrennt wurde.|  
|2|Nicht gesendetes Protokoll|Gibt an, bei welcher Menge (in KB) an nicht gesendeten Protokolldaten eine Warnung auf der Prinzipalserverinstanz generiert wird. Diese Warnung bietet die Möglichkeit, die Wahrscheinlichkeit eines Datenverlusts in KB zu messen. Sie ist besonders relevant für den Modus für hohe Leistung. Die Warnung ist aber auch für den Modus für hohe Sicherheit relevant, wenn die Spiegelung angehalten oder unterbrochen wird, weil die Verbindung zwischen den Partnern getrennt wurde.|  
|3|Nicht wiederhergestelltes Protokoll|Gibt an, bei welcher Menge (in KB) an nicht wiederhergestellten Protokolldaten eine Warnung auf der Spiegelserverinstanz generiert wird. Diese Warnung ermöglicht die Messung der Failoverzeit. Die*Failoverzeit* besteht hauptsächlich aus der Zeit, die der frühere Spiegelserver benötigt, um ein Rollforward für die Protokolldaten auszuführen, die sich noch in seiner Wiederholungswarteschlange befinden, sowie einer zusätzlichen kurzen Zeitspanne.|  
|4|Spiegelungscommitaufwand|Gibt die durchschnittliche Verzögerung (in Anzahl der Millisekunden) pro Transaktion an, die toleriert wird, bevor auf dem Prinzipalserver eine Warnung generiert wird. Hierbei handelt es sich um die Verzögerung, die entsteht, während die Prinzipalserverinstanz darauf wartet, dass die Spiegelserverinstanz den Transaktionsprotokolldatensatz in die Wiederholungswarteschlange schreibt. Dieser Wert ist nur im Modus für hohe Sicherheit relevant.|  
|5|Beibehaltungsdauer|Metadaten, die steuern, wie lange Zeilen in der Datenbankspiegelungs-Statustabelle beibehalten werden.|  
  
 Weitere Informationen zu den Ereignis-IDs, die Warnungen entspricht, finden Sie unter [Verwenden von Warnungsschwellenwerten und Warnmeldungen für Spiegelungsleistungsmetriken &#40; SQLServer &#41; ](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
 *alert_threshold*  
 Der Schwellenwert für die Warnung. Wenn der Rückgabewert beim Aktualisieren des Spiegelungsstatus diesen Schwellenwert überschreitet, wird ein Eintrag im Windows-Ereignisprotokoll generiert. Der Wert stellt je nach Leistungsmetrik KB, Minuten oder Millisekunden dar.  
  
> [!NOTE]  
>  Um die aktuellen Werte anzuzeigen, führen Sie die [Sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) gespeicherte Prozedur.  
  
 *aktiviert*  
 Ist die Warnung aktiviert?  
  
 0 = Die Warnung ist deaktiviert.  
  
 1 = Die Warnung ist aktiviert.  
  
> [!NOTE]  
>  Die Beibehaltungsdauer ist immer aktiviert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 Keine  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der festen Serverrolle **sysadmin** .  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden Schwellenwerte für jede Leistungsmetrik sowie die Beibehaltungsdauer für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]-Datenbank festgelegt. In den folgende Tabelle werden die im Beispiel verwendeten Werte gezeigt.  
  
|*alert_id*|Leistungsmetrik|Schwellenwert für Warnung|Ist die Warnung aktiviert?|  
|-----------------|------------------------|-----------------------|-----------------------------|  
|1|Älteste, nicht gesendete Transaktion|30 Minuten|ja|  
|2|Nicht gesendetes Protokoll|10,000 KB|ja|  
|3|Nicht wiederhergestelltes Protokoll|10,000 KB|ja|  
|4|Spiegelungscommitaufwand|1.000 Millisekunden|Nein|  
|5|Beibehaltungsdauer|8 Stunden|ja|  
  
```  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 1, 30, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 2, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 3, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 4, 1000, 0 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 5, 8, 1 ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Überwachen der Datenbankspiegelung &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [Sp_dbmmonitorhelpalert &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
  
