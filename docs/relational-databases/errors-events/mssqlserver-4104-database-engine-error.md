---
title: MSSQLSERVER_4104 | Microsoft-Dokumentation
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 6b6f3eb184b90716053e4a8860b3c6ef2c1505e1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver4104"></a>MSSQLSERVER_4104
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|4104|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|SQLEngine|  
|Symbolischer Name|ALG_MULTI_ID_BAD|  
|Meldungstext|Der mehrteilige Bezeichner '%.*ls' konnte nicht gebunden werden.|  
  
## <a name="explanation"></a>Erklärung  
Der Name einer Entität in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird *Bezeichner* genannt. Sie verwenden Bezeichner immer dann, wenn Sie auf Entitäten verweisen, z. B. durch das Angeben von Spalten- und Tabellennamen in einer Abfrage. Ein mehrteiliger Bezeichner enthält einen oder mehrere Qualifizierer als Präfix für den Bezeichner. Einem Tabellenbezeichner können z. B. Qualifizierer vorangestellt werden, wie z. B. der Datenbankname und der Name des Schemas, in dem die Tabelle enthalten ist, oder einer Spalten-ID können Qualifizierer vorangestellt werden, wie z. B. ein Tabellenname oder ein Tabellenalias.  
  
Der Fehler 4104 gibt an, dass der angegebene mehrteilige Bezeichner keiner vorhandenen Entität zugeordnet werden konnte. Dieser Fehler kann unter folgenden Bedingungen zurückgegeben werden:  
  
-   Der als Präfix für einen Spaltennamen angegebene Qualifizierer stimmt mit keinem in der Abfrage verwendeten Tabellen- oder Aliasnamen überein.  
  
    In der folgenden Anweisung wird beispielsweise ein Tabellenalias (`Dept`) als Spaltenpräfix verwendet, es wird jedoch in der FROM-Klausel nicht auf den Tabellenalias verwiesen.  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
    In den folgenden Anweisungen wird eine mehrteilige Spalten-ID `TableB.KeyCol` in der WHERE-Klausel als Teil einer JOIN-Bedingung zwischen zwei Tabellen angegeben, auf `TableB` wird in der Abfrage jedoch nicht explizit verwiesen.  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   In der FROM-Klausel wird ein Aliasname für die Tabelle festgelegt, aber der für eine Spalte angegebene Qualifizierer ist der Tabellenname. In der folgenden Anweisung wird beispielsweise der Tabellenname `Department` als Spaltenpräfix verwendet, die Tabelle verfügt jedoch über einen Alias (`Dept`), auf den in der FROM-Klausel verwiesen wird.  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
    Falls ein Alias verwendet wird, kann der Tabellenname nicht anderweitig in der Anweisung verwendet werden.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann nicht bestimmen, ob der mehrteilige Bezeichner sich auf eine Spalte bezieht, der eine Tabelle vorangestellt ist, oder auf eine Eigenschaft eines CLR-benutzerdefinierten Datentyps (user-defined data type, UDT), dem eine Spalte vorangestellt ist. Dies liegt daran, dass auf Eigenschaften von UDT-Spalten mithilfe eines Punkts als Trennzeichen (.) zwischen dem Spaltennamen und dem Eigenschaftsnamen auf dieselbe Weise verwiesen wird, wie einem Spaltennamen ein Tabellenname vorangestellt wird. Im folgenden Beispiel werden zwei Tabellen erstellt: `a` und `b`. Die Tabelle `b` enthält die Spalte `a`, die einen CLR UDT `dbo.myudt2` als Datentyp verwendet. Die SELECT-Anweisung enthält einem mehrteiligen Bezeichner `a.c2`.  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
    Wenn der UDT `myudt2` keine Eigenschaft namens `c2` hat, kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht ermitteln, ob der Bezeichner `a.c2` auf die Spalte `c2` in der Tabelle `a` oder auf die Spalte `a` mit der Eigenschaft `c2` in der Tabelle `b` verweist.  
  
## <a name="user-action"></a>Benutzeraktion  
  
-   Gleichen Sie die Spaltenpräfixe mit den in der FROM-Klausel der Abfrage angegeben Tabellen- oder Aliasnamen ab. Wenn in der FROM-Klausel ein Alias für einen Tabellennamen definiert wurde, kann der Alias nur als Qualifizierer für Spalten verwendet werden, die dieser Tabelle zugeordnet sind.  
  
    Die oben genannten Anweisungen, die auf die `HumanResources.Department`-Tabelle verweisen, können folgendermaßen korrigiert werden:  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   Stellen Sie sicher, dass alle Tabellen in der Abfrage angegeben werden und dass die JOIN-Bedingungen zwischen Tabellen ordnungsgemäß angegeben werden. Die oben genannte DELETE-Anweisung kann folgendermaßen korrigiert werden:  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
    Die oben genannte SELECT-Anweisung für `TableA` kann folgendermaßen korrigiert werden:  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
    oder  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   Verwenden Sie eindeutige, klar definierte Namen für Bezeichner. Dadurch wird der Code einfacher zu lesen und zu warten, und das Risiko mehrdeutiger Verweise auf mehrere Entitäten wird minimiert.  
  
## <a name="see-also"></a>Siehe auch  
[MSSQLSERVER_107](~/relational-databases/errors-events/mssqlserver-107-database-engine-error.md)  
[Datenbankbezeichner](~/relational-databases/databases/database-identifiers.md)  
  
