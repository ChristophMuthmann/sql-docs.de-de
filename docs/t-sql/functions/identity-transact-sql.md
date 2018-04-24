---
title: '@@IDENTITY (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs:
- TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1778fe53a4fc70a7e3edb70e25cfd2b473e32e5f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40;IDENTITY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Eine Systemfunktion, die den zuletzt eingefügten Identitätswert zurückgibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Remarks  
 Nachdem eine INSERT- oder eine SELECT INTO-Anweisung bzw. eine Massenkopieranweisung abgeschlossen ist, enthält @@IDENTITY den letzten von der Anweisung generierten Identitätswert. Wenn sich die Anweisung nicht auf Tabellen mit Identitätsspalten ausgewirkt hat, gibt @@IDENTITY den Wert NULL zurück. Wenn mehrere Zeilen eingefügt und dabei mehrere Identitätswerte generiert werden, gibt @@IDENTITY den zuletzt generierten Identitätswert zurück. Wenn die Anweisung mindestens einen Trigger auslöst, der Einfügevorgänge zum Generieren von Identitätswerten durchführt, wird durch das Aufrufen von @@IDENTITY sofort nach der Anweisung der letzte von den Triggern generierte Identitätswert zurückgegeben. Wenn nach einer Einfügeaktion bei einer Tabelle mit einer Identitätsspalte ein Trigger ausgelöst wird und der Trigger das Einfügen in einer anderen Tabelle bewirkt, in der keine Identitätsspalte vorhanden ist, dann gibt @@IDENTITY den Identitätswert der Einfügung zurück. Der @@IDENTITY-Wert kehrt nicht zu einer vorherigen Einstellung zurück, wenn die INSERT- oder SELECT INTO-Anweisung oder der Massenkopiervorgang fehlschlägt bzw. für die Transaktion ein Rollback ausgeführt wird.  
  
 Fehlgeschlagene Anweisungen oder Transaktionen können die aktuelle Identität für eine Tabelle ändern und zu Lücken in den Identitätsspaltenwerten führen. Für den Identitätswert erfolgt kein Rollback, auch wenn für die Transaktion, die versuchte, den Wert in die Tabelle einzufügen, kein Commit ausgeführt wird. Wenn beispielsweise eine INSERT-Anweisung aufgrund einer IGNORE_DUP_KEY-Verletzung fehlschlägt, wird der aktuelle Identitätswert für die Tabelle trotzdem inkrementiert.  
  
 Bei @@IDENTITY, SCOPE_IDENTITY und IDENT_CURRENT handelt es sich um ähnliche Funktionen. Sie geben den letzten Wert zurück, der in die IDENTITY-Spalte einer Tabelle eingefügt wurde.  
  
 @@IDENTITY und SCOPE_IDENTITY geben den letzten Identitätswert zurück, der in einer Tabelle in der aktuellen Sitzung generiert wurde. Allerdings gibt SCOPE_IDENTITY den Wert nur im aktuellen Gültigkeitsbereich zurück. @@IDENTITY ist nicht auf einen bestimmten Gültigkeitsbereich begrenzt.  
  
 IDENT_CURRENT ist nicht durch einen Gültigkeitsbereich oder eine Sitzung begrenzt, sondern auf eine angegebene Tabelle. IDENT_CURRENT gibt den für eine bestimmte Tabelle in einer Sitzung oder einem Gültigkeitsbereich generierten Identitätswert zurück. Weitere Informationen finden Sie unter [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md).  
  
 Der Gültigkeitsbereich der @@IDENTITY-Funktion erstreckt sich auf die aktuelle Sitzung auf dem lokalen Server, auf dem sie ausgeführt wird. Diese Funktion kann nicht für Remote- oder Verbindungsserver angewendet werden. Um einen Identitätswert auf einem anderen Server zu erhalten, müssen Sie eine gespeicherte Prozedur auf einem Remote- oder Verbindungsserver ausführen. Diese gespeicherte Prozedur (die im Kontext des Remote- bzw. Verbindungsservers ausgeführt wird) muss die Identitätswertinformationen sammeln und an die aufrufende Verbindung auf dem lokalen Server zurückgeben.  
  
 Die Replikation hat möglicherweise Auswirkungen auf den @@IDENTITY-Wert, da er in den Replikationstriggern und gespeicherten Prozeduren verwendet wird. @@IDENTITY stellt keinen zuverlässigen Indikator der zuletzt vom Benutzer erstellten Identität dar, wenn die Spalte Bestandteil eines Replikationsartikels ist. Sie können die Syntax der SCOPE_IDENTITY()-Funktion statt @@IDENTITY verwenden. Weitere Informationen finden Sie unter [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md).  
  
> [!NOTE]  
>  Die aufrufende gespeicherte Prozedur oder die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung muss neu geschrieben werden, um die `SCOPE_IDENTITY()`-Funktion zu verwenden, die die neueste Identität zurückgibt, die im Bereich dieser Benutzeranweisung verwendet wird, und nicht die Identität im Bereich des geschachtelten Triggers, der von der Replikation verwendet wird.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel fügt eine Zeile in eine Tabelle mit einer Identitätsspalte (`LocationID`) ein und zeigt mithilfe von `@@IDENTITY` den in der neuen Zeile verwendeten Identitätswert an.  
  
```  
USE AdventureWorks2012;  
GO  
--Display the value of LocationID in the last row in the table.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
INSERT INTO Production.Location (Name, CostRate, Availability, ModifiedDate)  
VALUES ('Damaged Goods', 5, 2.5, GETDATE());  
GO  
SELECT @@IDENTITY AS 'Identity';  
GO  
--Display the value of LocationID of the newly inserted row.  
SELECT MAX(LocationID) FROM Production.Location;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
