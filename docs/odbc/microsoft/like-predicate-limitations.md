---
title: WIE Prädikat Einschränkungen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 891c6499f54c56635d74289517e8cf33f66ba4ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="like-predicate-limitations"></a>WIE Prädikat Einschränkungen
Wenn Daten in einer Spalte mehr als 255 Zeichen sind, wird der Vergleich mit LIKE nur auf die ersten 255 Zeichen basieren.  
  
 LIKE verwendet wird, eine Prozedur ist nur bei Konstantenmuster unterstützt. Der Desktop-Datenbanktreiber unterstützt SQL-92 wie Mustervergleich.  
  
 Verwenden einer Escape-Klausel in einer LIKE-Prädikat wird nicht unterstützt.  
  
 Ein Vergleich mit LIKE sollten nicht für eine Spalte mit Daten eines Datentyps Numeric oder "float" ausgeführt werden. Die Ergebnisse möglicherweise nicht vorhersehbar. Weitere Informationen finden Sie unter der *Microsoft Jet-Datenbank-Engine-Programmiererhandbuch*.
