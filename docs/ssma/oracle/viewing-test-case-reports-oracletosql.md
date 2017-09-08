---
title: "Anzeigen von Berichten für Testfall (OracleToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99ee650698adb2536ebdcadf480ae0ccefda2628
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="viewing-test-case-reports-oracletosql"></a>Anzeigen von Berichten für Testfall (OracleToSQL)
Der Testfall-Bericht zeigt die Testergebnisse für die Überprüfung und allgemeine Testinformationen. Im Fall eines Testfehlers abgebrochen werden Informationen über alle nicht übereinstimmenden Daten in Objekten überprüft auch angezeigt.  
  
## <a name="report-structure"></a>Berichtsstruktur  
Der Anfang des Berichts zeigt diese Statistiken:  
  
-   Die Gesamtanzahl der getestete Objekte und die Anzahl der Objekte, die für die der Test erfolgreich war.  
  
-   Die Gesamtanzahl der überprüften Tabellen und Fremdschlüssel, und die Anzahl der Tabellen und Fremdschlüssel erfolgreich abgeglichen.  
  
-   Die Startzeit, Endzeit des Testfalls und die Gesamtzeit für die Ausführung.  
  
Der Rest des Berichts werden die Informationen in vier Kategorien unterteilt:  
  
**Erforderliche Komponenten Fehler**  
Zeigt Fehler an die **Voraussetzungen Schritt.** Normalerweise wird sie übersprungen.  
  
**Initialisierung**  
Zeigt den Status der Ausführung als **Erfolg** oder **Fehler**.  
  
**Testergebnis-Objekte**  
Ein Vergleich von Ergebnissen (Erfolg oder Fehler) und der stimmen nicht überein, die bei einem Ausfall SSMA Tester erkannt.  
  
**Der Abschluss**  
Zeigt den Status der Ausführung als **Erfolg** oder **Fehler**.  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen von Testfällen &#40; OracleToSQL &#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testen von migriert Datenbankobjekte &#40; OracleToSQL &#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  

