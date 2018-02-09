---
title: "Der Microsoft Cursor Service für OLE DB | Microsoft Docs"
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
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5dd9f4b279bd38028bb529dcdd0a49f32ffd7cc7
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>Der Dienst Microsoft Cursor für OLE DB
Wenn Sie einen clientseitigen Cursor auswählen, oder legen Sie die **CursorLocation** Eigenschaft **AdUseClient**, rufen Sie die Microsoft-Cursordiensts für OLE DB. Sehen Sie möglicherweise auch Verweise auf "Client Cursormoduls" also im Wesentlichen die gleiche Botschaft ADO-Kontext. Dieser Dienst ergänzt die cursorunterstützung Funktionen von Datenanbietern. Daher können Sie die relativ einheitliche Funktionalität von allen Datenanbietern wahrnehmen.  
  
 Der Cursor-Dienst für OLE DB stellt dynamische Eigenschaften zur Verfügung und verbessert das Verhalten bestimmter Methoden. Z. B. die **optimieren** dynamische Eigenschaft ermöglicht das Erstellen temporärer Indizes, um bestimmte Vorgänge wie z. B. erleichtern die **suchen** Methode.  
  
 Der Cursor-Dienst ermöglicht die Unterstützung für BatchUpdates in allen Fällen. Es simuliert auch leistungsfähigere Cursortypen, wie dynamische Cursor, wenn ein Datenanbieter nur weniger leistungsfähige Cursor, wie statische Cursor bereitstellen kann.  
  
## <a name="see-also"></a>Siehe auch  
 [Microsoft Cursordiensts für OLE DB (ADO-Dienstkomponente)](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
