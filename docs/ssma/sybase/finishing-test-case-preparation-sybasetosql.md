---
title: "Abschließen des Testfalls Vorbereitung (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Tester Component,Test Case Settings
ms.assetid: 8b2a49b0-4296-4f3f-9e56-323aa6a6fa8e
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0eec311acd9250b8bc5224e7bba46a4035f3f98
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="finishing-test-case-preparation-sybasetosql"></a>Testfall zur Vorbereitung (SybaseToSQL) beenden
Letzte Seite des Assistenten zeigt den Testfall Beschreibung und die Informationen zu Objekten, die am Test Beteiligter. Darüber hinaus können auf dieser Seite des Tests Ausführungsoptionen festlegen.  
  
Die **Testfall Informationen** Abschnitt wird gezeigt, Testfall Name und Beschreibung.  
  
Die **Testobjekten** Abschnitt enthält die benannte Liste der getesteten Objekte, gruppiert nach Objekttyp.  
  
Die **Affected Objects zu analysierenden** Abschnitt zeigt die benannte Liste von Objekten, die die Änderungen der Daten nach der Ausführung der getesteten Objekte verglichen werden sollen.  
  
## <a name="test-case-settings"></a>Testfall-Einstellungen  
In der **Testfall Einstellungen** Abschnitt können Sie die folgenden Ausführung Testoptionen festlegen:  
  
### <a name="stop-test-execution-after-first-failure"></a>Die Ausführung des Tests nach dem ersten Fehler beenden  
Gibt an, um den Test zu unterbrechen, wenn während der Ausführung des Tests ein Fehler auftritt.  
  
-   Falls gewünscht **Ja**, testen Sie Ausführung unterbrochen, wenn ein Fehler auftritt.  
  
-   Falls gewünscht **keine**, Ausführung des Tests nach einem Fehler fortgesetzt wird.  
  
### <a name="perform-data-rollback"></a>Ausführen von Rollbacks für Daten  
Aktivieren Sie automatische Rollback, nach der Ausführung des Tests.  
  
-   Falls gewünscht **Ja**, Änderungen der Daten nach der Ausführung des Tests geht verloren.  
  
-   Falls gewünscht **keine**, alle testausführung datenänderungen werden gespeichert.  
  
### <a name="auxiliary-tables-saving-mode"></a>Erweiterungstabellen Modus speichern  
Definiert den speichern für Erweiterungstabellen erstellt während der Ausführung des Tests. Siehe die Beschreibung der Erweiterungstabellen in der [Ausführen von Testfällen &#40; SybaseToSQL &#41; ](../../ssma/sybase/running-test-cases-sybasetosql.md) Thema.  
  
-   Bei Auswahl des **immer speichern**, Erweiterungstabellen Daten werden immer für die spätere Verwendung gespeichert werden.  
  
-   Bei Auswahl des **speichern, wenn die Tabelle Vergleich fehlgeschlagen**, Erweiterungstabellen Daten werden gespeichert werden, nur, wenn ein Fehler auftritt.  
  
-   Bei Auswahl des **immer löschen**, Erweiterungstabellen immer nach Ausführung des Tests gelöscht.  
  
-   Bei Auswahl des **Benutzer bitten, wenn Tabelle Vergleich fehlgeschlagen**, der Benutzer kann die erforderliche Aktion auswählen, wenn ein Fehler auftritt.  
  
Klicken Sie auf die **Fertig stellen** Schaltfläche zum Speichern des vorbereiteten Testfalls in [mithilfe von Test-Repositorys &#40; SybaseToSQL &#41; ](../../ssma/sybase/using-test-repositories-sybasetosql.md).  
  
## <a name="see-also"></a>Siehe auch  
[Mithilfe der Test-Repositorys &#40; SybaseToSQL &#41;](../../ssma/sybase/using-test-repositories-sybasetosql.md)  
[Ausführen von Testfällen &#40; SybaseToSQL &#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testen von migriert Datenbankobjekte &#40; SybaseToSQL &#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
