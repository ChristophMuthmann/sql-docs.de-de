---
title: Beibehalten von hierarchischen Recordsets | Microsoft Docs
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
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f86b9c6d133177464b994deb2e4299ee75808a75
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="persisting-hierarchical-recordsets"></a>Beibehalten von hierarchischen Recordsets
Sie können eine hierarchische speichern **Recordset** in eine Datei im ADTG oder XML-Format durch Aufrufen der [speichern](../../../ado/reference/ado-api/save-method.md) Methode. Gelten jedoch zwei Einschränkungen beim Speichern der hierarchischen **Recordset**s im XML-Format: Sie können im XML-Format speichern, wenn die hierarchische **Recordset** enthält ausstehende Updates, und Sie können nicht gespeichert werden eine parametrisierte hierarchische **Recordset**.  
  
 Weitere Informationen zum Strukturieren von Daten-Anbieter finden Sie unter [Microsoft-Datenstrukturierungsdiensts für OLE DB-](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) und [Überblick über die-Datenstrukturierungsdiensts für OLE DB-](http://msdn.microsoft.com/en-us/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)
