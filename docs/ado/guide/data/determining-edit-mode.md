---
title: Bestimmen des Bearbeitungsmodus | Microsoft Docs
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
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2730d4cec70b2cb29355e4e96742fed964d42900
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="determining-edit-mode"></a>Bestimmen des Bearbeitungsmodus
ADO verwaltet einen Bearbeitungspuffer mit dem aktuellen Datensatz verknüpft sind. Die **EditMode** Eigenschaft gibt an, ob Änderungen an diesen Puffer vorgenommen wurden oder ob ein neuer Datensatz erstellt wurde. Verwendung **EditMode** den Bearbeitungsstatus des aktuellen Datensatzes zu bestimmen. Sie können für ausstehende Änderungen testen, wenn ein Bearbeitungsprozess unterbrochen wurde und zu bestimmen, ob Sie benötigen die **Update** oder **CancelUpdate** Methode.  
  
 **EditMode** gibt eines der **EditModeEnum** Konstanten, die in der folgenden Tabelle aufgeführt sind.  
  
|Konstante|Description|  
|--------------|-----------------|  
|**adEditNone**|Gibt an, dass kein Bearbeitungsvorgang ausgeführt wird.|  
|**adEditInProgress**|Gibt an, dass die Daten im aktuellen Datensatz geändert, aber nicht gespeichert wurden.|  
|**adEditAdd**|Gibt an, dass die **AddNew** -Methode aufgerufen wurde, und der aktuelle Datensatz im Kopierpuffer ist ein neuer Datensatz, der nicht mit der Datenbank gespeichert wurde.|  
|**adEditDelete**|Gibt an, dass der aktuelle Datensatz gelöscht wurde.|  
  
 **EditMode** kann einen gültigen Wert zurückgeben, nur dann, wenn ein aktueller Datensatz vorhanden ist. **EditMode** gibt einen Fehler zurück, wenn **BOF** oder **EOF** ist **"true"** oder wenn der aktuelle Datensatz gelöscht wurde.
