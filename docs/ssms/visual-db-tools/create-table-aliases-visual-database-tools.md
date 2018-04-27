---
title: Erstellen von Tabellenaliasen (Visual Database Tools) | Microsoft-Dokumentation
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
- table aliases [SQL Server]
- aliases [SQL Server], tables
ms.assetid: 49e61e85-8abf-4ca7-8c70-7e9f8f1078bd
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 403ec79488077b308b94be0c02f6bd9870592272
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="create-table-aliases-visual-database-tools"></a>Erstellen von Tabellenaliasen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Aliase können das Arbeiten mit Tabellennamen erleichtern. Das Verwenden von Aliasen ist in folgenden Fällen hilfreich:  
  
-   Sie möchten die Anweisung im [SQL-Bereich](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) kürzen und lesbarer machen.  
  
-   Sie verweisen in der Abfrage häufig auf den Tabellennamen, z. B. in qualifizierenden Spaltennamen, und möchten sicherstellen, dass in der Abfrage eine bestimmte Anzahl von Zeichen nicht überschritten wird. (In einigen Datenbanken ist eine maximale Länge für Abfragen festgelegt.)  
  
-   Sie verwenden mehrere Instanzen derselben Tabelle (z. B. in einem Selbstjoin) und suchen nach einer Möglichkeit, um auf die eine oder andere Instanz zu verweisen.  
  
Sie können z.B. einen Alias `"e"` für einen Tabellennamen `employee_information` erstellen und in der restlichen Abfrage mit `"e"` auf die Tabelle verweisen.  
  
### <a name="to-create-an-alias-for-a-table-or-table-valued-object"></a>So erstellen Sie einen Alias für eine Tabelle oder ein Tabellenwertobjekt  
  
1.  Fügen Sie der Abfrage die Tabelle oder das Tabellenwertobjekt hinzu.  
  
2.  Klicken Sie im **Diagrammbereich**mit der rechten Maustaste auf das Objekt, für das Sie einen Alias erstellen möchten, und wählen Sie anschließend im Kontextmenü **Eigenschaften** aus.  
  
3.  Geben Sie im **Eigenschaftenfenster** den Alias in das Feld **Alias** ein.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Hinzufügen von Tabellen zu Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[Sortieren und Gruppieren von Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[Zusammenfassen von Abfrageergebnissen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
