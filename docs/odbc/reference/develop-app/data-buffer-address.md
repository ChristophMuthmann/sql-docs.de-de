---
title: Daten zu Puffern Adresse | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 863f6dda23748fc2c7c46cee40344f5e7acf4602
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="data-buffer-address"></a>Adresse des Puffers
Die Anwendung übergibt die Adresse des Datenpuffers des Treibers in ein Argument, häufig mit dem Namen *ValuePtr* oder einem ähnlichen Namen. Z. B. im folgenden Aufruf **SQLBindCol**, die Anwendung gibt die Adresse des dem *Datum* Variablen:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Siehe die [Allocating und Freigeben von Puffern](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) Abschnitt die Adresse eines Puffers verzögerte muss gültig bleiben, bis der Puffer aufgehoben wird.  
  
 Es sei denn, sie insbesondere nicht zulässig ist, kann die Adresse eines Puffers Daten ein null-Zeiger sein. Für Puffer zum Senden von Daten an den Treiber verwendet wird den Treiber, die normalerweise im Puffer enthaltene Informationen ignoriert werden sollen. Für Puffer zum Abrufen von Daten aus dem Treiber verwendet dazu den Treiber, die keinen Wert zurückgibt. In beiden Fällen ignoriert der Treiber die entsprechenden Daten Puffer Length-Argument.
