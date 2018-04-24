---
title: CREATE CONTRACT (Transact-SQL) | Microsoft-Dokumentation
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
- CONTRACT_TSQL
- CREATE_CONTRACT_TSQL
- CREATE CONTRACT
- CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE CONTRACT statement
- contracts [Service Broker], creating
- message types [Service Broker], contracts
ms.assetid: 494cbfa6-8e93-4161-a64d-90d681915211
caps.latest.revision: 48
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a685fc43b0ce595c98deefb0eac73e1e077d2fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-contract-transact-sql"></a>CREATE CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen Vertrag. Ein Vertrag definiert die in einer [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Konversation verwendeten Nachrichtentypen und legt fest, welche Seite der Konversation Nachrichten eines bestimmten Typs senden kann. Jede Konversation folgt einem Vertrag. Der initiierende Dienst gibt beim Start der Konversation den Vertrag für die Konversation an. Der Zieldienst gibt die Verträge an, für die der Zieldienst Konversationen annimmt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE CONTRACT contract_name  
   [ AUTHORIZATION owner_name ]  
      (  {   { message_type_name | [ DEFAULT ] }  
          SENT BY { INITIATOR | TARGET | ANY }   
       } [ ,...n] )   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *contract_name*  
 Der Name des zu erstellenden Vertrags. Ein neuer Vertrag wird in der aktuellen Datenbank erstellt; der Besitzer ist der in der AUTHORIZATION-Klausel angegebene Prinzipal. Server-, Datenbank- und Schemaname können nicht angegeben werden. *contract_name* kann aus bis zu 128 Zeichen bestehen.  
  
> [!NOTE]  
>  Erstellen Sie keinen Vertrag, der das Schlüsselwort ANY für *contract_name* verwendet. Wenn Sie in CREATE BROKER PRIORITY für einen Vertragsnamen ANY angeben, wird die Priorität für alle Verträge berücksichtigt. ANY steht nicht nur für einen Vertrag mit dem Namen ANY.  
  
 AUTHORIZATION *owner_name*  
 Legt den Besitzer des Vertrags auf den angegebenen Datenbankbenutzer oder die angegebene Datenbankrolle fest. Ist der aktuelle Benutzer **dbo** oder **sa**, kann *owner_name* der Name eines beliebigen gültigen Benutzers bzw. einer beliebigen gültigen Rolle sein. Andernfalls muss *owner_name* der Name des aktuellen Benutzers, der Name eines Benutzers, für den der aktuelle Benutzer Identitätswechselberechtigungen besitzt, oder der Name einer Rolle sein, der der aktuelle Benutzer angehört. Wenn diese Klausel weggelassen wird, gehört der Vertrag dem aktuellen Benutzer.  
  
 *message_type_name*  
 Der Name eines in den Vertrag eingeschlossenen Nachrichtentyps.  
  
 SENT BY  
 Gibt an, welcher Endpunkt eine Nachricht vom angegebenen Nachrichtentyp senden kann. Verträge dokumentieren die Nachrichten, die von Diensten für bestimmte Konversationen verwendet werden können. Jede Konversation verfügt über zwei Endpunkte: den *initiator*-Endpunkt, wobei es sich um den Dienst handelt, der die Konversation gestartet hat, und den *target*-Endpunkt, wobei es sich um den Dienst handelt, mit dem der Initiator Kontakt aufnimmt.  
  
 INITIATOR  
 Gibt an, dass nur der Initiator der Konversation Nachrichten eines bestimmten Nachrichtentyps senden kann. Ein Dienst, der eine Konversation startet, wird als der *Initiator* der Konversation bezeichnet.  
  
 TARGET  
 Gibt an, dass nur das Ziel der Konversation Nachrichten eines bestimmten Nachrichtentyps senden kann. Ein Dienst, der eine von einem anderen Dienst begonnene Konversation annimmt, wird als das *Ziel* der Konversation bezeichnet.  
  
 ANY  
 Gibt an, dass Nachrichten dieses Typs sowohl vom Initiator als auch vom Ziel gesendet werden können.  
  
 [DEFAULT]  
 Gibt an, dass dieser Vertrag Nachrichten vom Standardnachrichtentyp unterstützt. Standardmäßig enthalten alle Datenbanken einen Nachrichtentyp namens DEFAULT. Dieser Nachrichtentyp verwendet NONE für die Überprüfung. Im Kontext dieser Klausel ist DEFAULT kein Schlüsselwort und muss als Bezeichner begrenzt sein. Microsoft SQL Server stellt auch einen DEFAULT-Vertrag bereit, der den Nachrichtentyp DEFAULT angibt.  
  
## <a name="remarks"></a>Remarks  
 Die Reihenfolge von Nachrichtentypen im Vertrag ist nicht von Bedeutung. Nachdem das Ziel die erste Nachricht erhalten hat, ermöglicht [!INCLUDE[ssSB](../../includes/sssb-md.md)] beiden Seiten der Konversation, zu jeder Zeit Nachrichten zu senden, die für die jeweilige Konversationsseite zulässig sind. Kann der Initiator der Konversation beispielsweise den Nachrichtentyp **//Adventure-Works.com/Expenses/SubmitExpense** senden, ermöglicht [!INCLUDE[ssSB](../../includes/sssb-md.md)] dem Initiator das Senden beliebig vieler **SubmitExpense**-Nachrichten zu jeder Zeit im Verlauf der Konversation.  
  
 Die Nachrichtentypen und -richtungen in einem Vertrag können nicht geändert werden. Verwenden Sie die ALTER AUTHORIZATION-Anweisung, wenn Sie den Wert von AUTHORIZATION für einen Vertrag ändern möchten.  
  
 Ein Vertrag muss dem Initiator das Senden einer Nachricht ermöglichen. Die CREATE CONTRACT-Anweisung erzeugt einen Fehler, wenn der Vertrag nicht zumindest den Nachrichtentyp SENT BY ANY oder SENT BY INITIATOR enthält.  
  
 Unabhängig vom Vertrag kann ein Dienst immer die Nachrichtentypen `http://schemas.microsoft.com/SQL/ServiceBroker/DialogTimer`, `http://schemas.microsoft.com/SQL/ServiceBroker/Error` und `http://schemas.microsoft.com/SQL/ServiceBroker/EndDialog` empfangen. [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwendet diese Nachrichtentypen für Systemnachrichten an die Anwendung.  
  
 Ein Vertrag kann kein temporäres Objekt sein. Vertragsnamen, die mit # beginnen, sind zulässig. Es handelt sich dabei jedoch um dauerhafte Objekte.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können Mitglieder der festen Datenbankrolle **db_ddladmin** oder **db_owner** sowie der festen Serverrolle **sysadmin** Verträge erstellen.  
  
 Standardmäßig verfügen der Besitzer des Vertrags, Mitglieder der festen Datenbankrolle **db_ddladmin** oder **db_owner** sowie Mitglieder der festen Serverrolle **sysadmin** über die REFERENCES-Berechtigung für einen Vertrag.  
  
 Der Benutzer, der die CREATE CONTRACT-Anweisung ausführt, benötigt die REFERENCES-Berechtigung für alle angegebenen Nachrichtentypen.  
  
## <a name="examples"></a>Beispiele  
 **A. Erstellen eines Vertrags**  
  
 Im folgenden Beispiel wird ein Aufwandentschädigungsvertrag auf der Basis von drei Nachrichtentypen erstellt.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
    VALIDATION = WELL_FORMED_XML ;           
  
CREATE MESSAGE TYPE           
    [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
    VALIDATION= WELL_FORMED_XML ;           
  
CREATE CONTRACT            
    [//Adventure-Works.com/Expenses/ExpenseSubmission]           
    ( [//Adventure-Works.com/Expenses/SubmitExpense]           
          SENT BY INITIATOR,           
      [//Adventure-Works.com/Expenses/ExpenseApprovedOrDenied]           
          SENT BY TARGET,           
      [//Adventure-Works.com/Expenses/ExpenseReimbursed]           
          SENT BY TARGET           
    ) ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [DROP CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-contract-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
