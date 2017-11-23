---
title: "ODBC-Datenquellen Unterschlüssel | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3d2ed7d39772237f522320f227c49c773d12801
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-data-sources-subkey"></a>ODBC Data Sources Unterschlüssel
Die Werte unter dem ODBC-Datenquellen-Unterschlüssel Auflisten der Datenquellen. Das Format der folgenden Werte ist wie in der folgenden Tabelle gezeigt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|*Datenquellenname*|REG_SZ|*Treiber-Beschreibung*|  
  
 Die *-Datenquellennamen* Wert wird vom Verwaltungsprogramm (die in der Regel dafür der Benutzer aufgefordert wird), definiert und *treiberbeschreibung* wird vom Treiber Entwickler definiert (in der Regel ist dies der Name des der DBMS des Treibers zugeordnet).  
  
 Nehmen wir beispielsweise an, die drei Datenquellen definiert wurden: Inventur, die SQL Server; verwendet Payroll dBASE befindlichen; und Mitarbeiter, die verwendet, formatiert Textdateien. Die Werte unter dem Unterschlüssel ODBC-Datenquellen könnte folgendermaßen aussehen:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
