---
title: ntext, text und image (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 7/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2e60348cdf1407c653dcadf70a626c5fba8ecaac
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="ntext-text-and-image-transact-sql"></a>ntext, text und image (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Datentypen fester und variabler Länge zum Speichern von großen Nicht-Unicode- und Unicode-Zeichendaten sowie Binärdaten. Unicode-Daten verwenden den UNICODE UCS-2-Zeichensatz.
  
>**WICHTIG!**  Die Datentypen **ntext**, **text** und **image** werden in einer zukünftigen Version von SQL Server entfernt. Vermeiden Sie die Verwendung dieser Datentypen bei neuen Entwicklungen, und planen Sie die Änderung von Anwendungen, in denen sie aktuell verwendet werden. Verwenden Sie stattdessen [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)und [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) .  
  
  
## <a name="arguments"></a>Argumente  
**ntext**  
Unicode-Daten variabler Länge mit einer maximalen Zeichenfolgenlänge von 2^30 - 1 (1.073.741.823) Bytes. Die Speichergröße in Bytes ist doppelt so groß wie die eingegebene Zeichenfolgenlänge. Das ISO-Synonym für **ntext** lautet **national text**.
  
**text**  
Nicht-Unicode-Daten variabler Länge in der Codepage des Servers und mit einer maximalen Zeichenfolgenlänge von 2^31 - 1 (2.147.483.647). Auch wenn die Servercodepage Doppelbytezeichen verwendet, ist der Speicherplatz 2.147.483.647 Bytes groß. Abhängig von der Zeichenfolge kann die Speichergröße unter 2.147.483.647 Bytes liegen.
  
**image**  
Binärdaten variabler Länge von 0 bis 2^31-1 (2.147.483.647) Byte.
  
## <a name="remarks"></a>Remarks  
Die folgenden Funktionen und Anweisungen können mit **ntext**, **text** oder **image**-Daten verwendet werden.
  
|Funktionen|Anweisungen|  
|---|---|
|[DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)|[READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)|[SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)|[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT (Transact-SQL)](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  
  
## <a name="see-also"></a>Siehe auch
[CAST und CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Datentypkonvertierung &#40;Datenbank-Engine&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[Sortierung und Unicode-Unterstützung](../../relational-databases/collations/collation-and-unicode-support.md)

