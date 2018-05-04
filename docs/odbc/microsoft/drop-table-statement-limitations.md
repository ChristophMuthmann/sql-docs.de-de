---
title: DROP Tabelle Anweisung Einschränkungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2d5959fe83037a61e2dc3a0d25bee65c512fe08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="drop-table-statement-limitations"></a>Löschen von Einschränkungen für Tabelle-Anweisung
Wenn der Treiber für Microsoft Excel 5.0, 7.0 oder 97 verwendet wird, wird die DROP TABLE-Anweisung löscht das Arbeitsblatt jedoch nicht den Arbeitsblattnamen gelöscht. Da die Arbeitsblattnamen noch in der Arbeitsmappe vorhanden ist, kann ein anderes Arbeitsblatt mit dem gleichen Namen erstellt werden.
