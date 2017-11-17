---
title: OPENQUERY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 2a3ad57f9cd898d4c059df725b380be28622035e
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt die angegebene Pass-Through-Abfrage auf dem angegebenen Verbindungsserver aus. Bei diesem Server handelt es sich um eine OLE DB-Datenquelle. Auf OPENQUERY kann in der FROM-Klausel einer Abfrage so verwiesen werden, als ob es ein Tabellenname wäre. Auf OPENQUERY kann auch als Zieltabelle einer INSERT-, UPDATE- oder DELETE-Anweisung verwiesen werden. Dies hängt von den Funktionen des OLE DB-Anbieters ab. Obwohl die Abfrage möglicherweise mehrere Resultsets zurückgibt, gibt OPENQUERY nur das erste zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>Argumente  
 *linked_server*  
 Ein Bezeichner, der den Namen des Verbindungsservers darstellt.  
  
 **"** *Abfrage* **"**  
 Ist die Zeichenfolge der Abfrage, die auf dem Verbindungsserver ausgeführt wird. Die maximale Länge der Zeichenfolge beträgt 8 KB.  
  
## <a name="remarks"></a>Hinweise  
 Für die Argumente von OPENQUERY können keine Variablen verwendet werden.  
  
 Mit OPENQUERY können keine erweiterten gespeicherten Prozeduren für einen Verbindungsserver ausgeführt werden. Eine erweiterte gespeicherte Prozedur kann jedoch auf einem Verbindungsserver ausgeführt werden, wenn der vierteilige Name verwendet wird. Beispiel:  
  
```t-sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 Jeder Aufruf von OPENDATASOURCE, OPENQUERY oder OPENROWSET in der FROM-Klausel wird einzeln und unabhängig von anderen Aufrufen dieser Funktionen ausgewertet, die als Ziel des Updates verwendet werden, auch wenn für die beiden Aufrufe identische Argumente angegeben werden. Insbesondere haben Filter- oder Joinbedingungen, die auf das Ergebnis eines dieser Aufrufe angewendet werden, keine Auswirkungen auf die Ergebnisse des jeweils anderen.  
  
## <a name="permissions"></a>Berechtigungen  
 Jeder beliebige Benutzer kann OPENQUERY ausführen. Die Berechtigungen, die für die Verbindung mit dem Remoteserver verwendet werden, werden aus den Einstellungen für den Verbindungsserver abgerufen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. Ausführen einer UPDATE-Pass-Through-Abfrage  
 Im folgenden Beispiel wird eine `UPDATE`-Pass-Through-Abfrage für den in Beispiel A erstellten Verbindungsserver verwendet.  
  
```t-sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. Ausführen einer INSERT-Pass-Through-Abfrage  
 Im folgenden Beispiel wird eine `INSERT`-Pass-Through-Abfrage für den in Beispiel A erstellten Verbindungsserver verwendet.  
  
```t-sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. Ausführen einer DELETE-Pass-Through-Abfrage  
 Im folgenden Beispiel wird eine `DELETE`-Pass-Through-Abfrage verwendet, um die in Beispiel C eingefügte Zeile zu löschen.  
  
```t-sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. Ausführen einer SELECT-Pass-Through-Abfrage  
 Im folgenden Beispiel wird ein Pass-Through- `SELECT` Abfrage, die in Beispiel c eingefügte Zeile auszuwählen.  
  
```t-sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>Siehe auch  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE (Transact-SQL)](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Rowset-Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Sp_serveroption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE (Transact-SQL)](../../t-sql/queries/update-transact-sql.md)   
 [WOBEI &#40; Transact-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

