---
title: "Der Deskriptor Übergänge | Microsoft Docs"
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
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 280d35d8ce03d3d7685441c12d99c05c9ff5f451
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="descriptor-transitions"></a>Der Deskriptor Übergänge
ODBC-Deskriptoren werden die folgenden drei Status haben.  
  
|Status|Description|  
|-----------|-----------------|  
|D0|Nicht zugeordnete Sicherheitsbeschreibung|  
|D1i|Implizit zugeordneten Deskriptor|  
|D1e|Explizit reservierte Deskriptor|  
  
 Die folgenden Tabellen zeigen, wie jede ODBC-Funktion den Zustand des Deskriptors auswirkt.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> Nicht zugeordnet|D1i<br /><br /> Implizit|D1e<br /><br /> Explizit|  
|------------------------|----------------------|----------------------|  
|D1i [1]|--|--|  
|D1e [2]|--|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Nicht zugeordnet|D1i<br /><br /> Implizit|D1e<br /><br /> Explizit|  
|------------------------|----------------------|----------------------|  
|(SODASS)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Nicht zugeordnet|D1i<br /><br /> Implizit|D1e<br /><br /> Explizit|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(SODASS) [2]|(HY017)|D0|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DESC wurde.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField und SQLGetDescRec  
  
|D0<br /><br /> Nicht zugeordnet|D1i<br /><br /> Implizit|D1e<br /><br /> Explizit|  
|------------------------|----------------------|----------------------|  
|(SODASS)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField und SQLSetDescRec  
  
|D0<br /><br /> Nicht zugeordnet|D1i<br /><br /> Implizit|D1e<br /><br /> Explizit|  
|------------------------|----------------------|----------------------|  
|(SODASS) [1]|--|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *DescriptorHandle* wurde das Handle eines ARD, APD oder IPD, oder (für **SQLSetDescField**) beim *DescriptorHandle* wurde das Handle für ein IRD und *FieldIdentifier* SQL_DESC_ARRAY_STATUS_PTR oder SQL_DESC_ROWS_PROCESSED_PTR war.  
  
## <a name="all-other-odbc-functions"></a>Alle anderen ODBC-Funktionen  
  
|D0<br /><br /> Nicht zugeordnet|D1i<br /><br /> Implizit|D1e<br /><br /> Explizit|  
|------------------------|----------------------|----------------------|  
|--|--|--|

