---
title: Bezeichner Einschränkungen | Microsoft Docs
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 087d7ba056a5da10ae8d191592f06c312583b62b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="identifiers-limitations"></a>Einschränkungen von Bezeichnern
Wenn ein Bezeichner ein Leerzeichen oder ein Sonderzeichen enthält, muss der Bezeichner in Back Anführungszeichen eingeschlossen werden. Ein gültiger Name ist eine Zeichenfolge mit nicht mehr als 64 Zeichen enthalten, von denen das erste Zeichen ein Leerzeichen nicht sein muss. Gültige Namen darf keine Steuerzeichen und folgenden Sonderzeichen enthalten: " &#124; # *? [ ] . ! $ .  
  
 Verwenden Sie nicht die reservierten Wörtern, in der SQL-Grammatik in Anhang C aufgeführt die *ODBC Programmer's Reference* (oder die Kurzform dieser reservierte Wörter) als Bezeichner (d. h. Tabellen- oder Spaltennamen), es sei denn, Sie Sichern des Worts umschließen Anführungszeichen (').
