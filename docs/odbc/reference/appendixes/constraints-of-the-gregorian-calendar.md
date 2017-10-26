---
title: "Einschränkungen des gregorianischen Kalenders | Microsoft Docs"
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
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1b149b1e9df8338b5502d57e6e7eb355b66bcc3f
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="constraints-of-the-gregorian-calendar"></a>Einschränkungen des gregorianischen Kalenders
Date und Datetime-Datentypen und die nachfolgende Felder von Interval-Datentypen, müssen den Einschränkungen des gregorianischen Kalenders entsprechen. Diese Einschränkungen lauten wie folgt:  
  
-   Der Wert des Felds Monat muss zwischen 1 und 12 einschließlich sein.  
  
-   Der Wert des Felds Tag muss im Bereich von 1 bis zur Anzahl der Tage im Monat. Die Anzahl der Tage im Monat richtet sich die Werte der Felder Jahr und Monaten und 28, 29, 30 und 31 sein kann. (Die Anzahl der Tage im Monat kann auch davon abhängen, ob es sich um ein Schaltjahr handelt.)  
  
-   Der Wert des Felds Stunden muss zwischen 0 und 23 sein.  
  
-   Der Wert des Felds für die Minuten muss zwischen 0 und 59.  
  
-   Für die nachfolgende Sekundenfeld der Interval-Datentypen, muss der Wert im Sekundenfeld zwischen 0 und einen Anteil von 59,9 (*n*), einschließlich, in denen * n * ist die Anzahl der Ziffern in der Genauigkeit in Sekundenbruchteilen.  
  
-   Für die nachfolgende Sekundenfeld der Datetime-Datentyp, der Wert im Sekundenfeld muss zwischen 0 und 61.9 sein (*n*) (einschließlich), wobei * n * gibt die Anzahl der "9" Ziffern und den Wert der * n * ist die Genauigkeit der Sekundenbruchteile. (Der Bereich von Sekunden kann bis zu zwei Schaltsekunden Synchronisierung siderischen Zeit beibehalten.)

