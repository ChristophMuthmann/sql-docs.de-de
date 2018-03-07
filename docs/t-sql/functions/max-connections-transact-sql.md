---
title: '@@MAX_CONNECTIONS (Transact-SQL) | Microsoft Docs'
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
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de4460e3f5dbc0ff2aba83f4c3794528f9100a2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40maxconnections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt die maximale Anzahl gleichzeitiger Benutzerverbindungen an, die für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz zulässig sind. Die zurückgegebene Anzahl ist nicht notwendigerweise die aktuell konfigurierte Anzahl.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **integer**  
  
## <a name="remarks"></a>Hinweise  
 Die tatsächliche Anzahl der zulässigen Benutzerverbindungen hängt außerdem von der installierten Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sowie den Beschränkungen durch Ihre Anwendungen und Hardware ab.  
  
 So konfigurieren Sie neu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für kleinere Anzahl von Verbindungen verwenden **Sp_configure**.  
  
## <a name="examples"></a>Beispiele  
 Das folgende Beispiel zeigt die maximale Anzahl von benutzerverbindungen in einer Instanz von zurückgeben [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Im Beispiel wird vorausgesetzt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht für eine geringere Anzahl von Benutzerverbindungen neu konfiguriert wurde.  
  
```  
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Konfigurationsfunktionen](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Konfigurieren der Serverkonfigurationsoption Benutzerverbindungen](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
