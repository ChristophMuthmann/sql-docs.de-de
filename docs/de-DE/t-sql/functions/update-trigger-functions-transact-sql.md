---
title: UPDATE() (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
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
- UPDATE()_TSQL
- UPDATE()
dev_langs:
- TSQL
helpviewer_keywords:
- INSERT statement [SQL Server], UPDATE function
- testing column updates
- UPDATE function
- UPDATE() function
- detecting changes
- columns [SQL Server], change detection
- UPDATE statement [SQL Server], UPDATE function
- verifying column updates
- checking column updates
ms.assetid: 8e3be25b-2e3b-4d1f-a610-dcbbd8d72084
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b91d175788e3f67e8a4e4cc1484e9648072c4cef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="update---trigger-functions-transact-sql"></a>UPDATE: Triggerfunktionen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt einen booleschen Wert zurück, der zeigt, ob der Versuch einer INSERT- oder UPDATE-Aktion an einer angegebenen Tabellenspalte oder Sicht unternommen wurde. UPDATE() wird im Text eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-INSERT- oder UPDATE-Triggers verwendet, um zu testen, ob der Trigger bestimmte Aktionen ausführen sollte.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
UPDATE ( column )   
```  
  
## <a name="arguments"></a>Argumente  
 *column*  
 Der Name der auf eine INSERT- oder UPDATE-Aktion zu testenden Spalte. Da der Tabellenname in der ON-Klausel des Triggers angegeben ist, nehmen Sie den Tabellennamen nicht vor dem Spaltennamen in die Klausel auf. Die Spalte kann einen beliebigen [Datentyp](../../t-sql/data-types/data-types-transact-sql.md) enthalten, der von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt wird. Berechnete Spalten können jedoch in diesem Kontext nicht verwendet werden.  
  
## <a name="return-types"></a>Rückgabetypen  
 Boolean  
  
## <a name="remarks"></a>Remarks  
 UPDATE() gibt TRUE zurück, und zwar unabhängig davon, ob ein INSERT- oder UPDATE-Versuch erfolgreich ist oder nicht.  
  
 Um mehrere Spalten auf eine INSERT- oder UPDATE-Aktion zu testen, geben Sie nach der ersten eine separate UPDATE(*column*)-Klausel an. Mithilfe von COLUMNS_UPDATED können auch mehrere Spalten auf INSERT- oder UPDATE-Aktionen getestet werden. Das hierbei zurückgegebene Bitmuster gibt an, welche Spalten eingefügt oder aktualisiert wurden.  
  
 IF UPDATE gibt den TRUE-Wert in INSERT-Aktionen zurück, da in die Spalten entweder explizite Werte oder implizite Werte (NULL) eingefügt werden.  
  
> [!NOTE]  
>  Die IF UPDATE(*column*)-Klausel funktioniert genauso wie eine IF-, IF…ELSE- oder WHILE-Klausel und kann den BEGIN…END-Block verwenden. Weitere Informationen finden Sie unter [Control-of-Flow Language &#40;Transact-SQL&#41; (Sprachkonstrukte zur Ablaufsteuerung &#40;Transact-SQL&#41;)](~/t-sql/language-elements/control-of-flow.md).  
  
 UPDATE(*column*) kann überall innerhalb des Texts eines [!INCLUDE[tsql](../../includes/tsql-md.md)]-Triggers verwendet werden.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel erstellt einen Trigger, der eine Meldung an den Client ausgibt, wenn jemand versucht, die `StateProvinceID`- oder `PostalCode`-Spalten der `Address`-Tabelle zu aktualisieren.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
