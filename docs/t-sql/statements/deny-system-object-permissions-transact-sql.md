---
title: "Verweigern von Berechtigungen für Systemobjekte (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
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
- DENY statement, system objects
- encryption [SQL Server], system objects
- system objects [SQL Server]
- cryptography [SQL Server], system objects
ms.assetid: 4e43f954-0982-470b-a239-08a13c61563a
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 563210a6798b6b3886ab2b62dc2204ff4d77b243
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="deny-system-object-permissions-transact-sql"></a>DENY (Berechtigungen für Systemobjekte) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Verweigert Berechtigungen für Systemobjekte wie z. B. gespeicherte Prozeduren, erweiterte gespeicherte Prozeduren, Funktionen und Sichten.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DENY { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>Argumente  
 [ **Sys.** ]  
 Die **Sys** Qualifizierer ist erforderlich, nur, wenn auf Katalogsichten und dynamische Verwaltungssichten verwiesen wird.  
  
 *system_object*  
 Gibt das Objekt an, für das die Berechtigung verweigert wird.  
  
 *Prinzipal*  
 Gibt den Prinzipal an, für den die Berechtigung aufgehoben wird.  
  
## <a name="remarks"></a>Hinweise  
 Mit dieser Anweisung können Berechtigungen für bestimmte gespeicherte Prozeduren, erweiterte gespeicherte Prozeduren, Tabellenwertfunktionen, Skalarfunktionen, Sichten, Katalogsichten, Kompatibilitätssichten, INFORMATION_SCHEMA-Sichten, dynamische Verwaltungssichten und Systemtabellen verweigert werden, die von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert wurden. Jedes dieser Systemobjekte vorhanden ist, als eindeutiger Datensatz in der Ressourcendatenbank (**Mssqlsystemresource**). Die Ressourcendatenbank ist schreibgeschützt. Ein Link zum Objekt wird verfügbar gemacht, als Datensatz in der **Sys** -Schema jeder Datenbank.  
  
 Die Standardnamensauflösung löst nicht qualifizierte Prozedurnamen für die Ressourcendatenbank auf. Aus diesem Grund die **Sys** Qualifizierer ist nur erforderlich, wenn Katalogsichten und dynamische Verwaltungssichten angegeben werden.  
  
> [!CAUTION]  
>  Durch Verweigern von Berechtigungen für Systemobjekte werden Fehler in abhängigen Anwendungen verursacht. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwendet Katalogsichten und funktioniert möglicherweise nicht wie erwartet, wenn Sie die Standardberechtigungen für Katalogsichten ändern.  
  
 Das Verweigern von Berechtigungen für Trigger und in Spalten von Systemobjekten wird nicht unterstützt.  
  
 Berechtigungen für Systemobjekte werden bei Upgrades von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beibehalten.  
  
 Systemobjekte werden in der [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) -Katalogsicht angezeigt. Die Berechtigungen für Systemobjekte werden in der [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) -Katalogsicht in der **master** -Datenbank angezeigt.  
  
 Die folgende Abfrage gibt Informationen zu Berechtigungen für Systemobjekte zurück:  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CONTROL SERVER-Berechtigung.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die `EXECUTE`-Berechtigung für `xp_cmdshell` für die `public`-Rolle verweigert.  
  
```  
DENY EXECUTE ON sys.xp_cmdshell TO public;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)   
 [database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [Erteilen Sie Berechtigungen für Systemobjekte &#40; Transact-SQL &#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [WIDERRUFEN Sie Berechtigungen für Systemobjekte &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)  
  
  

