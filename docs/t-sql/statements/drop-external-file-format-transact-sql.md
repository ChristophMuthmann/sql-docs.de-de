---
title: "Löschen von EXTERNEN DATEIFORMATS (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cf9009b-59f9-4aac-bef1-dcf2cf0708b2
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 9c30ce4ee5d28cb55b824827de6c89f8d673640c
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="drop-external-file-format-transact-sql"></a>Löschen von EXTERNEN DATEIFORMATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Entfernt ein externes Dateiformat PolyBase an.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Drop an external file format  
DROP EXTERNAL FILE FORMAT external_file_format_name  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 *external_file_format_name*  
 Der Name des externen Dateiformats gelöscht.  
  
## <a name="metadata"></a>Metadaten  
 Zum Anzeigen einer Liste der externen Datei Formate verwenden die [sys.external_file_formats &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md) -Systemsicht.  
  
```  
SELECT * FROM sys.external_file_formats;  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert ALTER eines beliebigen EXTERNEN DATEIFORMATS.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Löschen ein externes Dateiformat, werden die externen Daten nicht entfernt.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine gemeinsame Sperre für das Objekt der externen Datei-Format an.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-using-basic-syntax"></a>A. Verwenden die grundlegende syntax  
  
```  
DROP EXTERNAL FILE FORMAT myfileformat;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  


