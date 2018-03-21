---
title: '@@SERVICENAME (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 09/18/2017
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
- '@@SERVICENAME_TSQL'
- '@@SERVICENAME'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVICENAME function'
- names [SQL Server], registry keys
- registry keys [SQL Server]
ms.assetid: 5b0b35be-50ae-411d-a607-bf7464b73624
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee3d62f8e55469b6ca84fae4e11daaace604c7e7
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="x40x40servicename-transact-sql"></a>&#x40;&#x40;SERVICENAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Gibt den Namen des Registrierungsschlüssels zurück, unter dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird. @@SERVICENAME gibt „MSSQLSERVER“ zurück, wenn die aktuelle Instanz die Standardinstanz ist. Diese Funktion gibt den Namen der Instanz zurück, wenn die aktuelle Instanz eine benannte Instanz ist.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@SERVICENAME  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird als Dienst mit dem Namen MSSQLServer ausgeführt.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Verwendung von `@@SERVICENAME` gezeigt.  
  
```  
SELECT @@SERVICENAME AS 'Service Name';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Service Name                    
------------------------------  
MSSQLSERVER                     
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Verwalten der Datenbankmoduldienste](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
