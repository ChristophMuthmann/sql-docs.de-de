---
title: Parametrisierte Befehle mit dazwischen liegenden COMPUTE-Befehlen | Microsoft Docs
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
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
- APPEND clause [ADO]
- COMPUTE command [ADO]
ms.assetid: 732f624f-8900-4608-9815-194302d22e8b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 18bfbc4a2e18e0232380edf157410fbd4eb3b12c
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="parameterized-commands-with-intervening-compute-commands"></a>Parametrisierte Befehle mit dazwischen liegenden COMPUTE-Befehlen
Eine typische parametrisierte Form ANFÜGEN-Befehl hat eine Klausel, die ein übergeordnetes Element erstellt **Recordset** mit einem Abfragebefehl und eine weitere Klausel, die ein untergeordnetes Element erstellt **Recordset** mit einer parametrisierten Abfrage-Befehl: d. h. einen Befehl mit einem Platzhalter für Parameter (ein Fragezeichen "?"). Das resultierende strukturierte **Recordset** hat zwei Ebenen, in dem das übergeordnete Element die obere Ebene belegt, und das untergeordnete Element nimmt die untere Ebene.  
  
 Die Klausel, die das untergeordnete Element erstellt **Recordset** jetzt möglicherweise eine beliebige Anzahl von geschachtelten Form COMPUTE-Befehle, die am tiefsten geschachtelte Befehl, in denen die parametrisierte Abfrage enthält. Das resultierende strukturierte **Recordset** hat mehrere Ebenen, in dem das übergeordnete Element die oberste Ebene belegt, das untergeordnete Element nimmt die unterste Ebene und eine beliebige Anzahl von **Recordset**s generiert, indem Sie die Shape-Befehlen COMPUTE belegen die dazwischen liegenden Ebenen.  
  
 Die typische Verwendung für dieses Feature zum Aufrufen der Aggregatfunktion und Gruppierungsfunktionen von ShapeCOMPUTE wird Befehle, um sich dazwischen erstellen **Recordset** Objekte mit analytischen Informationen über das untergeordnete Element **Recordset** . Darüber hinaus, da dies einen Befehl für die parametrisierte Form ist, jedes Mal eine Kapitelspalte des übergeordneten Elements erfolgt, eine neue untergeordnete **Recordset** abgerufen werden kann. Da die dazwischen liegenden Ebenen von untergeordneten abgeleitet sind, werden sie auch neu berechnet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Data Shaping Example (Beispiele der Datenstrukturierung)](../../../ado/guide/data/data-shaping-example.md)
