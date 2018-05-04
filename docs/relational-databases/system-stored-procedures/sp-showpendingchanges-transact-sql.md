---
title: Sp_showpendingchanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9b05623d177bac68c5aafe0b4ac9df2931b27732
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="spshowpendingchanges-transact-sql"></a>sp_showpendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt ein Resultset zurück, das die Änderungen anzeigt, die noch repliziert werden müssen. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank und auf dem Abonnenten für die Abonnementdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  Diese Prozedur liefert einen geschätzten Wert für die Anzahl der Änderungen und die an diesen Änderungen beteiligten Zeilen. Beispielsweise ruft die Prozedur Informationen entweder vom Verleger oder vom Abonnenten ab, jedoch nicht beides gleichzeitig. Informationen, die im anderen Knoten gespeichert sind, ergeben möglicherweise einen kleineren Änderungssatz für die Synchronisierung als von der Prozedur geschätzt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_showpendingchanges [ [ @destination_server = ] 'destination_server' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article']  
    [ , [ @show_rows = ] show_rows]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @destination_server **=** ] **"***Destination_server***"**  
 Der Name des Servers, auf dem die replizierten Änderungen angewendet werden. *Destination_server* ist **Sysname**, mit dem Standardwert NULL.  
  
 [ @publication **=** ] **"***Veröffentlichung***"**  
 Der Name der Veröffentlichung. *Veröffentlichung* ist **Sysname**, hat den Standardwert NULL. Wenn *Veröffentlichung* angegeben ist, werden die Ergebnisse auf die angegebene Veröffentlichung beschränkt.  
  
 [ @article **=** ] **"***Artikel***"**  
 Der Name des Artikels. *Artikel* ist **Sysname**, hat den Standardwert NULL. Wenn *Artikel* angegeben ist, werden die Ergebnisse nur auf den angegebenen Artikel beschränkt.  
  
 [ @show_rows **=** ] *Show_rows*  
 Gibt an, ob das Resultset spezifischere Informationen zu ausstehenden Änderungen, die mit einem Standardwert von enthält **0**. Wenn ein Wert von **1** angegeben ist, wird das Resultset enthält die Spalten Is_delete und Rowguid.  
  
## <a name="result-set"></a>Resultset  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|Name des Servers, auf den die Änderungen repliziert werden|  
|pub_name|**sysname**|Der Name der Veröffentlichung.|  
|destination_db_name|**sysname**|Name der Datenbank, in die die Änderungen repliziert werden|  
|is_dest_subscriber|**bit**|Gibt an, ob Änderungen auf einen Abonnenten repliziert werden. Der Wert **1** gibt an, dass die Änderungen an einen Abonnenten repliziert werden. **0** bedeutet, dass Änderungen auf einen Verleger repliziert werden.|  
|article_name|**sysname**|Der Name des Artikels für die Tabelle, aus der die Änderungen stammen.|  
|pending_deletes|**int**|Die Anzahl von Löschvorgängen, die auf die Replikation warten.|  
|pending_ins_and_upd|**int**|Die Anzahl von Einfügungen und Updates, die auf die Replikation warten.|  
|is_delete|**bit**|Gibt an, ob die anstehende Änderung ein Löschvorgang ist. Der Wert **1** gibt an, dass die Änderung ein Löschvorgang ist. Erfordert einen Wert von **1** für @show_rows.|  
|rowguid|**uniqueidentifier**|Die GUID, die die geänderte Zeile identifiziert. Erfordert einen Wert von **1** für @show_rows.|  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 sp_showpendingchanges wird für die Mergereplikation verwendet.  
  
 sp_showpendingchanges wird für die Problembehandlung der Mergereplikation verwendet.  
  
 Das Ergebnis von sp_showpendingchanges enthält keine Zeilen in Generation 0.  
  
 Wenn ein Artikel für angegebene *Artikel* gehört nicht zu der für die angegebene Veröffentlichung *Veröffentlichung* für Pending_deletes und Pending_ins_and_upd die Anzahl 0 zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Serverrolle sysadmin oder der festen Datenbankrolle db_owner können sp_showpendingchanges ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Automatisierungsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
