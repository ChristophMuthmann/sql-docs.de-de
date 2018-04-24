---
title: Trennen und erneutes Herstellen einer Verbindung des Recordsets | Microsoft Docs
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
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c8a3f26ec756ac328c7b717f5f25b566d543d0ff
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Trennen und erneutes Herstellen einer Verbindung des Recordsets
Eine der leistungsstärksten Funktionen in ADO ist die Möglichkeit, öffnen Sie ein Recordset clientseitige aus einer Datenquelle, und trennen Sie das Recordset aus der Datenquelle. Sobald das Recordset getrennt wurde, kann die Verbindung zur Datenquelle geschlossen werden, wodurch Freigabe der Ressourcen auf dem Server verwendet, um ihn beizubehalten. Weiterhin anzeigen und bearbeiten die Daten in das Recordset, während dieser getrennt ist und später wieder herstellen, mit der Datenquelle, und senden Ihre Änderungen im Batchmodus ausgeführt.  
  
 Wenn Sie ein Recordset trennen möchten, öffnen Sie diese in einer Cursorposition des AdUseClient, und legen Sie die Eigenschaft ActiveConnection auf nichts verweist. (C++-Benutzer sollte ActiveConnection gleich NULL trennen festgelegt.)  
  
 Wir verwenden ein getrenntes Recordset später in diesem Abschnitt, wenn wir erörtern Recordset Persistenz um ein Szenario zu behandeln, in denen müssen wir haben die Daten in einem Recordset für eine Anwendung verfügbar, während der Clientcomputer nicht mit einem Netzwerk verbunden ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Batchmodus](../../../ado/guide/data/batch-mode.md)
