---
title: Standard-Datenquelle | Microsoft Docs
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
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b756f9b553c622028266d1fc591596bf58ddf45
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="default-data-source"></a>Standard-Datenquelle
Der Treiber kann wählen Sie eine Datenquelle, die Standarddatenquelle in bestimmten Fällen, in denen die Anwendung keine explizit angeben wird, aufgerufen:  
  
-   In einem Aufruf von **SQLConnect** , in dem die *ServerName* Argument ist eine Zeichenfolge der Länge 0 (null), ein null-Zeiger oder DEFAULT.  
  
-   In einem Aufruf von **SQLDriverConnect** , in denen *InConnectionString* gibt an, entweder **DSN**= Standard oder gibt an, mit der **DSN** Schlüsselwort ein die Datenquelle, die nicht in die Systeminformationen enthalten ist.  
  
 Es ist treiberdefinierten, wie die Standarddatenquelle angegeben wird. Dies kann zur Folge haben Verwaltungsaktion und kann, hängt davon ab, der Benutzer.
