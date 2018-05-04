---
title: ODBC-Treiber-Unterschlüssel | Microsoft Docs
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
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17e0a418957aa4413d0fd7d02ebdc0243596d013
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-drivers-subkey"></a>ODBC-Treiber-Unterschlüssel
Die Werte unter der ODBC-Treiber-Unterschlüssel Auflisten der installierten Treiber. Das Format dieser Werte wird in der folgenden Tabelle dargestellt.  
  
|Name|Datentyp|data|  
|----------|---------------|----------|  
|*Treiber-Beschreibung*|REG_SZ|**Installiert**|  
  
 Die *treiberbeschreibung* Name wird vom Treiber Entwickler definiert. Normalerweise ist der Name des DBMS an, mit dem Treiber verknüpft sind.  
  
 Nehmen Sie z. B. an, dass Treiber für formatierte Textdateien und SQL Server installiert wurden. Die Werte unter dem Unterschlüssel ODBC-Treibern möglicherweise:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
