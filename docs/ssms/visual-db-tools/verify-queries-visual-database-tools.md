---
title: "Überprüfen von Abfragen (Visual Database Tools) | Microsoft-Dokumentation"
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
f1_keywords: vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8a9f8c5c3c3ae2bf057284bbc10b97737b664eb
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="verify-queries-visual-database-tools"></a>Überprüfen von Abfragen (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Um Probleme zu vermeiden, können Sie die erstellte Abfrage auf richtige Syntax überprüfen. Diese Option ist insbesondere dann nützlich, wenn Sie Anweisungen im [SQL-Bereich](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)eingeben.  
  
Einige Hinweise, die beim Überprüfen von Abfragen bedacht werden sollten:  
  
-   Eine Anweisung kann gültig und daher problemlos überprüfbar sein, auch wenn sie sich im **Diagrammbereich** und **Kriterienbereich**nicht darstellen lässt.  
  
-   Bei einer SQL-Überprüfung werden einige, aber möglicherweise nicht alle SQL-Fehler erkannt. Wenn eine Abfrage einen bei der SQL-Überprüfung nicht erkannten Fehler enthält, erkennt die Datenbank den Fehler beim Ausführen der Abfrage.  
  
-   Abfragen, die Parameter enthalten, können nicht überprüft werden.  
  
### <a name="to-verify-an-sql-statement"></a>So überprüfen Sie eine SQL-Anweisung  
  
-   Klicken Sie mit der rechten Maustaste in den **SQL-Bereich**, und wählen Sie im Kontextmenü den Befehl **SQL-Syntax überprüfen** aus.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Ausführen von Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/run-queries-visual-database-tools.md)  
[Ausführen grundlegender Vorgänge mit Abfragen &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
