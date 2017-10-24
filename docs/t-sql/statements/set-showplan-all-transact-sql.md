---
title: SET SHOWPLAN_ALL (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SET SHOWPLAN_ALL
- SET_SHOWPLAN_ALL_TSQL
- SHOWPLAN_ALL
- SHOWPLAN_ALL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], estimates
- execution information and estimates [SQL Server]
- statements [SQL Server], information without processing
- SET SHOWPLAN_ALL statement
- SHOWPLAN_ALL option
- canceling statement execution
- stopping statement execution
- estimated execution information [SQL Server]
ms.assetid: a500b682-bae4-470f-9e00-47de905b851b
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: beb2d1647869da3ebb3f7463c896d8f6f986c387
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="set-showplanall-transact-sql"></a>SET SHOWPLAN_ALL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Bewirkt, dass Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen nicht ausführt. Stattdessen gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detaillierte Informationen darüber zurück, wie die Anweisungen ausgeführt werden, und stellt Schätzungen zu Ressourcenanforderungen für die Anweisungen bereit.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET SHOWPLAN_ALL { ON | OFF }  
```  
  
## <a name="remarks"></a>Hinweise  
 Die Einstellung von SET SHOWPLAN_ALL wird zur Ausführungszeit und nicht zur Analysezeit festgelegt.  
  
 Wenn SET SHOWPLAN_ALL auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Informationen zur Ausführung jeder Anweisung zurück, ohne sie jedoch auszuführen, und [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen werden nicht ausgeführt. Nachdem diese Option auf ON festgelegt wurde, werden Informationen zu allen weiteren [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen zurückgegeben, bis die Option auf OFF festgelegt wird. Wenn z. B. eine CREATE TABLE-Anweisung ausgeführt wird, während SET SHOWPLAN_ALL auf ON festgelegt ist, gibt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bei einer nachfolgenden SELECT-Anweisung, die dieselbe Tabelle betrifft, eine Fehlermeldung zurück, in der der Benutzer informiert wird, dass diese Tabelle nicht vorhanden ist. Daher schlagen spätere Verweise auf diese Tabelle fehl. Wenn SET SHOWPLAN_ALL auf OFF festgelegt ist, führt [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Anweisungen aus, ohne einen Bericht zu generieren.  
  
 SET SHOWPLAN_ALL ist dafür gedacht, von Anwendungen verwendet zu werden, die seine Ausgabe verarbeiten. Verwenden Sie SET SHOWPLAN_TEXT, um lesbare Ausgabe für Microsoft Win32-eingabeaufforderungsanwendungen, zurückgeben, z. B. die **Osql** Hilfsprogramm.  
  
 SET SHOWPLAN_TEXT und SET SHOWPLAN_ALL können nicht in einer gespeicherten Prozedur angegeben werden; diese Anweisungen müssen die einzigen Anweisungen in einem Batch sein.  
  
 SET SHOWPLAN_ALL gibt ein Rowset in Form einer hierarchischen Baumstruktur zurück, die zeigt, welche Schritte vom [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Abfrageprozessor beim Ausführen einer Anweisung ausgeführt werden. Jede in der Ausgabe widergespiegelte Anweisung enthält zuerst eine Zeile mit dem Text der Anweisung, auf die mehrere Zeilen mit den Details der Ausführungsschritte folgen. Die Tabelle zeigt die Spalten, die in der Ausgabe enthalten sind.  
  
|Spaltenname|Description|  
|-----------------|-----------------|  
|**StmtText**|Für Zeilen, die nicht vom Typ PLAN_ROW sind, enthält diese Spalte den Text der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung. Für Zeilen vom Typ PLAN_ROW enthält diese Spalte eine Beschreibung des Vorgangs. Diese Spalte enthält den physischen Operator und optional auch den logischen Operator. Auf die Spalte kann auch eine Beschreibung folgen, die vom physischen Operator bestimmt wird. Weitere Informationen finden Sie unter [Showplan logischen und physischen Operatoren Verweis](../../relational-databases/showplan-logical-and-physical-operators-reference.md).|  
|**StmtId**|Nummer der Anweisung im aktuellen Batch.|  
|**NodeId**|ID des Knotens in der aktuellen Abfrage.|  
|**Parent**|Knoten-ID des übergeordneten Schrittes.|  
|**PhysicalOp**|Algorithmus der physischen Implementierung für den Knoten. Nur für Zeilen vom Typ PLAN_ROWS.|  
|**LogicalOp**|Relationaler algebraischer Operator, den dieser Knoten darstellt. Nur für Zeilen vom Typ PLAN_ROWS.|  
|**Argument**|Gibt Zusatzinformationen zur durchgeführten Operation. Der Inhalt dieser Spalte hängt vom physischen Operator ab.|  
|**DefinedValues**|Enthält eine Liste mit durch Trennzeichen getrennten Werten, die dieser Operator einführt. Die Werte können berechnete Ausdrücke aus der aktuellen Abfrage (z. B. aus der SELECT-Liste oder der WHERE-Klausel) oder interne Werte sein, die der Abfrageprozessor eingeführt hat, um diese Abfrage zu verarbeiten. Auf diese definierten Werte kann dann an anderer Stelle in dieser Abfrage verwiesen werden. Nur für Zeilen vom Typ PLAN_ROWS.|  
|**EstimateRows**|Geschätzte Anzahl der Zeilen, die dieser Operator ausgibt. Nur für Zeilen vom Typ PLAN_ROWS.|  
|**EstimateIO**|Geschätzte E/A-Kosten* für diesen Operator. Nur für Zeilen vom Typ PLAN_ROWS.|  
|**EstimateCPU**|Geschätzte CPU-Kosten* für diesen Operator. Nur für Zeilen vom Typ PLAN_ROWS.|  
|**AvgRowSize**|Geschätzte mittlere Zeilenlänge (in Bytes) der Zeile, die durch diesen Operator übergeben wird.|  
|**TotalSubtreeCost**|Geschätzte (kumulierte) Kosten* dieses Vorgangs und aller untergeordneten Vorgänge.|  
|**Ausgabeliste**|Enthält eine Liste mit durch Trennzeichen getrennten Spalten, die vom aktuellen Vorgang projiziert werden.|  
|**Warnungen**|Enthält eine Liste mit durch Trennzeichen getrennten Warnmeldungen, die die aktuelle Operation betreffen. Warnmeldungen können die Zeichenfolge "NO STATS:()" mit einer Spaltenliste enthalten. Diese Warnmeldung bedeutet, dass der Abfrageoptimierer versucht hat, eine Entscheidung auf der Grundlage der Statistik für diese Spalte zu treffen, wobei jedoch keine Statistik verfügbar war. Daher musste der Abfrageoptimierer eine Schätzung vornehmen, die möglicherweise zur Auswahl eines ineffizienten Abfrageplans führte. Weitere Informationen zum Erstellen oder Aktualisieren einer Spaltenstatistik (derer den Abfrageoptimierer einen effizienteren Abfrageplan wählen) finden Sie unter [UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md). Diese Spalte kann optional die Zeichenfolge "MISSING JOIN PREDICATE" enthalten. Sie gibt an, dass ein Join (mit Tabellen) ohne Joinprädikat vorgenommen wird. Das unbeabsichtigte Löschen eines Joinprädikats kann zu einer Abfrage führen, die eine erheblich längere Ausführungszeit als erwartet hat und ein sehr umfangreiches Resultset zurückgibt. Wenn diese Warnung besteht, überprüfen Sie, ob das Fehlen des Joinprädikats absichtlich ist.|  
|**Typ**|Der Knotentyp. Für den übergeordneten Knoten jeder Abfrage ist dies der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungstyp (z. B. SELECT, INSERT, EXECUTE usw.). Für untergeordnete Knoten, die Ausführungspläne darstellen, ist der Typ PLAN_ROW.|  
|**Parallel**|**0** = Operator wird nicht parallel ausgeführt.<br /><br /> **1** = Operator wird parallel ausgeführt.|  
|**EstimateExecutions**|Geschätzte Anzahl der Ausführungen dieses Operators, die während der Ausführung der aktuellen Abfrage ausgeführt werden.|  
  
 *Kosteneinheiten basieren auf einer internen Zeitmessung und nicht auf der normalen Uhrzeit. Sie werden zur Ermittlung der relativen Kosten eines Plans im Vergleich zu anderen Plänen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Zur Verwendung von SET SHOWPLAN_ALL benötigen Sie für die Ausführung der Anweisungen, auf die SET SHOWPLAN_ALL angewendet wird, ausreichende Berechtigungen sowie die SHOWPLAN-Berechtigung für alle Datenbanken mit Objekten, auf die verwiesen wird.  
  
 Für SELECT, INSERT, UPDATE, DELETE, EXEC *Stored_procedure*, und den AUSFÜHRUNGSTYP *User_defined_function* -Anweisungen, um einen Showplan zu erstellen, der Benutzer muss:  
  
-   Berechtigungen für die Ausführung der [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisungen.  
  
-   SHOWPLAN-Berechtigung für alle Datenbanken, die mit Objekten verwiesen wird, indem Sie haben die [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen, z. B. Tabellen, Sichten und So weiter.  
  
 Für alle anderen Anweisungen, z. B. DDL, USE *Database_name*, SET, DECLARE, dynamisches SQL usw., nur die entsprechenden Berechtigungen zum Ausführen der [!INCLUDE[tsql](../../includes/tsql-md.md)] Anweisungen erforderlich sind.  
  
## <a name="examples"></a>Beispiele  
 In den beiden folgenden Anweisungen werden die SET SHOWPLAN_ALL-Einstellungen verwendet, um zu zeigen, wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] die Verwendung von Indizes in Abfragen analysiert und optimiert.  
  
 Die erste Abfrage verwendet den Vergleichsoperator gleich (=) in der WHERE-Klausel auf eine indizierte Spalte an. Dadurch wird der Wert Clustered Index Seek, in der **LogicalOp** Spalte und den Namen des Indexes in der **Argument** Spalte.  
  
 In der zweiten Abfrage wird der LIKE-Operator in der WHERE-Klausel verwendet. Deshalb muss [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Scan des gruppierten Indexes ausführen und die Daten finden, die die Bedingung in der WHERE-Klausel erfüllen. Dadurch wird der Wert Clustered Index Scan in der **LogicalOp** Spalte mit dem Namen des Indexes in der **Argument** Spalte und der Filterwert in der **LogicalOp** Spalte mit der Bedingung der WHERE-Klausel in der **Argument** Spalte.  
  
 Die Werte in der **EstimateRows** und **TotalSubtreeCost** Spalten sind bei der ersten indizierten Abfrage deutlich schnellere Verarbeitung und verwendet weniger Ressourcen als bei nicht indizierten Abfrage hinweist .  
  
```  
USE AdventureWorks2012;  
GO  
SET SHOWPLAN_ALL ON;  
GO  
-- First query.  
SELECT BusinessEntityID   
FROM HumanResources.Employee  
WHERE NationalIDNumber = '509647174';  
GO  
-- Second query.  
SELECT BusinessEntityID, EmergencyContactID   
FROM HumanResources.Employee  
WHERE EmergencyContactID LIKE '1%';  
GO  
SET SHOWPLAN_ALL OFF;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [SET-Anweisungen (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET SHOWPLAN_TEXT &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-text-transact-sql.md)   
 [SET SHOWPLAN_XML &#40; Transact-SQL &#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)  
  
  

