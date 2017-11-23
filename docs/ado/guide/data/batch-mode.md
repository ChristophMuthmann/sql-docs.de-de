---
title: Batch-Modus | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f763d43aed3312a87fb4c4a16b3ad28b77f0efaf
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="batch-mode"></a>Batchmodus
Batchmodus im Endeffekt dasselbe ist bei der **LockType** -Eigenschaftensatz auf **AdLockBatchOptimistic** und BatchUpdates wird vom Anbieter unterstützt. Bestimmte Einstellungen für den Sperren sind nicht verfügbar, abhängig von der Cursorposition. Z. B. eine eingeschränkte Sperrtyp ist nicht verfügbar, wenn die **CursorLocation** festgelegt ist, um **AdUseClient**. Im Gegensatz dazu kann kein Anbieter optimistische unterstützt, wenn die Cursorposition auf dem Server befindet. Sie sollten Batchaktualisierung mit einem Keyset oder static-Cursor verwenden.  
  
 Die **UpdateBatch** Methode wird verwendet, um das Senden von **Recordset** Änderungen in den Kopierpuffer frei, die an den Server zum Aktualisieren der Datenquelle. Im folgenden Abschnitt, öffnen wir eine **Recordset** im Batchmodus, nehmen Sie Änderungen an den Kopierpuffer, und senden Sie unsere Änderungen an der mit der Datenquelle, die über einen Aufruf an **UpdateBatch**.  
  
 Dieser Abschnitt enthält die folgenden Themen:  
  
-   [Senden der Updates: UpdateBatch-Methode](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtern nach aktualisierten Datensätzen](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Umgang mit fehlerhaften Updates](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Erkennen und Lösen von Konflikten](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Trennen und erneutes Herstellen einer Verbindung des Recordsets](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Aktualisieren von verknüpften Ergebnissen: Eindeutige Tabelle](../../../ado/guide/data/updating-joined-results-unique-table.md)
