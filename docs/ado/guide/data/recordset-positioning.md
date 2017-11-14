---
title: Positionieren von Recordset | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: aee0d64d0fe1e310f42d79de36f5cf36c3813bf3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="recordset-positioning"></a>Positionieren von Recordsets
Verwenden der **AbsolutePosition** -Eigenschaft verschieben auf einen Datensatz basierend auf ihre Ordnungsposition in der **Recordset** -Objekt, oder die Ordnungsposition des aktuellen Datensatzes ermitteln möchten. Der Anbieter muss die entsprechende Funktionalität für diese Eigenschaft verfügbar sein unterstützen.  
  
 **AbsolutePosition** ist 1-basiert und entspricht 1, wenn der aktuelle Datensatz der erste Datensatz im ist die **Recordset**. Wie bereits erwähnt, erhalten Sie die Gesamtanzahl von Datensätzen in der **Recordset** -Objekt aus der **RecordCount** Eigenschaft.  
  
 Beim Festlegen der **AbsolutePosition** -Eigenschaft, auch wenn es sich um einen Datensatz im aktuellen Cache ist ADO lädt den Cache mit einer neuen Gruppe von Datensätzen, die mit dem angegebenen Datensatz ab. Die **CacheSize** Eigenschaft bestimmt die Größe dieser Gruppe.  
  
> [!NOTE]
>  Verwenden Sie nicht die **AbsolutePosition** ein Ersatzzeichen Datensatznummer-Eigenschaft. Die Position eines bestimmten Datensatzes ändert, wenn Sie einen vorherigen Datensatz zu löschen. Auch ist es keine Garantie dafür, dass ein bestimmter Datensatz die gleiche hat **AbsolutePosition** Wenn die **Recordset** Objekt erneut abgefragt oder geöffnet wird. Lesezeichen sind die empfohlene Art, an einer bestimmten Position zurückgegeben, und sind die einzige Möglichkeit der Positionierung für alle Typen von **Recordset** Objekte.

