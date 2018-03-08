---
title: "Bezeichner Einschränkungen | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6bc9deecbd06b3bcb0aec9d3e0d3b8790c7af0b6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/21/2017
---
# <a name="identifiers-limitations"></a>Einschränkungen von Bezeichnern
Wenn ein Bezeichner ein Leerzeichen oder ein Sonderzeichen enthält, muss der Bezeichner in Back Anführungszeichen eingeschlossen werden. Ein gültiger Name ist eine Zeichenfolge mit nicht mehr als 64 Zeichen enthalten, von denen das erste Zeichen ein Leerzeichen nicht sein muss. Gültige Namen darf keine Steuerzeichen und folgenden Sonderzeichen enthalten: "&#124; # * ? [ ] . ! $ .  
  
 Verwenden Sie nicht die reservierten Wörtern, in der SQL-Grammatik in Anhang C aufgeführt die *ODBC Programmer's Reference* (oder die Kurzform dieser reservierte Wörter) als Bezeichner (d. h. Tabellen- oder Spaltennamen), es sei denn, Sie Sichern des Worts umschließen Anführungszeichen (').
