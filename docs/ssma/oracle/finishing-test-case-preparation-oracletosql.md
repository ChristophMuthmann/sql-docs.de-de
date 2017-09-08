---
title: "Abschließen des Testfalls Vorbereitung (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 32f38713-7ae4-48d3-980d-74cadc8545a0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92bb189027afd6c5e91428017c5aa356676d575c
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="finishing-test-case-preparation-oracletosql"></a>Testfall zur Vorbereitung (OracleToSQL) beenden
Letzte Seite des Assistenten zeigt den Testfall Beschreibung und die Informationen zu Objekten, die am Test Beteiligter. Darüber hinaus können auf dieser Seite des Tests Ausführungsoptionen festlegen.  
  
Die **Testfall Informationen** Abschnitt wird gezeigt, Testfall Name und Beschreibung.  
  
Die **Objekte ausgewählt, getestet werden** Abschnitt enthält die benannte Liste der getesteten Objekte, gruppiert nach Objekttyp.  
  
Die **Objekte betroffen von Tests, dass analysiert** Abschnitt zeigt die benannte Liste von Objekten, die die Änderungen der Daten nach der Ausführung der getesteten Objekte verglichen werden sollen.  
  
## <a name="test-case-settings"></a>Testfall-Einstellungen  
In der **Testfall Einstellungen** Abschnitt können Sie die folgenden Ausführung Testoptionen festlegen:  
  
### <a name="stop-test-execution-after-first-failure"></a>Die Ausführung des Tests nach dem ersten Fehler beenden  
Gibt an, um den Test zu unterbrechen, wenn während der Ausführung des Tests ein Fehler auftritt.  
  
-   Falls gewünscht **Ja**, testen Sie Ausführung unterbrochen, wenn ein Fehler auftritt.  
  
-   Falls gewünscht **keine**, Ausführung des Tests nach einem Fehler fortgesetzt wird.  
  
### <a name="perform-data-rollback"></a>Ausführen von Rollbacks für Daten  
Ermöglicht die automatische Rollback nach Ausführung des Tests.  
  
-   Falls gewünscht **Ja**, Änderungen der Daten nach der Ausführung des Tests geht verloren.  
  
-   Falls gewünscht **keine**, alle testausführung datenänderungen werden gespeichert.  
  
### <a name="auxiliary-tables-saving-mode"></a>Erweiterungstabellen Modus speichern  
Definiert den speichern für Erweiterungstabellen erstellt während der Ausführung des Tests. Siehe die Beschreibung der Erweiterungstabellen in der [Ausführen von Testfällen &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md) Thema.  
  
-   Bei Auswahl des **immer speichern**, Erweiterungstabellen Daten werden immer für die spätere Verwendung gespeichert werden.  
  
-   Bei Auswahl des **speichern, wenn die Tabelle Vergleich fehlgeschlagen**, Erweiterungstabellen Daten werden gespeichert werden, nur, wenn ein Fehler auftritt.  
  
-   Bei Auswahl des **immer löschen**, Erweiterungstabellen immer nach Ausführung des Tests gelöscht.  
  
-   Bei Auswahl des **Benutzer bitten, wenn Tabelle Vergleich fehlgeschlagen**, der Benutzer kann die erforderliche Aktion auswählen, wenn ein Fehler auftritt.  
  
Klicken Sie auf die **Fertig stellen** Schaltfläche zum Speichern des vorbereiteten Testfalls in [mithilfe von Test-Repositorys (OracleToSQL)](http://msdn.microsoft.com/en-us/f941cce4-d3e3-4aeb-a88a-4f101a97a9f4).  
  
## <a name="see-also"></a>Siehe auch  
[Mithilfe von Test-Repositorys &#40; OracleToSQL &#41;](../../ssma/oracle/using-test-repositories-oracletosql.md)  
[Ausführen von Testfällen &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testen von migriert Datenbankobjekte &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

