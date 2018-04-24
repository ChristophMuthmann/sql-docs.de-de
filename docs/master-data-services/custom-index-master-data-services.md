---
title: Benutzerdefinierter Index (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c57bf8b8-55a6-4b6c-9adb-91b5f4f1ee3c
caps.latest.revision: 9
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ddcb1f8799cd3428981003a9c7996c3b86061425
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="custom-index-master-data-services"></a>Benutzerdefinierter Index (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen eines Indexes|[Erstellen eines Indexes &#40;Master Data Services&#41;](../master-data-services/create-an-index-master-data-services.md)|  
|Bearbeiten und Löschen eines Indexes|[Bearbeiten und Löschen eines Indexes &#40;Master Data Services&#41;](../master-data-services/edit-and-delete-an-index-master-data-services.md)|  
  
  
