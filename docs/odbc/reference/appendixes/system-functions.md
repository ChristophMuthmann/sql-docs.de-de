---
title: Systemfunktionen | Microsoft Docs
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
- system functions [ODBC]
- functions [ODBC], system functions
ms.assetid: 36614b4c-e037-43ef-8692-67f4861b144d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1537c769de2c0f421ed533ea73d75a1578a10559
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="system-functions"></a>Systemfunktionen
Die folgende Tabelle enthält die Systemfunktionen, die in der ODBC-Skalarfunktion Menge enthalten sind. Durch Aufrufen von **SQLGetInfo** mit einem *Informationstyp* von SQL_SYSTEM_FUNCTIONS, kann eine Anwendung ermitteln, welche Systemfunktionen vom Treiber unterstützt werden.  
  
 Als Argumente bezeichnet *exp* kann der Name einer Spalte, die das Ergebnis von einem anderen skalaren Funktion oder ein Literal sein, in denen die zugrunde liegenden Datentyp als SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL dargestellt werden konnte _BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP.  
  
 Als Argumente bezeichnet *Wert* kann eine literale Konstante sein, in denen die zugrunde liegenden Datentyp als SQL_NUMERIC, SQL_DECIMAL, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_FLOAT, SQL_REAL, SQL_DOUBLE, SQL_ dargestellt werden kann TYPE_DATE, SQL_TYPE_TIME und SQL_TYPE_TIMESTAMP.  
  
 Zurückgegebenen Werte werden als ODBC-Datentypen dargestellt.  
  
|Funktion|Description|  
|--------------|-----------------|  
|**DATENBANK ()** (ODBC 1.0)|Gibt den Namen der Datenbank entspricht dem Verbindungshandle zurück. (Der Name der Datenbank ist auch verfügbar durch Aufrufen von **SQLGetConnectOption** mit SQL_CURRENT_QUALIFIER-Verbindungsoption.)|  
|**IFNULL (** *exp*,*Wert***)** (ODBC 1.0)|Wenn *exp* ist null, *Wert* zurückgegeben. Wenn *exp* ist ungleich null, *exp* zurückgegeben wird. Die möglichen Datentyp oder die Arten von *Wert* muss kompatibel mit dem Datentyp der *exp*.|  
|**BENUTZER ()** (ODBC 1.0)|Gibt den Benutzernamen in das DBMS zurück. (Der Benutzername steht auch über **SQLGetInfo** durch Angabe der Informationstyp: SQL_USER_NAME.) Dies kann sich der Anmeldename sein.|
