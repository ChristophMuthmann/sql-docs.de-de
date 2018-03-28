---
title: '@@SERVERNAME (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 40f441998f2f5055bdacb0ac6d796a6d3ad56f68
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt den Namen des lokalen Servers zurück, auf dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausgeführt wird.  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Artikellinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 **nvarchar**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup legt den Servernamen während der Installation auf den Computernamen fest. Verwenden Sie zum Ändern des Namens des Servers **sp_addserver**, und starten Sie dann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu.  
  
 Wenn mehrere Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert sind, gibt @@SERVERNAME die folgenden Informationen zum Namen des lokalen Servers zurück, wenn der Name des lokalen Servers seit der Installation nicht geändert wurde:  
  
|Instanz|Serverinformationen|  
|--------------|------------------------|  
|Standardinstanz|'*servername*'|  
|Benannte Instanz|'*servername*\\*instancename*'|  
|Failoverclusterinstanz – Standardinstanz|'*virtualservername*'|  
|Failoverclusterinstanz – benannte Instanz|'*virtualservername*\\*instancename*'|  
  
 Obwohl die @@SERVERNAME-Funktion und die SERVERNAME-Eigenschaft der SERVERPROPERTY-Funktion möglicherweise Zeichenfolgen mit ähnlichen Formaten zurückgeben, kann die Information abweichen. Die SERVERNAME-Eigenschaft meldet Änderungen des Netzwerknamens des Computers automatisch.  
  
 @@SERVERNAME meldet diese Änderungen hingegen nicht. @@SERVERNAME meldet mithilfe der gespeicherten Prozeduren **sp_addserver** oder **sp_dropserver** Änderungen des Namens des lokalen Servers.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird die Verwendung von `@@SERVERNAME` gezeigt.  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 Hier ist ein Beispielresultset.  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Konfigurationsfunktionen (Transact-SQL)](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
