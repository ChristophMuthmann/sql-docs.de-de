---
title: RECEIVE (Transact-SQL) | Microsoft-Dokumentation
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
- RECEIVE_TSQL
- RECEIVE
dev_langs:
- TSQL
helpviewer_keywords:
- queues [Service Broker], message retrieval
- messages [Service Broker], retrieving
- RECEIVE statement
- receiving messages
- retrieving messages
ms.assetid: 878c6c14-37ab-4b87-9854-7f8f42bac7dd
caps.latest.revision: 50
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0ec4c3011336b8feca6df673bf06021d46b30bdd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="receive-transact-sql"></a>RECEIVE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ruft eine oder mehrere Nachrichten aus einer Warteschlange ab. Je nach den Einstellungen für die Warteschlange wird entweder die Nachricht aus der Warteschlange entfernt oder der Status der Nachricht in der Warteschlange aktualisiert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
[ WAITFOR ( ]  
    RECEIVE [ TOP ( n ) ]   
        <column_specifier> [ ,...n ]  
        FROM <queue>  
        [ INTO table_variable ]  
        [ WHERE {  conversation_handle = conversation_handle  
                 | conversation_group_id = conversation_group_id } ]  
[ ) ] [ , TIMEOUT timeout ]  
[ ; ]  
  
<column_specifier> ::=  
{    *   
  |  { column_name | [ ] expression } [ [ AS ] column_alias ]  
  |  column_alias = expression   
}     [ ,...n ]   
  
<queue> ::=  
{  
    [ database_name . [ schema_name ] . | schema_name . ]  
        queue_name  
}  
  
```  
  
## <a name="arguments"></a>Argumente  
 WAITFOR  
 Gibt an, dass die RECEIVE-Anweisung darauf wartet, dass eine Nachricht für die Warteschlange eintrifft, wenn derzeit keine Nachrichten vorhanden sind.  
  
 TOP( *n* )  
 Gibt die maximale Anzahl von Nachrichten an, die zurückgegeben werden. Wird diese Klausel nicht angegeben, werden alle Nachrichten zurückgegeben, die die Kriterien der Anweisung erfüllen.  
  
 \*  
 Gibt an, dass das Resultset alle Spalten in der Warteschlange umfasst.  
  
 *column_name*  
 Der Name einer Spalte, die in das Resultset aufgenommen werden soll.  
  
 *expression*  
 Ein Spaltenname, eine Konstante, eine Funktion oder eine beliebige, durch Operatoren verknüpfte Kombination von Spaltennamen, Konstanten und Funktionen.  
  
 *column_alias*  
 Ein alternativer Name, der den Spaltennamen im Resultset ersetzt.  
  
 FROM  
 Gibt die Warteschlange an, die die Nachrichten enthält, die abgerufen werden sollen.  
  
 *database_name*  
 Der Name der Datenbank, die die Warteschlange enthält, von der Nachrichten empfangen werden. Wenn *database_name* nicht bereitgestellt wird, wird standardmäßig die aktuelle Datenbank verwendet.  
  
 *schema_name*  
 Der Name des Schemas, das Besitzer der Warteschlange ist, von der Nachrichten empfangen werden. Wenn *schema_name* nicht angegeben wird, wird standardmäßig das Standardschema für den aktuellen Benutzer verwendet.  
  
 *queue_name*  
 Der Name der Warteschlange, von der Nachrichten empfangen werden.  
  
 INTO *table_variable*  
 Gibt die Tabellenvariable an, in der RECEIVE die Nachrichten platziert. Die Tabellenvariable muss die gleiche Anzahl von Spalten wie die Nachrichten enthalten. Die Datentypen der einzelnen Spalten in der Tabellenvariablen müssen implizit in den Datentyp der entsprechenden Spalte in den Nachrichten konvertiert werden können. Wenn INTO nicht angegeben wird, werden die Nachrichten als Resultset zurückgegeben.  
  
 WHERE  
 Gibt die Konversation oder Konversationsgruppe für die empfangenen Nachrichten an. Wird kein Wert angegeben, werden Nachrichten aus der nächsten verfügbaren Konversationsgruppe zurückgegeben.  
  
 conversation_handle = *conversation_handle*  
 Gibt die Konversation für die empfangenen Nachrichten an. Der bereitgestellte *Konversationshandle* muss dem Typ **uniqueidentifer** oder einem Typ entsprechen, der in **uniqueidentifer** konvertierbar ist.  
  
 conversation_group_id = *conversation_group_id*  
 Gibt die Konversationsgruppe für die empfangenen Nachrichten an. Der bereitgestellte *Konversationsgruppen-ID* muss dem Typ **uniqueidentifer** oder einem Typ entsprechen, der in **uniqueidentifer** konvertierbar ist.  
  
 TIMEOUT *timeout*  
 Gibt in Millisekunden an, wie lange die Anweisung auf eine Nachricht warten soll. Diese Klausel kann nur zusammen mit der WAITFOR-Klausel verwendet werden. Wenn die Klausel nicht angegeben wird oder das Timeout den Wert –**1** hat, dann ist die Wartezeit unbegrenzt. Läuft das Timeout ab, gibt RECEIVE ein leeres Resultset zurück.  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  Wenn es sich bei der RECEIVE-Anweisung nicht um die erste Anweisung in einem Batch oder in einer gespeicherten Prozedur handelt, muss die vorhergehende Anweisung mit einem Semikolon (;) abgeschlossen werden.  
  
 Die RECEIVE-Anweisung liest Nachrichten aus einer Warteschlange und gibt ein Resultset zurück. Das zurückgegebene Resultset besteht aus null oder mehr Zeilen, wobei jede Zeile eine Nachricht umfasst. Wenn die INTO-Klausel nicht verwendet wird und *column_specifier* die Werte nicht lokalen Variablen zuordnet, dann gibt die Anweisung ein Resultset an das aufrufende Programm zurück.  
  
 Die Nachrichten, die von der RECEIVE-Anweisung zurückgegeben werden, können von anderen Nachrichtentypen sein. In Anwendungen kann die Spalte **message_type_name** verwendet werden, um jede Nachricht an Code weiterzuleiten, der den zugehörigen Nachrichtentyp behandelt. Die folgenden zwei Klassen von Nachrichtentypen stehen zur Verfügung:  
  
-   Anwendungsdefinierte Nachrichtentypen, die mit der CREATE MESSAGE TYPE-Anweisung erstellt wurden. Der in einer Konversation zulässige Satz von anwendungsdefinierten Nachrichtentypen wird durch den für die Konversation angegebenen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Vertrag definiert.  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Systemmeldungen, die Status- oder Fehlerinformationen zurückgeben.  
  
 Mit der RECEIVE-Anweisung werden erhaltene Nachrichten aus der Warteschlange entfernt, es sei denn, für die Warteschlange ist die Aufbewahrung von Nachrichten festgelegt. Ist als Einstellung für RETENTION für die Warteschlange der Wert ON festgelegt, dann aktualisiert die RECEIVE-Anweisung den Wert in der Spalte **status** auf **0** und belässt die Nachricht in der Warteschlange. Wenn ein Rollback für eine Transaktion erfolgt, die eine RECEIVE-Anweisung enthält, erfolgt auch ein Rollback für alle Änderungen in der Warteschlange innerhalb der Transaktion, und die Nachrichten werden in die Warteschlange zurückgegeben.  
  
 Alle Nachrichten, die von einer RECEIVE-Anweisung zurückgegeben werden, gehören derselben Konversationsgruppe an. Die RECEIVE-Anweisung sperrt die Konversationsgruppe für die zurückgegebenen Nachrichten so lange, bis die Transaktion, die die Anweisung enthält, abgeschlossen ist. Eine RECEIVE-Anweisung gibt Nachrichten zurück, die einen **Status** von **1** aufweisen. Das Resultset, das von einer RECEIVE-Anweisung zurückgegeben wird, ist implizit geordnet.  
  
-   Wenn Nachrichten aus mehreren Konversationen den Bedingungen der WHERE-Klausel entsprechen, gibt die RECEIVE-Anweisung alle Nachrichten aus einer Konversation zurück, bevor Nachrichten für eine andere Konversation zurückgegeben werden. Die Konversationen werden in der Reihenfolge absteigender Priorität verarbeitet.  
  
-   Für eine gegebene Konversation gibt eine RECEIVE-Anweisung Nachrichten in aufsteigender **message_sequence_number**-Reihenfolge zurück.  
  
 Die WHERE-Klausel der RECEIVE-Anweisung kann nur eine Suchbedingung enthalten, in der entweder **conversation_handle** oder **conversation_group_id** verwendet wird. Die Suchbedingung kann keine der anderen Spalten in der Warteschlange umfassen. Ein Ausdruck kann nicht **conversation_handle** oder **conversation_group_id** enthalten. Welcher Satz an Nachrichten zurückgegeben wird, hängt von den Bedingungen ab, die in der WHERE-Klausel angegeben sind:  
  
-   Wenn **conversation_handle** angegeben wird, dann gibt RECEIVE alle Nachrichten aus der angegebenen Konversation zurück, die in der Warteschlange verfügbar sind.  
  
-   Wenn **conversation_group_id** angegeben wird, dann gibt RECEIVE alle Nachrichten zurück, die in der Warteschlange aus Konversationen verfügbar sind, die der angegebenen Konversationsgruppe angehören.  
  
-   Wenn keine WHERE-Klausel angegeben wurde, bestimmt RECEIVE die Konversationsgruppe:  
  
    -   Es sind eine oder mehrere Nachrichten in der Warteschlange verfügbar.  
  
    -   Wurde nicht von einer anderen RECEIVE-Anweisung gesperrt.  
  
    -   Weist von allen Konversationsgruppen, die diese Kriterien erfüllen, die höchste Prioritätsebene auf.  
  
     RECEIVE gibt dann alle Nachrichten zurück, die in der Warteschlange aus Konversationen verfügbar sind, die der ausgewählten Konversationsgruppe angehören.  
  
 Ist das in der WHERE-Klausel angegebene Konversationshandle oder der für die Konversationsgruppe angegebene Bezeichner nicht vorhanden oder nicht mit der angegebenen Warteschlange verknüpft, dann gibt die RECEIVE-Anweisung einen Fehler zurück.  
  
 Ist als Status für die in der RECEIVE-Anweisung angegebene Warteschlange der Wert OFF festgelegt, schlägt die Anweisung mit einem [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler fehl.  
  
 Wird die WAITFOR-Klausel angegeben, wird mit der Ausführung der Anweisung bis zum Ablauf des angegebenen Timeouts oder so lange gewartet, bis ein Resultset verfügbar ist. Wird die Warteschlange gelöscht, oder wird als Status für die Warteschlange OFF angegeben, während eine Anweisung wartet, gibt die Anweisung sofort einen Fehler zurück. Wenn die RECEIVE-Anweisung eine Konversationsgruppe oder ein Konversationshandle angibt und wenn der Dienst für diese Konversation gelöscht oder zu einer anderen Warteschlange verschoben wird, dann gibt die RECEIVE-Anweisung einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Fehler zurück.  
  
 RECEIVE ist in einer benutzerdefinierten Funktion nicht gültig.  
  
 Die RECEIVE-Anweisung verfügt über keinen prioritätsbezogenen Ausschlussverhinderungsmechanismus. Wenn eine einzelne RECEIVE-Anweisung eine Konversationsgruppe sperrt und viele Nachrichten aus Konversationen mit niedrigerer Priorität abruft, können keine Nachrichten aus Konversationen mit hoher Priorität in der Gruppe empfangen werden. Um dies beim Abruf von Nachrichten aus Konversationen mit niedriger Priorität zu verhindern, verwenden Sie die TOP-Klausel, um die Anzahl von Nachrichten zu beschränken, die von jeder einzelnen RECEIVE-Anweisung empfangen werden.  
  
## <a name="queue-columns"></a>Spalten in der Warteschlange  
 In der folgenden Tabelle werden die Spalten einer Warteschlange aufgelistet.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**status**|**tinyint**|Status der Nachricht. Für Nachrichten, die vom RECEIVE-Befehl zurückgegeben werden, ist der Status immer **0**. Nachrichten in der Warteschlange können einen der folgenden Werte enthalten:<br /><br /> **0**=Bereit **1**=Nachricht empfangen **2**=Noch nicht abgeschlossen **3**=Gesendete Nachricht wurde beibehalten|  
|**priority**|**tinyint**|Die Prioritätsebene der Konversation, die auf die Nachricht angewendet wird.|  
|**queuing_order**|**bigint**|Fortlaufende Nummer der Nachricht in der Warteschlange.|  
|**conversation_group_id**|**uniqueidentifier**|Bezeichner für die Konversationsgruppe, zu der diese Nachricht gehört.|  
|**conversation_handle**|**uniqueidentifier**|Handle der Konversation, von der diese Nachricht ein Teil ist.|  
|**message_sequence_number**|**bigint**|Sequenznummer der Nachricht in der Konversation.|  
|**service_name**|**nvarchar(512)**|Name des Diensts, an den die Konversation gerichtet ist.|  
|**service_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objektbezeichner des Diensts, an den die Konversation gerichtet ist.|  
|**service_contract_name**|**nvarchar(256)**|Name des Vertrags, dem die Konversation entspricht.|  
|**service_contract_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objektbezeichner des Vertrags, dem die Konversation entspricht.|  
|**message_type_name**|**nvarchar(256)**|Name des Nachrichtentyps, der das Format der Nachricht beschreibt. Nachrichten können entweder vom Typ Anwendungsnachricht oder Brokersystemmeldungen sein.|  
|**message_type_id**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Objektbezeichner des Nachrichtentyps, der die Nachricht beschreibt.|  
|**validation**|**nchar(2)**|Für die Nachricht verwendete Überprüfung.<br /><br /> **E**=Empty**N**=None**X**=XML|  
|**message_body**|**varbinary(MAX)**|Inhalt der Nachricht.|  
  
## <a name="permissions"></a>Berechtigungen  
 Um eine Nachricht erhalten zu können, muss der aktuelle Benutzer über eine RECEIVE-Berechtigung für die Warteschlange verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-receiving-all-columns-for-all-messages-in-a-conversation-group"></a>A. Empfangen sämtlicher Spalten für alle Nachrichten in einer Konversationsgruppe  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die nächste verfügbare Konversationsgruppe aus der `ExpenseQueue`-Warteschlange empfangen. Die Anweisung gibt die Nachrichten als Resultset zurück.  
  
```  
RECEIVE * FROM ExpenseQueue ;  
```  
  
### <a name="b-receiving-specified-columns-for-all-messages-in-a-conversation-group"></a>B. Empfangen angegebener Spalten für alle Nachrichten in einer Konversationsgruppe  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die nächste verfügbare Konversationsgruppe aus der `ExpenseQueue`-Warteschlange empfangen. Die Anweisung gibt die Nachrichten als Resultset zurück, das die Spalten `conversation_handle`, `message_type_name` und `message_body` umfasst.  
  
```  
RECEIVE conversation_handle, message_type_name, message_body  
FROM ExpenseQueue ;  
```  
  
### <a name="c-receiving-the-first-available-message-in-the-queue"></a>C. Empfangen der ersten verfügbaren Nachricht in der Warteschlange  
 Im folgenden Beispiel wird die erste verfügbare Nachricht aus der `ExpenseQueue`-Warteschlange als Resultset empfangen.  
  
```  
RECEIVE TOP (1) * FROM ExpenseQueue ;  
```  
  
### <a name="d-receiving-all-messages-for-a-specified-conversation"></a>D. Empfangen aller Nachrichten für eine angegebene Konversation  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die angegebene Konversation aus der `ExpenseQueue`-Warteschlange als Resultset empfangen.  
  
```  
DECLARE @conversation_handle UNIQUEIDENTIFIER ;  
  
SET @conversation_handle = <retrieve conversation from database> ;  
  
RECEIVE *  
FROM ExpenseQueue  
WHERE conversation_handle = @conversation_handle ;  
```  
  
### <a name="e-receiving-messages-for-a-specified-conversation-group"></a>E. Empfangen von Nachrichten für eine angegebene Konversationsgruppe  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die angegebene Konversationsgruppe aus der `ExpenseQueue`-Warteschlange als Resultset empfangen.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
SET @conversation_group_id =   
    <retrieve conversation group ID from database> ;  
  
RECEIVE *  
FROM ExpenseQueue  
WHERE conversation_group_id = @conversation_group_id ;  
```  
  
### <a name="f-receiving-into-a-table-variable"></a>F. Empfangen in einer Tabellenvariablen  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für eine angegebene Konversationsgruppe aus der `ExpenseQueue`-Warteschlange in einer Tabellenvariablen empfangen.  
  
```  
DECLARE @conversation_group_id UNIQUEIDENTIFIER ;  
  
DECLARE @procTable TABLE(  
     service_instance_id UNIQUEIDENTIFIER,  
     handle UNIQUEIDENTIFIER,  
     message_sequence_number BIGINT,  
     service_name NVARCHAR(512),  
     service_contract_name NVARCHAR(256),  
     message_type_name NVARCHAR(256),  
     validation NCHAR,  
     message_body VARBINARY(MAX)) ;  
  
SET @conversation_group_id = <retrieve conversation group ID from database> ;  
  
RECEIVE TOP (1)  
    conversation_group_id,  
    conversation_handle,  
    message_sequence_number,  
    service_name,  
    service_contract_name,  
    message_type_name,  
    validation,  
    message_body  
FROM ExpenseQueue  
INTO @procTable  
WHERE conversation_group_id = @conversation_group_id ;  
```  
  
### <a name="g-receiving-messages-and-waiting-indefinitely"></a>G. Empfangen von Nachrichten ohne Begrenzung der Wartezeit  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die nächste verfügbare Konversationsgruppe in der `ExpenseQueue`-Warteschlange empfangen. Die Anweisung wartet, bis mindestens eine Nachricht verfügbar ist. Sie gibt dann ein Resultset zurück, das alle Nachrichtenspalten enthält.  
  
```  
WAITFOR (  
    RECEIVE *  
    FROM ExpenseQueue) ;  
```  
  
### <a name="h-receiving-messages-and-waiting-for-a-specified-interval"></a>H. Empfangen von Nachrichten und Warten für ein angegebenes Intervall  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die nächste verfügbare Konversationsgruppe in der `ExpenseQueue`-Warteschlange empfangen. Die Anweisung wartet 60 Sekunden oder so lange, bis mindestens eine Nachricht verfügbar ist, je nachdem, welches Ereignis zuerst eintritt. Die Anweisung gibt ein Resultset zurück, das alle Nachrichtenspalten enthält, wenn mindestens eine Nachricht verfügbar ist. Andernfalls gibt die Anweisung ein leeres Resultset zurück.  
  
```  
WAITFOR (  
    RECEIVE *  
    FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="i-receiving-messages-modifying-the-type-of-a-column"></a>I. Empfangen von Nachrichten und Ändern des Typs einer Spalte  
 Im folgenden Beispiel werden alle verfügbaren Nachrichten für die nächste verfügbare Konversationsgruppe in der `ExpenseQueue`-Warteschlange empfangen. Wenn über den Nachrichtentyp angegeben wird, dass die Nachricht ein XML-Dokument enthält, dann konvertiert die Anweisung den Nachrichtentext in XML.  
  
```  
WAITFOR (  
    RECEIVE message_type_name,  
        CASE  
            WHEN validation = 'X' THEN CAST(message_body as XML)  
            ELSE NULL  
         END AS message_body   
         FROM ExpenseQueue ),  
TIMEOUT 60000 ;  
```  
  
### <a name="j-receiving-a-message-extracting-data-from-the-message-body-retrieving-conversation-state"></a>J. Empfangen einer Nachricht, Extrahieren von Daten aus dem Nachrichtentext und Abrufen des Konversationsstatus  
 Im folgenden Beispiel wird die nächste verfügbare Nachricht für die nächste verfügbare Konversationsgruppe in der `ExpenseQueue`-Warteschlange empfangen. Im Falle des Nachrichtentyps `//Adventure-Works.com/Expenses/SubmitExpense` extrahiert die Anweisung die Employee ID und eine Liste von Elementen aus dem Nachrichtentext. Die Anweisung ruft auch den Status der Konversation aus der `ConversationState`-Tabelle ab.  
  
```  
WAITFOR(  
    RECEIVE   
    TOP(1)  
      message_type_name,  
      COALESCE(  
           (SELECT TOP(1) ConversationState  
            FROM CurrentConversations AS cc  
            WHERE cc.ConversationHandle = conversation_handle),  
           'NEW')  
      AS ConversationState,  
      COALESCE(  
          (SELECT TOP(1) ErrorCount  
           FROM CurrentConversations AS cc  
           WHERE cc.ConversationHandle = conversation_handle),   
           0)  
      AS ConversationErrors,  
      CASE WHEN message_type_name = N'//Adventure-Works.com/Expenses/SubmitExpense'  
          THEN CAST(message_body AS XML).value(  
                'declare namespace rpt = "http://Adventure-Works.com/schemas/expenseReport"  
                   (/rpt:ExpenseReport/rpt:EmployeeID)[1]', 'nvarchar(20)')  
         ELSE NULL  
      END AS EmployeeID,  
      CASE WHEN message_type_name = N'//Adventure-Works.com/Expenses/SubmitExpense'  
          THEN CAST(message_body AS XML).query(  
                'declare namespace rpt = "http://Adventure-Works.com/schemas/expenseReport"   
                     /rpt:ExpenseReport/rpt:ItemDetail')  
          ELSE NULL  
      END AS ItemList  
    FROM ExpenseQueue   
), TIMEOUT 60000 ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [BEGIN CONVERSATION TIMER &#40;Transact-SQL&#41;](../../t-sql/statements/begin-conversation-timer-transact-sql.md)   
 [END CONVERSATION &#40;Transact-SQL&#41;](../../t-sql/statements/end-conversation-transact-sql.md)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [SEND &#40;Transact-SQL&#41;](../../t-sql/statements/send-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [ALTER QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-queue-transact-sql.md)   
 [DROP QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-queue-transact-sql.md)  
  
  
