---
title: Anzeigen von Berichten für Testfall (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8da14323-9dd6-4019-bf79-3e8b972a9bc0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 5a109a69e73f4ec556a3eef9981a0af67985d021
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
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
[Ausführen von Testfällen &#40;OracleToSQL&#41;](../../ssma/oracle/running-test-cases-oracletosql.md)  
[Testen von Datenbankobjekten migriert &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
