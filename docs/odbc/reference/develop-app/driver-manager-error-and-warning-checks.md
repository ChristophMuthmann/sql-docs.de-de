---
title: Treiber-Manager-Fehler und Warnung überprüft | Microsoft Docs
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
- diagnostic information [ODBC], driver manager error checking
- driver manager [ODBC], error checking
ms.assetid: eeb5ab3f-987d-4f30-87d2-7425a81ad1d7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4f212af4169b4c0be2a840f6ff8d7310abb40f53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="driver-manager-error-and-warning-checks"></a>Treiber-Manager-Fehler und Warnung überprüft
Der Treiber-Manager vollständig oder teilweise implementiert eine Reihe von Funktionen und daher für alle oder einige der Fehler und Warnungen in diesen Funktionen überprüft.  
  
-   Der Treiber-Manager implementiert **SQLDataSources** und **SQLDrivers** und sucht nach allen Fehlern und Warnungen in diese Funktionen.  
  
-   Der Treiber-Manager überprüft, ob ein Treiber implementiert **SQLGetFunctions**. Wenn der Treiber keine implementiert **SQLGetFunctions**, der Treiber-Manager implementiert und überprüft, ob alle Fehler und Warnungen darin.  
  
-   Der Treiber-Manager teilweise implementiert **SQLAllocHandle**, **SQLConnect**, **SQLDriverConnect**, **SQLBrowseConnect**,  **SQLFreeHandle**, **SQLGetDiagRec**, und **SQLGetDiagField** und sucht nach Fehlern in dieser Funktionen. Sie können die gleichen Fehler wie der Treiber für einiger dieser Funktionen zurückgeben, da beide ähnliche Vorgänge ausführen. Z. B. der Treiber-Manager oder Treiber gelegten SQLSTATE IM008 (Dialogfeld ' ') Wenn entweder eine kann nicht für eine Anmeldedialogfeldes **SQLDriverConnect**.
