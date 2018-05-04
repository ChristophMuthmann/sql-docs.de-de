---
title: String-Einschränkungen | Microsoft Docs
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 740a6688d80d104d483c67c6998d20ec204ab41f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="string-limitations"></a>Zeichenfolge-Einschränkungen
Die maximale Länge einer Zeichenfolge, SQL-Anweisung ist 65.000 Zeichen.  
  
 Wenn der Microsoft Access-Treiber verwendet wird, werden nur SQL-92 Zeichenfolgenkonstanten (durch einfache Anführungszeichen, keine doppelten Anführungszeichen) unterstützt.  
  
 Einen senkrechten Strich (&#124;) kann nicht in einer Zeichenfolge verwendet werden, ob das Zeichen in Back Anführungszeichen eingeschlossen ist.  
  
 Für eine optimale Interoperabilität Anwendungen sollten Zeichenfolgen Parameter übergeben, anstatt Übergabe in Anführungszeichen in Zeichenfolgen.
