---
title: Schweregrade von Datenbankmodulfehlern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- user-defined error messages [SQL Server]
- severity levels [SQL Server]
- retrieving error severity
- errors [SQL Server], severity
- TRY...CATCH [SQL Server]
ms.assetid: 3e7f5925-6edd-42e1-bf17-f7deb03993a7
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f5b2b6fbe1d6d46c045452430067a542a99623bd
ms.contentlocale: de-de
ms.lasthandoff: 04/11/2017

---
# <a name="database-engine-error-severities"></a>Schweregrade von Datenbankmodulfehlern
  Wenn von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ein Fehler ausgelöst wird, gibt der Schweregrad des Fehlers den Problemtyp an, das in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]aufgetreten ist.  
  
## <a name="levels-of-severity"></a>Schweregrade  
 In der folgenden Tabelle sind die Schweregrade der Fehler aufgeführt und beschrieben, die von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]ausgelöst werden.  
  
|Schweregrad|Beschreibung|  
|--------------------|-----------------|  
|0-9|Informationsmeldungen, die Statusinformationen zurückgeben oder Fehler melden, die nicht schwerwiegend sind. [!INCLUDE[ssDE](../../includes/ssde-md.md)] löst keine Systemfehler mit Schweregraden zwischen 0 und 9 aus.|  
|10|Informationsmeldungen, die Statusinformationen zurückgeben oder Fehler melden, die nicht schwerwiegend sind. Aus Kompatibilitätsgründen konvertiert [!INCLUDE[ssDE](../../includes/ssde-md.md)] den Schweregrad 10 in Schweregrad 0, bevor die Fehlerinformationen an die aufrufende Anwendung zurückgegeben werden.|  
|11-16|Verweisen auf Fehler, die der Benutzer beheben kann.|  
|11|Gibt an, dass das Objekt oder die Entität nicht vorhanden ist.|  
|12|Ein spezieller Schweregrad für Abfragen, die aufgrund von speziellen Abfragehinweisen keine Sperren verwenden. In einigen Fällen können von diesen Anweisungen ausgeführte Lesevorgänge zu inkonsistenten Daten führen, da Sperren nicht zur Sicherstellung der Konsistenz verwendet werden.|  
|13|Verweist auf Deadlockfehler der Transaktion.|  
|14|Verweist auf sicherheitsbezogene Fehler, wie z. B. eine verweigerte Berechtigung.|  
|15|Verweist auf Syntaxfehler im [!INCLUDE[tsql](../../includes/tsql-md.md)] -Befehl.|  
|16|Verweist auf allgemeine Fehler, die der Benutzer beheben kann.|  
|17-19|Verweisen auf Softwarefehler, die der Benutzer nicht beheben kann. Informieren Sie Ihren Systemadministrator über das Problem.|  
|17|Gibt an, dass die Anweisung dazu geführt hat, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht genügend Ressourcen hat (z. B. Arbeitsspeicher, Sperren oder Speicherplatz für die Datenbank) oder ein vom Systemadministrator festgelegter Grenzwert überschritten wurde.|  
|18|Verweist auf ein Problem in der Software von [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Die Ausführung der Anweisung wird jedoch abgeschlossen, und die Verbindung mit der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] wird aufrechterhalten. Der Systemadministrator sollte informiert werden, wenn eine Meldung mit dem Schweregrad 18 auftritt.|  
|19|Gibt an, dass ein nicht konfigurierbarer Grenzwert von [!INCLUDE[ssDE](../../includes/ssde-md.md)] überschritten worden ist und der aktuelle Batchprozess beendet wurde. Durch Fehlermeldungen mit einem Schweregrad von 19 oder höher wird die Ausführung des aktuellen Batches beendet. Fehlermeldungen mit dem Schweregrad 19 sind selten und müssen vom Systemadministrator oder Ihrem bevorzugten Anbieter für technischen Support behoben werden. Wenden Sie sich an Ihren Systemadministrator, wenn eine Meldung mit dem Schweregrad 19 ausgelöst wird. Fehlermeldungen mit den Schweregraden 19 bis 25 werden im Fehlerprotokoll aufgezeichnet.|  
|20-24|Verweisen auf Systemprobleme und sind schwerwiegende Fehler, d. h., der Task von [!INCLUDE[ssDE](../../includes/ssde-md.md)] , der eine Anweisung oder einen Batch ausführt, wird nicht mehr ausgeführt. Der Task zeichnet Informationen über den Vorfall auf und wird dann beendet. In den meisten Fällen wird möglicherweise auch die Anwendungsverbindung mit der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] beendet. In diesem Fall ist die Anwendung je nach Problem möglicherweise nicht in der Lage, erneut eine Verbindung herzustellen.<br /><br /> Fehlermeldungen in diesem Bereich können sich auf alle Vorgänge auswirken, die auf Daten in der gleichen Datenbank zugreifen, und weisen möglicherweise darauf hin, dass eine Datenbank oder ein Objekt beschädigt ist. Fehlermeldungen mit den Schweregraden 19 bis 24 werden im Fehlerprotokoll aufgezeichnet.|  
|20|Gibt an, dass bei einer Anweisung ein Problem aufgetreten ist. Da sich das Problem nur auf den aktuellen Task auswirkt, ist es unwahrscheinlich, dass die Datenbank selbst beschädigt wurde.|  
|21|Gibt an, dass ein Problem aufgetreten ist, das sich auf alle Tasks in der aktuellen Datenbank auswirkt. Es ist jedoch unwahrscheinlich, dass die Datenbank selbst beschädigt wurde.|  
|22|Zeigt an, dass die Tabelle oder der Index, die bzw. der in der Meldung angegeben ist, durch ein Software- oder Hardwareproblem beschädigt wurde.<br /><br /> Fehler mit dem Schweregrad 22 treten selten auf. Führen Sie DBCC CHECKDB aus, wenn ein solcher Fehler auftritt. So stellen Sie fest, ob weitere Objekte in der Datenbank beschädigt sind. Möglicherweise betrifft das Problem nur den Puffercache und nicht der Datenträger selbst. In diesem Fall behebt ein Neustart der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] das Problem. Sie müssen erneut eine Verbindung mit der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]herstellen, um Ihre Arbeit fortzusetzen. Beheben Sie das Problem andernfalls mit DBCC. In einigen Fällen müssen Sie möglicherweise die Datenbank wiederherstellen.<br /><br /> Sollte das Problem durch einen Neustart der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] nicht behoben werden, liegt ein Problem mit dem Datenträger vor. Manchmal kann das Problem durch Löschen des in der Fehlermeldung angegebenen Objekts behoben werden. Wenn die Meldung z. B. besagt, dass die Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] eine Zeile mit der Länge 0 in einem nicht gruppierten Index gefunden hat, löschen Sie den Index, und erstellen Sie ihn neu.|  
|23|Zeigt an, dass die Integrität der gesamten Datenbank aufgrund einer Beschädigung durch ein Hardware- oder Softwareproblem zweifelhaft ist.<br /><br /> Fehler mit dem Schweregrad 23 treten selten auf. Wenn ein solcher Fehler auftritt, führen Sie DBCC CHECKDB aus, um das Ausmaß des Schadens festzustellen. Möglicherweise betrifft das Problem nur den Cache und nicht der Datenträger selbst. In diesem Fall behebt ein Neustart der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)] das Problem. Sie müssen erneut eine Verbindung mit der Instanz von [!INCLUDE[ssDE](../../includes/ssde-md.md)]herstellen, um Ihre Arbeit fortzusetzen. Beheben Sie das Problem andernfalls mit DBCC. In einigen Fällen müssen Sie möglicherweise die Datenbank wiederherstellen.|  
|24|Verweist auf einen Medienfehler. Der Systemadministrator muss möglicherweise die Datenbank wiederherstellen. Außerdem müssen Sie möglicherweise den Hardwarehersteller anrufen.|  
  
## <a name="user-defined-error-message-severity"></a>Schweregrad von benutzerdefinierten Fehlermeldungen  
 Mithilfe von**sp_addmessage** können benutzerdefinierte Fehlermeldungen mit Schweregraden zwischen 1 und 25 der **sys.messages** -Katalogsicht hinzugefügt werden. Diese benutzerdefinierten Fehlermeldungen können von RAISERROR verwendet werden. Weitere Informationen finden Sie unter [sp_addmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
  
 Mithilfe von RAISERROR können benutzerdefinierte Fehlermeldungen mit Schweregraden zwischen 1 und 25 generiert werden. RAISERROR kann auf eine benutzerdefinierte, in der **sys.messages** -Katalogsicht gespeicherte Fehlermeldung verweisen oder eine Meldung dynamisch erstellen. Wird beim Generieren eines Fehlers die benutzerdefinierte Fehlermeldung in **sys.messages** verwendet, überschreibt der von RAISERROR angegebene Schweregrad den in **sys.messages** angegebenen Schweregrad. Weitere Informationen finden Sie unter [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
## <a name="error-severity-and-trycatch"></a>Schweregrad von Fehlern und TRY…CATCH  
 Ein TRY…CATCH-Konstrukt findet alle Ausführungsfehler, deren Schweregrad größer als 10 ist und die die Datenbankverbindung nicht beenden.  
  
 Fehler mit einem Schweregrad zwischen 0 und 10 sind Informationsmeldungen und bewirken nicht, dass die Ausführung aus dem CATCH-Block eines TRY…CATCH-Konstrukts springt.  
  
 Fehler, die die Datenbankverbindung beenden, normalerweise mit einem Schweregrad zwischen 20 und 25, werden nicht von dem CATCH-Block behandelt, da die Ausführung beim Beenden der Verbindung abgebrochen wird.  
  
 Weitere Informationen finden Sie unter [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)aufgetreten ist.  
  
## <a name="retrieving-error-severity"></a>Abrufen des Schweregrads eines Fehlers  
 Mithilfe der Systemfunktion ERROR_SEVERITY kann der Schweregrad des Fehlers abgerufen werden, der bewirkt hat, dass der CATCH-Block eines TRY…CATCH-Konstrukts ausgeführt wurde. ERROR_SEVERITY gibt NULL zurück, wenn die Funktion außerhalb des Bereichs eines CATCH-Blocks aufgerufen wird. Weitere Informationen finden Sie unter [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu Datenbankmodulfehlern](../../relational-databases/errors-events/understanding-database-engine-errors.md)   
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)  
  
  
