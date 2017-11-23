---
title: "Der Deskriptor Übergänge | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 82dd5d9fe22a33c50ac33426f71a25524a2b5c2f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
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
