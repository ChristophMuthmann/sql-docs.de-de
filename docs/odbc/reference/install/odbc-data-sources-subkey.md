---
title: ODBC-Datenquellen Unterschlüssel | Microsoft Docs
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
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e81fe6cc77d92a8fde7530c1f79381025a05856b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
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
