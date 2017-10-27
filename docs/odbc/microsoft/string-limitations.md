---
title: "String-Einschränkungen | Microsoft Docs"
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6f9d8add08f80b59adaa42f02bc1da006356081
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="string-limitations"></a>Zeichenfolge-Einschränkungen
Die maximale Länge einer Zeichenfolge, SQL-Anweisung ist 65.000 Zeichen.  
  
 Wenn der Microsoft Access-Treiber verwendet wird, werden nur SQL-92 Zeichenfolgenkonstanten (durch einfache Anführungszeichen, keine doppelten Anführungszeichen) unterstützt.  
  
 Einen senkrechten Strich (&#124;) kann nicht in einer Zeichenfolge verwendet werden, ob das Zeichen in Back Anführungszeichen eingeschlossen ist.  
  
 Für eine optimale Interoperabilität Anwendungen sollten Zeichenfolgen Parameter übergeben, anstatt Übergabe in Anführungszeichen in Zeichenfolgen.

