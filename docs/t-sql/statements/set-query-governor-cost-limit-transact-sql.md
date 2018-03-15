---
title: SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a96642c6a0dd50ccb8717e84a6defec516196d87
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="set-querygovernorcostlimit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Überschreibt den zurzeit konfigurierten Wert für **Kostenbeschränkung der Abfragekontrolle** für die aktuelle Verbindung.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
## <a name="arguments"></a>Argumente  
 *value*  
 Ein numerischer oder ganzzahliger Wert, der angibt, wie lange die Ausführung der Abfrage maximal dauern kann. Werte werden zur nächsten Ganzzahl abgerundet. Negative Werte werden zu 0 gerundet. Die Abfragekontrolle lässt die Ausführung von Abfragen, deren geschätzte Kosten über diesem Wert liegen, nicht zu. Wenn Sie 0 (den Standardwert) für diese Option angeben, wird die Abfragekontrolle deaktiviert. In diesem Fall können alle Abfragen ohne zeitliche Begrenzung ausgeführt werden.  
  
 Die Abfragekosten beziehen sich auf die geschätzte Zeit in Sekunden, die für das Ausführen einer Abfrage bei einer bestimmten Hardwarekonfiguration benötigt wird.  
  
## <a name="remarks"></a>Remarks  
 SET QUERY_GOVERNOR_COST_LIMIT bezieht sich nur auf die aktuelle Verbindung und gilt für die Dauer der aktuellen Verbindung. Verwenden Sie die Serverkonfigurationsoption [Kostenbeschränkung der Abfragekontrolle](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) von **sp_configure**, um das serverweite Kostenlimit der Abfragekontrolle zu ändern. Weitere Informationen zum Konfigurieren dieser Option finden Sie unter [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) und [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 Die Einstellung von SET QUERY_GOVERNOR_COST_LIMIT wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
