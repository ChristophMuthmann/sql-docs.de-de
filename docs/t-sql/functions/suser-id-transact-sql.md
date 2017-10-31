---
title: SUSER_ID (Transact-SQL) | Microsoft Docs
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
- SUSER_ID_TSQL
- SUSER_ID
dev_langs:
- TSQL
helpviewer_keywords:
- users [SQL Server], IDs
- logins [SQL Server], IDs
- SUSER_ID function
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- user IDs [SQL Server]
ms.assetid: 348911ab-b0b6-4867-aee7-e6f42e053a4a
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7e098c614f4e70cabf718ee4413920e61eb634c1
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anmelde-ID des Benutzers zurück.  
  
> [!NOTE]  
>  Beginnend mit [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], SUSER_ID gibt den Wert, der als **Principal_id** in der **Sys. server_principals** -Katalogsicht angezeigt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argumente  
 **"** *Anmeldung* **"**  
 Der Anmeldename des Benutzers. *Anmeldung* ist **Nchar**. Wenn *Anmeldung* angegeben ist, als **Char**, *Anmeldung* wird implizit in konvertiert **Nchar**. *Anmeldung* kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldung oder Windows-Benutzer oder Gruppe mit der Berechtigung zur Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Wenn *Anmeldung* ist nicht angegeben wird, wird die Anmelde-ID für den aktuellen Benutzer zurückgegeben. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Hinweise  
 SUSER_ID gibt nur für die Anmeldungen eine ID zurück, die explizit in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wurden. Diese ID wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Nachverfolgung des Besitzes und der Berechtigungen verwendet. Diese ID ist nicht gleichbedeutend mit der Sicherheits-ID (SID) der Anmeldung, die von SUSER_SID zurückgegeben wird. Wenn *Anmeldung* ist eine SQL Server-Anmeldung, die SID einem GUID zugeordnet. Wenn *Anmeldung* ist ein Windows-Anmeldename oder Windows-Gruppe, die SID einer Windows-Sicherheits-ID zugeordnet.  
  
 SUSER_SID gibt eine SUID nur für eine Anmeldung, das einen Eintrag in der **Syslogins** -Systemtabelle.  
  
 Systemfunktionen können in der Auswahlliste, in der WHERE-Klausel und überall dort, wo ein Ausdruck zulässig ist, verwendet werden. Auf den Funktionsnamen müssen immer Klammern folgen (auch wenn kein Parameter angegeben wird).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die Anmelde-ID für die `sa`-Anmeldung zurück.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40; Transact-SQL &#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Systemfunktionen &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

