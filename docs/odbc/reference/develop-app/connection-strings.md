---
title: Verbindungszeichenfolgen | Microsoft Docs
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
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e48311df773abe0549ee447564c01a437bd0cca9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="connection-strings"></a>Verbindungszeichenfolgen
Eine Verbindungszeichenfolge enthält Informationen zum Herstellen einer Verbindung verwendet. Eine vollständige Verbindungszeichenfolge enthält alle Informationen, die zum Herstellen einer Verbindung benötigt. Die Verbindungszeichenfolge ist eine Reihe von durch Semikolons getrennten Paaren aus Schlüsselwort-Wert. (Die vollständige Syntax der Verbindungszeichenfolge finden Sie unter der [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) funktionsbeschreibung.) Die Verbindungszeichenfolge wird von:  
  
-   **SQLDriverConnect**, dem Abschluss der Verbindungszeichenfolge an, indem Sie Interaktion mit dem Benutzer.  
  
-   **SQLBrowseConnect**, der die Verbindungszeichenfolge iterativ mit der Datenquelle abgeschlossen.  
  
 **SQLConnect** keine Verbindungszeichenfolge, mithilfe von **SQLConnect** ist analog zum Herstellen einer Verbindung mithilfe einer Verbindungszeichenfolge mit genau drei Schlüsselwort-Wert-Paaren (Datenquellenname und, optional, Benutzer-ID und Kennwort) .
