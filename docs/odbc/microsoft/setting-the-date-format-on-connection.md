---
title: "Das Datumsformat für Verbindung festlegen | Microsoft Docs"
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
- date formats [ODBC]
- ODBC driver for Oracle [ODBC], date formats
ms.assetid: ba0d5123-db52-448b-8e19-b7647ce4b361
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36011b0a1ea6fbb753c2e091a1e74edce498a31b
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-date-format-on-connection"></a>Das Datumsformat festlegen für Verbindung
> [!IMPORTANT]  
>  Diese Funktion wird in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Verwenden Sie stattdessen den ODBC-Treiber von Oracle bereitgestellt.  
  
 Die neue Version von Microsoft ODBC Driver for Oracle wird nicht automatisch vom Datumsformat für Oracle-Datumsfelder festgelegt. Zuvor der Treiber eine Verbindung hergestellt, auch wenn es verwendet `ALTER SESSION SET NLS_DATE_FORMAT ='YYYY-MM-DD HH:MI:SS'`.  
  
 Klicken Sie zum Festlegen der Datumsformat rufen Sie ALTER SITZUNG SET auf, und führen Sie dann auf Einfügen. Beispiel:  
  
```  
conn.Execute "ALTER SESSION SET NLS_DATE_FORMAT = 'YYYY-MM-DD HH:MI:SS' "  
sSql = "INSERT INTO DATETEST VALUES (24,'1988-12-01 10:23:03')"  
conn.Execute sSql  
```
