---
title: Sortieren von Zeilen (Visual Database Tools) | Microsoft-Dokumentation
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sorting rows [SQL Server]
- sorting query results [SQL Server]
ms.assetid: 780ef467-f96e-4373-8235-6dacbedb05a2
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a044ed67ea4b7ba2eedeafbc4af8fcd1e20e7061
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="sort-rows-visual-database-tools"></a>Sortieren von Zeilen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Sie können die Zeilen in einem Abfrageergebnis sortieren. Das heißt, Sie können eine bestimmte Spalte oder eine Spaltengruppe angeben und die Zeilen im Resultset anhand der Werte in diesen Spalten neu ordnen.  
  
> [!NOTE]  
> Die Sortierreihenfolge wird teilweise durch die Sortierreihenfolge der Spalte bestimmt. Sie können die Sortierreihenfolge im [Dialogfeld Sortierreihenfolge](../../ssms/visual-db-tools/collation-dialog-box-visual-database-tools.md)ändern.  
  
Zum Sortieren der Abfrageergebnisse stehen Ihnen mehrere Möglichkeiten zur Verfügung:  
  
-   **Sie können Zeilen in auf- oder absteigender Reihenfolge sortieren.** Standardmäßig werden die ORDER BY-Spalten in SQL verwendet, um Zeilen in aufsteigender Reihenfolge zu sortieren. Wenn Sie z. B. Buchtitel in aufsteigender Reihenfolge nach dem Preis ordnen möchten, sortieren Sie die Zeilen einfach nach der Preisspalte. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price  
    ```  
  
    Wenn Sie die Titel beginnend mit den teuersten Büchern ordnen möchten, können Sie dies für die Sortierreihenfolge explizit festlegen. Das heißt, Sie legen fest, dass die Ergebniszeilen nach absteigenden Werten in der Preisspalte sortiert werden sollen. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT *  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **Sie können nach mehreren Spalten sortieren.** Sie können z. B. ein Resultset mit einer Zeile für jeden Autor erstellen und die Zeilen zunächst nach dem Land bzw. der Region und anschließend nach der Stadt sortieren. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT *  
    FROM authors   
    ORDER BY state, city  
    ```  
  
-   **Sie können nach Spalten sortieren, die nicht im Resultset angezeigt werden.** Sie können z. B. ein Resultset erstellen, in dem die teuersten Titel zuerst aufgeführt werden, das jedoch keine Preisspalte enthält. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT title_id, title  
    FROM titles  
    ORDER BY price DESC  
    ```  
  
-   **Sie können nach abgeleiteten Spalten sortieren.** Sie können z. B. ein Resultset erstellen, in dem jede Zeile einen Buchtitel enthält und in dem die Bücher zuerst aufgeführt werden, die die höchsten Tantiemen pro Exemplar erzielen. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT title, price * royalty / 100 as royalty_per_unit  
    FROM titles  
    ORDER BY royalty_per_unit DESC  
    ```  
  
    (Die Formel zur Berechnung der erzielten Tantiemen pro Buchexemplar ist hervorgehoben.)  
  
    Zum Berechnen einer abgeleiteten Spalte können Sie wie im vorhergehenden Beispiel SQL-Syntax verwenden, Sie können aber auch eine benutzerdefinierte Funktion verwenden, die einen Skalarwert zurückgibt. Weitere Informationen über benutzerdefinierte Funktionen finden Sie in der SQL Server-Dokumentation.  
  
-   **Sie können gruppierte Zeilen sortieren.** Sie können z. B. ein Resultset erstellen, in dem jede Zeile eine Stadt sowie die Anzahl der in dieser Stadt lebenden Autoren enthält, wobei die Städte mit mehreren Autoren zuerst aufgeführt werden. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ORDER BY COUNT(*) DESC, state  
    ```  
  
    Beachten Sie, dass die Abfrage `state` als zweite Sortierspalte verwendet. Wenn daher mehrere Länder/Regionen mit der gleichen Anzahl Autoren vorhanden sind, werden die Länder/Regionen in alphabetischer Reihenfolge aufgeführt.  
  
-   **Sie können Daten nach internationalen Kriterien sortieren.** Das heißt, Sie können beim Sortieren einer Spalte Ordnungskonventionen zugrunde legen, die von den Standardkonventionen für diese Spalte abweichen. Sie können z. B. eine Abfrage schreiben, mit der alle Buchtitel von Jaime Patiño abgerufen werden. Um die Titel in alphabetischer Reihenfolge anzuzeigen, verwenden Sie eine spanische Sortierreihenfolge für die Titelspalte. Hierfür kann folgende SQL-Anweisung formuliert werden:  
  
    ```  
    SELECT title  
    FROM   
        authors   
        INNER JOIN   
            titleauthor   
            ON authors.au_id   
            =  titleauthor.au_id   
            INNER JOIN  
                titles   
                ON titleauthor.title_id   
                =  titles.title_id   
    WHERE   
         au_fname = 'Jaime' AND   
         au_lname = 'Patiño'  
    ORDER BY   
         title COLLATE SQL_Spanish_Pref_CP1_CI_AS  
    ```  
  
## <a name="see-also"></a>Siehe auch  
[Sortieren und Gruppieren von Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
