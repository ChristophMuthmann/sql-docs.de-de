---
title: Sp_changedbowner (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_changedbowner
- sp_changedbowner_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_changedbowner
ms.assetid: 516ef311-e83b-45c9-b9cd-0e0641774c04
caps.latest.revision: "35"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 11b80fef363bd33f725a34e5cebd7fd8710be3b4
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/27/2017
---
# <a name="spchangedbowner-transact-sql"></a>sp_changedbowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Ändert den Besitzer der aktuellen Datenbank.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Verwendung [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) stattdessen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_changedbowner [ @loginame = ] 'login'  
     [ , [ @map = ] remap_alias_flag ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @loginame=] '*Anmeldung*"  
 Die Anmelde-ID des neuen Besitzers der aktuellen Datenbank. *login* ist vom Datentyp **sysname**und hat keinen Standardwert. *Anmeldung* muss ein bereits vorhandener [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anmeldename oder Windows-Benutzer. *Anmeldung* kann nicht der Besitzer der aktuellen Datenbank werden, wenn er bereits Zugriff auf die Datenbank über ein vorhandenes Benutzersicherheitskonto innerhalb der Datenbank. Um dies zu vermeiden, löschen Sie zunächst den Benutzer innerhalb der aktuellen Datenbank.  
  
 [ @map=] *Remap_alias_flag*  
 Die *Remap_alias_flag* Parameter ist veraltet, da Aliase für die Anmeldung von entfernten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Mithilfe der *Remap_alias_flag* Parameter führt nicht dazu, dass einen Fehler hat jedoch keine Auswirkung.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 Nach der Ausführung von sp_changedbowner ist der neue Besitzer als Benutzer dbo innerhalb der Datenbank bekannt. dbo besitzt die impliziten Berechtigungen, alle Aktivitäten in der Datenbank auszuführen.  
  
 Der Besitzer der Systemdatenbanken master, model oder tempdb kann nicht geändert werden.  
  
 Um eine Liste der gültigen anzuzeigen *Anmeldung* Werte und führen Sie die gespeicherte Prozedur sp_helplogins aus.  
  
 Ausführung von Sp_changedbowner lediglich mit der *Anmeldung* Datenbankbesitz an Parameter *Anmeldung*.  
  
 Sie können den Besitzer jedes sicherungsfähigen Elements mit der ALTER AUTHORIZATION-Anweisung ändern. Weitere Informationen finden Sie unter [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die TAKE OWNERSHIP-Berechtigung für die Datenbank. Wenn der neue Besitzer über einen entsprechenden Benutzer in der Datenbank verfügt, wird die IMPERSONATE-Berechtigung für den Anmeldenamen benötigt. Andernfalls ist die CONTROL SERVER-Berechtigung auf dem Server erforderlich.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Anmeldename `Albert` als Besitzer der aktuellen Datenbank festgelegt.  
  
```  
EXEC sp_changedbowner 'Albert';  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Systemprozeduren &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Sp_dropalias &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [Sp_helpdb &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [Sp_helplogins &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
