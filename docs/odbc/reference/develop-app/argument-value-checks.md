---
title: Argument Wert überprüft | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- argument value checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 37a65f8b-83aa-456c-b7cf-500404abb38a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 46a947e362f9c6e614d4e28c50b7046048bf8fa0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="argument-value-checks"></a>Argument Wert überprüft
Der Treiber-Manager überprüft die folgenden Typen von Argumenten. Sofern nicht anders angegeben, gibt der Treiber-Manager SQL_ERROR Argumentwerte auf Fehler.  
  
-   Umgebung, Verbindungs- und Anweisung Handles darf nicht in der Regel mit null-Zeiger sein. Der Treiber-Manager gibt SQL_INVALID_HANDLE zurück, wenn ein null-Handle gefunden wird.  
  
-   Zeigerargumente, z. B. erforderlich *OutputHandlePtr* in **SQLAllocHandle** und *CursorName* in **SQLSetCursorName**, ist nicht möglich NULL-Zeiger.  
  
-   Optionsflags, die nicht treiberspezifische Werte unterstützen muss ein gültiger Wert. Beispielsweise *Vorgang* in **SQLSetPos** SQL_POSITION, SQL_REFRESH, SQL_UPDATE, SQL_DELETE oder SQL_ADD werden muss.  
  
-   Optionsflags müssen in der Version von ODBC unterstützt, die vom Treiber unterstützt werden. Beispielsweise *Infotyp* in **SQLGetInfo** SQL_ASYNC_MODE (eingeführt in ODBC 3.0) darf nicht sein beim Aufrufen von ODBC 2.0-Treiber.  
  
-   Anzahl von Spalten und Parameter muss größer als 0 oder größer als oder gleich 0 ist, abhängig von der Funktion. Der Treiber muss die Obergrenze von diesen Argumentwerten auf Grundlage des aktuellen Resultset oder eine SQL-Anweisung überprüfen.  
  
-   Längenindikator/Argumente und Daten Puffer Länge Argumente müssen entsprechende Werte enthalten. Beispielsweise das Argument, der angibt, die Länge eines Tabellennamens in **SQLColumns** (*NameLength3*) muss SQL_NTS oder einen Wert größer als 0; *Pufferlänge* in **SQLDescribeCol** muss größer als oder gleich 0 sein. Der Treiber möglicherweise müssen Sie auch diesen Argumenten überprüfen. Beispielsweise können sie überprüfen, *NameLength3* ist kleiner oder gleich der maximal einen Tabellennamen in der Datenquelle.
