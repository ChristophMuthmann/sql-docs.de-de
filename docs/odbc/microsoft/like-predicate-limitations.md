---
title: WIE Prädikat Einschränkungen | Microsoft Docs
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
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73e4ec1b4177b02869939628cb408df500958694
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="like-predicate-limitations"></a>WIE Prädikat Einschränkungen
Wenn Daten in einer Spalte mehr als 255 Zeichen sind, wird der Vergleich mit LIKE nur auf die ersten 255 Zeichen basieren.  
  
 LIKE verwendet wird, eine Prozedur ist nur bei Konstantenmuster unterstützt. Der Desktop-Datenbanktreiber unterstützt SQL-92 wie Mustervergleich.  
  
 Verwenden einer Escape-Klausel in einer LIKE-Prädikat wird nicht unterstützt.  
  
 Ein Vergleich mit LIKE sollten nicht für eine Spalte mit Daten eines Datentyps Numeric oder "float" ausgeführt werden. Die Ergebnisse möglicherweise nicht vorhersehbar. Weitere Informationen finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.
