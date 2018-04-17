---
title: DROP Tabelle Anweisung Einschränkungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae6cfb8306c2422585dbb8775e4863108004a5a7
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="drop-table-statement-limitations"></a>Löschen von Einschränkungen für Tabelle-Anweisung
Wenn der Treiber für Microsoft Excel 5.0, 7.0 oder 97 verwendet wird, wird die DROP TABLE-Anweisung löscht das Arbeitsblatt jedoch nicht den Arbeitsblattnamen gelöscht. Da die Arbeitsblattnamen noch in der Arbeitsmappe vorhanden ist, kann ein anderes Arbeitsblatt mit dem gleichen Namen erstellt werden.
