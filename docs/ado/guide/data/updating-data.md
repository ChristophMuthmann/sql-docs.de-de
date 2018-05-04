---
title: Aktualisieren von Daten | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f9979faafbccf87f2e410da7708b67d841fbf347
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data"></a>Aktualisieren von Daten
Updateverhalten und Funktionalität richtet sich größtenteils nach update-Modus (Sperrtyp), Cursortyp und Cursorposition.  
  
 Verwenden der **Update** Methode, um die Änderungen zu speichern, an der der aktuelle Datensatz vorgenommen wurden, eine **Recordset** Objekt seit dem Aufrufen der **AddNew** Methode oder seit alle Feldwerte ändern in einem vorhandenen Datensatz. Die **Recordset** Objekt muss Updates unterstützen.  
  
 Wenn die **Recordset** Objekt unterstützt BatchUpdates, mehrere Änderungen an einem oder mehreren Datensätzen können zwischengespeichert werden, lokal, bis Sie rufen die **UpdateBatch** Methode. Wenn Sie den aktuellen Datensatz bearbeiten oder Hinzufügen eines neuen Datensatzes beim Aufrufen der **UpdateBatch** Methode, ADO wird automatisch aufgerufen haben die **Update** Methode, um alle ausstehenden Änderungen in den aktuellen Datensatz vor dem Speichern die Übertragung von der zusammengefasste Änderungen an den Anbieter.  
  
 Der aktuelle Datensatz bleibt der aktuelle nach dem Aufruf der **Update** oder **UpdateBatch** Methoden.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Immediate Mode (Immediate-Modus)](../../../ado/guide/data/immediate-mode.md)  
  
-   [Batchmodus](../../../ado/guide/data/batch-mode.md)  
  
-   [Transaktionsverarbeitung](../../../ado/guide/data/transaction-processing.md)
