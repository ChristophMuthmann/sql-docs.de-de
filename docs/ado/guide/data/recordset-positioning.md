---
title: Positionieren von Recordset | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
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
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28dcc44f38c763056a7a7f78979eee4f6de7df48
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="recordset-positioning"></a>Positionieren von Recordsets
Verwenden der **AbsolutePosition** -Eigenschaft verschieben auf einen Datensatz basierend auf ihre Ordnungsposition in der **Recordset** -Objekt, oder die Ordnungsposition des aktuellen Datensatzes ermitteln möchten. Der Anbieter muss die entsprechende Funktionalität für diese Eigenschaft verfügbar sein unterstützen.  
  
 **AbsolutePosition** ist 1-basiert und entspricht 1, wenn der aktuelle Datensatz der erste Datensatz im ist die **Recordset**. Wie bereits erwähnt, erhalten Sie die Gesamtanzahl von Datensätzen in der **Recordset** -Objekt aus der **RecordCount** Eigenschaft.  
  
 Beim Festlegen der **AbsolutePosition** -Eigenschaft, auch wenn es sich um einen Datensatz im aktuellen Cache ist ADO lädt den Cache mit einer neuen Gruppe von Datensätzen, die mit dem angegebenen Datensatz ab. Die **CacheSize** Eigenschaft bestimmt die Größe dieser Gruppe.  
  
> [!NOTE]
>  Verwenden Sie nicht die **AbsolutePosition** ein Ersatzzeichen Datensatznummer-Eigenschaft. Die Position eines bestimmten Datensatzes ändert, wenn Sie einen vorherigen Datensatz zu löschen. Auch ist es keine Garantie dafür, dass ein bestimmter Datensatz die gleiche hat **AbsolutePosition** Wenn die **Recordset** Objekt erneut abgefragt oder geöffnet wird. Lesezeichen sind die empfohlene Art, an einer bestimmten Position zurückgegeben, und sind die einzige Möglichkeit der Positionierung für alle Typen von **Recordset** Objekte.
