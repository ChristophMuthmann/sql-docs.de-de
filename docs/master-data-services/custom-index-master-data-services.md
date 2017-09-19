---
title: Benutzerdefinierter Index (Master Data Services) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c57bf8b8-55a6-4b6c-9adb-91b5f4f1ee3c
caps.latest.revision: 9
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 2347f26d041c15142487420440a470f87a822e3e
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="custom-index-master-data-services"></a>Benutzerdefinierter Index (Master Data Services)
  Benutzerdefinierte Indizes erstellen einen nicht gruppierten Index mit einem Attribut (einzelner Index) oder eine Liste von Attributen (zusammengesetzter Index) in einer Entität. Im Allgemeinen verbessern Indizes die Leistung einer Abfrage. Weitere Informationen zu SQL Server-Indizes finden Sie unter [Indizes](../relational-databases/indexes/indexes.md).  
  
## <a name="type-of-indexes"></a>Indextypen  
 Sie können die folgenden Typen von benutzerdefinierten Indizes für jede Entität erstellen.  
  
-   Eindeutiger Index  
  
-   Nicht eindeutiger Index  
  
 Ein eindeutiger Index stellt sicher, dass die indizierten Spalten keine doppelten Werte enthalten. Für zusammengesetzte eindeutige Indizes stellt der Index sicher, dass jede Kombination von Werten in der Liste der ausgewählten Attribute eindeutig ist. Ein eindeutiger Index kann nicht erstellt werden, wenn doppelte Werte für die ausgewählten Attribute vorhanden sind.  
  
## <a name="rules"></a>Regeln  
 Die folgenden Regeln gelten sowohl für eindeutige als auch für nicht eindeutige benutzerdefinierte Indizes.  
  
-   Sie müssen mindestens ein Attribut auswählen, um einen benutzerdefinierten Index zu erstellen.  
  
-   Wenn Sie versuchen, einen Index zu speichern, der dieselbe Attributliste und dasselbe Eindeutigkeitsflag wie eine anderer Index enthält, kann der Index nicht gespeichert werden. Ein Fehler wird angezeigt.  
  
    > [!NOTE]  
    >  MDS erstellt automatisch Indizes mit bestimmten Attributen (z.B. DBAs und Code). Dies bedeutet, dass Sie keinen anderen Index erstellen können, der eines dieser Attribute und kein weiteres enthält.  
  
-   Attribute können in mehr als einem benutzerdefinierten Index aufgenommen werden, solange in den anderen Indizes mindestens ein Attribut vorhanden ist, das sich unterscheidet. Andernfalls sind die Indizes identisch.  
  
-   Wenn Sie einen Index erstellen, der viele oder große Attribute enthält, und die Gesamtgröße der ausgewählten Attribute die maximale Größe des Indexschlüssels (900 Byte) überschreitet, kann der Index nicht gespeichert werden.  
  
-   Ein benutzerdefinierter Index kann mit Attributen von Blattelementen erstellt werden, Dateiattribute ausgenommen.  
  
-   Wenn Sie ein Attribut aus einem benutzerdefinierten Index löschen möchten, gilt Folgendes.  
  
    -   Wenn der Index mit einem einzigen Attribut (einzelner Index) erstellt wird, werden sowohl das Attribut als auch der Index gelöscht.  
  
    -   Wenn der Index mit mehr als einem Attribut (zusammengesetzter Index) erstellt wird, kann das Attribut nicht gelöscht werden, bis Sie den Index bearbeiten.  
  
-   Der Typ eines Attributs in einem benutzerdefinierten Index kann nicht geändert werden.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen eines Indexes|[Erstellen eines Indexes &#40;Master Data Services&#41;](../master-data-services/create-an-index-master-data-services.md)|  
|Bearbeiten und Löschen eines Indexes|[Bearbeiten und Löschen eines Indexes &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)|  
  
  
