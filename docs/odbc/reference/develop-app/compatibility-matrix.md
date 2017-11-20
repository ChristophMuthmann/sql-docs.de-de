---
title: "Kompatibilitätsmatrix | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c980058ea2cacba7b9160571b1b42884ea02e41
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="compatibility-matrix"></a>Kompatibilitätsmatrix
Die folgende Tabelle beschreibt die Kompatibilität der Typen von Anwendungen und Treiber, die zuvor in diesem Abschnitt definiert.  
  
|Anwendungstyp<br /><br /> und version|32-Bit-ODBC<br /><br /> 2.*x* Treiber|ODBC-3. *x*<br /><br /> Treiber|3.8 der ODBC-Treiber|ISO "und" Open Group-kompatible Treiber|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|16-Bit-Anwendung, eine beliebige version|Kompatibel|Kompatibel|Kompatibel|Kompatibel|  
|Reine 2. *x* Anwendung|Kompatibel|Kompatibel|Kompatibel|Nicht kompatible [3]|  
|Reine 2. *x* erneut kompiliert, Anwendung|Kompatibel|Kompatible [1]|Kompatible [1]|Nicht kompatible [3]|  
|Reine 2. *x* Unicode-Anwendung|Kompatibel|Kompatible [1]|Kompatible [1]|Nicht kompatible [3]|  
|Reine Open Group und ISO-kompatible Anwendung|Nicht kompatibel|Kompatible [2]|Kompatible [2]|Kompatible [2]|  
|Reine 3.0-Anwendung|Nicht kompatibel|Kompatibel|Kompatibel|Nicht kompatible [4]|  
|Reine 3.5-Anwendung|Nicht kompatibel|Kompatibel|Kompatibel|Nicht kompatible [4]|  
|Reine 3.8 (oder höher)-Anwendung|Nicht kompatible [5]|Nicht kompatible [5]|Kompatibel|Nicht kompatible [4]|  
|Ersetzten Anwendung|Kompatibel|Kompatibel|Kompatibel|Nicht kompatible [3]|  
  
 [1]. die Anwendung neu kompilieren mithilfe von ODBC 3.5 (oder höher)-Header mit der Unicode-Option (bei einer Unicode-Anwendung) und muss ODBCVER 0x0250 festgelegt.  
  
 [2] die Anwendung muss Kompilieren mithilfe von ODBC 3.5 (oder höher)-Header und Verknüpfen mit der ODBC-Treiber-Manager. Sie müssen auch das Header-Flag ODBC_STD festgelegt.  
  
 [3] in dieser Konfiguration kann ausfallen arbeiten, da die Funktionen in ODBC 2. vorhanden sind. *x* , die nicht in den Standards, z. B. Lesezeichen sind.  
  
 [4] in dieser Konfiguration kann ausfallen arbeiten, da in ODBC 3. Features stehen*.x* , die nicht in den Standards, z. B. Lesezeichen sind.  
  
 [5] für diese Konfiguration kann möglicherweise fehlschlagen, da stehen Funktionen in ODBC 3.8, nicht in ODBC 2.x oder 3.x-Treiber, wie z. B. treiberspezifische [C-Datentypen in ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Treiber-Manager-Kompatibilität  
 Eine ODBC 3.0-Anwendung, die mit allen Versionen der Treiber-Manager ausgeführt werden muss sollten gehen beim Start:  
  
-   Ein Umgebungshandle zuzuordnen.  
  
-   Das Attribut der SQL_ATTR_ODBC_VERSION-Umgebung auf SQL_OV_ODBC3_80 festgelegt. Wenn der Treiber-Manager SQL_ERROR zurückgibt, ist der Treiber-Manager älter als 3.8. Setzen Sie SQL_ATTR_ODBC_VERSION auf SQL_OV_ODBC3 oder SQL_OV_ODBC2, entsprechend zur Anpassung an den Treiber-Manager.  
  
-   Zuordnen eines Verbindungshandles.  
  
-   Stellen Sie eine Verbindung.  
  
-   Rufen Sie SQLGetInfo für SQL_DRIVER_ODBC_VER, um zu bestimmen, der Version des Treibers. Wenn der Treiber ODBC 3.8-Treiber ist, können Sie die Treiber-spezifischen C-Typen verwenden. Verwenden Sie andernfalls nicht treiberspezifische C-Datentypen.  
  
 Beachten Sie, dass es sich bei eine neu kompilierten ODBC 3.x-Anwendung ODBC 3.8-Funktionen treiberspezifische C-Typen ohne Angabe von SQL_OV_ODBC3_80 für SQL_ATTR_ODBC_VERSION verwenden kann. Dieser Vorgang ähnelt einer neu kompilierten ODBC 2.x-Anwendung mit ODBC 3.x-Funktionen.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Verwenden von SQLCancelHandle in einer Anwendung kompatibel mit allen Treiber-Manager  
 Da [SQLCancelHandle Funktion](../../../odbc/reference/syntax/sqlcancelhandle-function.md) wird nicht unterstützt in-Treiber-Manager, die vor Windows 7 veröffentlicht wurden, kann keine Anwendung in früheren Versionen von Windows geladen werden, wenn aufgerufen **SQLCancelHandle** direkt. Arbeiten mit allen Versionen der Treiber-Manager, und verwenden **SQLCancelHandle** auf neue Versionen von Windows, sollte eine Anwendung aufrufen **SQLCancelHandle** indirekt mithilfe **LoadLibrary** und **GetProcAddress.**  
  
## <a name="see-also"></a>Siehe auch  
 [Was ist neu in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)

