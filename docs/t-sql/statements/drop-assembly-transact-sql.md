---
title: DROP ASSEMBLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs: TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
caps.latest.revision: "32"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9c6156ff11476e91f13285c1db7d4cc545d5e8e5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Entfernt eine Assembly und alle zugehörigen Dateien aus der aktuellen Datenbank. Assemblys werden erstellt, mit [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md) und mithilfe von geändert [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *IF VORHANDEN IST*  
 **Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] bis [aktuelle Version](http://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 Bedingt löscht die Assembly nur dann, wenn sie bereits vorhanden ist.  
  
 *assembly_name*  
 Der Name der zu löschenden Assembly.  
  
 WITH NO DEPENDENTS  
 Wenn angegeben, löscht nur *Assembly_name* und keines der abhängigen Assemblys, die von der Assembly verwiesen werden. Wenn nicht angegeben ist, löscht DROP ASSEMBLY *Assembly_name* sowie alle abhängigen Assemblys.  
  
## <a name="remarks"></a>Hinweise  
 Durch Löschen einer Assembly werden die Assembly sowie alle zugehörigen Dateien, wie Quellcode und Debugdateien, aus der Datenbank entfernt.  
  
 Wenn WITH NO DEPENDENTS nicht angegeben ist, löscht DROP ASSEMBLY *Assembly_name* sowie alle abhängigen Assemblys. Schlägt der Versuch fehl, alle abhängigen Assemblys zu löschen, gibt DROP ASSEMBLY einen Fehler zurück.  
  
 DROP ASSEMBLY gibt einen Fehler zurück, wenn eine andere Assembly in der Datenbank auf die Assembly verweist oder diese von CLR-basierten Funktionen (Common Language Runtime), Prozeduren, Triggern, benutzerdefinierten Typen oder Aggregaten in der aktuellen Datenbank verwendet wird.  
  
 DROP ASSEMBLY schränkt Code nicht ein, der auf die zurzeit ausgeführte Assembly verweist. Nach der Ausführung von DROP ASSEMBLY wird jedoch bei allen Versuchen, den Assemblycode aufzurufen, ein Fehler erzeugt.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert den Besitz der Assembly oder die CONTROL-Berechtigung für die Assembly.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird davon ausgegangen, dass die Assembly `HelloWorld` bereits in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz erstellt wurde.  
  
```  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Abrufen von Informationen zu Assemblys](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
