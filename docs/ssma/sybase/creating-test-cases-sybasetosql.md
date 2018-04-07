---
title: Erstellen von Testfällen (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester component,Test Case Wizard
ms.assetid: b52dfd93-95af-4299-bc8f-83f2a7a6a518
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0647f807a6a28eb1dc450d3e38b2e591f1b51dd2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="creating-test-cases-sybasetosql"></a>Erstellen von Testfällen (SybaseToSQL)
Verwenden Sie den Testfall-Assistenten, um einen Test zu erstellen. Mit diesem Assistenten können Sie die Testfälle erstellen, durch Auswahl von Objekten überprüft und getestet, und geben Sie die Parameter testen.  
  
## <a name="starting-the-test-case-wizard"></a>Starten des Assistenten für Testfall  
Starten Sie den Testfall-Assistenten klicken Sie auf **neue Testfall...** aus der **Tester** Menü.  
  
Beim Starten überprüft des Assistenten für die Datenbank ssmatester2005db oder ssmatester2008db (je nach Projekttyp) auf dem Quellserver für die Sybase. Es ist der Tester Erweiterungsschema zum Speichern von erweiterten Objekten verwendet. Der Assistent Testfall ssmatester2005db oder ssmatester2008db gefunden, wird ein Dialogfenster, die zum Erstellen der Tester Erweiterung Datenbank vorgeschlagen werden angezeigt. (Diese Situation tritt in der Regel während der ersten Ausführung von SSMA Tester.)  
  
Wenn Sie im Dialogfenster erhalten, klicken Sie auf **Ja** Sybase Tester-Datenbank auf dem Quellserver zu erstellen. Anschließend wird ein neues Dialogfeld angezeigt, in dem Sie ein oder mehrere Geräte für die neue Datenbank der Tester zu suchen hinzufügen sollten. Klicken Sie auf **hinzufügen** zum Hinzufügen eines Geräts. In der **Zuordnung von Speicherplatz für Tester Datenbank** Dialogfeld Wählen Sie das Gerät, und geben Sie die Größe von Tester-Datenbank verwendet. Darüber hinaus können Sie die separaten Medium für die Protokolle zu Datenbank festlegen. Beachten Sie, dass Sie Sybase-Berechtigungen zum Erstellen von Datenbanken verfügen müssen.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Übersicht über das Erstellen von Testfällen, die mithilfe des Assistenten  
Das Verfahren zum Erstellen eines Testfalls besteht aus fünf Schritten:  
  
1.  [Initialisieren von Testfällen &#40;SybaseToSQL&#41;](../../ssma/sybase/initializing-test-cases-sybasetosql.md).  
  
2.  [Auswählen und Konfigurieren von Objekten mit Test &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md).  
  
3.  [Auswählen und Konfigurieren von betroffene Objekte &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md).  
  
4.  [Anpassen der Reihenfolge der Aufrufe &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md).  
  
5.  [Abschließen des Testfalls Vorbereitung &#40;SybaseToSQL&#41;](../../ssma/sybase/finishing-test-case-preparation-sybasetosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Testen von Datenbankobjekten migriert &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
