---
title: DELETE-Anweisung Einschränkungen | Microsoft Docs
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
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caa4855c83815c8876c4674bf01de3f9c4bd4231
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="delete-statement-limitations"></a>Anweisung Einschränkungen löschen
Die DELETE-Anweisung wird für den Microsoft Excel- oder Textdateien-Treiber nicht unterstützt. Beachten Sie, dass die INSERT-Anweisung für den Text-Treiber unterstützt wird.  
  
 DBASE-Treiber unterstützt keine Packen einer Tabelle, um die Werte "gelöscht" zu entfernen.  
  
 Für den Treiber Paradox, eine Zeile aus einer Tabelle löschen muss die Tabelle einen eindeutigen Index (Paradox Primärschlüssel) aufweisen.
