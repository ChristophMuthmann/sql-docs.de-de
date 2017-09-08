---
title: Datentypen (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8220765c51455b20a12439c18dcd2fb4bde6bb3d
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---

# <a name="data-types-transact-sql"></a>Datentypen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verfügt jede Spalte, jede lokale Variable, jeder Ausdruck und jeder Parameter einen entsprechenden Datentyp. Ein Datentyp ist ein Attribut, das für das jeweilige Objekt angibt, welchen Typ von Daten ein Objekt aufnehmen kann: Ganzzahlige Daten, Zeichendaten, Währungsdaten, Datums- und Uhrzeitdaten, binäre Zeichenfolgen usw.
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt eine Reihe von Systemdatentypen zur Verfügung, die alle Typen von Daten definieren, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden können. Sie können auch eigene Datentypen in definieren [!INCLUDE[tsql](../../includes/tsql-md.md)] oder [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Aliasdatentypen basieren auf den vom System bereitgestellten Datentypen. Weitere Informationen zu Aliasdatentypen finden Sie unter [CREATE TYPE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-type-transact-sql.md). Benutzerdefinierte Typen erhalten ihre Merkmale von den Methoden und Operatoren einer Klasse, die Sie mithilfe einer der von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] unterstützten Programmiersprachen erstellen.
  
Wenn zwei Ausdrücke, die unterschiedliche Datentypen, Sortierungen, Genauigkeiten, Dezimalstellen oder Längen haben, durch einen Operator kombiniert werden, wird das Ergebnis durch Folgendes bestimmt:
-   Der Datentyp des Ergebnisses wird bestimmt, indem die Regeln zur Rangfolge der Datentypen auf die Eingabeausdrücke angewendet werden. Weitere Informationen finden Sie unter [Rangfolge der Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
-   Die Sortierung des Ergebnisses wird von den Regeln der Sortierungspriorität festgelegt, wenn der Datentyp des Ergebnisses ist **Char**, **Varchar**, **Text**, **Nchar**, **Nvarchar**, oder **Ntext**. Weitere Informationen finden Sie unter [Rangfolge von Sortierungen &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   Die Genauigkeit, die Dezimalstellen und die Länge des Ergebniswertes hängen von der Genauigkeit, den Dezimalstellen und der Länge der Eingabeausdrücke ab. Weitere Informationen finden Sie unter [Genauigkeit, Dezimalstellen und Länge &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Stellt Datentypsynonyme für ISO-Kompatibilität bereit. Weitere Informationen finden Sie unter [Synonyme für Datentypen &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>Datentypkategorien
Datentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind in den folgenden Kategorien organisiert:
  
|||  
|-|-|  
|Genaue numerische Werte|Unicode-Zeichenfolgen|  
|Ungefähre numerische Ausdrücke|Binärzeichenfolgen|  
|Datum und Uhrzeit|Andere Datentypen|  
|Zeichenfolgen||  
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind einige Datentypen aufgrund ihrer Speichermerkmale als den folgenden Gruppen zugehörig definiert:
-   Große Datenwerttypen: **varchar(max)**, und **nvarchar(max)**  
-   LOB-Datentypen: **Text**, **Ntext**, **Image**, **varbinary(max)**, und **Xml**  
  
    > [!NOTE]  
    >  Sp_help gibt-1 als Länge für Datentypen mit umfangreichen Werten und **Xml** -Datentypen.  
  
### <a name="exact-numerics"></a>Genaue numerische Werte
  
|||  
|-|-|  
|[bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)|[smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|  
|[money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)||  
  
### <a name="approximate-numerics"></a>Ungefähre numerische Ausdrücke
  
|||  
|-|-|  
|[float](../../t-sql/data-types/float-and-real-transact-sql.md)|[real](../../t-sql/data-types/float-and-real-transact-sql.md)|  
  
### <a name="date-and-time"></a>Datum und Uhrzeit
  
|||  
|-|-|  
|[Datum](../../t-sql/data-types/date-transact-sql.md)|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|[Uhrzeit](../../t-sql/data-types/time-transact-sql.md)|  
  
### <a name="character-strings"></a>Zeichenfolgen
  
|||  
|-|-|  
|[char](../../t-sql/data-types/char-and-varchar-transact-sql.md)|[varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)|  
|[text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="unicode-character-strings"></a>Unicode-Zeichenfolgen
  
|||  
|-|-|  
|[nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|[nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)|  
|[ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="binary-strings"></a>Binärzeichenfolgen
  
|||  
|-|-|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|  
|[image](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)||  
  
### <a name="other-data-types"></a>Andere Datentypen
  
|||  
|-|-|  
|[Cursor](../../t-sql/data-types/cursor-transact-sql.md)|[timestamp](../../t-sql/data-types/rowversion-transact-sql.md)|  
|[hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)|[uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)|  
|[sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)|[xml](../../t-sql/xml/xml-transact-sql.md)|  
|[table](../../t-sql/data-types/table-transact-sql.md)|[Räumliche Typen](http://msdn.microsoft.com/library/d1715574-34b1-4ce5-a29f-25e35027a54c)|  
  
## <a name="see-also"></a>Siehe auch
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[Deklarieren Sie @local_variable &#40; Transact-SQL &#41; ](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
 [EXECUTE &#40; Transact-SQL &#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[Ausdrücke &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funktionen &#40; Transact-SQL &#41;](../../t-sql/functions/functions.md)  
[WIE &#40; Transact-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)  
[Sp_droptype &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[Sp_help &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[Sp_rename &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  

