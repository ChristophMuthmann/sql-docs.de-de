---
title: Bestimmen des Bearbeitungsmodus | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], edit mode
- ADO, editing data
ms.assetid: 4c7e010d-08cd-4e22-9b32-23c36f02f88c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8557d0d514e37491a7d0952afcc14ae60d03d1ae
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
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
