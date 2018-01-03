---
title: Recordset dynamischen Eigenschaften in XML | Microsoft Docs
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
helpviewer_keywords: Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
caps.latest.revision: "3"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b05609621af12607d11448028fc48a940f531ee
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
