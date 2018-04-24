---
title: ALTER MESSAGE TYPE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_MESSAGE_TYPE_TSQL
- ALTER MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER MESSAGE TYPE statement
- modifying message types
- message types [Service Broker], modifying
ms.assetid: 98c94176-2bdf-4725-b4bc-d33b6b14817d
caps.latest.revision: 27
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfc68182a45984d492edf5638058f2b39dbb46ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="alter-message-type-transact-sql"></a>ALTER MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften eines Nachrichtentyps.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER MESSAGE TYPE message_type_name  
   VALIDATION =  
    {  NONE   
     | EMPTY   
     | WELL_FORMED_XML   
     | VALID_XML WITH SCHEMA COLLECTION schema_collection_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *message_type_name*  
 Der Name des Nachrichtentyps, der geändert werden soll. Server-, Datenbank- und Schemaname können nicht angegeben werden.  
  
 VALIDATION  
 Gibt an, wie [!INCLUDE[ssSB](../../includes/sssb-md.md)] den Nachrichtentext für Nachrichten von diesem Typ überprüft.  
  
 Keine  
 Es wird keine Überprüfung ausgeführt. Der Nachrichtentext kann beliebige Daten enthalten oder kann NULL sein.  
  
 EMPTY  
 Der Nachrichtentext muss NULL sein.  
  
 WELL_FORMED_XML  
 Der Nachrichtentext muss wohlgeformte XML-Daten enthalten.  
  
 VALID_XML_WITH_SCHEMA = *schema_collection_name*  
 Der Nachrichtentext muss XML-Daten enthalten, die einem Schema in der angegebenen Schemaauflistung entsprechen. *schema_collection_name* muss der Name einer vorhandenen XML-Schemaauflistung sein.  
  
## <a name="remarks"></a>Remarks  
 Das Ändern der Überprüfung eines Nachrichtentyps hat auf Nachrichten, die bereits an eine Warteschlange übermittelt wurden, keine Auswirkungen.  
  
 Verwenden Sie die ALTER AUTHORIZATION-Anweisung, wenn Sie AUTHORIZATION für einen Nachrichtentyp ändern möchten.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Ändern eines Nachrichtentyps wird standardmäßig Mitgliedern der festen Datenbankrollen **db_ddladmin** oder **db_owner** sowie Mitgliedern der festen Serverrolle **sysadmin** erteilt.  
  
 Wenn in der ALTER MESSAGE TYPE-Anweisung eine Schemaauflistung angegeben ist, muss der Benutzer, der die Anweisung ausführt, über die REFERENCES-Berechtigung in der angegebenen Schemaauflistung verfügen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Nachrichtentyp `//Adventure-Works.com/Expenses/SubmitExpense` geändert, sodass der Nachrichtentext ein wohlgeformtes XML-Dokument enthalten muss.  
  
```  
ALTER MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = WELL_FORMED_XML ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [DROP MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
