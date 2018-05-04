---
title: Abhängige Namen | Microsoft Docs
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
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0451d231f6d157c32c001c34e5faa20ea8ec80be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="correlation-names"></a>Abhängige Namen
Abhängige Namen werden vollständig unterstützt, einschließlich der in der Liste ' Tabelle '. Beispielsweise ist in der folgenden Zeichenfolge E1 der abhängige Name für die Tabelle Emp auf:  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```
