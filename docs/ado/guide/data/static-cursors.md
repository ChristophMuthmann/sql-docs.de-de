---
title: Statische Cursor | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fd0ace9aabf10c2b7e5b34d28bd54dbde84cfd0a
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="static-cursors"></a>Statische Cursor
Der statische Cursor zeigt immer das Resultset, wie dem ersten Öffnen des Cursors wurde. Statische Cursor je nach Implementierung, sind entweder nur-Lese oder Lese-/Schreibzugriff, und geben Sie einen Bildlauf vorwärts und rückwärts. Der statische Cursor erkennt in der Regel keine Änderungen an der Mitgliedschaft, Reihenfolge oder Werte des Resultsets nach dem Öffnen des Cursors. Statische Cursor erkennt möglicherweise eigene Updates, löschungen und einfügungen, obwohl sie nicht dazu erforderlich sind.  
  
 Statische Cursor erkennen nie andere aktualisiert, gelöscht und fügt ein. Nehmen wir beispielsweise an ein statischer Cursor abruft, eine Zeile und einer anderen Anwendung wird diese Zeile aktualisiert. Wenn die Anwendung die Zeile aus der statische Cursor refetches, sind die Werte, die er angezeigt wird trotz der Änderungen, die von der anderen Anwendung unverändert. Alle Typen von Durchführen eines Bildlaufs werden unterstützt, aber Anbieter möglicherweise Lesezeichen möglicherweise nicht unterstützt.  
  
 Wenn Ihre Anwendung nicht erkennen, Daten geändert und erfordern, Durchführen eines Bildlaufs muss, ist der statische Cursor die beste Wahl. Verwenden Sie die **AdOpenStatic CursorTypeEnum** um anzugeben, dass Sie einen statischen Cursor in ADO verwenden möchten.  
  
## <a name="see-also"></a>Siehe auch  
 [Vorwärtscursor](../../../ado/guide/data/forward-only-cursors.md)   
 [KEYSET-Cursor](../../../ado/guide/data/keyset-cursors.md)   
 [Dynamische Cursor](../../../ado/guide/data/dynamic-cursors.md)

