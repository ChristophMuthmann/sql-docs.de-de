---
title: Trennen und erneutes Herstellen einer Verbindung des Recordsets | Microsoft Docs
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
- Recordset object [ADO], disconnecting and reconnecting
ms.assetid: c5134af7-81d6-4de4-9fd1-cfe29973545e
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a6ddbc392ae0bd0c378a4d08cd2c76f3119d8332
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="disconnecting-and-reconnecting-the-recordset"></a>Trennen und erneutes Herstellen einer Verbindung des Recordsets
Eine der leistungsstärksten Funktionen in ADO ist die Möglichkeit, öffnen Sie ein Recordset clientseitige aus einer Datenquelle, und trennen Sie das Recordset aus der Datenquelle. Sobald das Recordset getrennt wurde, kann die Verbindung zur Datenquelle geschlossen werden, wodurch Freigabe der Ressourcen auf dem Server verwendet, um ihn beizubehalten. Weiterhin anzeigen und bearbeiten die Daten in das Recordset, während dieser getrennt ist und später wieder herstellen, mit der Datenquelle, und senden Ihre Änderungen im Batchmodus ausgeführt.  
  
 Wenn Sie ein Recordset trennen möchten, öffnen Sie diese in einer Cursorposition des AdUseClient, und legen Sie die Eigenschaft ActiveConnection auf nichts verweist. (C++-Benutzer sollte ActiveConnection gleich NULL trennen festgelegt.)  
  
 Wir verwenden ein getrenntes Recordset später in diesem Abschnitt, wenn wir erörtern Recordset Persistenz um ein Szenario zu behandeln, in denen müssen wir haben die Daten in einem Recordset für eine Anwendung verfügbar, während der Clientcomputer nicht mit einem Netzwerk verbunden ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Batchmodus](../../../ado/guide/data/batch-mode.md)
