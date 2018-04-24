---
title: BEGIN DIALOG CONVERSATION (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/26/2017
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
- DIALOG CONVERSATION
- DIALOG
- BEGIN_DIALOG_TSQL
- BEGIN_DIALOG_CONVERSATION_TSQL
- DIALOG_CONVERSATION_TSQL
- DIALOG_TSQL
- BEGIN DIALOG
- BEGIN DIALOG CONVERSATION
dev_langs:
- TSQL
helpviewer_keywords:
- conversations [Service Broker]
- beginning dialogs
- dialogs [Service Broker], beginning
- BEGIN DIALOG CONVERSATION statement
- cryptography [SQL Server], conversations
- opening conversations
- encryption [SQL Server], conversations
- starting conversations
ms.assetid: 8e814f9d-77c1-4906-b8e4-668a86fc94ba
caps.latest.revision: 47
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 465c4d071315329a404ac0705719279d68570223
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="begin-dialog-conversation-transact-sql"></a>BEGIN DIALOG CONVERSATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Beginnt einen Dialog zwischen zwei Diensten. Ein Dialog ermöglicht eine Konversation zwischen zwei Diensten, bei der jede Nachricht genau einmal übertragen wird, und zwar an der Reihenfolgeposition, an der sie gesendet wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
BEGIN DIALOG [ CONVERSATION ] @dialog_handle  
   FROM SERVICE initiator_service_name  
   TO SERVICE 'target_service_name'  
       [ , { 'service_broker_guid' | 'CURRENT DATABASE' }]   
   [ ON CONTRACT contract_name ]  
   [ WITH  
   [  { RELATED_CONVERSATION = related_conversation_handle   
      | RELATED_CONVERSATION_GROUP = related_conversation_group_id } ]   
   [ [ , ] LIFETIME = dialog_lifetime ]   
   [ [ , ] ENCRYPTION = { ON | OFF }  ] ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 **@** *dialog_handle*  
 Eine Variable, die zum Speichern des systemgenerierten Dialoghandles für den neuen Dialog verwendet wird, der von der BEGIN DIALOG CONVERSATION-Anweisung zurückgegeben wird. Die Variable muss vom Typ **uniqueidentifier** sein.  
  
 FROM SERVICE *initiator_service_name*  
 Gibt den Dienst an, der den Dialog initialisiert. Bei dem angegebenen Namen muss es sich um den Namen eines Diensts in der aktuellen Datenbank handeln. Die als Initiatordienst angegebene Warteschlange empfängt Nachrichten, die vom Zieldienst zurückgegeben werden, sowie Nachrichten, die von Service Broker für diese Konversation erstellt wurden.  
  
 TO SERVICE **'***target_service_name***'**  
 Gibt den Zieldienst an, mit dem der Dialog initialisiert werden soll. Der *target_service_name* ist vom Typ **nvarchar(256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)] führt einen bitweisen Vergleich mit der *target_service_name*-Zeichenfolge aus. Das heißt, dass bei dem Vergleich die Groß- und Kleinschreibung beachtet und die aktuelle Sortierung nicht berücksichtigt wird.  
  
 *service_broker_guid*  
 Gibt die Datenbank an, auf der sich der Zieldienst befindet. Wenn mehrere Datenbanken eine Instanz des Zieldiensts hosten, können Sie mit einer bestimmten Datenbank kommunizieren, indem Sie *service_broker_guid* angeben.  
  
 Die *service_broker_guid* ist vom Typ **nvarchar(128)**. Führen Sie die folgende Abfrage in der Datenbank aus, um die *service_broker_guid* für eine Datenbank zu ermitteln:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID() ;  
```  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 **'** CURRENT DATABASE **'**  
 Gibt an, dass die Konversation für die aktuelle Datenbank *service_broker_guid* verwendet.  
  
 ON CONTRACT *contract_name*  
 Gibt den Vertrag an, dem diese Konversation entspricht. Der Vertrag muss in der aktuellen Datenbank vorhanden sein. Wenn der Zieldienst für den angegebenen Vertrag keine neuen Konversationen akzeptiert, gibt [!INCLUDE[ssSB](../../includes/sssb-md.md)] eine Fehlermeldung zur Konversation zurück. Wird diese Klausel weggelassen, folgt die Konversation dem Vertrag mit dem Namen **DEFAULT**.  
  
 RELATED_CONVERSATION **=***related_conversation_handle*  
 Gibt die vorhandene Konversationsgruppe an, der der neue Dialog hinzugefügt wird. Wenn diese Klausel vorhanden ist, gehört der neue Dialog derselben Konversationsgruppe an, wie der mit *related_conversation_handle* angegebene Dialog. *related_conversation_handle* muss implizit in den Typ **uniqueidentifier** konvertierbar sein. Die Anweisung schlägt fehl, wenn *related_conversation_handle* nicht auf einen vorhandenen Dialog verweist.  
  
 RELATED_CONVERSATION_GROUP **=***related_conversation_group_id*  
 Gibt die vorhandene Konversationsgruppe an, der der neue Dialog hinzugefügt wird. Wenn diese Klausel vorhanden ist, wird der neue Dialog zu der mit *related_conversation_group_id* angegebenen Konversationsgruppe hinzugefügt. *related_conversation_group_id* muss implizit in den Typ **uniqueidentifier** konvertierbar sein. Wenn *related_conversation_group_id* nicht auf eine vorhandene Konversationsgruppe verweist, erstellt der Service Broker eine neue Konversationsgruppe mit der angegebenen *related_conversation_group_id* und verknüpft den neuen Dialog mit dieser Konversationsgruppe.  
  
 LIFETIME **=***dialog_lifetime*  
 Gibt den maximalen Zeitraum an, in dem der Dialog geöffnet bleibt. Damit der Dialog erfolgreich abgeschlossen wird, müssen beide Endpunkte den Dialog explizit beenden, bevor die Lebensdauer abläuft. Der Wert für *dialog_lifetime* muss in Sekunden angegeben werden. „Lifetime“ ist vom Typ **int**. Wird keine LIFETIME-Klausel angegeben, entspricht die Lebensdauer des Dialogs dem maximalen Wert des Datentyps **int**.  
  
 ENCRYPTION  
 Gibt an, ob Nachrichten, die über diesen Dialog versandt und empfangen werden, verschlüsselt werden müssen, wenn sie außerhalb einer Instanz von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versandt werden. Ein Dialog, der verschlüsselt werden muss, ist ein *sicherer Dialog*. Wenn ENCRYPTION = ON festgelegt wurde und wenn die für die Verschlüsselung erforderlichen Zertifikate nicht konfiguriert sind, gibt [!INCLUDE[ssSB](../../includes/sssb-md.md)] für die Konversation eine Fehlermeldung zurück. Wenn ENCRYPTION = OFF festgelegt ist, wird die Verschlüsselung nur dann verwendet, wenn eine Remotedienstbindung für *target_service_name* konfiguriert ist; andernfalls werden Nachrichten unverschlüsselt versandt. Ist diese Klausel nicht vorhanden, ist die Standardeinstellung ON.  
  
> [!NOTE]  
>  Nachrichten, die mit Diensten in derselben Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgetauscht werden, sind nie verschlüsselt. Jedoch sind ein Hauptschlüssel für die Datenbank und die Zertifikate für die Verschlüsselung für diejenigen Konversationen mit Verschlüsselung erforderlich, bei denen sich die Dienste für die Konversation auf verschiedenen Datenbanken befinden. Damit kann die Konversation auch dann fortgesetzt werden, wenn während der Ausführung der Konversation eine der Datenbanken auf eine andere Instanz verschoben wird.  
  
## <a name="remarks"></a>Remarks  
 Alle Nachrichten sind Teil einer Konversation. Deshalb muss ein initialisierender Dienst eine Konversation mit dem Zieldienst beginnen, bevor eine Nachricht an den Zieldienst gesandt wird. Die in der BEGIN DIALOG CONVERSATION-Anweisung angegebenen Informationen sind mit der Adresse auf einem Brief vergleichbar; [!INCLUDE[ssSB](../../includes/sssb-md.md)] verwendet diese Informationen, um Nachrichten an den richtigen Dienst zu übermitteln. Der Dienst, der in der TO SERVICE-Klausel angegeben wird, ist die Adresse, an die die Nachrichten gesandt werden. Der Dienst, der in der FROM SERVICE-Klausel angegeben wird, ist die Rückadresse für Antwortnachrichten.  
  
 Das Ziel einer Konversation muss nicht BEGIN DIALOG CONVERSATION aufrufen. [!INCLUDE[ssSB](../../includes/sssb-md.md)] erstellt eine Konversation in der Zieldatenbank, wenn die erste Nachricht in der Konversation vom Initiator eintrifft.  
  
 Durch das Erstellen eines Dialogs wird ein Konversationsendpunkt für den initiierenden Dienst in der Datenbank erstellt, jedoch wird keine Netzwerkverbindung mit der Instanz erstellt, die den Zieldienst hostet. [!INCLUDE[ssSB](../../includes/sssb-md.md)] stellt erst die Kommunikation mit dem Ziel des Dialogs her, wenn die erste Nachricht gesendet wird.  
  
 Wenn die BEGIN DIALOG CONVERSATION-Anweisung keine verknüpfte Konversation oder verknüpfte Konversationsgruppe angibt, legt [!INCLUDE[ssSB](../../includes/sssb-md.md)] für die neue Konversation eine neue Konversationsgruppe an.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] lässt für Konversationen keine beliebigen Gruppierungen zu. Für alle Konversationen in einer Konversationsgruppe muss der Dienst in der FROM-Klausel entweder als Initiator oder als Ziel der Konversation angegeben werden.  
  
 Mit dem BEGIN DIALOG CONVERSATION-Befehl wird die Konversationsgruppe gesperrt, die das zurückgegebene *dialog_handle* enthält. Wenn der Befehl eine RELATED_CONVERSATION_GROUP-Klausel umfasst, dann ist die Konversationsgruppe für *dialog_handle* die Konversationsgruppe, die im *related_conversation_group_id*-Parameter angegeben ist. Wenn der Befehl eine RELATED_CONVERSATION-Klausel umfasst, dann ist die Konversationsgruppe für *dialog_handle* die Konversationsgruppe, die mit dem angegebenen *related_conversation_handle* verknüpft ist.  
  
 BEGIN DIALOG CONVERSATION ist in einer benutzerdefinierten Funktion nicht gültig.  
  
## <a name="permissions"></a>Berechtigungen  
 Um einen Dialog zu beginnen, muss der aktuelle Benutzer eine RECEIVE-Berechtigung für die Warteschlange für den Dienst haben, der in der FROM-Klausel des Befehls angegeben wird. Außerdem muss er über die Berechtigung REFERENCES für den angegebenen Vertrag verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-beginning-a-dialog"></a>A. Starten eines Dialogs  
 Im folgenden Beispiel wird eine Dialogkonversation begonnen, und ein Bezeichner für den Dialog wird in `@dialog_handle.` gespeichert. Der Dienst `//Adventure-Works.com/ExpenseClient` ist der Initiator für den Dialog, und der Dienst `//Adventure-Works.com/Expenses` ist das Ziel des Dialogs. Der Dialog entspricht dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="b-beginning-a-dialog-with-an-explicit-lifetime"></a>B. Starten eines Dialogs mit einer expliziten Lebensdauer  
 Im folgenden Beispiel wird eine Dialogkonversation begonnen, und ein Bezeichner für den Dialog wird in `@dialog_handle` gespeichert. Der Dienst `//Adventure-Works.com/ExpenseClient` ist der Initiator für den Dialog, und der Dienst `//Adventure-Works.com/Expenses` ist das Ziel des Dialogs. Der Dialog entspricht dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission`. Wenn der Dialog nicht innerhalb von `60` Sekunden mit dem Befehl END CONVERSATION geschlossen wird, beendet Service Broker den Dialog mit einem Fehler.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH LIFETIME = 60 ;  
```  
  
### <a name="c-beginning-a-dialog-with-a-specific-broker-instance"></a>C. Starten eines Dialogs mit einer bestimmten Brokerinstanz  
 Im folgenden Beispiel wird eine Dialogkonversation begonnen, und ein Bezeichner für den Dialog wird in `@dialog_handle` gespeichert. Der Dienst `//Adventure-Works.com/ExpenseClient` ist der Initiator für den Dialog, und der Dienst `//Adventure-Works.com/Expenses` ist das Ziel des Dialogs. Der Dialog entspricht dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission`. Service Broker leitet Nachrichten für diesen Dialog an den Broker weiter, der über folgenden GUID angegeben wird: `a326e034-d4cf-4e8b-8d98-4d7e1926c904.`  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses',   
              'a326e034-d4cf-4e8b-8d98-4d7e1926c904'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
### <a name="d-beginning-a-dialog-and-relating-it-to-an-existing-conversation-group"></a>D. Starten eines Dialogs und Zuordnen des Dialogs zu einer vorhandenen Konversationsgruppe  
 Im folgenden Beispiel wird eine Dialogkonversation begonnen, und ein Bezeichner für den Dialog wird in `@dialog_handle` gespeichert. Der Dienst `//Adventure-Works.com/ExpenseClient` ist der Initiator für den Dialog, und der Dienst `//Adventure-Works.com/Expenses` ist das Ziel des Dialogs. Der Dialog entspricht dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission`. Service Broker verknüpft den Dialog mit der durch `@conversation_group_id` angegebenen Konversationsgruppe, statt eine neue Konversationsgruppe zu erstellen.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER ;  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION_GROUP = @conversation_group_id ;  
```  
  
### <a name="e-beginning-a-dialog-with-an-explicit-lifetime-and-relating-the-dialog-to-an-existing-conversation"></a>E. Starten eines Dialogs mit einer expliziten Lebensdauer und Zuordnen des Dialogs zu einer vorhandenen Konversation  
 Im folgenden Beispiel wird eine Dialogkonversation begonnen, und ein Bezeichner für den Dialog wird in `@dialog_handle` gespeichert. Der Dienst `//Adventure-Works.com/ExpenseClient` ist der Initiator für den Dialog, und der Dienst `//Adventure-Works.com/Expenses` ist das Ziel des Dialogs. Der Dialog entspricht dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission`. Der neue Dialog gehört der gleichen Konversationsgruppe an, zu der `@existing_conversation_handle` gehört. Wenn der Dialog nicht innerhalb von `600` Sekunden mit dem Befehl END CONVERSATION geschlossen wird, beendet [!INCLUDE[ssSB](../../includes/sssb-md.md)] den Dialog mit einem Fehler.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
DECLARE @existing_conversation_handle UNIQUEIDENTIFIER  
  
SET @existing_conversation_handle = <retrieve conversation handle from database>  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH RELATED_CONVERSATION = @existing_conversation_handle  
   LIFETIME = 600 ;  
```  
  
### <a name="f-beginning-a-dialog-with-optional-encryption"></a>F. Starten eines Dialogs mit optionaler Verschlüsselung  
 Im folgenden Beispiel wird ein Dialog begonnen, und ein Bezeichner für den Dialog wird in `@dialog_handle` gespeichert. Der Dienst `//Adventure-Works.com/ExpenseClient` ist der Initiator für den Dialog, und der Dienst `//Adventure-Works.com/Expenses` ist das Ziel des Dialogs. Der Dialog entspricht dem Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission`. Die Konversation in diesem Beispiel lässt es zu, dass die Nachricht unverschlüsselt über das Netzwerk weitergeleitet wird, wenn die Verschlüsselung nicht verfügbar ist.  
  
```  
DECLARE @dialog_handle UNIQUEIDENTIFIER  
  
BEGIN DIALOG CONVERSATION @dialog_handle  
   FROM SERVICE [//Adventure-Works.com/ExpenseClient]  
   TO SERVICE '//Adventure-Works.com/Expenses'  
   ON CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]  
   WITH ENCRYPTION = OFF ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BEGIN CONVERSATION TIMER &#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [MOVE CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/move-conversation-transact-sql.md)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql.md)  
  
  
