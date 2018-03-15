---
title: ALTER BROKER PRIORITY (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/03/2017
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
- ALTER_BROKER_TSQL
- ALTER BROKER PRIORITY
- ALTER BROKER
- ALTER_BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER BROKER PRIORITY statement
- ssbdiagnose
ms.assetid: 15fda1b2-e4dd-4f9d-935a-2e38926075b2
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 833c0bed38d02905b3a260f50824825c9859484f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="alter-broker-priority-transact-sql"></a>ALTER BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert die Eigenschaften einer [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Konversationspriorität.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
ALTER BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
{ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = { PriorityValue | DEFAULT } ]  
              )  
}  
[;]  
  
```  
  
## <a name="arguments"></a>Argumente  
 *ConversationPriorityName*  
 Gibt den Namen der zu ändernden Konversationspriorität an. Der Name muss auf eine Konversationspriorität in der aktuellen Datenbank verweisen.  
  
 SET  
 Gibt die Kriterien an, anhand derer bestimmt wird, ob die Konversationspriorität für eine Konversation übernommen wird. SET ist erforderlich und muss mindestens ein Kriterium enthalten: CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME oder PRIORITY_LEVEL.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 Gibt den Namen eines Vertrags an, der als Kriterium für die Festlegung verwendet wird, ob die Konversationspriorität für eine Konversation gelten soll. *ContractName* ist ein [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Bezeichner und muss den Namen eines Vertrags in der aktuellen Datenbank angeben.  
  
 *ContractName*  
 Gibt an, dass die Konversationspriorität nur für Konversationen übernommen werden kann, bei denen die BEGIN DIALOG-Anweisung, mit der die Konversation gestartet wurde, auf ON CONTRACT *ContractName* festgelegt ist.  
  
 ANY  
 Gibt an, dass die Konversationspriorität für jede Konversation unabhängig vom verwendeten Vertrag übernommen werden kann.  
  
 Wenn CONTRACT_NAME nicht angegeben ist, wird die Eigenschaft für den Vertrag der Konversationspriorität nicht geändert.  
  
 LOCAL_SERVICE_NAME = {*LocalServiceName* | **ANY**}  
 Gibt den Namen eines Diensts an, der als Kriterium verwendet werden kann, um zu bestimmen, ob die Konversationspriorität für einen Konversationsendpunkt übernommen wird.  
  
 *LocalServiceName* ist ein [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Bezeichner, der den Namen eines Diensts in der aktuellen Datenbank angeben muss.  
  
 *LocalServiceName*  
 Gibt an, dass die Konversationspriorität für Folgendes übernommen werden kann:  
  
-   Jeder Konversationsendpunkt für den Initiator, dessen Initiatordienstname *LocalServiceName* entspricht.  
  
-   Jeder Konversationsendpunkt für das Ziel, dessen Zieldienstname *LocalServiceName* entspricht.  
  
 ANY  
 -   Gibt an, dass die Konversationspriorität unabhängig vom Namen des vom Endpunkt verwendeten lokalen Diensts für jeden Konversationsendpunkt übernommen werden kann.  
  
 Wenn LOCAL_SERVICE_NAME nicht angegeben ist, wird die Eigenschaft für den lokalen Dienst der Konversationspriorität nicht geändert.  
  
 REMOTE_SERVICE_NAME = {'*RemoteServiceName*' | **ANY**}  
 Gibt den Namen eines Diensts an, der als Kriterium verwendet werden kann, um zu bestimmen, ob die Konversationspriorität für einen Konversationsendpunkt übernommen wird.  
  
 *RemoteServiceName* ist ein Literal vom Typ **nvarchar(256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwendet einen bitweisen Vergleich für den Abgleich der *RemoteServiceName*-Zeichenfolge. Bei dem Vergleich wird die Groß-/Kleinschreibung beachtet, die aktuelle Sortierung hingegen wird nicht berücksichtigt. Der Zieldienst kann in der aktuellen Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] oder in einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] vorhanden sein.  
  
 '*RemoteServiceName*'  
 Gibt an, dass die Konversationspriorität Folgendem zugewiesen werden kann:  
  
-   Jeder Konversationsendpunkt für den Initiator, dessen zugeordneter Zieldienstname *RemoteServiceName* entspricht.  
  
-   Jeder Konversationsendpunkt für das Ziel, dessen zugeordneter Initiatordienstname *RemoteServiceName* entspricht.  
  
 ANY  
 Gibt an, dass die Konversationspriorität unabhängig vom Namen des dem Endpunkt zugeordneten Remotediensts für jeden Konversationsendpunkt übernommen wird.  
  
 Wenn REMOTE_SERVICE_NAME nicht angegeben ist, wird die Eigenschaft für den Remotedienst der Konversationspriorität nicht geändert.  
  
 PRIORITY_LEVEL = { *PriorityValue* | **DEFAULT** }  
 Gibt die Prioritätsebene an, die jedem Konversationsendpunkt zugeordnet werden soll, der die Verträge und Dienste verwendet, die für die Konversationspriorität angegeben werden. *PriorityValue* muss ein ganzahliges Literal zwischen 1 (niedrigste Priorität) und 10 (höchste Priorität) sein.  
  
 Wenn PRIORITY_LEVEL nicht angegeben ist, wird die Eigenschaft für die Prioritätsebene der Konversationspriorität nicht geändert.  
  
## <a name="remarks"></a>Remarks  
 Keine Eigenschaften, die von ALTER BROKER PRIORITY geändert werden, werden für vorhandene Konversationen übernommen. Die vorhandenen Konversationen werden mit der Priorität fortgesetzt, die beim Starten der Konversationen zugewiesen wurde.  
  
 Weitere Informationen finden Sie unter [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen einer Konversationspriorität erhalten standardmäßig die Mitglieder der festen Datenbankrolle **db_ddladmin** oder **db_owner** und die feste Serverrolle **sysadmin**. Erfordert die ALTER-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-only-the-priority-level-of-an-existing-conversation-priority"></a>A. Ändern der Prioritätsstufe einer vorhandenen Konversationspriorität.  
 Ändert die Prioritätsebene, nicht hingegen die Eigenschaften für den Vertrag, lokalen Dienst oder Remotedienst.  
  
```  
ALTER BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-changing-all-of-the-properties-of-an-existing-conversation-priority"></a>B. Ändern aller Eigenschaften einer vorhandenen Konversationspriorität.  
 Ändert die Eigenschaften für Prioritätsebene, Vertrag, lokalen Dienst und Remotedienst.  
  
```  
ALTER BROKER PRIORITY SimpleContractPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContractB,  
         LOCAL_SERVICE_NAME = TargetServiceB,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceB',  
         PRIORITY_LEVEL = 8);  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/create-broker-priority-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [sys.conversation_priorities &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
