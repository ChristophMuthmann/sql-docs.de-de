---
title: Erstellen der Warteschlange (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
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
- QUEUE_TSQL
- CREATE QUEUE
- QUEUE
- CREATE_QUEUE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE QUEUE statement
- internal activation [Service Broker]
- stored procedure activation [Service Broker]
- message retention [Service Broker]
- unavailable queues [Service Broker]
- activation stored procedures [Service Broker]
- queues [Service Broker], creating
ms.assetid: fce80faf-2bdc-475d-8ca1-31438ed41fb0
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7bd20267a78f9a0fcaf2d854b6e94553b7c80167
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="create-queue-transact-sql"></a>CREATE QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine neue Warteschlange in einer Datenbank. Fügt einer Warteschlange gespeicherte Nachrichten hinzu. Wenn eine Nachricht für einen Dienst eintrifft, platziert [!INCLUDE[ssSB](../../includes/sssb-md.md)] die Nachricht in der dem Dienst zugeordneten Warteschlange.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE QUEUE <object>  
   [ WITH  
     [ STATUS = { ON | OFF }  [ , ] ]  
     [ RETENTION = { ON | OFF } [ , ] ]   
     [ ACTIVATION (  
         [ STATUS = { ON | OFF } , ]   
           PROCEDURE_NAME = <procedure> ,  
           MAX_QUEUE_READERS = max_readers ,   
           EXECUTE AS { SELF | 'user_name' | OWNER }   
            ) [ , ] ]  
     [ POISON_MESSAGE_HANDLING (  
         [ STATUS = { ON | OFF } ] ) ] 
    ]  
     [ ON { filegroup | [ DEFAULT ] } ]  
[ ; ]  
  
<object> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        queue_name  
}   
  
<procedure> ::=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        stored_procedure_name  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 *Database_name* (Objekt)  
 Der Name der Datenbank, in der die neue Warteschlange erstellt werden soll. *Database_name* müssen den Namen einer vorhandenen Datenbank angeben. Wenn *Database_name* nicht angegeben wird, die Warteschlange in der aktuellen Datenbank erstellt wird.  
  
 *Schema_name* (Objekt)  
 Der Name des Schemas, zu dem die neue Warteschlange gehört. Standardmäßig handelt es sich bei dem Schema um das Standardschema für den Benutzer, der die Anweisung ausführt. Wenn die CREATE QUEUE-Anweisung von einem Mitglied der festen Serverrolle "Sysadmin" ausgeführt wird, oder ein Mitglied der Db_dbowner oder Db_ddladmin Datenbankrollen in der Datenbank gemäß festen *Database_name*, *Schema_name* können ein anderes als das dem Anmeldenamen der aktuellen Verbindung zugeordnete Schema angeben. Andernfalls *Schema_name* muss das Standardschema für den Benutzer, der die Anweisung ausführt.  
  
 *queue_name*  
 Der Name der zu erstellenden Warteschlange. Dieser Name muss den Richtlinien für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner entsprechen.  
  
 STATUS (Warteschlange)  
 Gibt an, ob die Warteschlange verfügbar ist (ON) oder nicht (OFF). Ist die Warteschlange nicht verfügbar, können der Warteschlange keine Nachrichten hinzugefügt oder aus ihr entfernt werden. Sie können die Warteschlange im nicht verfügbaren Status erstellen, damit Nachrichten erst dann in der Warteschlange ankommen, wenn die Warteschlange mit einer ALTER QUEUE-Anweisung zur Verfügung gestellt wird. Wird diese Klausel nicht angegeben, ist die Standardeinstellung ON, und die Warteschlange ist verfügbar.  
  
 RETENTION  
 Gibt die Beibehaltungseinstellung für die Warteschlange an. Wenn RETENTION = ON, alle Nachrichten gesendete oder empfangene für Konversationen, die diese Warteschlange verwenden, werden in der Warteschlange beibehalten, bis die Konversationen beendet sind. Dies ermöglicht es Ihnen, Nachrichten zu Überwachungszwecken oder zur Ausführung von kompensierenden Transaktionen beim Auftreten eines Fehlers beizubehalten. Wird diese Klausel nicht angegeben, wird die Beibehaltungseinstellung standardmäßig auf OFF festgelegt.  
  
> [!NOTE]  
>  Das Festlegen von RETENTION = ON kann die Leistung reduzieren. Diese Einstellung sollte nur verwendet werden, wenn sie für die Anwendung erforderlich ist.  
  
 ACTIVATION  
 Gibt Informationen über die gespeicherte Prozedur an, die Sie für die Verarbeitung von Nachrichten in dieser Warteschlange starten müssen.  
  
 STATUS (Aktivierung)  
 Gibt an, ob [!INCLUDE[ssSB](../../includes/sssb-md.md)] die gespeicherte Prozedur startet. Ist STATUS = ON, startet die Warteschlange die mit PROCEDURE_NAME angegebene gespeicherte Prozedur, wenn die Anzahl der zurzeit ausgeführten Prozeduren kleiner als MAX_QUEUE_READERS ist und wenn Nachrichten schneller in der Warteschlange ankommen, als die gespeicherten Prozeduren Nachrichten empfangen. Ist STATUS = OFF, startet die Warteschlange die gespeicherte Prozedur nicht. Wird diese Klausel nicht angegeben, ist die Standardeinstellung ON.  
  
 PROCEDURE_NAME = \<procedure>  
 Gibt den Namen der gespeicherten Prozedur an, die für die Verarbeitung von Nachrichten in dieser Warteschlange gestartet werden soll. Dieser Wert muss ein [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Bezeichner sein.  
  
 *database_name*(procedure)  
 Der Name der Datenbank, die die gespeicherte Prozedur enthält.  
  
 *schema_name*(procedure)  
 Der Name des Schemas, das die gespeicherte Prozedur enthält.  
  
 *procedure_name*  
 Der Name der gespeicherten Prozedur.  
  
 MAX_QUEUE_READERS =*Max_readers*  
 Gibt die maximale Anzahl von Instanzen der gespeicherten Aktivierungsprozedur an, die von der Warteschlange gleichzeitig gestartet werden. Der Wert der *Max_readers* muss eine Zahl zwischen **0** und **32767**.  
  
 EXECUTE AS  
 Gibt das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenbank-Benutzerkonto an, unter dem die gespeicherte Aktivierungsprozedur ausgeführt wird. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss zum Zeitpunkt des Startens der gespeicherten Prozedur durch die Warteschlange die Berechtigungen für diesen Benutzer überprüfen können. Bei einem Domänenbenutzer muss der Server mit der Domäne verbunden sein, wenn die Prozedur gestartet wird. Andernfalls erzeugt die Aktivierung einen Fehler. Bei einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Benutzer kann der Server immer die Berechtigungen überprüfen.  
  
 SELF  
 Gibt an, dass die gespeicherte Prozedur als der aktuelle Benutzer ausgeführt wird. (Der Datenbankprinzipal, der diese CREATE QUEUE-Anweisung ausführt.)  
  
 "*User_name*"  
 Der Name des Benutzers, als der die gespeicherte Prozedur ausgeführt wird. Die *User_name* Parameter muss ein gültiger [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] als angegebenen Benutzers eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Bezeichner. Der aktuelle Benutzer benötigen die IMPERSONATE-Berechtigung für die *User_name* angegebenen.  
  
 OWNER  
 Gibt an, dass die gespeicherte Prozedur als der Besitzer der Warteschlange ausgeführt wird.  
  
 POISON_MESSAGE_HANDLING  
 Gibt an, ob die Behandlung nicht verarbeitbarer Nachrichten für die Warteschlange aktiviert ist. Der Standardwert ist ON.  
  
 Eine Warteschlange, für die die Behandlung nicht verarbeitbarer Nachrichten auf OFF festgelegt ist, wird erst nach fünf aufeinander folgenden Transaktionsrollbacks deaktiviert. Daher ist es möglich, dass von der Anwendung ein System für die Behandlung nicht verarbeitbarer Nachrichten definiert wird.  
  
 ON *Dateigruppe |* [**Standard**]  
 Gibt die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dateigruppe an, in der diese Warteschlange erstellt werden soll. Sie können die *Dateigruppe* Parameter für eine Dateigruppe identifizieren, oder verwenden die Standard-ID, um die Standarddateigruppe für die Service Broker-Datenbank verwenden. Im Kontext dieser Klausel ist DEFAULT kein Schlüsselwort und muss als Bezeichner begrenzt sein. Wird keine Dateigruppe angegeben, verwendet die Warteschlange die Standarddateigruppe für die Datenbank.  
  
## <a name="remarks"></a>Hinweise  
 Eine Warteschlange kann das Ziel einer SELECT-Anweisung sein. Der Inhalt einer Warteschlange kann jedoch nur mithilfe von Anweisungen geändert werden, die für [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Konversationen verwendet werden, wie beispielsweise SEND, RECEIVE und END CONVERSATION. Eine Warteschlange kann nicht das Ziel einer INSERT-, UPDATE-, DELETE- oder TRUNCATE-Anweisung sein.  
  
 Eine Warteschlange ist möglicherweise kein temporäres Objekt. Deshalb Warteschlangennamen ab  **#**  sind nicht gültig.  
  
 Das Erstellen einer Warteschlange im inaktiven Status ermöglicht es Ihnen, die Infrastruktur für einen Dienst einzurichten, bevor der Empfang von Nachrichten in der Warteschlange zugelassen wird.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] beendet gespeicherte Aktivierungsprozeduren nicht, wenn sich keine Nachrichten in der Warteschlange befinden. Eine gespeicherte Aktivierungsprozedur sollte beendet werden, wenn eine kurze Zeit lang keine Nachrichten in der Warteschlange verfügbar sind.  
  
 Berechtigungen für die gespeicherte Aktivierungsprozedur werden überprüft, wenn [!INCLUDE[ssSB](../../includes/sssb-md.md)] die gespeicherte Prozedur startet, nicht, wenn die Warteschlange erstellt wird. Die CREATE QUEUE-Anweisung überprüft nicht, ob der in der EXECUTE AS-Klausel angegebene Benutzer über die Berechtigung verfügt, die in der PROCEDURE NAME-Klausel angegebene gespeicherte Prozedur auszuführen.  
  
 Ist eine Warteschlange nicht verfügbar, speichert [!INCLUDE[ssSB](../../includes/sssb-md.md)] Nachrichten für Dienste, die die Warteschlange verwenden, in der Übertragungswarteschlange für die Datenbank. Die sys.transmission_queue-Katalogsicht stellt eine Sicht der Übertragungswarteschlange bereit.  
  
 Eine Warteschlange ist ein Objekt, dessen Besitzer ein Schema ist. Warteschlangen werden in der sys.objects-Katalogsicht angezeigt.  
  
 In der folgenden Tabelle werden die Spalten in einer Warteschlange aufgelistet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|status|**tinyint**|Status der Nachricht. Die RECEIVE-Anweisung gibt alle Nachrichten, die den Status **1**. Wenn die Nachrichtenbeibehaltung aktiviert ist, wird der Status auf 0 festgelegt. Wenn die Nachrichtenbeibehaltung deaktiviert ist, wird die Meldung aus der Warteschlange gelöscht. Nachrichten in der Warteschlange können einen der folgenden Werte enthalten:<br /><br /> **0**= empfangene Nachricht wurde beibehalten<br /><br /> **1**= bereit zu empfangen<br /><br /> **2**= noch nicht abgeschlossen<br /><br /> **3**= gesendete Nachricht wurde beibehalten|  
|priority|**tinyint**|Die Prioritätsebene, die der Nachricht zugewiesen wird.|  
|queuing_order|**bigint**|Fortlaufende Nummer der Nachricht in der Warteschlange.|  
|conversation_group_id|**uniqueidentifier**|Bezeichner für die Konversationsgruppe, zu der diese Nachricht gehört.|  
|conversation_handle|**uniqueidentifier**|Handle der Konversation, von der diese Nachricht ein Teil ist.|  
|message_sequence_number|**bigint**|Sequenznummer der Nachricht in der Konversation.|  
|service_name|**nvarchar(512)**|Name des Diensts, an den die Konversation gerichtet ist.|  
|service_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objektbezeichner des Diensts, an den die Konversation gerichtet ist.|  
|service_contract_name|**nvarchar(256)**|Name des Vertrags, dem die Konversation entspricht.|  
|service_contract_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objektbezeichner des Vertrags, dem die Konversation entspricht.|  
|message_type_name|**nvarchar(256)**|Name des Nachrichtentyps, der die Nachricht beschreibt.|  
|message_type_id|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objektbezeichner des Nachrichtentyps, der die Nachricht beschreibt.|  
|validation|**nchar(2)**|Für die Nachricht verwendete Überprüfung.<br /><br /> E = leer<br /><br /> N = Keine<br /><br /> X = XML|  
|message_body|**varbinary(max)**|Inhalt der Nachricht.|  
|message_id|**uniqueidentifier**|Eindeutiger Bezeichner für die Nachricht.|  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen einer Warteschlange liegt bei Mitgliedern der festen Datenbankrollen db_ddladmin und db_owner  sowie der festen Serverrolle sysadmin.  
  
 Die REFERENCES-Berechtigung für eine Warteschlange liegt standardmäßig beim Besitzer der Warteschlange, bei Mitgliedern der festen Datenbankrollen db_ddladmin und db_owner  sowie bei Mitgliedern der festen Serverrolle sysadmin.  
  
 RECEIVE-Berechtigungen für eine Warteschlange liegen standardmäßig beim Besitzer der Warteschlange, bei Mitgliedern der festen Datenbankrolle db_owner und bei Mitgliedern der festen Serverrolle sysadmin.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-queue-with-no-parameters"></a>A. Erstellen einer Warteschlange ohne Parameter  
 Im folgenden Beispiel wird eine Warteschlange erstellt, die für den Empfang von Nachrichten verfügbar ist. Für die Warteschlange wird keine gespeicherte Aktivierungsprozedur angegeben.  
  
```  
CREATE QUEUE ExpenseQueue ;  
```  
  
### <a name="b-creating-an-unavailable-queue"></a>B. Erstellen einer nicht verfügbaren Warteschlange  
 Im folgenden Beispiel wird eine Warteschlange erstellt, die nicht für den Empfang von Nachrichten verfügbar ist. Für die Warteschlange wird keine gespeicherte Aktivierungsprozedur angegeben.  
  
```  
CREATE QUEUE ExpenseQueue WITH STATUS=OFF ;  
```  
  
### <a name="c-creating-a-queue-and-specify-internal-activation-information"></a>C. Erstellen einer Warteschlange und Angeben von internen Aktivierungsinformationen  
 Im folgenden Beispiel wird eine Warteschlange erstellt, die für den Empfang von Nachrichten verfügbar ist. Die Warteschlange startet die gespeicherte Prozedur `expense_procedure`, wenn eine Nachricht in der Warteschlange angeordnet wird. Die gespeicherte Prozedur wird als der Benutzer `ExpenseUser` ausgeführt. Die Warteschlange startet ein Maximum von `5` Instanzen der gespeicherten Prozedur.  
  
```  
CREATE QUEUE ExpenseQueue  
    WITH STATUS=ON,  
    ACTIVATION (  
        PROCEDURE_NAME = expense_procedure,  
        MAX_QUEUE_READERS = 5,  
        EXECUTE AS 'ExpenseUser' ) ;  
```  
  
### <a name="d-creating-a-queue-on-a-specific-filegroup"></a>D. Erstellen einer Warteschlange in einer bestimmten Dateigruppe  
 Im folgenden Beispiel wird eine Warteschlange in der `ExpenseWorkFileGroup`-Dateigruppe erstellt.  
  
```  
CREATE QUEUE ExpenseQueue  
    ON ExpenseWorkFileGroup ;  
```  
  
### <a name="e-creating-a-queue-with-multiple-parameters"></a>E. Erstellen einer Warteschlange mit mehreren Parametern  
 Das folgende Beispiel erstellt eine Warteschlange auf dem `DEFAULT` Dateigruppe. Die Warteschlange ist nicht verfügbar. Nachrichten werden in der Warteschlange bis die Konversation beibehalten, die sie endet angehören. Wenn die Warteschlange über ALTER QUEUE zur Verfügung gestellt wird, startet die Warteschlange die gespeicherte Prozedur `2008R2.dbo.expense_procedure` für die Verarbeitung von Nachrichten. Die gespeicherte Prozedur wird als der Benutzer ausgeführt, der die `CREATE QUEUE`-Anweisung ausgeführt hat. Die Warteschlange startet ein Maximum von `10` Instanzen der gespeicherten Prozedur.  
  
```  
CREATE QUEUE ExpenseQueue  
    WITH STATUS = OFF,  
      RETENTION = ON,  
      ACTIVATION (  
          PROCEDURE_NAME = AdventureWorks2012.dbo.expense_procedure,  
          MAX_QUEUE_READERS = 10,  
          EXECUTE AS SELF )  
    ON [DEFAULT] ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)   
 [RECEIVE &#40;Transact-SQL&#41;](../../t-sql/statements/receive-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
