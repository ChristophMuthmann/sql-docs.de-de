---
title: Tabellennamen | Microsoft Docs
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
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 480ca31108b608139b5563f0c18d1fa020e76f75
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="table-names"></a>Tabellennamen
Wenn Dateinamenerweiterung dBASE, Microsoft Excel, Paradox, oder Text-Treiber verwendet wird, Tabellennamen, Spaltennamen, die in der FROM-Klausel von SELECT- oder "DELETE", nachdem der INTO-Klausel in INSERT- und UPDATE auftreten CREATE TABLE und DROP TABLE einen gültigen Pfad enthalten kann, Name des primären und Datei .  
  
 Verwenden eines Tabellennamens ein an anderer Stelle in einer SQL­Anweisung unterstützt nicht die Verwendung von Pfaden oder Erweiterungen jedoch akzeptiert nur den primären Namen (z. B. von EMP aus C:\ABC\EMP).  
  
 Abhängige Namen (Aliase) können verwendet werden. Beispiel:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```

