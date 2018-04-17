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
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 925e24f295602d7e66fe37935b53724b4d162adf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
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
