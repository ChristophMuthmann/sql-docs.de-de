---
title: SUSER_ID (Transact-SQL) | Microsoft-Dokumentation
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4b00485c741857f1e3438c3e50995886900fe29
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="suserid-transact-sql"></a>SUSER_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die Anmelde-ID des Benutzers zurück.  
  
> [!NOTE]  
>  Ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] gibt SUSER_ID den Wert zurück, der als **principal_id** in der **sys.server_principals**-Katalogsicht aufgeführt ist.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SUSER_ID ( [ 'login' ] )   
```  
  
## <a name="arguments"></a>Argumente  
 **'** *login* **'**  
 Der Anmeldename des Benutzers. *login* ist vom Typ **nchar**. Wenn *login* als **char** angegeben ist, wird *login* implizit in **nchar** konvertiert. *login* kann jeder beliebigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anmeldung oder Windows-Gruppen oder jedem Windows-Benutzer entsprechen, die bzw. der die Berechtigung zum Herstellen einer Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hat. Falls *login* nicht angegeben wird, wird die Anmelde-ID für den aktuellen Benutzer zurückgegeben. Wenn der Parameter das Wort NULL enthalten ist, wird NULL zurückgegeben.  
  
## <a name="return-types"></a>Rückgabetypen  
 **int**  
  
## <a name="remarks"></a>Remarks  
 SUSER_ID gibt nur für die Anmeldungen eine ID zurück, die explizit in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bereitgestellt wurden. Diese ID wird in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zur Nachverfolgung des Besitzes und der Berechtigungen verwendet. Diese ID ist nicht gleichbedeutend mit der Sicherheits-ID (SID) der Anmeldung, die von SUSER_SID zurückgegeben wird. Wenn *login* eine SQL Server-Anmeldung ist, ist die SID einem GUID zugeordnet. Wenn *login* eine Windows-Anmeldung oder eine Windows-Gruppe ist, ist die SID einer Windows-Sicherheits-ID zugeordnet.  
  
 SUSER_SID gibt SUIDs nur für einen Anmeldenamen zurück, für den es einen Eintrag in der **syslogins**-Systemtabelle gibt.  
  
 Systemfunktionen können in der Auswahlliste, in der WHERE-Klausel und überall dort, wo ein Ausdruck zulässig ist, verwendet werden. Auf den Funktionsnamen müssen immer Klammern folgen (auch wenn kein Parameter angegeben wird).  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel gibt die Anmelde-ID für die `sa`-Anmeldung zurück.  
  
```  
SELECT SUSER_ID('sa');  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Systemfunktionen &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  
