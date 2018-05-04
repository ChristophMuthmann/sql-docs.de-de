---
title: Ausführen von Testfällen (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Tester Component,Execution Steps
ms.assetid: 195ffdef-cfde-4bf4-a3ae-e7402bb07972
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4d6f735977f11940c1fb16837012062086ec2876
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="running-test-cases-sybasetosql"></a>Ausführen von Testfällen (SybaseToSQL)
Wenn SSMA Tester einen Testfall ausgeführt wird, führt die Objekte, die zu Testzwecken ausgewählt und erstellt einen Bericht über die Ergebnisse der Überprüfung. Wenn die Ergebnisse auf beiden Plattformen identisch sind, war der Test erfolgreich. Die Entsprechung von Objekten zwischen Sybase und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] richtet sich danach die schemazuordnung Einstellungen für das aktuelle SSMA-Projekt.  
  
Für einen erfolgreichen Test zwingend erforderlich ist, dass alle Sybase-Objekte konvertiert und in die Zieldatenbank geladen werden. Darüber hinaus sollte die Tabellendaten migriert werden, damit der Inhalt der Tabellen auf beiden Plattformen synchronisiert werden.  
  
## <a name="run-test-case"></a>Testfall ausführen  
So führen Sie die vorbereiteten Testfall aus:  
  
1.  Klicken Sie auf die **ausführen** Schaltfläche.  
  
2.  In der **Herstellen einer Verbindung mit der Sybase** (Dialogfeld), geben Sie die Verbindungsinformationen, und klicken Sie dann auf **verbinden**.  
  
Wenn der Test abgeschlossen ist, ist der Testfall Bericht erstellt. Klicken Sie auf die **Bericht** Schaltfläche zum Anzeigen der [Testfall Berichte anzeigen &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md). Das Ergebnis des Tests (Bericht "Testfall") werden automatisch gespeichert, der [mithilfe-Repositorys &#40;SybaseToSQL&#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md) zur späteren Verwendung.  
  
## <a name="test-case-execution-steps"></a>Testfall Ausführungsschritte folgen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
SSMA-Tester wird überprüft, ob alle erforderlichen Komponenten für die Ausführung des Tests vor Beginn des Tests erfüllt sind. Wenn bestimmte Bedingungen nicht erfüllt sind, wird eine Fehlermeldung angezeigt.  
  
### <a name="initialization"></a>Initialisierung  
An diesem Punkt SSMA-Tester zusätzlichen Objekte (Tabellen, Trigger und Sichten) sowohl auf die Sybase erstellt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie ermöglichen Tracing Änderungen in den betroffenen Tabellen, die für die Überprüfung ausgewählt werden, wenn Tabelle Vergleiche Modus ist **ändert nur**.  
  
Wird davon ausgegangen Sie, dass die überprüfte Tabelle USER_TABLE heißt. Bei einer Tabelle werden die folgenden zusätzlichen Objekte in Sybase erstellt.  
  
Die folgenden Objekte werden an Sybase erstellt, in der Datenbank SSMATESTER2005db oder SSMATESTER2008db und am [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in der Datenbank Ssmatesterdb_syb.  
  
|Name|Typ|Description|  
|--------|--------|---------------|  
|USER_TABLE$ "TRG"|Trigger|Trigger, der die Änderungen in der überprüften Tabelle überwachen.|  
|USER_TABLE$ Aud|Tabelle|Die Tabelle, in dem überschriebene, und gelöschte Zeilen gespeichert werden.|  
|USER_TABLE$ AudID|Tabelle|Die Tabelle, in dem neue und geänderte Zeilen gespeichert werden.|  
|USER_TABLE|Sicht|Vereinfachte Darstellung der tabellenänderungen.|  
|USER_TABLE$new|Sicht|Vereinfachte Darstellung der eingefügten Zeilen überschrieben.|  
|USER_TABLE$new_id|Sicht|Kennung des eingefügten und geänderten Zeilen.|  
|USER_TABLE$old|Sicht|Vereinfachte Darstellung der Zeilen gelöscht und überschrieben.|  
  
Das folgende Objekt wird in der überprüften Tabelle auf Sybase-Datenbank erstellt und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
|Name|Typ|Description|  
|--------|--------|---------------|  
|USER_TABLE$ "TRG"|Trigger|Trigger, der die Änderungen in der überprüften Tabelle überwachen.|  
  
### <a name="test-object-calls"></a>Testen der Aufrufe  
SSMA-Tester an diesem Punkt ruft jedes Objekt, das für die Tests ausgewählt, vergleichen Sie die Ergebnisse und zeigt den Bericht.  
  
### <a name="finalization"></a>Der Abschluss  
Während der Finalisierung bereinigt SSMA Tester die zusätzlichen Objekte erstellt, auf die **Initialisierung** Schritt.  
  
## <a name="next-step"></a>Nächster Schritt  
[Anzeigen von Berichten Testfall &#40;SybaseToSQL&#41;](../../ssma/sybase/viewing-test-case-reports-sybasetosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Auswählen und Konfigurieren von Objekten mit Test &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-objects-to-test-sybasetosql.md)  
[Auswählen und Konfigurieren von betroffene Objekte &#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
[Testen von Datenbankobjekten migriert &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
