---
title: DROP-Standard (Transact-SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_DEFAULT_TSQL
- DROP DEFAULT
dev_langs:
- TSQL
helpviewer_keywords:
- DROP DEFAULT statement
- defaults [SQL Server], removing
ms.assetid: d2d3af25-8877-46ba-95d9-1844961d97ee
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cb7de5514d74ed4650d44bed145c32e9bea2c845
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="drop-default-transact-sql"></a>DROP DEFAULT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt einen oder mehrere benutzerdefinierte Standardwerte aus der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  DROP DEFAULT werden in der nächsten Version von entfernt [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verwenden Sie DROP DEFAULT nicht bei neuen Entwicklungsarbeiten, und planen Sie die Änderung von Anwendungen, die DROP DEFAULT derzeit verwenden. Verwenden Sie stattdessen Standarddefinitionen, die Sie erstellen können, mit dem DEFAULT-Schlüsselwort der [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) oder [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP DEFAULT [ IF EXISTS ] { [ schema_name . ] default_name } [ ,...n ] [ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis zur [aktuellen Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Bedingt löscht die Standardeinstellung, wenn es bereits vorhanden ist.  
  
 *schema_name*  
 Der Name des Schemas, zu dem der Standardwert gehört.  
  
 *default_name*  
 Der Name eines vorhandenen Standardwerts. Führen Sie zum Anzeigen einer Liste von Standardwerten, die vorhanden sind, **Sp_help**. Standardwerte müssen den Regeln für entsprechen [Bezeichner](../../relational-databases/databases/database-identifiers.md). Das Angeben des Standardschemanamens ist optional.  
  
## <a name="remarks"></a>Hinweise  
 Vor dem Löschen eines Standardwerts, Standardwerts durch Ausführen **Sp_unbindefault** , wenn der Standardwert aktuell an eine Spalte oder einen Aliasdatentyp gebunden ist.  
  
 Nachdem ein Standardwert aus einer Spalte gelöscht wurde, die NULL-Werte zulässt, wird NULL an dessen Stelle eingefügt, wenn Zeilen hinzugefügt und keine Werte explizit angegeben werden. Nachdem ein Standardwert einer Spalte gelöscht wurde, in der keine NULL-Werte zulässig sind, wird eine Fehlermeldung zurückgegeben, wenn Zeilen hinzugefügt und keine Werte explizit angegeben werden. Diese Zeilen werden später als Teil des typischen Verhaltens der INSERT-Anweisung hinzugefügt.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen von DROP DEFAULT muss ein Benutzer mindestens über die ALTER-Berechtigung für das Schema verfügen, zu dem der Standardwert gehört.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-dropping-a-default"></a>A. Löschen eines Standardwerts  
 Wenn ein Standardwert nicht an eine Spalte oder an einen Aliasdatentyp gebunden ist, kann er einfach mithilfe von DROP DEFAULT gelöscht werden. Im folgenden Beispiel wird der vom Benutzer erstellte Standardwert `datedflt` entfernt.  
  
```  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
         WHERE name = 'datedflt'   
            AND type = 'D')  
   DROP DEFAULT datedflt;  
GO  
```  
  
 Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] können Sie die folgende Syntax.  
  
```  
DROP DEFAULT IF EXISTS datedflt;  
GO  
```  
  
### <a name="b-dropping-a-default-that-has-been-bound-to-a-column"></a>B. Löschen eines Standardwerts, der an eine Spalte gebunden war  
 Im folgenden Beispiel wird die Bindung des Standardwerts an die `EmergencyContactPhone`-Spalte in der `Contact`-Tabelle aufgehoben und dann der Standardwert `phonedflt` gelöscht.  
  
```  
USE AdventureWorks2012;  
GO  
   BEGIN   
      EXEC sp_unbindefault 'Person.Contact.Phone'  
      DROP DEFAULT phonedflt  
   END;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE DEFAULT &#40;Transact-SQL&#41;](../../t-sql/statements/create-default-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [Sp_unbindefault &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-unbindefault-transact-sql.md)  
  
  

