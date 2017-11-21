---
title: SESSIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SESSIONPROPERTY
- SESSIONPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, SESSIONPROPERTY function
- SESSIONPROPERTY function
- sessions [SQL Server], SET options settings
ms.assetid: 1f3730b4-1495-4d3a-af43-e57952812df9
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0d2d3eb935bd003d88795d748de2a5fb4a08c9c4
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="sessionproperty-transact-sql"></a>SESSIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt die Einstellungen der SET-Optionen einer Sitzung zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SESSIONPROPERTY (option)  
```  
  
## <a name="arguments"></a>Argumente  
 *Option*  
 Die aktuelle Optionseinstellung für diese Sitzung. *Option* kann eines der folgenden Werte sein.  
  
|Option|Description|  
|------------|-----------------|  
|ANSI_NULLS|Gibt an, ob das ISO-Verhalten von gleich (=) und ungleich (<>) bei NULL-Werten Anwendung findet.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_PADDING|Steuert die Speicherung von Werten in der Spalte, wenn die Werte kürzer als die definierte Spaltengröße sind oder nachfolgende Leerzeichen in Zeichen- und Binärdaten besitzen.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_WARNINGS|Gibt an, ob das ISO-Standardverhalten für das Auslösen von Fehlermeldungen oder Warnungen unter bestimmten Bedingungen verwendet wird, einschließlich der Division durch Null und arithmetischer Überlauffehler.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ARITHABORT|Bestimmt, ob eine Abfrage beendet wird, wenn während der Abfrageausführung ein Überlauffehler oder ein Fehler aufgrund einer Division durch 0 auftritt.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|CONCAT_NULL_YIELDS_ NULL|Steuert die Behandlung von Verkettungsergebnissen als NULL-Werte oder als leere Zeichenfolgen.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|NUMERIC_ROUNDABORT|Gibt an, ob Fehlermeldungen und Warnungen generiert werden, wenn beim Runden in einem Ausdruck Genauigkeitsverluste entstehen.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|QUOTED_IDENTIFIER|Gibt an, ob die ISO-Regeln zum Verwenden von Anführungszeichen zum Begrenzen von Bezeichnern und Literalzeichenfolgen eingehalten werden sollen.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|\<Eine beliebige andere Zeichenfolge >|NULL = Eingabe ist nicht gültig.|  
  
## <a name="return-types"></a>Rückgabetypen  
 **sql_variant**  
  
## <a name="remarks"></a>Hinweise  
 SET-Optionen sind eine Kombination von Optionen auf Serverebene, Datenbankebene und benutzerdefinierten Optionen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Einstellung für die Option `CONCAT_NULL_YIELDS_NULL` zurückgegeben.  
  
```  
SELECT   SESSIONPROPERTY ('CONCAT_NULL_YIELDS_NULL')  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  

