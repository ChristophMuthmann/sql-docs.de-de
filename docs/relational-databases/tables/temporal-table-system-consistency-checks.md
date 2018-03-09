---
title: "Systemkonsistenzprüfungen von temporalen Tabellen | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ec081d42-57e4-43c7-9e1c-317ba8f23437
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cc854ba076a5f5a831beb5009bdd5c0e25f654c5
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="temporal-table-system-consistency-checks"></a>Systemkonsistenzprüfungen von temporalen Tabellen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Bei der Verwendung von temporaler Tabellen führt das System eine Reihe von Konsistenzprüfungen durch, um sicherzustellen, dass das Schema die Anforderungen an temporale Tabellen erfüllt, und dass die Daten konsistent sind und bleiben. Darüber hinaus wurden temporale Prüfungen zur **DBCC CHECKCONSTRAINTS** -Anweisung hinzugefügt.  
  
## <a name="system-consistency-checks"></a>Systemkonsistenzprüfungen  
 Bevor **SYSTEM_VERSIONING** auf **ON**festgelegt wird, wird eine Reihe von Überprüfungen für die Verlaufstabelle und die aktuelle Tabelle ausgeführt. Diese Überprüfungen werden in Schemaüberprüfungen und Datenüberprüfungen gruppiert (sofern die Tabelle nicht leer ist). Darüber hinaus führt das System auch eine Konsistenzprüfung der Laufzeit durch.  
  
### <a name="schema-check"></a>Schemaüberprüfung  
 Wenn eine temporale Tabelle erstellt oder eine vorhandene Tabelle dahingehend geändert wird, überprüft das System, ob die Anforderungen erfüllt werden:  
  
1.  Die Namen und die Anzahl der Spalten sind in der aktuellen Tabelle und der Verlaufstabelle identisch.  
  
2.  Die Datentypen jeder Spalte in der aktuellen Tabelle und der Verlaufstabelle entsprechen einander.  
  
3.  Die Zeitraumspalten wurden auf **NOT NULL**festgelegt.  
  
4.  Die aktuelle Tabelle besitzt eine Primärschlüsseleinschränkung, während die Verlaufstabelle keine Primärschlüsseleinschränkung aufweist.  
  
5.  Es wurden keine **IDENTITY** -Spalten in der Verlaufstabelle definiert.  
  
6.  Es wurden keine Trigger in der Verlaufstabelle definiert.  
  
7.  Es wurden keine Fremdschlüssel in der Verlaufstabelle definiert.  
  
8.  Es wurden keine Tabellen- oder Spalteneinschränkungen für die Verlaufstabelle definiert. Standardspaltenwerte sind für die Verlaufstabelle jedoch zulässig.  
  
9. Die Verlaufstabelle wird nicht in einer schreibgeschützten Dateigruppe platziert.  
  
10. Die Verlaufstabelle wurde nicht für die Änderungsnachverfolgung oder Change Data Capture konfiguriert.  
  
### <a name="data-consistency-check"></a>Datenkonsistenzprüfung  
 Bevor **SYSTEM_VERSIONING** auf **ON** festgelegt wird, führt das System die folgende Überprüfung durch: **SysEndTime** ≥**SysStartTime**. Sie wird auch im Rahmen jedes DML-Vorgangs durchgeführt.  
  
 Wenn Sie einen Link zu einer vorhandenen Verlaufstabelle erstellen, können Sie eine Datenkonsistenzprüfung durchführen. Diese Datenkonsistenzprüfung stellt sicher, dass vorhandene Einträge sich nicht überlappen, und dass temporale Anforderungen für jeden einzelnen Eintrag erfüllt werden. Die Datenkonsistenzprüfung ist standardmäßig aktiviert. Die Verwendung der Datenkonsistenzprüfung wird generell immer dann empfohlen, wenn Daten zwischen der aktuellen und der Verlaufstabelle möglicherweise nicht mehr synchronisiert sind. Dies geschieht z.B., wenn eine vorhandene Verlaufstabelle mit Verlaufsdaten aufgefüllt wird.  
  
> [!WARNING]  
>  Manuelle Änderungen an der Systemuhr führen zu unerwarteten Systemfehlern, da bei den Konsistenzprüfungen der Datenlaufzeit, die Überlappungsbedingungen verhindern sollen (d.h. dass die Endzeit für einen Eintrag nicht kleiner als die Startzeit ist), dass ein Fehler auftritt.  
  
## <a name="dbcc-checkconstraints"></a>DBCC CHECKCONSTRAINTS  
 Der Befehl **DBCC CHECKCONSTRAINTS** enthält Konsistenzprüfungen temporaler Daten. Weitere Informationen finden Sie unter [DBCC CHECKCONSTRAINTS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md).  
  
## <a name="did-this-article-help-you-were-listening"></a>Fanden Sie diesen Artikel nützlich? Wir hören Ihnen zu  
 Welche Informationen suchen Sie, und haben Sie sie gefunden? Wir nehmen uns Ihr Feedback zu Herzen, um unsere Inhalte zu verbessern. Bitte senden Sie Ihre Kommentare an [sqlfeedback@microsoft.com](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Temporal%20Table%20System%20Consistency%20Checks%20page)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Temporale Tabellen](../../relational-databases/tables/temporal-tables.md)   
 [Erste Schritte mit temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)   
 [Partitionierung mit temporären Tabellen](../../relational-databases/tables/partitioning-with-temporal-tables.md)   
 [Überlegungen und Einschränkungen zu temporalen Tabellen](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)   
 [Sicherheit bei temporale Tabellen](../../relational-databases/tables/temporal-table-security.md)   
 [Verwalten der Beibehaltung von Verlaufsdaten in temporalen Tabellen mit Systemversionsverwaltung](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)   
 [Temporale Tabellen mit Systemversionsverwaltung und speicheroptimierten Tabellen](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)   
 [Metadatenansichten und Funktionen für temporale Tabellen](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)  
  
  
