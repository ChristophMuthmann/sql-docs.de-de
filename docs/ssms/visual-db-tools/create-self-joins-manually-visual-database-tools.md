---
title: Manuelles Erstellen von Selbstjoins (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- self-joins
- manual joins [SQL Server]
- joins [SQL Server], self
ms.assetid: 910ed516-cb84-481b-95d0-cba3e89afdba
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ba962073bffba27b985fa08b59c6a46ed253fbee
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-self-joins-manually-visual-database-tools"></a>Manuelles Erstellen von Selbstjoins (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Sie können eine Tabelle mit sich selbst verknüpfen, auch wenn die Tabelle über keine reflexive Beziehung in der Datenbank verfügt. Mit einem Selbstjoin können Sie z. B. nach Paaren von Autoren suchen, die in derselben Stadt leben.  
  
Wie bei jedem Join werden für einen Selbstjoin mindestens zwei Tabellen benötigt. Der Unterschied besteht darin, dass Sie der Abfrage keine zweite Tabelle, sondern eine zweite Instanz derselben Tabelle hinzufügen. Auf diese Weise können Sie eine Spalte in der ersten Instanz der Tabelle mit derselben Spalte in der zweiten Instanz vergleichen, wodurch Sie die Werte einer Spalte miteinander vergleichen können. Der [Abfrage- und Sicht-Designer](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) weist der zweiten Instanz der Tabelle einen Alias zu.  
  
Wenn Sie z. B. einen Selbstjoin zum Suchen aller Autorenpaare in Berkeley erstellen, vergleichen Sie die Spalte `city` in der ersten Instanz der Tabelle mit der Spalte `city` in der zweiten Instanz. Die entsprechende Abfrage könnte folgendermaßen aussehen:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
Das Erstellen eines Selbstjoins erfordert oft mehrere Joinbedingungen. Die Gründe dafür werden aus dem Ergebnis der vorherigen Abfrage ersichtlich:  
  
```  
Cheryl Carson       Cheryl Carson  
   Abraham Bennet      Abraham Bennet  
   Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
Die erste Zeile ist ohne Belang; sie gibt an, dass Cheryl Carson in derselben Stadt wie Cheryl Carson lebt. Die zweite Zeile wird ebenfalls nicht benötigt. Fügen Sie eine weitere Bedingung hinzu, durch die nur die Ergebniszeilen beibehalten werden, in denen die Autorennamen verschiedene Autoren bezeichnen, um diese überflüssigen Daten auszuschließen. Die sich ergebende Abfrage könnte so aussehen:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                <> authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
Das Resultset wurde verbessert:  
  
```  
Cheryl Carson       Abraham Bennet  
   Abraham Bennet      Cheryl Carson  
```  
  
Die zwei Ergebniszeilen sind jedoch redundant. Die erste Zeile gibt an, dass Carson in derselben Stadt wie Bennet lebt, und mit der zweiten Zeile wird angegeben, dass Bennet in derselben Stadt wie Carson lebt. Sie können Sie die zweite Joinbedingung von "ungleich" in "kleiner als" ändern, um diese Redundanz auszuschließen. Die sich ergebende Abfrage könnte so aussehen:  
  
```  
SELECT   
         authors.au_fname,   
         authors.au_lname,   
         authors1.au_fname AS Expr2,   
         authors1.au_lname AS Expr3  
      FROM   
         authors   
            INNER JOIN  
            authors authors1   
               ON authors.city   
                = authors1.city  
               AND authors.au_id  
                < authors1.au_id  
      WHERE  
         authors.city = 'Berkeley'  
```  
  
Das Resultset sieht wie folgt aus:  
  
```  
Cheryl Carson       Abraham Bennet  
```  
  
### <a name="to-create-a-self-join-manually"></a>So erstellen Sie manuell einen Selbstjoin  
  
1.  Fügen Sie dem [Diagrammbereich](../../ssms/visual-db-tools/diagram-pane-visual-database-tools.md) die gewünschte Tabelle bzw. das gewünschte Tabellenwertobjekt hinzu.  
  
2.  Fügen Sie dieselbe Tabelle erneut hinzu, sodass die Tabelle bzw. das Tabellenwertobjekt im Diagrammbereich zweimal angezeigt wird.  
  
    Der Abfrage- und Sicht-Designer weist der zweiten Instanz einen Alias zu, indem dem Tabellennamen eine laufende Nummer hinzugefügt wird. Außerdem erstellt der Abfrage- und Sicht-Designer im Diagrammbereich eine Joinlinie zwischen den beiden Instanzen der Tabelle bzw. des Tabellenwertobjekts.  
  
3.  Klicken Sie mit der rechten Maustaste auf die Joinlinie, und wählen Sie im Kontextmenü die Option **Eigenschaften** aus.  
  
4.  Klicken Sie im Eigenschaftenfenster auf **Joinkondition und -typ** und anschließend auf die Auslassungszeichen **(…)** , die rechts neben der Eigenschaft angezeigt werden.  
  
5.  Ändern Sie nach Bedarf im [Dialogfeld „Join“](../../ssms/visual-db-tools/join-dialog-box-visual-database-tools.md) den Vergleichsoperator zwischen den Primärschlüsseln. Sie können z. B. den Operator in "kleiner als" (<) ändern.  
  
6.  Erstellen Sie die zusätzliche Joinbedingung (z. B. authors.zip = authors1.zip), indem Sie den Namen der primären Joinspalte aus der ersten Instanz der Tabelle bzw. des Tabellenwertobjekts ziehen und in der entsprechenden Spalte der zweiten Instanz ablegen.  
  
7.  Geben Sie weitere Optionen für die Abfrage an (z. B. Ausgabespalten, Suchbedingungen und Sortierreihenfolge).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Automatisches Erstellen von Selbstjoins &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-self-joins-automatically-visual-database-tools.md)  
[Erstellen von Abfragen mit Joins &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
