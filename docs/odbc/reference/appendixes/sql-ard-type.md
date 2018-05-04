---
title: SQL_ARD_TYPE | Microsoft Docs
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
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9e02377c4f192e9cbf5f6a41ab62ef5345ba4ab
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="sqlardtype"></a>SQL_ARD_TYPE
Der Typbezeichner SQL_ARD_TYPE wird verwendet, um anzugeben, dass die Daten in einem Puffer des Typs im Feld SQL_DESC_CONCISE_TYPE der ARD angegeben werden. SQL_ARD_TYPE eingegeben wird, der *TargetType* Argument eines Aufrufs von **SQLGetData** anstelle von einem bestimmten Datentyp und geben Sie eine Anwendung so ändern Sie die Daten des Puffers durch Ändern des Deskriptors aktiviert Feld. Dieser Wert verknüpft, den den Datentyp des der  *\*TargetValuePtr* Puffer, in dem Deskriptorfeld. (SQL_ARD_TYPE wird nicht in einem Aufruf eingegeben **SQLBindCol** oder **SQLBindParameter** daran, dass der Typ der gebundenen Puffer bereits an den SQL_DESC_TYPE und SQL_DESC_CONCISE_TYPE gebunden ist und geändert werden kann zu einem beliebigen Zeitpunkt durch entweder dieser Felder ändern.)  
  
 Der Typbezeichner SQL_ARD_TYPE kann verwendet werden, um nicht standardmäßige Werte für führende Genauigkeit und Sekunden Genauigkeit des Datentyps Interval anzugeben, und geben Sie die Genauigkeit und Dezimalstellenanzahl Werte für die SQL_C_NUMERIC-Daten. Weitere Informationen finden Sie unter [führende Standard überschreiben und die Sekunden Genauigkeit Intervalldatentypen](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) und [überschreiben-Standard-Genauigkeit und Dezimalstellenanzahl für numerische Datentypen](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)weiter unten in diesem Anhang.
