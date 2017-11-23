---
title: Aktivieren neue Datentypen durch Festlegen von ExtendedAnsiSQL | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9eeff1a55315b30ab0d2cafa92f0aa4a511f9ab9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>Neue Datentypen aktivieren durch Festlegen von ExtendedAnsiSQL
Zwei neue Datentypen sind in Jet 4.0-Datenbanken verfügbar, wenn das ExtendedAnsiSQL-Flag aktiviert ist: SQL_DECIMAL und SQL_NUMERIC. Die standardmäßige Genauigkeit und Dezimalstellenanzahl sind 18 und 0 (null) bzw.. Daten, die über ODBC, der als SQL_DECIMAL oder SQL_NUMERIC eingegeben wird zugegriffen werden Microsoft Jet Decimal anstatt Währung zugeordnet werden.  
  
 Wenn das Flag ExtendedAnsiSQL deaktiviert ist, Tabellen mit Datentypen decimal und numeric kann nicht erstellt werden können, und diese Typen nicht in SQLGetTypeInfo() angezeigt. Jedoch, wenn die Tabelle die neuen Datentypen enthält, können sie mit den richtigen Datentypen verwendet werden.
