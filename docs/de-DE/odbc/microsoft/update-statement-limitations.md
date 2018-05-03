---
title: UPDATE-Anweisung Einschränkungen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbb1e6cbf0660f7b016391d5881b77d7e89e1f81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>Einschränkungen beim UPDATE-Anweisung
Für den Treiber Paradox, eine Tabelle zu aktualisieren muss die Tabelle einen eindeutigen Index (Paradox Primärschlüssel) aufweisen. Wenn Sie den Paradox-Treiber verwenden, ohne das Datenbankmodul Borland implementieren, ist es nicht möglich, zum Aktualisieren einer Tabelle Paradox.  
  
 Vom Text-Treiber unterstützt nicht.  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, ist es möglich, Werte zu aktualisieren, aber eine Zeile kann nicht gelöscht werden, aus einer Tabelle basierend auf einer Microsoft Excel-Arbeitsblatt. Daher wird die UPDATE-Anweisung nicht berücksichtigt offiziell von Microsoft Excel-Treiber unterstützt. Die INSERT-Anweisung gilt unterstützt.
