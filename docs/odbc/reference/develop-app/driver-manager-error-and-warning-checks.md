---
title: "Treiber-Manager-Fehler und Warnung überprüft | Microsoft Docs"
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
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ce87b9dbed8cfa6ca621cb72c36220c13ecb0929
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-error-and-warning-checks"></a>Treiber-Manager-Fehler und Warnung überprüft
Der Treiber-Manager vollständig oder teilweise implementiert eine Reihe von Funktionen und daher für alle oder einige der Fehler und Warnungen in diesen Funktionen überprüft.  
  
-   Der Treiber-Manager implementiert **SQLDataSources** und **SQLDrivers** und sucht nach allen Fehlern und Warnungen in diese Funktionen.  
  
-   Der Treiber-Manager überprüft, ob ein Treiber implementiert **SQLGetFunctions**. Wenn der Treiber keine implementiert **SQLGetFunctions**, der Treiber-Manager implementiert und überprüft, ob alle Fehler und Warnungen darin.  
  
-   Der Treiber-Manager teilweise implementiert **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**, ** SQLFreeHandle**, **SQLGetDiagRec**, und **SQLGetDiagField** und sucht nach Fehlern in dieser Funktionen. Sie können die gleichen Fehler wie der Treiber für einiger dieser Funktionen zurückgeben, da beide ähnliche Vorgänge ausführen. Z. B. der Treiber-Manager oder Treiber gelegten SQLSTATE IM008 (Dialogfeld ' ') Wenn entweder eine kann nicht für eine Anmeldedialogfeldes **SQLDriverConnect**.
