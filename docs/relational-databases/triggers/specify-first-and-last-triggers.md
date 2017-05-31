---
title: Angeben des ersten und des letzten Triggers | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-dml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- first triggers [SQL Server]
- last triggers
- DML triggers, first or last triggers
- INSTEAD OF triggers
- AFTER triggers
ms.assetid: 9e6c7684-3dd3-46bb-b7be-523b33fae4d5
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99935796043bf8ea14c32a2f98867ca2c7612a2d
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="specify-first-and-last-triggers"></a>Angeben des ersten und des letzten Triggers
  Sie können angeben, dass einer der AFTER-Trigger, der einer Tabelle zugeordnet ist, der erste oder der letzte AFTER-Trigger ist, der für jede der auslösenden INSERT-, DELETE- und UPDATE-Aktionen ausgelöst wird. Die AFTER-Trigger, die zwischen dem ersten und letzten Trigger ausgelöst werden, werden in einer nicht definierten Reihenfolge ausgeführt.  
  
 Um die Ausführungsreihenfolge für einen AFTER-Trigger anzugeben, verwenden Sie die gespeicherte Prozedur **sp_settriggerorder** . **sp_settriggerorder** besitzt die folgenden Optionen.  
  
|Option|Beschreibung|  
|------------|-----------------|  
|**Erster**|Gibt an, dass der DML-Trigger der erste AFTER-Trigger ist, der für eine Triggeraktion ausgelöst wird.|  
|**Letzter**|Gibt an, dass der DML-Trigger der letzte AFTER-Trigger ist, der für eine Triggeraktion ausgelöst wird.|  
|**Keine**|Gibt an, dass keine besondere Reihenfolge vorhanden ist, in der der DML-Trigger ausgelöst werden soll. Diese Option wird hauptsächlich verwendet, um einen ersten oder letzten Trigger zurückzusetzen.|  
  
 Das folgende Beispiel zeigt die Verwendung von **sp_settriggerorder**:  
  
```  
sp_settriggerorder @triggername = 'MyTrigger', @order = 'first', @stmttype = 'UPDATE'  
```  
  
> [!IMPORTANT]  
>  Der erste und der letzte Trigger müssen zwei unterschiedliche Trigger sein.  
  
 Für eine Tabelle können gleichzeitig INSERT-, UPDATE- und DELETE-Trigger definiert sein. Jeder Anweisungstyp kann über eigene erste und letzte Trigger verfügen; es darf sich dabei jedoch nicht um dieselben Trigger handeln.  
  
 Wenn der für eine Tabelle definierte erste oder letzte Trigger keine Triggeraktion abdeckt, wie beispielsweise FOR UPDATE, FOR DELETE oder FOR INSERT, gibt es keinen ersten oder letzten Trigger für die fehlenden Aktionen.  
  
 INSTEAD OF-Trigger können nicht als erste oder letzte Trigger angegeben werden. INSTEAD OF-Trigger werden ausgelöst, bevor Updates an den zugrunde liegenden Tabellen vorgenommen werden. Wenn die Updates an zugrunde liegenden Tabellen durch einen INSTEAD OF-Trigger vorgenommen werden, erfolgen die Updates, bevor einer der für die Tabelle definierten AFTER-Trigger ausgelöst wird. Wenn z. B. ein INSTEAD OF INSERT-Trigger für eine Sicht Daten in eine Basistabelle einfügt und die Basistabelle selbst einen INSTEAD OF INSERT-Trigger und drei AFTER INSERT-Trigger enthält, wird der INSTEAD OF INSERT-Trigger für die Basistabelle statt der Einfügeaktion ausgelöst, und die AFTER-Trigger für die Basistabelle werden nach einer Einfügeaktion für die Basistabelle ausgelöst. Weitere Informationen finden Sie unter [DML Triggers](../../relational-databases/triggers/dml-triggers.md).  
  
 Wenn eine ALTER TRIGGER-Anweisung den ersten oder letzten Trigger ändert, wird das **First** - oder **Last** -Attribut gelöscht, und der Reihenfolgewert wird auf **None**festgelegt. Die Reihenfolge muss mit **sp_settriggerorder**zurückgesetzt werden.  
  
 Die OBJECTPROPERTY-Funktion gibt mithilfe der **ExecIsFirstTrigger** - und **ExecIsLastTrigger**-Eigenschaften an, ob es sich um einen ersten oder letzten Trigger handelt.  
  
 Die Replikation generiert automatisch einen ersten Trigger für alle Tabellen, die in einem Abonnement mit sofortigem Update oder verzögertem Update über eine Warteschlange enthalten sind. Für die Replikation gilt, dass ihr Trigger der erste Trigger sein muss. Die Replikation meldet einen Fehler, wenn Sie versuchen, eine Tabelle, die einen ersten Trigger aufweist, in ein Abonnement mit sofortigem Update bzw. verzögertem Update über eine Warteschlange einzufügen. Wenn Sie versuchen, einen Trigger zum ersten Trigger zu erklären, nachdem eine Tabelle in ein Abonnement aufgenommen wurde, gibt **sp_settriggerorder** einen Fehler zurück. Wenn Sie ALTER für den Replikationstrigger verwenden oder **sp_settriggerorder** verwenden, um den Replikationstrigger auf einen Trigger vom Typ LAST oder NONE festzulegen, funktioniert das Abonnement nicht ordnungsgemäß.  
  
## <a name="see-also"></a>Siehe auch  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_settriggerorder &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-settriggerorder-transact-sql.md)  
  
  
