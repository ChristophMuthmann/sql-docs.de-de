---
title: Verhaltensänderungen | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 51737ccc21f8ee4d3d1943433f88393d4847ea8a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="behavioral-changes"></a>Verhaltensänderungen
Verhaltensänderungen werden diese Änderungen für die die *Syntax* der Schnittstelle bleibt dieselbe, aber die *Semantik* geändert haben. Damit diese Änderungen die Funktionalität, die in ODBC 2. verwendet. *x* verhält sich anders als die gleiche Funktionalität in ODBC 3. *X*.  
  
 Gibt an, ob eine Anwendung ODBC 2. aufweist. *x* Verhalten oder die ODBC 3. *X* Verhalten richtet sich nach dem SQL_ATTR_ODBC_VERSION Umgebung-Attribut. Dieser 32-Bit-Wert wird auf SQL_OV_ODBC2 festgelegt, mit ODBC 2. ausgeführt. *x* Verhalten und SQL_OV_ODBC3 ODBC 3. aufweisen. *X* Verhalten.  
  
 Das SQL_ATTR_ODBC_VERSION Umgebung-Attribut wird festgelegt, durch den Aufruf von **SQLSetEnvAttr**. Nachdem eine Anwendung ruft **SQLAllocHandle** um ein Umgebungshandle zuzuordnen, müssen sie aufrufen**SQLSetEnvAttr** sofort auf das Verhalten festgelegt, es weist. (Daher besteht ein neue Umgebung Zustand, beschreiben das Umgebungshandle in einer zugeordneten jedoch versionless, Status.) Weitere Informationen finden Sie unter [Anhang B: ODBC-Übergang-Statustabellen](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Eine Anwendung gibt es mit dem SQL_ATTR_ODBC_VERSION Umgebung-Attribut, aber das Attribut weist das Verhalten hat keine Auswirkung auf die Anwendung die Verbindung mit einer ODBC 2. *x* oder ODBC-3. *X* Treiber. Eine ODBC-3. *x* Anwendung entweder einer ODBC 2. verbinden kann. *X* oder 3. *X* -Treiber verwenden, unabhängig davon, welche die Einstellung des Attributs Umgebung.  
  
 ODBC-3. *x* Anwendungen sollten niemals Aufrufen **SQLAllocEnv**. Als Ergebnis, wenn der Treiber-Manager einen Aufruf empfängt **SQLAllocEnv**, erkennt die Anwendung als ein ODBC 2. *X* Anwendung.  
  
 Das SQL_ATTR_ODBC_VERSION-Attribut wirkt sich auf drei verschiedene Aspekte von einer ODBC-3. *x* Verhalten des Treibers:  
  
-   SQLSTATEs  
  
-   Datentypen für Datum, Uhrzeit und Zeitstempel  
  
-   Die *CatalogName* Argument in **SQLTables** Suchmuster in ODBC 3. akzeptiert. *X*, aber nicht in der ODBC-2. *x*  
  
 Die Einstellung des Attributs SQL_ATTR_ODBC_VERSION Umgebung wirkt sich nicht **SQLSetParam** oder **SQLBindParam**. **SQLColAttribute** wird auch durch dieses Bit nicht beeinflusst. Obwohl **SQLColAttribute** Gibt Attribute, die betroffen sind von der Version des ODBC (Datentyp, Genauigkeit, Dezimalstellen und Länge), wird das beabsichtigte Verhalten durch den Wert bestimmt die *FieldIdentifier*Argument. Wenn *FieldIdentifier* gleich SQL_DESC_TYPE, **SQLColAttribute** gibt die ODBC 3. *X* Codes für Date, Time und Timestamp; Wenn *FieldIdentifier* gleich SQL_COLUMN_TYPE, **SQLColAttribute** gibt der ODBC 2. *X* Codes für Date, Time und Timestamp.  
  
 Dieser Abschnitt enthält die folgenden Themen.  
  
-   [SQLSTATE-Zuordnungen](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Änderungen des Datentyps „datetime“](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
