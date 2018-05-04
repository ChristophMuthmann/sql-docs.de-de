---
title: Arrays von Parameterwerten | Microsoft Docs
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
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38dc5fb0ed2286b3077e6198bc978808063b5d2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="arrays-of-parameter-values"></a>Arrays von Parameterwerten
Es ist häufig nützlich für Anwendungen mit Arrays von Parametern zu übergeben. Z. B. Verwenden von Arrays von Parametern und einer parametrisierten **einfügen** -Anweisung kann eine Anwendung eine Anzahl von Zeilen auf einmal einfügen. Es gibt mehrere Vorteile gegenüber der Verwendung von Arrays. Zunächst wird der Netzwerkverkehr verringert, da die Daten für mehrere Anweisungen in einem einzelnen Paket gesendet werden (wenn die Datenquelle Parameterarrays systemintern unterstützt). Zweitens können SQL-Anweisungen, die schneller als das Ausführen der gleichen Anzahl von unterschiedlichen SQL-Anweisungen verwenden von Arrays einige Datenquellen ausgeführt werden. Wenn die Daten in einem Array gespeichert werden, wie häufig der Fall für Bildschirmdaten ist, die Anwendung kann binden Sie schließlich alle Zeilen in einer bestimmten Spalte mit einem einzigen Aufruf **SQLBindParameter** und aktualisieren, indem Sie die Ausführung einer einzelnen Anweisung.  
  
 Unglücklicherweise unterstützen nicht viele Datenquellen Parameterarrays. Allerdings kann ein Treiber Parameterarrays emulieren, indem Sie eine SQL-Anweisung einmal für jeden Satz von Parameterwerten ausführen. Dies kann zu Zunahmen bei der Geschwindigkeit führen, da der Treiber klicken Sie dann die Anweisung vorzubereiten, die er einmal für jeden Parametersatz ausführen möchte. Es kann auch zu einfacher Anwendungscode führen.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [Binden von Parameterarrays](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Verwenden von Parameterarrays](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
