---
title: "Schnittstelle Übereinstimmungsebenen | Microsoft Docs"
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
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6f31ab70d00820fc1e0b279754c998c777dc6688
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="interface-conformance-levels"></a>Übereinstimmungsebenen-Schnittstelle
Der Zweck der Abgleich ist auf die Anwendung darüber zu informieren, welche Funktionen, aus dem Treiber verfügbar sind. Ein fehlerisolierung Schema basierend auf Funktionen ist nicht ausreichend dieses Ziel erreichen. In ODBC 3. *x*, Treiber klassifiziert sind, basierend auf den Funktionen, die sie besitzen. Unterstützung der Funktion kann sind die Unterstützung der Funktion; Er kann auch die Unterstützung von einem Beschreibungsfeld, ein Anweisungsattribut, einen Wert "Y" für ein zurückgegebenes Informationstyp enthalten **SQLGetInfo**und so weiter.  
  
 Zur Vereinfachung der Spezifikation der Schnittstelle Übereinstimmung definiert ODBC drei Übereinstimmungsebenen. Um einen bestimmten Konformitätsgrad zu erfüllen, muss ein Treiber alle Anforderungen von diesem Konformitätsgrad erfüllen. Übereinstimmung mit einer bestimmten Ebene impliziert vollständige Übereinstimmung mit alle niedrigeren Ebenen.  
  
 Übereinstimmungsebenen sind nicht immer unterteilen ordentlich Unterstützung für eine bestimmte Liste von ODBC-Funktionen, aber geben Sie unterstützten Funktionen, wie in den folgenden Abschnitten aufgeführt. Um Unterstützung für eine Funktion zu gewährleisten, muss ein Treiber einige oder alle Formen der Aufrufe von bestimmten ODBC-Funktionen unterstützen (Weitere Informationen finden Sie unter [Funktion Konformität](../../../odbc/reference/develop-app/function-conformance.md)), bestimmte Attribute festlegen (finden Sie unter [Attribut Konformität ](../../../odbc/reference/develop-app/attribute-conformance.md)), und bestimmte deskriptorfelder (finden Sie unter [Deskriptor Feld Konformität](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 Die Anwendung ermittelt Schnittstelle-Konformitätsgrad des Treibers durch Herstellen einer Verbindung mit einer Datenquelle und Aufrufen **SQLGetInfo** mit der Option SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Treiber können Features die Toleranzschwelle zu implementieren, zu dem er eine vollständige Übereinstimmung vorgibt. Anwendungen zusätzlichen Funktionen ermitteln, durch den Aufruf **SQLGetFunctions** (um zu bestimmen, welche ODBC-Funktionen vorhanden sind) und **SQLGetInfo** (zum Abfragen von verschiedenen ODBC-Funktionen).  
  
 Es gibt drei Übereinstimmungsebenen der ODBC-Schnittstelle: Core Level 1 und Level 2.  
  
> [!NOTE]  
>  Diese Übereinstimmungsebenen haben unterschiedliche Anforderungen an als der ODBC-API-Übereinstimmungsebenen mit demselben Namen in ODBC 2.*.x*. Insbesondere impliziert alle Funktionen von ODBC 2.*.x* API-Konformität Ebene 1 sind jetzt Bestandteil von dem Konformitätsgrad des Core-Schnittstelle. Viele ODBC-Treiber meldet daher möglicherweise Hauptebenen-Schnittstelle Übereinstimmung.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Core-Schnittstelle Konformität](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Ebene 1 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Ebene 2 Schnittstelle Konformität](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Funktion Konformität](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Attribut-Konformität](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Der Deskriptor Feld Konformität](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
