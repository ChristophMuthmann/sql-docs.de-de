---
title: "Abhängige Namen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- correlation names [ODBC]
- SQL grammar [ODBC], correlation names
ms.assetid: 76c36c6f-f8e1-4ece-a77b-611dde3bdd8a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7f757a0609490c280e2d6acb3679059e7f56dace
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="correlation-names"></a>Abhängige Namen
Abhängige Namen werden vollständig unterstützt, einschließlich der in der Liste ' Tabelle '. Beispielsweise ist in der folgenden Zeichenfolge E1 der abhängige Name für die Tabelle Emp auf:  
  
```  
SELECT * FROM Emp E1   
WHERE E1.LastName = 'Smith'  
```

