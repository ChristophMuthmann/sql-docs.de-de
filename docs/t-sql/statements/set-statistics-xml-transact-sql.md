---
title: SET STATISTICS XML (Transact-SQL) | Microsoft Docs
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
- SET_STATISTICS_XML_TSQL
- SET STATISTICS XML
dev_langs:
- TSQL
helpviewer_keywords:
- statistical information [SQL Server], statement processing
- STATISTICS XML option
- SET STATISTICS XML statement
- statements [SQL Server], statistical information
- XML [SQL Server], statement execution information
ms.assetid: 2b6d4c5a-a7f5-4dd1-b10a-7632265b1af7
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 45191a544866451e5208325eb2cafcab60bc8fb5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-statistics-xml-transact-sql"></a>SET STATISTICS XML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen ausführt und weitere Informationen zur Ausführung der Anweisungen in Form eines definierten XML-Dokuments generiert.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET STATISTICS XML { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Einstellung von SET STATISTICS XML wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Wenn SET STATISTICS XML auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ausführungsinformationen für jede Anweisung nach deren Ausführung zurück. Nachdem diese Option auf ON festgelegt wird, werden Informationen zu allen weiteren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zurückgegeben, bis die Option auf OFF festgelegt wird. SET STATISTICS XML muss nicht die einzige Anweisung in einem Batch sein.  
  
 SET STATISTICS XML gibt die Ausgabe als **nvarchar(max)** für Anwendungen, wie z. B. die **Sqlcmd** , in dem die XML-Ausgabe wird anschließend verwendet von anderen Tools zur Anzeige und Verarbeitung des Abfrageplans-Hilfsprogramm Informationen.  
  
 SET STATISTICS XML gibt Informationen als eine Gruppe von XML-Dokumenten zurück. Jede Anweisung nach der SET STATISTICS XML ON-Anweisung ist in der Ausgabe als einzelnes Dokument enthalten. Jedes Dokument enthält den Text der Anweisung, gefolgt von den Informationen zu den Ausführungsschritten. Die Ausgabe zeigt Laufzeitinformationen an, wie z. B. Kosten, zugegriffene Indizes und Typen der ausgeführten Vorgänge, Joinreihenfolge, Anzahl von Ausführungen eines physischen Vorgangs sowie die Anzahl der von einem physischen Operator erstellten Zeilen usw.  
  
 Das Dokument mit dem XML-Schema für die XML-Ausgabe von SET STATISTICS XML wird beim Setup in ein lokales Verzeichnis auf dem Computer kopiert, auf dem Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist. Es wird auf dem Laufwerk mit den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installationsdateien gespeichert unter:  
  
 \Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\showplan\showplanxml.xsd  
  
 Das Showplanschema auch finden Sie unter [diese Website](http://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409).  
  
 SET STATISTICS PROFILE und SET STATISTICS XML sind Gegenstücke zueinander. SET STATISTICS PROFILE erstellt Textausgaben, während SET STATISTICS XML XML-Ausgaben erstellt. In künftigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Versionen werden neue Informationen zum Abfrageausführungsplan nur über die SET STATISTICS XML-Anweisung und nicht die SET STATISTICS PROFILE-Anweisung angezeigt.  
  
> [!NOTE]  
>  Wenn **tatsächlichen Ausführungsplan einschließen** ausgewählt ist, im [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], gibt diese SET-Option wird kein XML-Showplan-Ausgabe erzeugt. Deaktivieren der **tatsächlichen Ausführungsplan einschließen** Schaltfläche vor der Verwendung dieser Option festgelegt.  
  
## <a name="permissions"></a>Berechtigungen  
 Für die Verwendung von SET STATISTICS XML und die Anzeige der Ausgabe benötigen Benutzer die folgenden Berechtigungen:  
  
-   Entsprechende Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   Die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die von den [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen verwiesen wird.  
  
 Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die keine STATISTICS XML-Resultsets erstellen, werden nur die Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen benötigt. Für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen, die STATISTICS XML-Resultsets erstellen, werden sowohl die Ausführungsberechtigung für [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen als auch die SHOWPLAN-Berechtigung benötigt, da die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung andernfalls abgebrochen und keine Showplaninformationen generiert werden.  
  
## <a name="examples"></a>Beispiele  
 In den beiden folgenden Anweisungen werden die SET STATISTICS XML-Einstellungen verwendet, um zu zeigen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Verwendung von Indizes in Abfragen analysiert und optimiert. In der ersten Abfrage wird der Vergleichsoperator Gleich (=) in der WHERE-Klausel auf eine indizierte Spalte angewendet. In der zweiten Abfrage wird der LIKE-Operator in der WHERE-Klausel verwendet. Deshalb muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Scan des gruppierten Indexes durchführen, um die Daten zu finden, die die Bedingung in der WHERE-Klausel erfüllen. Die Werte in der **EstimateRows** und **EstimatedTotalSubtreeCost** Attribute sind bei der ersten indizierten Abfrage gibt an, dass sie viel schneller verarbeitet wurde, und weniger Ressourcen als verwendet der nicht indizierten Abfrage.  
  
```  
USE AdventureWorks2012;  
GO  
SET STATISTICS XML ON;  
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
SET STATISTICS XML OFF;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)  
  
  

