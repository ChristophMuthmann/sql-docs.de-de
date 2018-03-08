---
title: "Verwerfen von Änderungen an Abfragen (Visual Database Tools) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reverting queries
- queries [SQL Server], discarding changes
- discarding query changes
ms.assetid: 7bb17ece-1222-4622-b476-5789d7641c64
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5412ede653f8bd6eb67091dd4ebc532b1d7f1b19
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="discard-changes-made-to-queries-visual-database-tools"></a>Verwerfen von Änderungen an Abfragen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Sie können an einer Abfragedefinition vorgenommene Änderungen vor dem Speichern verwerfen. Nach dem Speichern kann ein früherer Zustand nicht wiederhergestellt werden.  
  
> [!NOTE]  
> Um Änderungen an Werten im Ergebnisbereich rückgängig zu machen, drücken Sie die ESC-TASTE, bevor Sie zu einem anderen Datensatz wechseln. Wenn Sie zu einem anderen Datensatz wechseln und eine Benachrichtigung erhalten, dass die Änderungen nicht an die Datenbank übergeben werden, haben Sie nochmals die Gelegenheit, durch Drücken der ESC-TASTE den früheren Wert wiederherzustellen.  
  
### <a name="to-discard-changes-made-to-a-query-definition"></a>So verwerfen Sie die an einer Abfragedefinition vorgenommenen Änderungen  
  
1.  Klicken Sie, während die Abfrage im Abfrage- und Sicht-Designer geöffnet ist, im Menü **Datei** auf **Schließen**.  
  
2.  Klicken Sie im Dialogfeld **Microsoft SQL Server Management Studio** auf **Nein**.  
  
    Die Abfragedefinition wird in den Zustand beim letzten Speichern zurückgeführt.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Speichern von Abfragen (Visual Database Tools)](../../ssms/visual-db-tools/save-queries-visual-database-tools.md)  
[Themen zur Vorgehensweise: Entwerfen von Abfragen und Sichten (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
[Verwenden von Daten im Ergebnisbereich (Visual Database Tools)](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
  
