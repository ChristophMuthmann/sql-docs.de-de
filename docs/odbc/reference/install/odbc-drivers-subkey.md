---
title: "ODBC-Treiber-Unterschlüssel | Microsoft Docs"
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
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 171692642f04cbab5b1e289efdae89ab79f15831
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
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
