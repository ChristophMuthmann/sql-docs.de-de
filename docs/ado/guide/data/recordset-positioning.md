---
title: Positionieren von Recordset | Microsoft Docs
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
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c65a8da00ea92feadc21d0fd1ce3a28967d9a259
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-positioning"></a>Positionieren von Recordsets
Verwenden der **AbsolutePosition** -Eigenschaft verschieben auf einen Datensatz basierend auf ihre Ordnungsposition in der **Recordset** -Objekt, oder die Ordnungsposition des aktuellen Datensatzes ermitteln möchten. Der Anbieter muss die entsprechende Funktionalität für diese Eigenschaft verfügbar sein unterstützen.  
  
 **AbsolutePosition** ist 1-basiert und entspricht 1, wenn der aktuelle Datensatz der erste Datensatz im ist die **Recordset**. Wie bereits erwähnt, erhalten Sie die Gesamtanzahl von Datensätzen in der **Recordset** -Objekt aus der **RecordCount** Eigenschaft.  
  
 Beim Festlegen der **AbsolutePosition** -Eigenschaft, auch wenn es sich um einen Datensatz im aktuellen Cache ist ADO lädt den Cache mit einer neuen Gruppe von Datensätzen, die mit dem angegebenen Datensatz ab. Die **CacheSize** Eigenschaft bestimmt die Größe dieser Gruppe.  
  
> [!NOTE]
>  Verwenden Sie nicht die **AbsolutePosition** ein Ersatzzeichen Datensatznummer-Eigenschaft. Die Position eines bestimmten Datensatzes ändert, wenn Sie einen vorherigen Datensatz zu löschen. Auch ist es keine Garantie dafür, dass ein bestimmter Datensatz die gleiche hat **AbsolutePosition** Wenn die **Recordset** Objekt erneut abgefragt oder geöffnet wird. Lesezeichen sind die empfohlene Art, an einer bestimmten Position zurückgegeben, und sind die einzige Möglichkeit der Positionierung für alle Typen von **Recordset** Objekte.
