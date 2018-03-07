---
title: ALTER SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 69756a85873ddae09780e28b2ccc5481659e563f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert einen vorhandenen Dienst.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  
## <a name="arguments"></a>Argumente  
 *Dienstname*  
 Der Name des zu ändernden Diensts. Server-, Datenbank- und Schemaname können nicht angegeben werden.  
  
 ON-Warteschlange [ *Schema_name***.** ] *Warteschlangenname*  
 Gibt die neue Warteschlange für diesen Dienst an. [!INCLUDE[ssSB](../../includes/sssb-md.md)] verschiebt alle Meldungen für diesen Dienst aus der aktuellen Warteschlange in die neue.  
  
 Vertrag hinzufügen *Contract_name*  
 Gibt einen Vertrag an, der dem durch diesen Dienst verfügbar gemachten Vertragssatz hinzugefügt werden soll.  
  
 DROP CONTRACT *Contract_name*  
 Gibt einen Vertrag an, der aus dem von diesem Dienst verfügbar gemachten Vertragssatz gelöscht werden soll. [!INCLUDE[ssSB](../../includes/sssb-md.md)] sendet eine Fehlermeldung die vorhandene Konversationen mit diesem Dienst, die diesen Vertrag verwenden.  
  
## <a name="remarks"></a>Hinweise  
 Wenn mithilfe der ALTER SERVICE-Anweisung ein Vertrag aus einem Dienst gelöscht wird, kann der Dienst kein Ziel für Konversationen mehr sein, die diesen Vertrag verwenden. Deshalb lässt [!INCLUDE[ssSB](../../includes/sssb-md.md)] keine neuen Konversationen mit dem Dienst für diesen Vertrag zu. Bestehende Konversationen, die den Vertrag verwenden, sind davon nicht betroffen.  
  
 Verwenden Sie die ALTER AUTHORIZATION-Anweisung, wenn Sie AUTHORIZATION für einen Dienst ändern möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Berechtigung zum Ändern eines Diensts erhalten standardmäßig der Besitzer des Diensts, Mitglieder der der **Db_ddladmin** oder **Db_owner** festen Datenbankrollen und Mitglieder der **Sysadmin** feste Serverrolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. Ändern der Warteschlange für einen Dienst  
 Im folgenden Beispiel wird der `//Adventure-Works.com/Expenses`-Dienst so geändert, dass er die Warteschlange `NewQueue` verwendet.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. Hinzufügen eines neuen Vertrags zum Dienst  
 Im folgenden Beispiel wird der `//Adventure-Works.com/Expenses`-Dienst so geändert, dass Dialoge für den Vertrag `//Adventure-Works.com/Expenses` zugelassen sind.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. Hinzufügen eines neuen Vertrags zum Dienst und Löschen des vorhandenen Vertrags  
 Im folgenden Beispiel wird der `//Adventure-Works.com/Expenses`-Dienst so geändert, dass Dialoge für den Vertrag `//Adventure-Works.com/Expenses/ExpenseProcessing` zugelassen sind und Dialoge für den Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission` nicht zugelassen sind.  
  
```  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP SERVICE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
