---
title: Standard-Datenquelle | Microsoft Docs
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
ms.workload: Inactive
ms.openlocfilehash: 256d200ce0cb7b64fd011bdba343ca0aae292232
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="default-data-source"></a>Standard-Datenquelle
Der Treiber kann wählen Sie eine Datenquelle, die Standarddatenquelle in bestimmten Fällen, in denen die Anwendung keine explizit angeben wird, aufgerufen:  
  
-   In einem Aufruf von **SQLConnect** , in dem die *ServerName* Argument ist eine Zeichenfolge der Länge 0 (null), ein null-Zeiger oder DEFAULT.  
  
-   In einem Aufruf von **SQLDriverConnect** , in denen *InConnectionString* gibt an, entweder **DSN**= Standard oder gibt an, mit der **DSN** Schlüsselwort ein die Datenquelle, die nicht in die Systeminformationen enthalten ist.  
  
 Es ist treiberdefinierten, wie die Standarddatenquelle angegeben wird. Dies kann zur Folge haben Verwaltungsaktion und kann, hängt davon ab, der Benutzer.
