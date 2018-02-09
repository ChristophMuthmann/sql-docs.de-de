---
title: Recordset dynamischen Eigenschaften in XML | Microsoft Docs
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
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 221ecdff804539bf8ff80335c71f762cbe7b28de
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="recordset-dynamic-properties-in-xml"></a>Recordset dynamischen Eigenschaften in XML
Die folgenden Recordset anbieterspezifische Eigenschaften (aus der Client-Cursormoduls) werden derzeit in der XML-Format gespeichert:  
  
-   Aktualisieren Sie die erneute Synchronisierung  
  
-   Eindeutige Tabelle  
  
-   Eindeutiges Schema  
  
-   Eindeutige Katalog  
  
-   Resync-Befehl  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeout  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   Umstrukturieren von Namen  
  
-   AutoRecalc  
  
 Diese Eigenschaften werden als Attribute der Elementdefinition für das Recordset persistent gespeichert wird, im Schemaabschnitt gespeichert. Diese Attribute sind in der Rowset-Schemanamespace definiert und müssen haben das Präfix "Rs:".  
  
## <a name="see-also"></a>Siehe auch  
 [Beibehalten von Datensätzen im XML-Format](../../../ado/guide/data/persisting-records-in-xml-format.md)
