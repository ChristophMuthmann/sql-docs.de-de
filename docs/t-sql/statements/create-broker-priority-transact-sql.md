---
title: "Erstellen Sie die BROKERPRIORITÄT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE BROKER PRIORITY
- PRIORITY_TSQL
- CREATE_BROKER_PRIORITY_TSQL
- PRIORITY
- CREATE BROKER
- BROKER_TSQL
- BROKER
- CREATE_BROKER_TSQL
- BROKER PRIORITY
- BROKER_PRIORITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE BROKER PRIORITY statement
ms.assetid: e0bbebfa-b7c3-4825-8169-7281f7e6de98
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c7a1d85cba038eb3f7ef4a4e3198485943e8e194
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-broker-priority-transact-sql"></a>CREATE BROKER PRIORITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Definiert eine Prioritätsebene und die Gruppe von Kriterien, anhand derer bestimmt wird, welchen [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Konversationen die Prioritätsebene zugeordnet wird. Die Prioritätsebene wird jedem Konversationsendpunkt zugewiesen, die verwendet die gleiche Kombination aus Verträgen und Diensten, die die konversationspriorität angegeben sind. Die Prioritätswerte liegen zwischen 1 (niedrig) und 10 (hoch). Der Standardwert ist 5.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
CREATE BROKER PRIORITY ConversationPriorityName  
FOR CONVERSATION  
[ SET ( [ CONTRACT_NAME = {ContractName | ANY } ]  
        [ [ , ] LOCAL_SERVICE_NAME = {LocalServiceName | ANY } ]  
        [ [ , ] REMOTE_SERVICE_NAME = {'RemoteServiceName' | ANY } ]  
        [ [ , ] PRIORITY_LEVEL = {PriorityValue | DEFAULT } ]  
       )  
]  
[;]  
  
```  
  
## <a name="arguments"></a>Argumente  
 *ConversationPriorityName*  
 Gibt den Namen für diese Konversationspriorität an. Der Name muss in der aktuellen Datenbank eindeutig sein und muss den Regeln für entsprechen [!INCLUDE[ssDE](../../includes/ssde-md.md)] [Bezeichner](../../relational-databases/databases/database-identifiers.md).  
  
 SET  
 Gibt die Kriterien an, anhand derer bestimmt wird, ob die Konversationspriorität für eine Konversation übernommen wird. Wenn angegeben, muss SET mindestens ein Kriterium enthalten: CONTRACT_NAME, LOCAL_SERVICE_NAME, REMOTE_SERVICE_NAME oder PRIORITY_LEVEL. Wenn SET nicht angegeben wird, werden für alle drei Kriterien die Standardwerte festgelegt.  
  
 CONTRACT_NAME = {*ContractName* | **ANY**}  
 Gibt den Namen eines Vertrags an, der als Kriterium für die Festlegung verwendet wird, ob die Konversationspriorität für eine Konversation gelten soll. *ContractName* ist eine [!INCLUDE[ssDE](../../includes/ssde-md.md)] Bezeichner, und geben Sie den Namen eines Vertrags müssen in der aktuellen Datenbank.  
  
 *ContractName*  
 Gibt an, dass die konversationspriorität nur für Konversationen angewendet werden kann, wobei die BEGIN DIALOG-Anweisung, die die Konversation gestartet ON CONTRACT angegeben *ContractName*.  
  
 ANY  
 Gibt an, dass die Konversationspriorität für jede Konversation unabhängig vom verwendeten Vertrag übernommen werden kann.  
  
 Der Standardwert ist ANY.  
  
 LOCAL_SERVICE_NAME = {*"LocalServiceName"* | **ANY**}  
 Gibt den Namen eines Diensts an, der als Kriterium verwendet werden kann, um zu bestimmen, ob die Konversationspriorität für einen Konversationsendpunkt übernommen wird.  
  
 *"LocalServiceName"* ist eine [!INCLUDE[ssDE](../../includes/ssde-md.md)] Bezeichner. Mit diesem muss der Name eines Diensts in der aktuellen Datenbank angegeben werden.  
  
 *"LocalServiceName"*  
 Gibt an, dass die Konversationspriorität für Folgendes übernommen werden kann:  
  
-   Jeden Konversationsendpunkt für Initiator, dessen initiatordienstname entspricht *"LocalServiceName"*.  
  
-   Jeden Konversationsendpunkt für Ziel, dessen Zieldienstname entspricht *"LocalServiceName"*.  
  
 ANY  
 -   Gibt an, dass die Konversationspriorität unabhängig vom Namen des vom Endpunkt verwendeten lokalen Diensts für jeden Konversationsendpunkt übernommen werden kann.  
  
 Der Standardwert ist ANY.  
  
 REMOTE_SERVICE_NAME = {'*"RemoteServiceName"*"| **ANY**}  
 Gibt den Namen eines Diensts an, der als Kriterium verwendet werden kann, um zu bestimmen, ob die Konversationspriorität für einen Konversationsendpunkt übernommen wird.  
  
 *"RemoteServiceName"* ist ein Literal vom Typ **nvarchar(256)**. [!INCLUDE[ssSB](../../includes/sssb-md.md)]Führt einen Byte-pro-Byte-Vergleich mit der *"RemoteServiceName"* Zeichenfolge. Bei dem Vergleich wird die Groß-/Kleinschreibung beachtet, die aktuelle Sortierung hingegen wird nicht berücksichtigt. Der Zieldienst kann in der aktuellen Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] oder in einer Remoteinstanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] vorhanden sein.  
  
 "*" RemoteServiceName "*"  
 Gibt an, dass die Konversationspriorität für Folgendes übernommen werden kann:  
  
-   Jeden Konversationsendpunkt für Initiator, dessen zugeordneter Zieldienstname entspricht *"RemoteServiceName"*.  
  
-   Jeden Konversationsendpunkt für Ziel, dessen zugeordneter initiatordienstname entspricht *"RemoteServiceName"*.  
  
 ANY  
 Gibt an, dass die Konversationspriorität unabhängig vom Namen des dem Endpunkt zugeordneten Remotediensts für jeden Konversationsendpunkt übernommen werden kann.  
  
 Der Standardwert ist ANY.  
  
 PRIORITY_LEVEL = { *PriorityValue* | **Standard** }  
 Gibt die Priorität an, die jedem Konversationsendpunkt zugeordnet werden soll, der die für die Konversationspriorität angegebenen Verträge und Dienste verwendet. *PriorityValue* muss eine ganze Zahl zwischen 1 (niedrigste Priorität) und 10 (höchste Priorität) Zeichenfolgenliteral sein. Der Standardwert ist 5.  
  
## <a name="remarks"></a>Hinweise  
 In [!INCLUDE[ssSB](../../includes/sssb-md.md)] werden Prioritätsebenen Konversationsendpunkte zugeordnet. Mithilfe der Prioritätsebene wird die Priorität der dem Endpunkt zugeordneten Vorgänge gesteuert. Jede Konversation verfügt über zwei Konversationsendpunkte:  
  
-   Der Konversationsendpunkt für den Initiator ordnet eine Seite der Konversation dem Initiatordienst und der Initiatorwarteschlange zu. Der Konversationsendpunkt für den Initiator wird beim Ausführen der BEGIN DIALOG-Anweisung erstellt. Zu den dem Konversationsendpunkt für den Initiator zugeordneten Vorgängen zählen folgende:  
  
    -   Sendevorgänge vom Initiatordienst.  
  
    -   Empfangsvorgänge von der Initiatorwarteschlange.  
  
    -   Das Abrufen der nächsten Konversationsgruppe aus der Initiatorwarteschlange  
  
-   Der Konversationsendpunkt für das Ziel ordnet die andere Seite der Konversation dem Zieldienst und der Warteschlange zu. Der Konversationsendpunkt für das Ziel wird erstellt, wenn mithilfe der Konversation eine Nachricht an die Zielwarteschlange übermittelt wird. Zu den dem Konversationsendpunkt für das Ziel zugeordneten Vorgängen zählen folgende:  
  
    -   Empfangsvorgänge von der Zielwarteschlange.  
  
    -   Sendevorgänge vom Zieldienst.  
  
    -   Das Abrufen der nächsten Konversationsgruppe aus der Zielwarteschlange.  
  
 In [!INCLUDE[ssSB](../../includes/sssb-md.md)] werden Konversationsprioritätsebenen beim Erstellen von Endpunkten zugeordnet. Der Konversationsendpunkt behält die Prioritätsstufe bei, bis die Konversation beendet ist. Neue Prioritäten oder Änderungen an vorhandenen Prioritäten werden nicht für vorhandene Konversationen übernommen.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]Ordnet einem Konversationsendpunkt die Prioritätsebene von der konversationspriorität, deren Vertrags- und dienstkriterien die größte mit den Eigenschaften des Endpunkts übereinstimmen. In der folgenden Tabelle wird die Rangfolge bei Übereinstimmungen angezeigt:  
  
|Vertrag des Vorgangs|Lokaler Dienst des Vorgangs|Remotedienst des Vorgangs|  
|------------------------|-----------------------------|------------------------------|  
|*ContractName*|*"LocalServiceName"*|*"RemoteServiceName"*|  
|*ContractName*|*"LocalServiceName"*|ANY|  
|*ContractName*|ANY|*"RemoteServiceName"*|  
|*ContractName*|ANY|ANY|  
|ANY|*"LocalServiceName"*|*"RemoteServiceName"*|  
|ANY|*"LocalServiceName"*|ANY|  
|ANY|ANY|*"RemoteServiceName"*|  
|ANY|ANY|ANY|  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] sucht zuerst nach einer Priorität, bei der angegebene Vertrag, der lokale Dienst und der Remotedienst dem Vertrag, dem lokalen Dienst und dem Remotedienst des Vorgangs entsprechen. Wird keine entsprechende Priorität gefunden, sucht [!INCLUDE[ssSB](../../includes/sssb-md.md)] nach einer Priorität, bei der der Vertrag und der lokale Dienst dem Vertrag und dem lokalen Dienst des Vorgangs entsprechen und für die der Remotedienst als ANY angegeben wurde. Dieser Vorgang wird für alle Varianten fortgesetzt, die in der Rangfolgentabelle aufgeführt werden. Wenn keine Übereinstimmung gefunden wird, wird dem Vorgang die Standardpriorität 5 zugewiesen.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] weist allen Konversationsendpunkten unabhängig voneinander eine Prioritätsstufe zu. Damit [!INCLUDE[ssSB](../../includes/sssb-md.md)] Prioritätsebenen dem Konversationsendpunkt für den Initiator und das Ziel zuordnet, müssen Sie sicherstellen, dass beide Endpunkte von Konversationsprioritäten abgedeckt werden. Wenn sich die Konversationsendpunkte für den Initiator und das Ziel in verschiedenen Datenbanken befinden, müssen Sie in jeder Datenbank Konversationsprioritäten erstellen. In der Regel wird die gleiche Prioritätsebene für beide Konversationsendpunkte einer Konversation angegeben; Sie können aber auch verschiedene Prioritätsebenen angeben.  
  
 Prioritätsebenen werden immer für Vorgänge übernommen, die Nachrichten oder Konversationsgruppenbezeichner aus einer Warteschlange empfangen. Prioritätsebenen werden auch übernommen, wenn Nachrichten von einer Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] an eine andere übermittelt werden.  
  
 Prioritätsebenen werden nicht verwendet, wenn für die Nachrichtenübermittlung Folgendes zutrifft:  
  
-   Nachrichten werden aus einer Datenbank übermittelt, für die die Datenbankoption HONOR_BROKER_PRIORITY auf OFF festgelegt ist. Weitere Informationen zu dieser Einstellung finden Sie unter [ALTER DATABASE SET-Optionen &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
-   Nachrichten werden zwischen Diensten in der gleichen Instanz des Datenbankmoduls übermittelt.  
  
-   Alle [!INCLUDE[ssSB](../../includes/sssb-md.md)] Vorgänge in einer Datenbank sind Standardprioritäten von 5 zugewiesen, wenn keine konversationsprioritäten in der Datenbank erstellt wurden.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen einer Konversationspriorität erhalten standardmäßig die Mitglieder der festen Datenbankrolle db_ddladmin oder db_owner und die feste Serverrolle sysadmin. Erfordert die ALTER-Berechtigung für die Datenbank.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-assigning-a-priority-level-to-both-directions-of-a-conversation"></a>A. Zuweisen einer Prioritätsebene zu beiden Richtungen einer Konversation  
 Mit diesen beiden Konversationsprioritäten wird sichergestellt, dass allen Vorgänge, die `SimpleContract` zwischen `TargetService` und `InitiatorAService` verwenden, die Prioritätsebene 3 zugewiesen wird.  
  
```  
CREATE BROKER PRIORITY InitiatorAToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = InitiatorServiceA,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 3);  
CREATE BROKER PRIORITY TargetToInitiatorAPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'InitiatorServiceA',  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="b-setting-the-priority-level-for-all-conversations-that-use-a-contract"></a>B. Festlegen der Prioritätsebene für alle Konversationen, die einen Vertrag verwenden  
 Weist allen Vorgängen, die einen Vertrag mit dem Namen `7` verwenden, eine Prioritätsebene von `SimpleContract` zu. Dabei wird davon ausgegangen, dass keine anderen Prioritäten vorhanden sind, mit denen sowohl `SimpleContract` als auch entweder ein lokaler oder ein Remotedienst angegeben werden.  
  
```  
CREATE BROKER PRIORITY SimpleContractDefaultPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 7);  
```  
  
### <a name="c-setting-a-base-priority-level-for-a-database"></a>C. Festlegen einer Basisprioritätsebene für eine Datenbank  
 Definiert die Konversationsprioritäten für zwei bestimmte Dienste und definiert dann eine Konversationspriorität, die mit allen anderen Konversationsendpunkten übereinstimmt. Dadurch wird nicht die Standardpriorität ersetzt, die stets den Wert 5 aufweist, aber es wird die Anzahl von Elementen reduziert, denen die Standardpriorität zugewiesen ist.  
  
```  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ClaimPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 9);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/ApprovalPriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = //Adventure-Works.com/Expenses/ClaimService,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY [//Adventure-Works.com/Expenses/BasePriority]  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = ANY,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 3);  
```  
  
### <a name="d-creating-three-priority-levels-for-a-target-service-by-using-services"></a>D. Erstellen von drei Prioritätsebenen für einen Zieldienst mithilfe von Diensten  
 Unterstützt ein System, das drei Leistungsebenen bereitstellt: Gold (hoch), Silver (mittel) und Bronze (niedrig). Es gibt einen Vertrag, aber jede Ebene weist einen separaten Initiatordienst auf. Alle Initiatordienste kommunizieren mit einem zentralen Zieldienst.  
  
```  
CREATE BROKER PRIORITY GoldInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = GoldInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY GoldTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'GoldInitiatorService',  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = SilverInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY SilverTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'SilverInitiatorService',  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzeInitToTargetPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = BronzeInitiatorService,  
         REMOTE_SERVICE_NAME = N'TargetService',  
         PRIORITY_LEVEL = 2);  
CREATE BROKER PRIORITY BronzeTargetToInitPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SimpleContract,  
         LOCAL_SERVICE_NAME = TargetService,  
         REMOTE_SERVICE_NAME = N'BronzeInitiatorService',  
         PRIORITY_LEVEL = 2);  
```  
  
### <a name="e-creating-three-priority-levels-for-multiple-services-using-contracts"></a>E. Erstellen von drei Prioritätsebenen für mehrere Dienste mithilfe von Verträgen  
 Unterstützt ein System, das drei Leistungsebenen bereitstellt: Gold (hoch), Silver (mittel) und Bronze (niedrig). Jede Ebene weist einen separaten Vertrag auf. Diese Prioritäten werden für alle Dienste übernommen, auf die von Konversationen verwiesen wird, die die Verträge verwenden.  
  
```  
CREATE BROKER PRIORITY GoldPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = GoldContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 6);  
CREATE BROKER PRIORITY SilverPriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = SilverContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 4);  
CREATE BROKER PRIORITY BronzePriority  
    FOR CONVERSATION  
    SET (CONTRACT_NAME = BronzeContract,  
         LOCAL_SERVICE_NAME = ANY,  
         REMOTE_SERVICE_NAME = ANY,  
         PRIORITY_LEVEL = 2);  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER BROKER PRIORITY & #40; Transact-SQL & #41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [BEGIN DIALOG CONVERSATION & #40; Transact-SQL & #41;](../../t-sql/statements/begin-dialog-conversation-transact-sql.md)   
 [Erstellen Sie Vertrag & #40; Transact-SQL & #41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP BROKER PRIORITY & #40; Transact-SQL & #41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [GET CONVERSATION GROUP & #40; Transact-SQL & #41;](../../t-sql/statements/get-conversation-group-transact-sql.md)   
 [Empfangen von & #40; Transact-SQL & #41;](../../t-sql/statements/receive-transact-sql.md)   
 [SEND & #40; Transact-SQL & #41;](../../t-sql/statements/send-transact-sql.md)   
 [Sys. conversation_priorities & #40; Transact-SQL & #41;](../../relational-databases/system-catalog-views/sys-conversation-priorities-transact-sql.md)  
  
  
