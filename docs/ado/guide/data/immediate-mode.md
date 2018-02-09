---
title: Unmittelbarer Modus | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], immediate mode
- immediate mode [ADO]
- updating data [ADO], immediate mode
ms.assetid: 31fc53d0-97de-4315-a87b-3bf5cdd1f432
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f737d3b05e27eff7aae0aa95ee336a054c38f29f
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="immediate-mode"></a>Unmittelbarer Modus
Unmittelbarer Modus im Endeffekt dasselbe ist bei der **LockType** -Eigenschaftensatz auf **AdLockOptimistic** oder **AdLockPessimistic**. In unmittelbarer Modus sind Änderungen zu einem Datensatz mit der Datenquelle weitergegeben, sobald Sie die Arbeit in einer Zeile abgeschlossen durch Aufrufen von deklarieren die **Update** Methode.  
  
## <a name="calling-update"></a>Aufrufen von Update  
 Wenn Sie aus dem Datensatz verschieben Sie hinzufügen oder bearbeiten Sie vor dem Aufruf der **Update** , ADO wird automatisch-Methodenaufruf **Update** um die Änderungen zu speichern. Rufen Sie die **CancelUpdate** Methode vor der Navigation, wenn Sie "Abbrechen" Alle Änderungen an den aktuellen Datensatz oder einen neu hinzugefügten Datensatz verwerfen möchten.  
  
 Der aktuelle Datensatz bleibt der aktuelle nach dem Aufruf der **Update** Methode.  
  
## <a name="cancelupdate"></a>CancelUpdate  
 Verwenden der **CancelUpdate** -Methode Abbrechen von Änderungen an der aktuellen Zeile oder eine neu hinzugefügte Zeile zu verwerfen. Änderungen an der aktuellen Zeile oder eine neue Zeile kann nicht abgebrochen werden, nach dem Aufruf der **Update** -Methode, es sei denn, die Änderungen entweder Teil einer Transaktion sind, die Sie mit Rollback können die **RollbackTrans** -Methode oder einen Teil des einem BatchUpdate. Sie können bei einem BatchUpdate Abbrechen der **aktualisieren** mit der **CancelUpdate** oder **CancelBatch** Methode.  
  
 Wenn Sie eine neue Zeile, beim Aufrufen Hinzufügen der **CancelUpdate** -Methode, zur aktiven Zeile wird die Zeile, die vor dem aktuellen wurde die **AddNew** aufrufen.  
  
 Wenn Sie nicht die aktuelle Zeile geändert oder eine neue Zeile hinzugefügt haben, beim Aufrufen der **CancelUpdate** Methode wird ein Fehler generiert.
