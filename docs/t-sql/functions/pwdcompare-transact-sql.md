---
title: PWDCOMPARE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6aadde33d6d1ee1404170197c32ab77ade2dbfad
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt Hashing für ein Kennwort aus und vergleicht den Hash mit dem Hash eines vorhandenen Kennworts. PWDCOMPARE kann verwendet werden, um nach leeren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldekennwörtern oder allgemeinen unsicheren Kennwörtern zu suchen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Clear_text_password* **"**  
 Das unverschlüsselte Kennwort. *Clear_text_password* ist **Sysname** (**vom Datentyp nvarchar(128)**).  
  
 *password_hash*  
 Der Verschlüsselungshash eines Kennworts. *Password_hash* ist **varbinary(128)**.  
  
 *Version*  
 Veralteter Parameter, der auf 1 festgelegt werden kann *Password_hash* stellt einen Wert von einer Anmeldung vor [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] , migriert [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] oder höher, aber nie in konvertiert die [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] System. *Version* ist **Int**.  
  
> [!CAUTION]  
>  Dieser Parameter wird für Abwärtskompatibilität bereitgestellt, jedoch wird ignoriert, da Kennworthash-Blobs nun eigene versionsbeschreibungen enthalten. [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
 Gibt 1 zurück, wenn der Hash der *Clear_text_password* entspricht der *Password_hash* Parameter, und 0, wenn dies nicht der Fall.  
  
## <a name="remarks"></a>Hinweise  
 Die PWDCOMPARE-Funktion stellt keine Bedrohung der Sicherheit von Kennworthashs dar, da der gleiche Test ausgeführt werden kann, indem sich ein Benutzer mit dem als erstem Parameter bereitgestellten Kennwort anmeldet.  
  
 **PWDCOMPARE** kann nicht mit den Kennwörtern der Benutzer eigenständiger Datenbanken verwendet werden. Es gibt keine Entsprechung für eigenständige Datenbanken.  
  
## <a name="permissions"></a>Berechtigungen  
 PWDENCRYPT steht für die Öffentlichkeit zur Verfügung.  
  
 Die CONTROL SERVER-Berechtigung ist erforderlich, um die Spalte password_hash von sys.sql_logins zu untersuchen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-identifying-logins-that-have-no-passwords"></a>A. Identifizieren von Anmeldungen, die keine Kennwörter aufweisen  
 Im folgenden Beispiel werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldungen identifiziert, die keine Kennwörter aufweisen.  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('', password_hash) = 1 ;  
```  
  
### <a name="b-searching-for-common-passwords"></a>B. Suchen nach allgemeinen Kennwörtern  
 Um nach allgemeinen Kennwörtern zu suchen, geben Sie das Kennwort als ersten Parameter an. Führen Sie z. B. die folgende Anweisung aus, um nach einem mit `password` angegebenen Kennwort zu suchen.  
  
```  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('password', password_hash) = 1 ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [PWDENCRYPT &#40; Transact-SQL &#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [Sicherheitsfunktionen &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

