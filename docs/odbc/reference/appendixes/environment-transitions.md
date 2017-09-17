---
title: "Umgebungsübergänge | Microsoft Docs"
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
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a044161df57f81fee3639fd26c94b5860d5c1913
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="environment-transitions"></a>Umgebungsübergänge
ODBC-Umgebungen werden die folgenden drei Status haben.  
  
|Status|Description|  
|-----------|-----------------|  
|E0|Nicht zugeordnete Umgebung.|  
|E1|Zugeordnete-Umgebung verfügbaren Verbindung|  
|E2|Zugeordnete Verbindung zugeordneten-Umgebung|  
  
 Die folgenden Tabellen zeigen, wie jede ODBC-Funktion den Zustand der Umgebung auswirkt.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(SODASS) [2]|E2 [5]<br />(HY010) [6]|--[4]|  
|(SODASS) [3]|(SODASS)|--[4]|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT oder SQL_HANDLE_DESC war.  
  
 [4] aufrufen **SQLAllocHandle** mit *OutputHandlePtr* verweist auf ein gültiges Handle dieses Handle überschreibt. Dies ist möglicherweise ein Programmierfehler Anwendung.  
  
 [5] SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde für die Umgebung festgelegt wurde.  
  
 [6] SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde nicht für die Umgebung festgelegt wurde.  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources und SQLDrivers  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS)|--[1]<br />(HY010) [2]|--[1]<br />(HY010) [2]|  
  
 [1] SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde für die Umgebung festgelegt wurde.  
  
 [2] ' ist das SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde nicht für die Umgebung festgelegt wurde.  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS) [1]|--[3]<br />(HY010) [4]|--[3]<br />(HY010) [4]|  
|(SODASS) [2]|(SODASS)|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] Attribut ' ist das SQL_ATTR_ODBC_VERSION-Umgebung war für die Umgebung festgelegt wurde.  
  
 [4] ' ist das SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde nicht für die Umgebung festgelegt wurde.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS) [1]|E0|(HY010)|  
|(SODASS) [2]|(SODASS)|--[4]<br />E1 [5]|  
|(SODASS) [3]|(SODASS)|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC wurde.  
  
 [3] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_STMT oder SQL_HANDLE_DESC war.  
  
 [4] gab es andere zugeordneten Verbindungshandles.  
  
 [5] ' ist das Verbindungshandle im angegebenen *behandeln* wurde das einzige zugeordnete Verbindungshandle.  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField und SQLGetDiagRec  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS) [1]|--|--|  
|(SODASS) [2]|(SODASS)|--|  
  
 [1] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_ENV wurde.  
  
 [2] für diese Zeile zeigt die Übergänge beim *HandleType* SQL_HANDLE_DBC auf SQL_HANDLE_STMT oder SQL_HANDLE_DESC wurde.  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS)|--[1]<br />(HY010) [2]|--|  
  
 [1] SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde für die Umgebung festgelegt wurde.  
  
 [2] ' ist das SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde nicht für die Umgebung festgelegt wurde.  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS)|--[1]<br />(HY010) [2]|(HY011)|  
  
 [1] SQL_ATTR_ODBC_VERSION Umgebung-Attribut wurde für die Umgebung festgelegt wurde.  
  
 [2] der *Attribut* Argument war kein SQL_ATTR_ODBC_VERSION und SQL_ATTR_ODBC_VERSION-Umgebung-Attribut wurde nicht für die Umgebung festgelegt wurde.  
  
## <a name="all-other-odbc-functions"></a>Alle anderen ODBC-Funktionen  
  
|E0<br /><br /> Nicht zugeordnet|E1<br /><br /> Belegt|E2<br /><br /> Verbindung|  
|------------------------|----------------------|-----------------------|  
|(SODASS)|(SODASS)|--|
