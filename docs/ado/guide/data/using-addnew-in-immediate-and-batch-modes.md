---
title: Mit Batch-Modi "und" AddNew im sofortigen | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- AddNew method [ADO]
- ADO, editing data
- ADO, adding data
- editing data [ADO], AddNew method
ms.assetid: ed314bb9-e188-4658-a68c-a2abc49610be
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 32d4298351d214912947ead9322fe1fc5a208eba
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-addnew-in-immediate-and-batch-modes"></a>Verwenden von Batch-Modi "und" AddNew im sofortigen
Das Verhalten von der **AddNew** Methode hängt vom Aktualisierungsmodus von der **Recordset** -Objekt und gibt an, ob Sie übergeben die *FieldList* und *Werte*Argumente.  
  
 Im sofortupdatemodus (in dem der Anbieter schreibt Änderungen in der zugrunde liegenden Datenquelle nach Aufrufen der **aktualisieren** Methode) wird beim Aufrufen der **AddNew** -Methode ohne Argumente legt die ** EditMode** Eigenschaft **AdEditAdd.** Der Anbieter werden alle Feld Wert ändert sich lokal zwischengespeichert. Aufrufen der **Update** Methode wird der neue Datensatz in der Datenbank und setzt die **EditMode** Eigenschaft **AdEditNone.** Wenn Sie übergeben die *FieldList* und *Werte* Argumente, ADO sofort wird der neue Datensatz in der Datenbank (keine **Update** Aufruf ist erforderlich); das **EditMode ** Eigenschaftswert ändert sich nicht (**AdEditNone**).  
  
 Im Batch Updatemodus Aufrufen der **AddNew** -Methode ohne Argumente legt die **EditMode** Eigenschaft, um **AdEditAdd**. Der Anbieter werden alle Feld Wert ändert sich lokal zwischengespeichert. Aufrufen der **Update** Methode fügt den neuen Eintrag mit dem aktuellen **Recordset** und setzt die **EditMode** Eigenschaft **AdEditNone**, aber der Anbieter nicht die Änderungen an der zugrunde liegenden Datenbank bereitstellen, erst nach dem Aufruf der **UpdateBatch** Methode. Wenn Sie übergeben der *FieldList* und *Werte* Argumente, ADO sendet den neuen Eintrag an den Anbieter für die Speicherung in einem Cache; aufrufen, müssen Sie die **UpdateBatch** Methode zum Bereitstellen der neuen Notieren Sie sich an den zugrunde liegenden Datenbank. Weitere Informationen zu **Update** und **UpdateBatch**, finden Sie unter [wird aktualisiert und Beibehalten von Daten](../../../ado/guide/data/updating-and-persisting-data.md).

