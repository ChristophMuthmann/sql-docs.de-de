---
title: Tabellennamen | Microsoft Docs
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
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1b1032ccda48d5a645e9992e2c501c851f51b7e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
