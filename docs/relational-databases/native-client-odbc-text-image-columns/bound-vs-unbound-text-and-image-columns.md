---
title: Gebundene im Vergleich zu Ungebundenen Text- und Image-Spalten | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: ffd3442e-d880-46e9-b848-2365a09a2406
caps.latest.revision: "29"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: faaf7ed4d573f3d8ba5ca08594211e682a18e482
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="bound-vs-unbound-text-and-image-columns"></a>Gebundene im Vergleich zu Ungebundenen Text- und Image-Spalten
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Wenn Servercursor verwendet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber optimiert und überträgt keine Daten für ungebundene **Text**, **Ntext**, oder **Image** Spalten, die zum Zeitpunkt **SQLFetch** erfolgt. Die **Text**, **Ntext**, oder **Image** Daten werden erst der Anwendungsprobleme nicht tatsächlich vom Server abgerufenen [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) für die Spalte.  
  
 Viele Clientanwendungen können geschrieben werden, damit keine **Text**, **Ntext**, oder **Image** Daten werden angezeigt, während ein Benutzer in einem Cursor einfach nach oben oder unten scrollen ist. Wenn ein Benutzer eine Zeile aus, um weitere Details abzurufen auswählt, wird die Anwendung kann dann aufrufen **SQLGetData** zum Abrufen der **Text**, **Ntext**, oder **Image** Daten. Wird verhindert, dass Übertragung der **Text**, **Ntext**, oder **Image** Daten für alle Zeilen der Benutzer nicht auswählen, und kann daher zu verhindern, dass die Übertragung sehr großer Datenmengen.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Text- und Image-Spalten](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)   
 [Verhalten von Cursorn](../../relational-databases/native-client-odbc-cursors/cursor-behaviors.md)  
  
  
