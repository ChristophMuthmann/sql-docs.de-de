---
title: Cursortypen (ADO) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7c8ab039bfe5754587e3f7adda36c0b715138d65
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="types-of-cursors-ado"></a>Cursortypen (ADO)
Als allgemeine Regel sollte Ihre Anwendung den einfachsten Cursor verwenden den Zugriff erforderlichen Daten ermöglicht. Jedes Cursormerkmal zusätzliche, die Grundlagen (Vorwärtscursor, schreibgeschützte, statische, Durchführen eines Bildlaufs, ungepufferten) weist einen Preis – im Clientspeicher, Netzwerklast oder Leistung. In vielen Fällen generieren die Standardcursoroptionen einen komplexeren Cursor, als tatsächlich Ihre Anwendung benötigt.  
  
 Die Auswahl des Cursortyps hängt von dazu, wie die Anwendung das Resultset verwendet und auch mehrere entwurfsüberlegungen, u. a. die Größe des Resultsets, Prozentsatz der Daten, die zu verwendende vermutlich, Sensitivität gegenüber Änderungen der Daten und die Leistung der Anwendung Anforderungen an.  
  
 Ihrer Cursorauswahl hängt in seiner einfachsten, ob Sie müssen die Daten einfach anzeigen oder ändern:  
  
-   Wenn Sie nur einen Bildlauf durch einen Satz von Ergebnissen, jedoch keine Änderungsdaten müssen, verwenden Sie eine [Vorwärtscursor](../../../ado/guide/data/forward-only-cursors.md) oder [statische](../../../ado/guide/data/static-cursors.md) Cursor.  
  
-   Wenn Sie ein großes Resultset und müssen nur wenige Zeilen ausgewählt haben, verwenden Sie eine [Keyset](../../../ado/guide/data/keyset-cursors.md) Cursor.  
  
-   Wenn Sie synchronisieren möchten ein Resultset mit aktuellen hinzufügt, ändert und löscht alle gleichzeitigen Benutzer verwenden ein [dynamische](../../../ado/guide/data/dynamic-cursors.md) Cursor.  
  
 Obwohl alle Cursortypen unterscheiden, sollten Sie bedenken, dass diese Cursortypen nicht so viel Datenbankprodukte als einfach das Ergebnis der überlappende Merkmale und Optionen sind.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Vorwärtscursor](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [Statische Cursor](../../../ado/guide/data/static-cursors.md)  
  
-   [KEYSET-Cursor](../../../ado/guide/data/keyset-cursors.md)  
  
-   [Dynamische Cursor](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Vorwärtscursor](../../../ado/guide/data/forward-only-cursors.md)   
 [Statische Cursor](../../../ado/guide/data/static-cursors.md)   
 [KEYSET-Cursor](../../../ado/guide/data/keyset-cursors.md)   
 [Dynamische Cursor](../../../ado/guide/data/dynamic-cursors.md)
