---
title: Sp_repldone (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
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
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: afc84474a5aff0fff81efc702239dfa3f0ff85e7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sprepldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Aktualisiert den Datensatz, mit dem die letzte verteilte Transaktion des Servers identifiziert wird. Diese gespeicherte Prozedur wird auf dem Verleger für die Veröffentlichungsdatenbank ausgeführt.  
  
> [!CAUTION]  
>  Wenn Sie nicht ausführen **Sp_repldone** manuell, Sie die Reihenfolge und Konsistenz übermittelter Transaktionen ungültig werden können. **Sp_repldone** sollte nur für die Problembehandlung bei der Replikation erfahrener ein Supportmitarbeiter verwendet werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@xactid=**] *Xactid*  
 Ist die protokollfolgenummer (LSN) des ersten Datensatzes für die letzte verteilte Transaktion des Servers an. *Xactid* ist **("Binary(10)").**, hat keinen Standardwert.  
  
 [  **@xact_seqno=**] *Xact_seqno*  
 Ist die LSN des letzten Datensatzes für die letzte verteilte Transaktion des Servers an. *Xact_seqno* ist **("Binary(10)").**, hat keinen Standardwert.  
  
 [  **@numtrans=**] *Numtrans*  
 Ist die Anzahl der verteilten Transaktionen. *Numtrans* ist **Int**, hat keinen Standardwert.  
  
 [  **@time=**] *Zeit*  
 Entspricht der Anzahl an Millisekunden (sofern angegeben), die für die Verteilung des letzten Transaktionsbatches erforderlich ist. *Zeit* ist **Int**, hat keinen Standardwert.  
  
 [  **@reset=**] *zurücksetzen*  
 Entspricht dem Rücksetzungsstatus. *Zurücksetzen* ist **Int**, hat keinen Standardwert. Wenn **1**, werden alle replizierten Transaktionen im Protokoll markiert werden als verteilt. Wenn **0**, wird das Transaktionsprotokoll auf die erste replizierte Transaktion zurückgesetzt und keine replizierten Transaktionen gekennzeichnet werden als verteilt. *Zurücksetzen* ist nur gültig, wenn beide *Xactid* und *Xact_seqno* NULL sind.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **Sp_repldone** wird bei der Transaktionsreplikation verwendet.  
  
 **Sp_repldone** wird vom Protokollleserprozess verwendet, um nachzuverfolgen, welche Transaktionen verteilt wurden.  
  
 Mit **Sp_repldone**, Sie können dem Server manuell mitteilen, dass eine Transaktion repliziert (an den Verteiler gesendet) wurde. Außerdem haben Sie damit die Möglichkeit, anstelle der entsprechend markierten Transaktion eine andere Transaktion für die nächste Replikation festzulegen. Sie können sich in der Liste mit den replizierten Transaktionen vorwärts oder rückwärts bewegen (alle Transaktionen vor dieser Transaktion und diese selbst werden als verteilt gekennzeichnet).  
  
 Die erforderlichen Parameter *Xactid* und *Xact_seqno* erhalten Sie, indem Sie mithilfe von **Sp_repltrans** oder **Sp_replcmds**.  
  
## <a name="permissions"></a>Berechtigungen  
 Mitglieder der **Sysadmin** festen Serverrolle oder die **Db_owner** feste Datenbankrolle können ausführen **Sp_repldone**.  
  
## <a name="examples"></a>Beispiele  
 Wenn *Xactid* NULL ist, *Xact_seqno* NULL ist, und *zurücksetzen* ist **1**, werden alle replizierten Transaktionen im Protokoll markiert werden als verteilt. Dies bietet sich an, wenn replizierte Transaktionen im Protokoll nicht mehr gültig sind und das Protokoll abgeschnitten werden soll, wie im folgenden Beispiel:  
  
```  
EXEC sp_repldone @xactid = NULL, @xact_segno = NULL, @numtrans = 0,     @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  Diese Prozedur kann in Notsituationen verwendet werden, damit das Transaktionsprotokoll abgeschnitten werden kann, wenn Transaktionen mit ausstehender Replikation vorhanden sind.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [Sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
