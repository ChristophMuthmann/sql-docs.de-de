---
title: String-Einschränkungen | Microsoft Docs
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
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd397b02f72a9962e4fe87683141fa98f81cfbdc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="string-limitations"></a>Zeichenfolge-Einschränkungen
Die maximale Länge einer Zeichenfolge, SQL-Anweisung ist 65.000 Zeichen.  
  
 Wenn der Microsoft Access-Treiber verwendet wird, werden nur SQL-92 Zeichenfolgenkonstanten (durch einfache Anführungszeichen, keine doppelten Anführungszeichen) unterstützt.  
  
 Einen senkrechten Strich (&#124;) kann nicht in einer Zeichenfolge verwendet werden, ob das Zeichen in Back Anführungszeichen eingeschlossen ist.  
  
 Für eine optimale Interoperabilität Anwendungen sollten Zeichenfolgen Parameter übergeben, anstatt Übergabe in Anführungszeichen in Zeichenfolgen.
