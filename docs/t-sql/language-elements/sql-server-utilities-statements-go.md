---
title: GO (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- GO
- GO_TSQL
dev_langs: TSQL
helpviewer_keywords:
- batches [SQL Server], ending
- ending batches [SQL Server]
- GO command
ms.assetid: b2ca6791-3a07-4209-ba8e-2248a92dd738
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 60c121767ffbf4e4ab222968eb27e4e170fa7fdd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-utilities-statements---go"></a>Anweisungen für SQL Server-Hilfsprogramme - GO
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]enthält Befehle, die nicht [!INCLUDE[tsql](../../includes/tsql-md.md)] sind aber -Anweisungen erkannt, durch die **Sqlcmd** und **Osql** Hilfsprogramme und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Code-Editor. Die Befehle können zur Vereinfachung der Lesbarkeit und Ausführung von Batches und Skripts verwendet werden.  
  
  GO signalisiert das Ende eines Batches von [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, die die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Hilfsprogramme.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
GO [count]  
```  
  
## <a name="arguments"></a>Argumente  
 *count*  
 Eine positive ganze Zahl. Der Batch, der GO vorausgeht, wird so oft wie angegeben ausgeführt.  
  
## <a name="remarks"></a>Hinweise  
 GO ist keine [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisung; Es wird ein Befehl erkannt durch die **Sqlcmd** und **Osql** Hilfsprogramme und [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Code-Editor.  
  
 Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramme interpretieren GO als ein Signal zum Senden des aktuellen Batches von [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Der aktuelle Anweisungsbatch besteht aus allen Anweisungen, die seit dem letzten GO eingegeben wurden. Wenn dies das erste GO ist, besteht er aus allen Anweisungen, die seit dem Beginn der Ad-hoc-Sitzung oder des Skripts eingegeben wurden.  
  
 Eine [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung kann nicht dieselbe Zeile wie ein GO-Befehl belegen. Allerdings kann die Zeile Kommentare enthalten.  
  
 Benutzer müssen die Regeln für Batches befolgen. So muss z. B. jede Ausführung einer gespeicherten Prozedur nach der ersten Anweisung in einem Batch das EXECUTE-Schlüsselwort einschließen. Der Bereich von lokalen (benutzerdefinierten) Variablen ist auf einen Batch beschränkt, auf die nicht nach einem GO-Befehl verwiesen werden kann.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @MyMsg VARCHAR(50)  
SELECT @MyMsg = 'Hello, World.'  
GO -- @MyMsg is not valid after this GO ends the batch.  
  
-- Yields an error because @MyMsg not declared in this batch.  
PRINT @MyMsg  
GO  
  
SELECT @@VERSION;  
-- Yields an error: Must be EXEC sp_who if not first statement in   
-- batch.  
sp_who  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Anwendungen können zum Ausführen eines Batches mehrere [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senden. Die Anweisungen im Batch werden dann in einen einzelnen Ausführungsplan kompiliert. Programmierer, die Ad-hoc-Anweisungen in den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogrammen ausführen oder aus [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen Skripts zur Ausführung durch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramme erstellen, verwenden GO, um das Ende eines Batches zu signalisieren.  
  
 Auf den ODBC- oder OLE DB-APIs basierende Anwendungen erhalten einen Syntaxfehler, wenn sie versuchen, einen GO-Befehl auszuführen. Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Hilfsprogramme senden nie einen GO-Befehl an den Server.  
  
 Verwenden Sie kein Semikolon als Abschlusszeichen für Anweisung nach GO.  
  
## <a name="permissions"></a>Berechtigungen  
 GO ist ein Hilfsprogrammbefehl, für den keine Berechtigungen erforderlich sind. Der Befehl kann von jedem Benutzer ausgeführt werden.  
  
```  
-- Yields an error because ; is not permitted after GO  
SELECT @@VERSION;  
GO;  
```  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden zwei Batches erstellt. Der erste Batch enthält nur eine `USE``AdventureWorks2012` Anweisung, um den Datenbankkontext festzulegen. Die verbleibenden Anweisungen verwenden eine lokale Variable. Daher müssen alle Deklarationen von lokalen Variablen in einem einzelnen Batch gruppiert werden. Dies wird erreicht, indem ein `GO`-Befehl erst nach der letzten Anweisung, die auf die Variable verweist, ausgeführt wird.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NmbrPeople int  
SELECT @NmbrPeople = COUNT(*)  
FROM Person.Person;  
PRINT 'The number of people as of ' +  
      CAST(GETDATE() AS char(20)) + ' is ' +  
      CAST(@NmbrPeople AS char (10));  
GO  
```  
  
 Im folgenden Beispiel werden die Anweisungen im Batch zweimal ausgeführt.  
  
```  
SELECT DB_NAME();  
SELECT USER_NAME();  
GO 2  
```  
  
  
