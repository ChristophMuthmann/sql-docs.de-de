---
title: '@@IDENTITY (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@IDENTITY_TSQL'
- '@@IDENTITY'
dev_langs: TSQL
helpviewer_keywords:
- last-inserted identity values
- identity values [SQL Server], last-inserted
- '@@IDENTITY function'
ms.assetid: 912e4485-683c-41c2-97b3-8831c0289ee4
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5ab8dcb49d8f799699df4f9af4c30b72a4a550be
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40identity-transact-sql"></a>&#x40;&#x40; Identität (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Eine Systemfunktion, die den zuletzt eingefügten Identitätswert zurückgibt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@IDENTITY  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **numeric(38,0)**  
  
## <a name="remarks"></a>Hinweise  
 Nach einer INSERT, SELECT INTO- oder Bulk Copy-Anweisung abgeschlossen ist, @@IDENTITY enthält den letzten Identitätswert, der von der Anweisung generiert wird. Wenn die Anweisung kein Tabellen mit Identitätsspalten ausgewirkt hat@IDENTITY gibt NULL zurück. Wenn mehrere Zeilen eingefügt werden, generieren Sie mehrere Identitätswerte@IDENTITY gibt den letzten generierten Identitätswert zurück. Wenn die Anweisung einen oder mehrere Trigger, die Einfügevorgänge, die Identity-Werte zu generieren auslöst, @ Aufrufen@IDENTITY sofort, nachdem die Anweisung gibt den letzten, durch die Trigger generierten Identitätswert zurück. Wenn ein Trigger ausgelöst wird, nach einer Einfügeaktion bei einer Tabelle mit einer Identity-Spalte und der Trigger in eine andere Tabelle, die eine Identity-Spalte keinen fügt @@IDENTITY gibt den Identitätswert der Einfügung zurück. Der @@IDENTITY Wert kehrt nicht zu einer vorherigen Einstellung, wenn die INSERT- oder SELECT INTO-Anweisung Massenkopiervorgang fehlschlägt oder die Transaktion ein Rollback ausgeführt wird.  
  
 Fehlgeschlagene Anweisungen oder Transaktionen können die aktuelle Identität für eine Tabelle ändern und zu Lücken in den Identitätsspaltenwerten führen. Für den Identitätswert erfolgt kein Rollback, auch wenn für die Transaktion, die versuchte, den Wert in die Tabelle einzufügen, kein Commit ausgeführt wird. Wenn beispielsweise eine INSERT-Anweisung aufgrund einer IGNORE_DUP_KEY-Verletzung fehlschlägt, wird der aktuelle Identitätswert für die Tabelle trotzdem inkrementiert.  
  
 @@IDENTITY, SCOPE_IDENTITY und IDENT_CURRENT sind ähnliche Funktionen auf, da sie alle zurückkehren, dass den letzten Wert in die Identitätsspalte einer Tabelle eingefügt.  
  
 @@IDENTITY und SCOPE_IDENTITY geben den letzten Identitätswert, der in einer beliebigen Tabelle in der aktuellen Sitzung generiert zurück. Allerdings gibt SCOPE_IDENTITY den Wert nur im aktuellen Gültigkeitsbereich zurück; @@IDENTITY ist nicht auf einen bestimmten Gültigkeitsbereich begrenzt.  
  
 IDENT_CURRENT ist nicht durch einen Gültigkeitsbereich oder eine Sitzung begrenzt, sondern auf eine angegebene Tabelle. IDENT_CURRENT gibt den für eine bestimmte Tabelle in einer Sitzung oder einem Gültigkeitsbereich generierten Identitätswert zurück. Weitere Informationen finden Sie unter [IDENT_CURRENT &#40; Transact-SQL &#41; ](../../t-sql/functions/ident-current-transact-sql.md).  
  
 Der Geltungsbereich der @@IDENTITY Funktion ist die aktuelle Sitzung auf dem lokalen Server, auf dem er ausgeführt wird. Diese Funktion kann nicht für Remote- oder Verbindungsserver angewendet werden. Um einen Identitätswert auf einem anderen Server zu erhalten, müssen Sie eine gespeicherte Prozedur auf einem Remote- oder Verbindungsserver ausführen. Diese gespeicherte Prozedur (die im Kontext des Remote- bzw. Verbindungsservers ausgeführt wird) muss die Identitätswertinformationen sammeln und an die aufrufende Verbindung auf dem lokalen Server zurückgeben.  
  
 Kann die Replikation Auswirkungen auf die @@IDENTITY Wert, da sie in den replikationstriggern und gespeicherten Prozeduren verwendet wird. @@IDENTITY ist nicht zuverlässiger Indikator der letzte Benutzer erstellten Identität dar, wenn die Spalte Teil eines replikationsartikels ist. Sie können die Syntax der SCOPE_IDENTITY()-Funktion statt @@IDENTITY. Weitere Informationen finden Sie unter [SCOPE_IDENTITY &#40; Transact-SQL &#41;](../../t-sql/functions/scope-identity-transact-sql.md)  
  
> [!NOTE]  
>  Die aufrufende gespeicherte Prozedur oder [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung muss umgeschrieben werden, um mithilfe der `SCOPE_IDENTITY()` -Funktion, die die neueste Identität, die innerhalb des Bereichs dieser benutzeranweisung verwendet und nicht die Identität innerhalb des Bereichs des geschachtelten Triggers verwendeten zurückgibt die Replikation.  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  
