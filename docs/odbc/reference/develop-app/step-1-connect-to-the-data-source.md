---
title: 'Schritt 1: Herstellen der Verbindung mit der Datenquelle | Microsoft Docs'
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
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 42da1bad914342a2f2973a63dc35f6e53f8b6c93
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-connect-to-the-data-source"></a>Schritt 1: Herstellen der Verbindung mit der Datenquelle
Der erste Schritt bei jeder Anwendung ist für die Verbindung mit der Datenquelle. In dieser Phase, einschließlich der Funktionen, die erforderlich ist, wird in der folgenden Abbildung gezeigt.  
  
 ![Herstellen einer Verbindung mit der Datenquelle in einer ODBC-Anwendung](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 Der erste Schritt beim Herstellen einer Verbindung mit der Datenquelle ist, um den Treiber-Manager zu laden, und weisen das Umgebungshandle mit **SQLAllocHandle**. Weitere Informationen finden Sie unter [Reservieren der Umgebung behandelt](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Klicken Sie dann die Anwendung registriert, der es durch Aufrufen von entspricht, ODBC-Version **SQLSetEnvAttr** mit dem SQL_ATTR_APP_ODBC_VER Umgebung-Attribut. Weitere Informationen finden Sie unter [deklarieren Sie der Anwendungsverzeichnis ODBC-Version von](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) und [Abwärtskompatibilität und zur Einhaltung von Standards](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Anschließend ordnet die Anwendung ein Verbindungshandle mit **SQLAllocHandle** und eine Verbindung mit der Datenquelle mit **SQLConnect**, **SQLDriverConnect**, oder **SQLBrowseConnect**. Weitere Informationen finden Sie unter [zuzuordnen, eine Verbindung zu behandeln](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) und [Herstellen einer Verbindung](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 Klicken Sie dann die Anwendung legt die Verbindungsattribute, z. B. ob manuellen commit der Transaktionen fest. Weitere Informationen finden Sie unter [Verbindungsattribute](../../../odbc/reference/develop-app/connection-attributes.md).

