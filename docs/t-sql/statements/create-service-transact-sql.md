---
title: CREATE SERVICE (Transact-SQL) | Microsoft-Dokumentation
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
- CREATE_SERVICE_TSQL
- SERVICE
- CREATE SERVICE
- SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- services [Service Broker], creating
- CREATE SERVICE statement
- contracts [Service Broker], service creation
ms.assetid: fb804fa2-48eb-4878-a12f-4e0d5f4bc9e3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5298494b6c3be0685df771f6d86e11c7b788d002
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="create-service-transact-sql"></a>CREATE SERVICE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen Dienst. Bei einem [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dienst handelt es sich um einen Namen für einen bestimmten Task oder eine Gruppe von Tasks. [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwendet den Namen des Diensts zum Weiterleiten von Nachrichten, zum Übermitteln von Nachrichten an die richtige Warteschlange innerhalb einer Datenbank und zum Erzwingen des Vertrags für eine Konversation.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE SERVICE service_name  
   [ AUTHORIZATION owner_name ]  
   ON QUEUE [ schema_name. ]queue_name  
   [ ( contract_name | [DEFAULT][ ,...n ] ) ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *service_name*  
 Der Name des zu erstellenden Diensts. Ein neuer Dienst wird in der aktuellen Datenbank erstellt. Der Besitzer dieses neuen Diensts ist der in der AUTHORIZATION-Klausel angegebene Prinzipal. Server-, Datenbank- und Schemaname können nicht angegeben werden. Bei *service_name* muss es sich um einen gültigen **sysname**-Wert handeln.  
  
> [!NOTE]  
>  Erstellen Sie keinen Dienst, der das Schlüsselwort ANY für *service_name* verwendet. Wenn Sie in CREATE BROKER PRIORITY für einen Dienstnamen ANY angeben, wird die Priorität für alle Dienste berücksichtigt. ANY steht nicht für einen Dienst mit dem Namen ANY.  
  
 AUTHORIZATION *owner_name*  
 Legt den Besitzer des Diensts auf den angegebenen Datenbankbenutzer bzw. die angegebene Rolle fest. Ist der aktuelle Benutzer **dbo** oder **sa**, kann *owner_name* der Name eines beliebigen gültigen Benutzers bzw. einer beliebigen gültigen Rolle sein. Andernfalls muss *owner_name* der Name des aktuellen Benutzers, der Name eines Benutzers, für den der aktuelle Benutzer IMPERSONATE-Berechtigungen besitzt, oder der Name einer Rolle sein, der der aktuelle Benutzer angehört.  
  
 ON QUEUE [ *schema_name***.** ] *queue_name*  
 Gibt den Namen der Warteschlange an, die Nachrichten für den Dienst empfängt. Die Warteschlange muss in der gleichen Datenbank vorhanden sein wie der Dienst. Wird *schema_name* nicht bereitgestellt, handelt es sich bei dem Schema um das Standardschema für den Benutzer, der die Anweisung ausführt.  
  
 *contract_name*  
 Gibt einen Vertrag an, der diesen Dienst zum Ziel haben kann. Dienstprogramme initiieren Konversationen mit diesem Dienst mithilfe der angegebenen Verträge. Werden keine Verträge angegeben, kann der Dienst nur Konversationen initiieren.  
  
 **[**DEFAULT**]**  
 Gibt an, dass der Dienst das Ziel von Konversationen sein kann, die dem DEFAULT-Vertrag entsprechen. Im Kontext dieser Klausel ist DEFAULT kein Schlüsselwort und muss als Bezeichner begrenzt sein. Der DEFAULT-Vertrag ermöglicht es beiden Seiten der Konversation, Nachrichten vom Nachrichtentyp DEFAULT zu senden. Der Nachrichtentyp DEFAULT verwendet für die Überprüfung NONE.  
  
## <a name="remarks"></a>Remarks  
 Ein Dienst macht die Funktionalität verfügbar, die von den Verträgen bereitgestellt wird, denen er zugeordnet ist, sodass sie von anderen Diensten verwendet werden können. Die CREATE SERVICE-Anweisung gibt die Verträge an, deren Ziel dieser Dienst ist. Ein Dienst kann nur ein Ziel für Konversationen sein, die die von dem Dienst angegebenen Verträge verwenden. Ein Dienst, der keine Verträge angibt, macht keine Funktionalität für andere Dienste verfügbar.  
  
 Konversationen, die von diesem Dienst initiiert werden, können einen beliebigen Vertrag verwenden. Sie erstellen einen Dienst ohne Angabe von Verträgen, wenn der Dienst nur Konversationen initiiert.  
  
 Wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine neue Konversation von einem Remotedienst annimmt, bestimmt der Name des Zieldiensts die Warteschlange, in der der Broker Nachrichten in der Konversation anordnet.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen eines Diensts liegt standardmäßig bei Mitgliedern der festen Datenbankrollen **db_ddladmin** und **db_owner** sowie der festen Serverrolle **sysadmin**. Der Benutzer, der die CREATE SERVICE-Anweisung ausführt, muss über die REFERENCES-Berechtigung für die Warteschlange und alle angegebenen Verträge verfügen.  
  
 Die REFERENCES-Berechtigung für einen Dienst liegt standardmäßig beim Besitzer des Diensts, bei Mitgliedern der festen Datenbankrollen **db_ddladmin** und **db_owner** sowie bei Mitgliedern der festen Serverrolle **sysadmin**. SEND-Berechtigungen für einen Dienst liegen standardmäßig beim Besitzer dieses Diensts, bei Mitgliedern der festen Datenbankrolle **db_owner** und bei Mitgliedern der festen Serverrolle **sysadmin**.  
  
 Ein Dienst kann kein temporäres Objekt sein. Dienstnamen, die mit **#** beginnen, sind zulässig. Hierbei handelt es sich jedoch um dauerhafte Objekte.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-service-with-one-contract"></a>A. Erstellen eines Diensts mit einem Vertrag  
 Im folgenden Beispiel wird der Dienst `//Adventure-Works.com/Expenses` in der `ExpenseQueue`-Warteschlange im `dbo`-Schema erstellt. Dialoge, die diesen Dienst zum Ziel haben, müssen dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission` entsprechen.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE [dbo].[ExpenseQueue]  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="b-creating-a-service-with-multiple-contracts"></a>B. Erstellen eines Diensts mit mehreren Verträgen  
 Im folgenden Beispiel wird der Dienst `//Adventure-Works.com/Expenses` für die `ExpenseQueue`-Warteschlange erstellt. Dialoge, die diesen Dienst zum Ziel haben, müssen entweder dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission` oder dem Vertrag `//Adventure-Works.com/Expenses/ExpenseProcessing` entsprechen.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue  
    ([//Adventure-Works.com/Expenses/ExpenseSubmission],  
     [//Adventure-Works.com/Expenses/ExpenseProcessing]) ;  
```  
  
### <a name="c-creating-a-service-with-no-contracts"></a>C. Erstellen eines Diensts ohne Verträge  
 Im folgenden Beispiel wird die Dienstwarteschlange `//Adventure-Works.com/Expenses on the ExpenseQueue` erstellt. Dieser Dienst verfügt über keine Vertragsinformationen. Daher kann der Dienst nur der Initiator eines Dialogs sein.  
  
```  
CREATE SERVICE [//Adventure-Works.com/Expenses] ON QUEUE ExpenseQueue ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
