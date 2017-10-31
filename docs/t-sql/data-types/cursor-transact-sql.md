---
title: Cursor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b0b96a3bc147f51102fa10f2dff96b7f1761759
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-transact-sql"></a>cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Ein Datentyp für Variablen oder für OUTPUT-Parameter von gespeicherten Prozeduren, die einen Verweis auf einen Cursor enthalten.
  
## <a name="remarks"></a>Hinweise  
Folgende Vorgänge können auf Variablen und Parameter vom Datentyp **cursor** verweisen:
-   Die DECLARE  *@local_variable*  und festgelegte  *@local_variable*  Anweisungen.  
-   Die Cursoranweisungen OPEN, FETCH, CLOSE und DEALLOCATE.  
-   Ausgabeparameter der gespeicherten Prozedur.  
-   Die CURSOR_STATUS-Funktion.  
-   Die gespeicherten Systemprozeduren **sp_cursor_list**, **sp_describe_cursor**, **sp_describe_cursor_tables**und **sp_describe_cursor_columns** .  
  
Die **cursor_name** -Ausgabespalte von **sp_cursor_list** und **sp_describe_cursor** gibt den Namen der Cursorvariablen zurück.
  
Alle Variablen, die mit dem **cursor** -Datentyp erstellt wurden, lassen NULL zu.
  
Der **cursor** -Datentyp kann nicht für eine Spalte in einer CREATE TABLE-Anweisung verwendet werden.
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Deklarieren Sie die CURSORPOSITION &#40; Transact-SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

