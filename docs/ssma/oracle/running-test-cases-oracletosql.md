---
title: "Ausführen von Testfällen (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc208cdb-7373-4f6b-8f6c-cdff9d3dcd02
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 8fd2e06a9d9dcaa243876638f405bcc78c6a9d33
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="running-test-cases-oracletosql"></a>Ausführen von Testfällen (OracleToSQL)
Wenn SSMA Tester einen Testfall ausgeführt wird, führt die Objekte, die zu Testzwecken ausgewählt und erstellt einen Bericht über die Ergebnisse der Überprüfung. Wenn die Ergebnisse auf beiden Plattformen identisch sind, war der Test erfolgreich. Die Entsprechung von Objekten zwischen Oracle und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] richtet sich danach die schemazuordnung Einstellungen für das aktuelle SSMA-Projekt.  
  
Für einen erfolgreichen Test zwingend erforderlich ist, dass alle Oracle Objekte konvertiert und in die Zieldatenbank geladen. Darüber hinaus sollte die Tabellendaten migriert werden, damit der Inhalt der Tabellen auf beiden Plattformen synchronisiert werden.  
  
## <a name="run-test-case"></a>Testfall ausführen  
So führen Sie die vorbereiteten Testfall aus:  
  
1.  Klicken Sie auf die **ausführen** Schaltfläche.  
  
2.  In der **Connect to Oracle** (Dialogfeld), geben Sie die Verbindungsinformationen, und klicken Sie dann auf **verbinden**.  
  
Wenn der Test abgeschlossen ist, ist der Testfall Bericht erstellt. Klicken Sie auf die **Bericht** Schaltfläche zum Anzeigen der [Testfall Bericht](http://msdn.microsoft.com/en-us/8da14323-9dd6-4019-bf79-3e8b972a9bc0). Das Ergebnis des Tests (Bericht "Testfall") werden automatisch gespeichert, der [Ergebnisrepository](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4) zur späteren Verwendung.  
  
## <a name="test-case-execution-steps"></a>Testfall Ausführungsschritte folgen  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
SSMA-Tester wird überprüft, ob alle erforderlichen Komponenten für die Ausführung des Tests vor Beginn des Tests erfüllt sind. Wenn bestimmte Bedingungen nicht erfüllt sind, wird eine Fehlermeldung angezeigt.  
  
### <a name="initialization"></a>Initialisierung  
In diesem Schritt erstellt SSMA Tester zusätzliche Objekte (Tabellen, Trigger und Sichten) in der Oracle-Server SSMATESTER_ORACLE Schema. Sie ermöglichen Tracing-Änderungen in die betroffenen Objekte, die für die Überprüfung ausgewählt.  
  
Wird davon ausgegangen Sie, dass die überprüfte Tabelle USER_TABLE heißt. Bei einer Tabelle werden die folgenden zusätzlichen Objekte in Oracle erstellt.  
  
||||  
|-|-|-|  
|Name|Typ|Description|  
|USER_TABLE$ "TRG"|Trigger (trigger)|Trigger, der die Änderungen in der überprüften Tabelle überwachen.|  
|USER_TABLE$ AUD|table|Die Tabelle, in dem überschriebene, und gelöschte Zeilen gespeichert werden.|  
|USER_TABLE$ AUDID|table|Die Tabelle, in dem neue und geänderte Zeilen gespeichert werden.|  
|USER_TABLE|Ansicht|Vereinfachte Darstellung der tabellenänderungen.|  
|NEUE USER_TABLE$|Ansicht|Vereinfachte Darstellung der eingefügten Zeilen überschrieben.|  
|USER_TABLE$ NEW_ID|Ansicht|Kennung des eingefügten und geänderten Zeilen.|  
|USER_TABLE$ ALTE|Ansicht|Vereinfachte Darstellung der Zeilen gelöscht und überschrieben.|  
  
Das folgende Objekt wird erstellt, in das Schema der überprüften Tabelle am [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
||||  
|-|-|-|  
|Name|Typ|Description|  
|USER_TABLE$ "TRG"|Trigger (trigger)|Trigger, der die Änderungen in der überprüften Tabelle überwachen.|  
  
Und die folgenden Objekte werden erstellt am [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]in der Datenbank Ssmatesterdb.  
  
||||  
|-|-|-|  
|Name|Typ|Description|  
|USER_TABLE$ Aud|table|Die Tabelle, in dem überschriebene, und gelöschte Zeilen gespeichert werden.|  
|USER_TABLE$ AudID|table|Die Tabelle, in dem neue und geänderte Zeilen gespeichert werden.|  
|USER_TABLE|Ansicht|Vereinfachte Darstellung der tabellenänderungen.|  
|USER_TABLE$ neue|Ansicht|Vereinfachte Darstellung der eingefügten Zeilen überschrieben.|  
|USER_TABLE$ new_id|Ansicht|Kennung des eingefügten und geänderten Zeilen.|  
|USER_TABLE$ alte|Ansicht|Vereinfachte Darstellung der Zeilen gelöscht und überschrieben.|  
  
### <a name="test-object-calls"></a>Testen der Aufrufe  
SSMA-Tester an diesem Punkt ruft jedes Objekt, das für die Tests ausgewählt, vergleichen Sie die Ergebnisse und zeigt den Bericht.  
  
### <a name="finalization"></a>Der Abschluss  
Während der Finalisierung bereinigt SSMA Tester die zusätzlichen Objekte erstellt, auf die **Initialisierung** Schritt.  
  
## <a name="next-step"></a>Nächster Schritt  
[Anzeigen von Berichten Testfall &#40; OracleToSQL &#41;](../../ssma/oracle/viewing-test-case-reports-oracletosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Auswählen und Konfigurieren von Objekten zum Test &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
[Auswählen und Konfigurieren von betroffenen Objekten &#40; OracleToSQL &#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
[Testen von migriert Datenbankobjekte &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
