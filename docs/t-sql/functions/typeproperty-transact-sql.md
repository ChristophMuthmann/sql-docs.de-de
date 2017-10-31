---
title: TYPEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TYPEPROPERTY
- TYPEPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], data types
- data types [SQL Server], status information
- TYPEPROPERTY function
ms.assetid: bc311c80-bac5-46ab-a5c8-68b1c6bbf24a
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 8608de51a13d2bc0109b9874b30749b10b65eaea
ms.contentlocale: de-de
ms.lasthandoff: 10/24/2017

---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu einem Datentyp zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>Argumente  
 *type*  
 Ist der Name des Datentyps.  
  
 *Eigenschaft*  
 Der Informationstyp, der für den Datentyp zurückgegeben werden soll. Für*property* sind die folgenden Werte möglich.  
  
|Eigenschaft|Description|Rückgabewert|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|Datentyp lässt NULL-Werte zu.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Datentyp nicht gefunden.|  
|**OwnerId**|Besitzer des Typs.<br /><br /> Hinweis: Der schemabesitzer ist nicht notwendigerweise der Typbesitzer.|Nicht NULL = Die Datenbankbenutzer-ID des Typbesitzers.<br /><br /> NULL = Nicht unterstützter Typ oder ungültige Typ-ID.|  
|**Genauigkeit**|Genauigkeit für diesen Datentyp.|Die Anzahl von Stellen oder Zeichen.<br /><br /> -1 = **Xml** oder großer Werttyp für Daten<br /><br /> NULL = Datentyp nicht gefunden.|  
|**Dezimalstellen**|Dezimalstellen für diesen Datentyp.|Die Anzahl der Dezimalstellen für den Datentyp.<br /><br /> NULL = Datentyp nicht ist **numerischen** oder wurde nicht gefunden.|  
|**UsesAnsiTrim**|Die Einstellung für ANSI-Auffüllung war aktiviert, als der Datentyp erstellt wurde.|1 = True<br /><br /> 0 = False<br /><br /> NULL = Datentyp nicht gefunden oder kein binärer oder Zeichenfolgen-Datentyp.|  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt NULL bei einem Fehler zurück oder wenn ein Aufrufer nicht über Berechtigungen zum Anzeigen des Objekts verfügt.  
  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann ein Benutzer nur die Metadaten sicherungsfähiger Elemente anzeigen, bei denen der Benutzer entweder der Besitzer ist oder für die dem Benutzer eine Berechtigung erteilt wurde. Dies bedeutet, dass Metadaten ausgebende integrierte Funktionen, z. B. TYPEPROPERTY, möglicherweise NULL zurückgeben, wenn dem Benutzer für das Objekt keine Berechtigung erteilt wurde. Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-identifying-the-owner-of-a-data-type"></a>A. Identifizieren des Besitzers eines Datentyps  
 Im folgenden Beispiel wird der Besitzer eines Datentyps zurückgegeben.  
  
```  
SELECT TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId') AS owner_id, name, system_type_id, user_type_id, schema_id  
FROM sys.types;  
```  
  
### <a name="b-returning-the-precision-of-the-tinyint-data-type"></a>B. Zurückgeben der Genauigkeit des tinyint-Datentyps  
 Im folgenden Beispiel wird die Genauigkeit bzw. die Anzahl der Stellen für den `tinyint`-Datentyp zurückgegeben.  
  
```  
SELECT TYPEPROPERTY( 'tinyint', 'PRECISION');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [TYPE_ID &#40; Transact-SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Metadatenfunktionen &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [Sys.Types &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  


