---
title: "UPDATE-Anweisung Einschränkungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 828fc042a4184bfedccf7c26210f899c1d73f2a4
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="update-statement-limitations"></a>Einschränkungen beim UPDATE-Anweisung
Für den Treiber Paradox, eine Tabelle zu aktualisieren muss die Tabelle einen eindeutigen Index (Paradox Primärschlüssel) aufweisen. Wenn Sie den Paradox-Treiber verwenden, ohne das Datenbankmodul Borland implementieren, ist es nicht möglich, zum Aktualisieren einer Tabelle Paradox.  
  
 Vom Text-Treiber unterstützt nicht.  
  
 Wenn der Microsoft Excel-Treiber verwendet wird, ist es möglich, Werte zu aktualisieren, aber eine Zeile kann nicht gelöscht werden, aus einer Tabelle basierend auf einer Microsoft Excel-Arbeitsblatt. Daher wird die UPDATE-Anweisung nicht berücksichtigt offiziell von Microsoft Excel-Treiber unterstützt. Die INSERT-Anweisung gilt unterstützt.
