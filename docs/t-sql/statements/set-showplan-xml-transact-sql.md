---
title: SET SHOWPLAN_XML (Transact-SQL) | Microsoft Docs
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
- SET SHOWPLAN_XML
- SET_SHOWPLAN_XML_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- SET SHOWPLAN_XML statement
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- XML [SQL Server], statement execution information
- SHOWPLAN_XML option
- estimated execution information [SQL Server]
ms.assetid: a467a1b3-10a5-43c4-9085-13d8aed549c9
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3414096227310460a0a1b58a34cb0fbc4e528649
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-showplanxml-transact-sql"></a>SET SHOWPLAN_XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht ausführt. Stattdessen gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detaillierte Informationen zur Ausführung der Anweisungen in Form eines definierten XML-Dokuments zurück.  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET SHOWPLAN_XML { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Einstellung von SET SHOWPLAN_XML wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Wenn SET SHOWPLAN_XML auf ON festgelegt ist [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ausführungsplaninformationen für jede Anweisung zurückgibt, ohne Sie auszuführen, und [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen werden nicht ausgeführt. Wenn diese Option auf ON festgelegt ist, werden Ausführungsplaninformationen zu allen weiteren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zurückgegeben, bis die Option auf OFF festgelegt wird. Wenn beispielsweise eine CREATE TABLE-Anweisung ausgeführt wird, während SET SHOWPLAN_XML auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei einer darauf folgenden SELECT-Anweisung, die dieselbe Tabelle betrifft, die Fehlermeldung zurück, dass diese Tabelle nicht vorhanden ist. Daher schlagen spätere Verweise auf diese Tabelle fehl. Wenn SET SHOWPLAN_XML auf OFF festgelegt ist, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anweisungen aus, ohne einen Bericht zu generieren.  
  
 SET SHOWPLAN_XML soll als Ausgabe zurückgegeben **nvarchar(max)** für Anwendungen, z. B. die **Sqlcmd** , in dem die XML-Ausgabe wird anschließend verwendet von anderen Tools zur Anzeige und Verarbeitung der Abfrage-Hilfsprogramm Informationen zum Abfrageausführungsplan.  
  
> [!NOTE]  
>  Die dynamische verwaltungssicht **dm_exec_query_plan**, gibt die gleiche Informationen wie SET SHOWPLAN XML in die **Xml** -Datentyp. Diese Informationen werden zurückgegeben, aus der **Query_plan** Spalte **dm_exec_query_plan**. Weitere Informationen finden Sie unter [dm_exec_query_plan &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md).  
  
 SET SHOWPLAN_XML kann innerhalb einer gespeicherten Prozedur nicht angegeben werden. Sie muss die einzige Anweisung in einem Batch sein.  
  
 SET SHOWPLAN_XML gibt Informationen als eine Gruppe von XML-Dokumenten zurück. Jeder Batch nach der SET SHOWPLAN_XML ON-Anweisung ist in der Ausgabe als einzelnes Dokument enthalten. Jedes Dokument enthält den Text der Anweisungen im Batch gefolgt von den Details der Ausführungsschritte. Das Dokument zeigt die geschätzten Kosten, Anzahl von Zeilen, Indexzugriffe und Typen der ausgeführten Operatoren, Joinreihenfolge und weitere Informationen zu den Ausführungsplänen.  
  
 Das Dokument mit dem XML-Schema für die XML-Ausgabe von SET SHOWPLAN_XML wird beim Setup in ein lokales Verzeichnis auf dem Computer kopiert, auf dem Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist. Es wird auf dem Laufwerk mit den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationsdateien gespeichert unter:  
  
 \Microsoft SQL Server\130\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 Das Showplanschema auch finden Sie unter [diese Website](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
> [!NOTE]  
>  Wenn **tatsächlichen Ausführungsplan einschließen** ausgewählt ist, im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], gibt diese SET-Option wird kein XML-Showplan-Ausgabe erzeugt. Deaktivieren der **tatsächlichen Ausführungsplan einschließen** Schaltfläche vor der Verwendung dieser Option festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Verwendung von SET SHOWPLAN_XML benötigen Sie für die Ausführung der Anweisungen, auf die SET SHOWPLAN_XML angewendet wird, ausreichende Berechtigungen sowie die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die verwiesen wird.  
  
 Für SELECT, INSERT, UPDATE, DELETE, EXEC *Stored_procedure*, und den AUSFÜHRUNGSTYP *User_defined_function* -Anweisungen, um einen Showplan zu erstellen, der Benutzer muss:  
  
-   Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   SHOWPLAN-Berechtigung für alle Datenbanken, die mit Objekten verwiesen wird, indem Sie haben die [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, z. B. Tabellen, Sichten und So weiter.  
  
 Für alle anderen Anweisungen, z. B. DDL, USE *Database_name*, SET, DECLARE, dynamisches SQL usw., nur die entsprechenden Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen erforderlich sind.  
  
## <a name="examples"></a>Beispiele  
 In den beiden folgenden Anweisungen werden die SET SHOWPLAN_XML-Einstellungen verwendet, um zu zeigen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Verwendung von Indizes in Abfragen analysiert und optimiert.  
  
 Die erste Abfrage verwendet den Vergleichsoperator gleich (=) in der WHERE-Klausel auf eine indizierte Spalte an. In der zweiten Abfrage wird der LIKE-Operator in der WHERE-Klausel verwendet. Deshalb muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Scan des gruppierten Indexes ausführen, um die Daten zu finden, die der Bedingung in der WHERE-Klausel entsprechen. Die Werte in der **EstimateRows** und **EstimatedTotalSubtreeCost** Attribute sind bei der ersten indizierten Abfrage, die anzeigt, dass es viel schneller verarbeitet ist und weniger Ressourcen als verwendet der nicht indizierten Abfrage.  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_XML ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, JobTitle  
FROM HumanResources.Employee  
WHERE JobTitle LIKE 'Production%';  
GO  
SET SHOWPLAN_XML OFF;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

