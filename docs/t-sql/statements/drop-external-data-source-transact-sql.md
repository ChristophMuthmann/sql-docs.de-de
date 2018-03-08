---
title: "Löschen der EXTERNEN Datenquelle (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 3f65a2f5-a6c6-4be5-8ca4-6057078fe10e
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b479c5fd28b97eb6fae75d9490a52c9e56c3fa7f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-external-data-source-transact-sql"></a>Löschen der EXTERNEN Datenquelle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Entfernt eine externe Datenquelle PolyBase an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Drop an external data source  
DROP EXTERNAL DATA SOURCE external_data_source_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *external_data_source_name*  
 Der Name der externen Datenquelle zu löschen.  
  
## <a name="metadata"></a>Metadaten  
 Verwenden Sie zum Anzeigen einer Liste von externen Daten Quellen sys.external_data_sources-Systemsicht.  
  
```  
SELECT * FROM sys.external_data_sources;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert ALTER jede externe Datenquelle.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das Quellobjekt für den externen Daten.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Löschen einer externen Datenquelle werden die externen Daten nicht entfernt werden.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-basic-syntax"></a>A. Verwenden die grundlegende syntax  
  
```  
DROP EXTERNAL DATA SOURCE mydatasource;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  

