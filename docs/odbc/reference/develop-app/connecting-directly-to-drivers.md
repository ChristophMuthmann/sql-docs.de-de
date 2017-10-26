---
title: Herstellen einer Verbindung direkt mit dem Treiber | Microsoft Docs
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
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bacb659cb6986f86151502998523ade468f7cedd
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="connecting-directly-to-drivers"></a>Herstellen einer Verbindung direkt mit dem Treiber
Wie in beschrieben wurde [Auswählen der Datenquelle oder Treiber](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)weiter oben in diesem Abschnitt einige Anwendungen möchten nicht an eine Datenquelle verwenden. Stattdessen sie direkt an einen Treiber eine Verbindung herstellen möchten. **SQLDriverConnect** bietet eine Möglichkeit für die Anwendung direkt an einen Treiber zu verbinden, ohne eine Datenquelle angeben. Vom Konzept her ist eine temporäre Datenquelle zur Laufzeit erstellt.  
  
 Um direkt auf einen Treiber zu verbinden, die Anwendung gibt die **Treiber** Schlüsselwort in der Verbindungszeichenfolge anstelle von der **DSN** Schlüsselwort. Der Wert, der die **Treiber** Schlüsselwort ist die Beschreibung des Treibers aus, wie Sie zurückgegeben **SQLDrivers**. Nehmen wir beispielsweise an ein Treiber wurde die Beschreibung Paradox-Treiber und erfordert den Namen eines Verzeichnisses, das die Datendateien enthält. Zur Verbindung mit dieser Treiber kann die Anwendung entweder die folgenden Verbindungszeichenfolgen verwenden:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Mit der ersten Zeichenfolge müsste der Treiber nicht keine weiteren Informationen. Der Treiber müssen mit der zweiten Zeichenfolge für den Namen des Verzeichnisses mit den Datendateien aufgefordert.

