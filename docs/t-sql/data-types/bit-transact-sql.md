---
title: Bit (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- bit_TSQL
- bit
dev_langs:
- TSQL
helpviewer_keywords:
- bit data type
ms.assetid: 40adfd08-a31c-49cb-a172-386bcaa6edee
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3817549e5846c68b422fb941907860896b956d9a
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="bit-transact-sql"></a>bit (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Ein ganzzahliger Datentyp, der den Wert 1, 0 oder NULL annehmen kann.  
  
## <a name="remarks"></a>Hinweise  
Die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] optimiert das Speichern von **Bit** Spalten. Wenn in einer Tabelle 8 oder weniger **bit** -Spalten vorhanden sind, werden die Spalten als 1 Byte gespeichert. Sind zwischen 9 und 16 **bit** -Spalten vorhanden, werden diese als 2 Byte gespeichert usw.
  
Die Zeichenfolgenwerte TRUE und FALSE können in **bit** -Werte konvertiert werden: TRUE wird in 1 konvertiert, und FALSE wird in 0 konvertiert.
  
Die Konvertierung in den bit-Datentyp ergibt für alle Werte ungleich 0 den Wert 1.
  
## <a name="see-also"></a>Siehe auch
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

