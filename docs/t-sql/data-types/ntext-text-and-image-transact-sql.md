---
title: Ntext, Text und Image (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ntext_TSQL
- ntext
dev_langs:
- TSQL
helpviewer_keywords:
- text data type, about text data type
- text [SQL Server], data types
- ntext data type
- ntext data type, about ntext data type
- image data type, about image data type
ms.assetid: b0d8769c-7598-4f97-8162-ace5f182b5bc
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 76b78b01596b484bc35df1a1e468c5b2bb8ece63
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="ntext-text-and-image-transact-sql"></a>ntext, text und image (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Datentypen fester und variabler Länge zum Speichern von großen Nicht-Unicode- und Unicode-Zeichendaten sowie Binärdaten. Unicode-Daten verwenden den UNICODE UCS-2-Zeichensatz.
  
>**WICHTIG!**  **Ntext**, **Text**, und **Image** Datentypen werden in einer zukünftigen Version von SQL Server entfernt. Vermeiden Sie die Verwendung dieser Datentypen bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden. Verwenden Sie stattdessen [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)und [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) .  
  
  
## <a name="arguments"></a>Argumente  
**ntext**  
Unicode-Daten variabler Länge mit einer maximalen Zeichenfolgenlänge von 2^30 - 1 (1.073.741.823) Bytes. Die Speichergröße in Bytes ist doppelt so groß wie die eingegebene Zeichenfolgenlänge. Das ISO-Synonym für **Ntext** ist **national Text**.
  
**text**  
Nicht-Unicode-Daten variabler Länge in der Codepage des Servers und mit einer maximalen Zeichenfolgenlänge von 2^31 - 1 (2.147.483.647). Auch wenn die Servercodepage Doppelbytezeichen verwendet, ist der Speicherplatz 2.147.483.647 Bytes groß. Abhängig von der Zeichenfolge kann die Speichergröße unter 2.147.483.647 Bytes liegen.
  
**image**  
Binärdaten variabler Länge von 0 bis 2^31-1 (2.147.483.647) Byte.
  
## <a name="remarks"></a>Hinweise  
Die folgenden Funktionen und Anweisungen mit verwendet werden können **Ntext**, **Text**, oder **Image** Daten.
  
|Funktionen|Anweisungen|  
|---|---|
|[DATALENGTH &#40; Transact-SQL &#41;](../../t-sql/functions/datalength-transact-sql.md)|[READTEXT &#40; Transact-SQL &#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40; Transact-SQL &#41;](../../t-sql/functions/patindex-transact-sql.md)|[SET TEXTSIZE &#40; Transact-SQL &#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[TEILZEICHENFOLGE &#40; Transact-SQL &#41;](../../t-sql/functions/substring-transact-sql.md)|[UPDATETEXT &#40; Transact-SQL &#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40; Transact-SQL &#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypkonvertierung &#40; Datenbankmodul &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)


