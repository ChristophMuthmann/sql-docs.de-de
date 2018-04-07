---
title: Anzeigen von Berichten für Testfall (SybaseToSQL) | Microsoft Docs
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
- Tester Component,Test Case Reports
ms.assetid: cb75d281-43ef-4f4a-b754-2c4ee3b62ae7
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fe87892c50992968da7ada9b5a3b33a34442fbe6
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="viewing-test-case-reports-sybasetosql"></a>Anzeigen von Berichten für Testfall (SybaseToSQL)
Der Testfall-Bericht zeigt die Testergebnisse für die Überprüfung und allgemeine Testinformationen. Im Fall eines Testfehlers abgebrochen werden Informationen über alle nicht übereinstimmenden Daten in Objekten überprüft auch angezeigt.  
  
## <a name="report-structure"></a>Berichtsstruktur  
Der Anfang des Berichts zeigt diese Statistiken:  
  
-   Die Gesamtanzahl der getestete Objekte und die Anzahl der Objekte, die für die der Test erfolgreich war.  
  
-   Die Gesamtanzahl der überprüften Tabellen und Fremdschlüssel, und die Anzahl der Tabellen und Fremdschlüssel erfolgreich abgeglichen.  
  
-   Die Startzeit, Endzeit des Testfalls und die Gesamtzeit für die Ausführung.  
  
Der Rest des Berichts werden die Informationen in vier Kategorien unterteilt:  
  
**Erforderliche Komponenten Fehler**  
Zeigt Fehler an die **Voraussetzungen** Schritt. Normalerweise wird sie übersprungen.  
  
**Initialisierung**  
Zeigt den Status der Ausführung als **Erfolg** oder **Fehler**.  
  
**Testergebnis-Objekte**  
Ein Vergleich von Ergebnissen (Erfolg oder Fehler) und der stimmen nicht überein, die bei einem Ausfall SSMA Tester erkannt.  
  
**Der Abschluss**  
Zeigt den Status der Ausführung als **Erfolg** oder **Fehler**.  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen von Testfällen &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[Testen von Datenbankobjekten migriert &#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
