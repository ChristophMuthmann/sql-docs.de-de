---
title: Festlegen von STATISTICS IO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET_STATISTICS_IO_TSQL
- IO
- IO_TSQL
- SET STATISTICS IO
dev_langs:
- TSQL
helpviewer_keywords:
- disk I/O statistics [SQL Server]
- I/O [SQL Server], disk activity information
- disks [SQL Server], statement statistics
- STATISTICS IO option
- statements [SQL Server], statistical information
- SET STATISTICS IO statement
- statistical information [SQL Server], disk activity
ms.assetid: 7033aac9-a944-4156-9ff4-6ef65717a28b
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 99e1dc183844f25002057b7cebd4729ff5f1bbe5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-io-transact-sql"></a>SET STATISTICS IO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen zum Umfang der Datenträgeraktivitäten anzeigt, die durch [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen generiert werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET STATISTICS IO { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Wenn STATISTICS IO auf ON festgelegt ist, werden statistische Informationen angezeigt. Bei OFF werden die Informationen nicht angezeigt.  
  
 Wenn diese Option auf ON festgelegt wird, geben alle nachfolgenden [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen so lange statistische Informationen zurück, bis die Option auf OFF festgelegt wird.  
  
 Die folgende Tabelle enthält eine Auflistung der Ausgabeelemente sowie entsprechende Beschreibungen.  
  
|Ausgabeelement|Bedeutung|  
|-----------------|-------------|  
|**Tabelle**|Der Name der Tabelle.|  
|**Scananzahl**|Die Anzahl von Suchen/Scans, die nach Erreichen der Blattebene in beliebiger Richtung gestartet wurden, um alle Werte zum Erstellen des abschließende Datasets für die Ausgabe abzurufen.<br /><br /> Die Scananzahl beträgt 0, wenn der verwendete Index ein eindeutiger Index oder ein gruppierter Index für eine Primärschlüsselspalte ist und Sie nur einen Wert suchen. Beispiel: `WHERE Primary_Key_Column = <value>`.<br /><br /> Die Scananzahl beträgt 1, wenn Sie anhand eines nicht eindeutigen gruppierten Indexes, der für eine Nicht-Primärschlüsselspalte definiert ist, nach einem Wert suchen. Auf diese Weise wird nach doppelten Werten eines Schlüsselwerts gesucht, der als Suchwert verwendet wird. Beispiel: `WHERE Clustered_Index_Key_Column = <value>`.<br /><br /> Die Scananzahl ist N, wenn N der Anzahl unterschiedlicher Suchen/Scans entspricht, die auf der Blattebene nach links oder rechts gestartet wurden, nachdem ein Schlüsselwert anhand des Indexschlüssels ermittelt wurde.|  
|**logische Lesevorgänge**|Anzahl der aus dem Datencache gelesenen Seiten|  
|**physische Lesevorgänge**|Anzahl der vom Datenträger gelesenen Seiten|  
|**Read-ahead-Lesevorgänge**|Anzahl der Seiten, die für die Abfrage im Cache platziert wurden|  
|**logische LOB-Lesevorgänge**|Anzahl der **Text**, **Ntext**, **Image**, oder großer Werttyp (**varchar(max)**, **nvarchar(max)**, **varbinary(max)**) Seiten aus dem Datencache gelesen.|  
|**physische LOB-Lesevorgänge**|Anzahl der **Text**, **Ntext**, **Image** oder großen Wert Typ Seiten vom Datenträger gelesen.|  
|**LOB-Read-ahead-Lesevorgänge**|Anzahl der **Text**, **Ntext**, **Image** oder großen Wert Geben Sie die Seiten im Cache für die Abfrage platziert wurden.|  
  
 Die Einstellung von SET STATISTICS IO wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
> [!NOTE]  
>  Wenn Transact-SQL-Anweisungen LOB-Spalten abrufen, kann es vorkommen, dass bestimmte LOB-Abrufvorgänge die LOB-Struktur mehrere Male durchlaufen müssen. Dadurch meldet SET STATISTICS IO möglicherweise mehr logische Lesevorgänge als erwartet.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Verwendung von SET STATISTICS IO müssen die Benutzer über die geeigneten Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung verfügen. Die SHOWPLAN-Berechtigung ist nicht erforderlich.  
  
## <a name="examples"></a>Beispiele  
 In diesem Beispiel wird gezeigt, wie viele logische und physische Lesevorgänge [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] während der Verarbeitung der Anweisungen verwendet.  
  
```  
USE AdventureWorks2012;  
GO         
SET STATISTICS IO ON;  
GO  
SELECT *   
FROM Production.ProductCostHistory  
WHERE StandardCost < 500.00;  
GO  
SET STATISTICS IO OFF;  
GO  
```  
  
 Im Folgenden wird das Resultset aufgeführt:  
  
```  
Table 'ProductCostHistory'. Scan count 1, logical reads 5, physical   
reads 0, read-ahead reads 0, lob logical reads 0, lob physical reads 0,   
lob read-ahead reads 0.  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_ALL &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-all-transact-sql.md)   
 [Festlegen der STATISTICS TIME &#40; Transact-SQL &#41;](../../t-sql/statements/set-statistics-time-transact-sql.md)  
  
  

