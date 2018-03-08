---
title: Sp_serveroption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_serveroption_TSQL
- sp_serveroption
dev_langs: TSQL
helpviewer_keywords:
- 7343 (Database Engine error)
- sp_serveroption
ms.assetid: 47d04a2b-dbf0-4f15-bd9b-81a2efc48131
caps.latest.revision: "40"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0827584d30844193bc9c15c3a4b7abac230d7bcc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="spserveroption-transact-sql"></a>sp_serveroption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Legt Serveroptionen für Remoteserver und Verbindungsserver fest.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sp_serveroption [@server = ] 'server'   
      ,[@optname = ] 'option_name'       
      ,[@optvalue = ] 'option_value' ;  
```  
  
## <a name="arguments"></a>Argumente  
 [  **@server =** ] **"***Server***"**  
 Der Name des Servers für den die Option festgelegt werden soll. *server* ist vom Datentyp **sysname**und hat keinen Standardwert.  
  
 [  **@optname =** ] **"***Option_name***"**  
 Die Option, die für den angegebenen Server festgelegt werden soll. *Option_name* ist **Varchar (**35**)**, hat keinen Standardwert. *Option_name* kann eines der folgenden Werte sein.  
  
|Wert|Description|  
|-----------|-----------------|  
|**Sortierung kompatibel**|Betrifft die Ausführung verteilter Abfragen für Verbindungsserver. Wenn diese Option, um festgelegt ist **"true"**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird davon ausgegangen, dass alle Zeichen auf dem Verbindungsserver mit dem lokalen Server bezüglich Zeichensatz und Sortierreihenfolge (Sortierreihenfolge) kompatibel sind. Dies ermöglicht [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Vergleiche für Zeichenspalten an den Provider zu senden. Wird diese Option nicht festgelegt, werden von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Vergleiche für Zeichenspalten immer lokal ausgewertet.<br /><br /> Diese Option sollte nur festgelegt werden, wenn sicher ist, dass die Datenquelle, die dem Verbindungsserver entspricht, den gleichen Zeichensatz und die gleiche Sortierreihenfolge wie der lokale Server verwendet.|  
|**Sortierungsname**|Gibt den Namen der Sortierung, die von der Remotedatenquelle verwendet wird, wenn **Remotesortierung verwenden** ist **"true"** und die Datenquelle ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle. Der Name muss eine von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützte Sortierung sein.<br /><br /> Verwenden Sie diese Option, wenn auf eine OLE DB-Datenquelle zugegriffen wird, die keine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datenquelle ist, deren Sortierung jedoch mit einer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierungen übereinstimmt.<br /><br /> Der Verbindungsserver muss eine einzige Sortierung unterstützen, die für alle Spalten in diesem Server verwendet wird. Legen Sie diese Option nicht fest, wenn der Verbindungsserver mehrere Sortierungen in einer einzelnen Datenquelle unterstützt oder wenn festgestellt wird, dass die Sortierung des Verbindungsservers nicht mit einer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierungen übereinstimmt.|  
|**Verbindungstimeout**|Timeout Varied Sekunden zum Herstellen einer Verbindung mit einem Verbindungsserver.<br /><br /> Wenn **0**, verwenden Sie die **Sp_configure** Standard.|  
|**Datenzugriff**|Aktiviert und deaktiviert den Zugriff auf verteilte Abfragen für Verbindungsserver. Kann verwendet werden, nur für **sys.server** Einträge hinzugefügt, die über **Sp_addlinkedserver**.|  
|**dist**|Der Verteiler.|  
|**Verzögerte schemaüberprüfung**|Bestimmt, ob das Schema von Remotetabellen überprüft wird.<br /><br /> Wenn **"true"**, überspringen Sie die schemaüberprüfung von Remotetabellen zu Beginn der Abfrage.|  
|**pub**|Verleger.|  
|**Abfragetimeout**|Der Timeoutwert für Abfragen auf einem Verbindungsserver.<br /><br /> Wenn **0**, verwenden Sie die **Sp_configure** Standard.|  
|**RPC**|Aktiviert RPC von dem betreffenden Server.|  
|**RPC-Ausgabe**|Aktiviert RPC zu dem betreffenden Server.|  
|**Sub**|Der Abonnent ist.|  
|**System**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Remotesortierung verwenden**|Bestimmt, ob die Sortierung einer Remotespalte oder eines lokalen Servers verwendet wird.<br /><br /> Wenn **"true"**, wird die Sortierung der Remotespalten zum [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenquellen und der im angegebenen Sortierung **Sortierungsname** dient für nicht-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenquellen.<br /><br /> Wenn **"false"**, verwenden verteilte Abfragen immer die standardsortierung des lokalen Servers, während **Sortierungsname** und die Sortierung der Remotespalten werden ignoriert. Der Standardwert ist **false**. (Die **"false"** Wert ist mit der im verwendeten sortierungssemantik kompatibel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0.)|  
|**Remote Proc Transaction promotion**|Verwenden Sie diese Option, um die Aktionen einer Server-zu-Server-Prozedur durch eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator-Transaktion (MS DTC) zu schützen. Wenn diese Option ist "true" (oder) Aufrufen einer remote gespeicherten Prozedur wird eine verteilte Transaktion gestartet und bei MS DTC eingetragen. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz, die die remote gespeicherte Prozedur aufruft, wird als Transaktionsurheber bezeichnet und steuert die Beendigung der Transaktion. Wenn im Anschluss eine COMMIT TRANSACTION- oder ROLLBACK TRANSACTION-Anweisung für die Verbindung ausgegeben wird, fordert die steuernde Instanz MS DTC auf, die Beendigung der verteilten Transaktion auf den beteiligten Computern zu verwalten.<br /><br /> Nachdem eine verteilte [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion gestartet wurde, können Aufrufe remote gespeicherter Prozeduren für weitere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanzen erfolgen, die als Verbindungsserver definiert wurden. Alle Verbindungsserver werden in der verteilten [!INCLUDE[tsql](../../includes/tsql-md.md)]-Transaktion eingetragen, und MS DTC stellt sicher, dass die Transaktion für jeden Verbindungsserver abgeschlossen wird.<br /><br /> Wenn diese Option auf FALSE (oder OFF) festgelegt ist, wird eine lokale Transaktion beim Aufruf einer remote gespeicherten Prozedur für einen Verbindungsserver nicht zu einer verteilten Transaktion höher gestuft.<br /><br /> Falls die Transaktion vor dem Server-zu-Server-Prozeduraufruf bereits eine verteilte Transaktion ist, hat diese Option keine Auswirkung. Der Prozeduraufruf für einen Verbindungsserver wird unter der gleichen verteilten Transaktion ausgeführt.<br /><br /> Falls vor dem Server-zu-Server-Prozeduraufruf keine Transaktion in der Verbindung aktiv ist, hat diese Option keine Auswirkung. Die Prozedur wird dann für einen Verbindungsserver ohne aktive Transaktionen ausgeführt.<br /><br /> Der Standardwert für diese Option ist TRUE (oder ON).|  
  
 [  **@optvalue =**] **"***Option_value***"**  
 Gibt an, und zwar unabhängig davon, ob die *Option_name* aktiviert werden soll (**"true"** oder **auf**) oder deaktiviert (**"false"** oder **deaktiviert**). *Option_value* ist **Varchar (**10**)**, hat keinen Standardwert.  
  
 *Option_value* möglicherweise eine nicht negative ganze Zahl, für die **Verbindungstimeout** und **Abfragetimeout** Optionen. Für die **Sortierungsname** Option *Option_value* kann ein Sortierungsname oder NULL sein.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Wenn die **Sortierung kompatibel** Option wird festgelegt, auf "true", **Sortierungsname** automatisch auf NULL festgelegt. Wenn **Sortierungsname** auf einen Wert ungleich NULL festgelegt ist **Sortierung kompatibel** automatisch auf "false" festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert ALTER ANY LINKED SERVER-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird ein Verbindungsserver, der einer anderen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz (`SEATTLE3`) entspricht, so konfiguriert, dass seine Sortierung mit der Sortierung der lokalen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz kompatibel ist.  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Verteilte Abfragen, gespeicherte Prozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [Sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
