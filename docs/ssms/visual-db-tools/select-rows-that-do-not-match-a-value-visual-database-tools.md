---
title: Auswählen von Zeilen, die mit einem Wert nicht übereinstimmen (Visual Database Tools) | Microsoft-Dokumentation
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
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 32e53f7bde5317bb3c28a733ce98d1b397601758
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>Auswählen von Zeilen, die mit einem Wert nicht übereinstimmen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Zum Suchen von Zeilen, die mit einem Wert nicht übereinstimmen, wird der Operator NOT verwendet.  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>So suchen Sie nach Zeilen, die mit einem Wert nicht übereinstimmen  
  
1.  Fügen Sie im [Kriterienbereich](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)die Spalten oder Ausdrücke hinzu, die in der Suchbedingung verwendet werden sollen, falls dies nicht bereits geschehen ist.  
  
2.  Wechseln Sie zu der Zeile, die die Datenspalte oder den Ausdruck für die Suche enthält. Geben Sie anschließend in der Datenblattspalte **Filter** den Operator NOT gefolgt von einem Suchwert ein.  
  
Um beispielsweise alle Zeilen in der Tabelle `products` zu suchen, in denen der Wert in der Spalte für den Produktcode nicht mit "A" beginnt, können Sie folgende Suchbedingung eingeben:  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Regeln für das Eingeben von Suchwerten (Visual Database Tools)](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[Angeben von Suchkriterien (Visual Database Tools)](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
