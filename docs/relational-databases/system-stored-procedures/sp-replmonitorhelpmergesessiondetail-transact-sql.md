---
title: Sp_replmonitorhelpmergesessiondetail (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_replmonitorhelpmergesessiondetail
- sp_replmonitorhelpmergesessiondetail_TSQL
helpviewer_keywords:
- sp_replmonitorhelpmergesessiondetail
ms.assetid: 805c92fc-3169-410c-984d-f37e063b791d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85338afafa7ca61b6cea5388c7a5f362edf35caa
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spreplmonitorhelpmergesessiondetail-transact-sql"></a>sp_replmonitorhelpmergesessiondetail (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt detaillierte Artikelinformationen zu einer bestimmten Replikationsmerge-Agent-Sitzung zurück, mit der die Mergereplikation überwacht wird. Das Resultset enthält eine detaillierte Zeile für jeden Artikel, der während der Sitzung synchronisiert wurde. Es enthält außerdem eine Zeile, die die Sitzungsinitialisierung darstellt, und Zeilen mit Zusammenfassungen der Upload- und Downloadphasen der Sitzung. Diese gespeicherte Prozedur wird auf dem Verteiler für die Verteilungsdatenbank oder auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replmonitorhelpmergesessiondetail [ @session_id = ] session_id  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@session_id**  =] *Session_id*  
 Gibt eine Agentsitzung an. *Session_id* ist **Int** hat keinen Standardwert.  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**PhaseID**|**int**|Die Phase der Synchronisierungssitzung. Die folgenden Werte sind möglich:<br /><br /> **0** = Initialisierungs- oder Zusammenfassungszeile<br /><br /> **1** = Upload<br /><br /> **2** = Download|  
|**ArticleName**|**sysname**|Der Name des Artikels, der synchronisiert wird. **ArticleName** enthält auch Zusammenfassungsinformationen für Zeilen im Resultset, die keine Artikeldetails darstellen.|  
|**PercentComplete**|**decimal**|Gibt die prozentualen Änderungen an, die insgesamt in einer Artikeldetailzeile für aktuell ausgeführte oder fehlerhafte Sitzungen angewendet wurden.|  
|**RelativeCost**|**decimal**|Gibt den Zeitaufwand zum Synchronisieren des Artikels als Prozentsatz der Gesamtsynchronisierungszeit für die Sitzung an.|  
|**Dauer**|**int**|Dauer der Agentsitzung|  
|**Inserts**|**int**|Anzahl von Einfügungen in einer Sitzung|  
|**Updates**|**int**|Anzahl von Updates in einer Sitzung|  
|**Löschvorgang**|**int**|Anzahl von Löschvorgängen in einer Sitzung|  
|**Konflikte**|**int**|Anzahl der in einer Sitzung aufgetretenen Konflikte|  
|**Fehler-ID**|**int**|ID eines Sitzungsfehlers|  
|**SeqNo**|**int**|Reihenfolge von Sitzungen im Resultset|  
|**Das RowType**|**int**|Gibt an, welchen Informationstyp jede Zeile im Resultset repräsentiert.<br /><br /> **0** = Initialisierung<br /><br /> **1** = uploadzusammenfassung<br /><br /> **2** = artikeluploaddetail<br /><br /> **3** = downloadzusammenfassung<br /><br /> **4** = artikeldownloaddetail|  
|**SchemaChanges**|**int**|Anzahl von Schemaänderungen in einer Sitzung|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_replmonitorhelpmergesessiondetail** wird zum Überwachen der Mergereplikation verwendet.  
  
 Wenn auf dem Abonnenten ausgeführt **Sp_replmonitorhelpmergesessiondetail** nur Gibt ausführliche Informationen zu den letzten 5 Merge-agentsitzungen zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der **Db_owner** oder **Replmonitor** festen Datenbankrolle "" für die Verteilungsdatenbank auf dem Verteiler oder für die Abonnementdatenbank auf dem Abonnenten ausführen kann **"sp_" Replmonitorhelpmergesessiondetail**.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
