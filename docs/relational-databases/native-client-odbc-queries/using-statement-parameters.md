---
title: Verwenden von Anweisungsparametern | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, parameters
- parameters [SQL Server Native Client], ODBC
- ODBC, parameters
- statements [ODBC], parameters
- parameter markers [ODBC]
- SQL Server Native Client ODBC driver, statements
- ODBC applications, statements
ms.assetid: 2427d886-ec6c-49d7-b0b6-0d998b64cdb9
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 84fa75e75d21017b310fc807948bb4ed42e3d673
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="using-statement-parameters"></a>Verwenden von Anweisungsparametern
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ein Parameter ist eine Variable in einer SQL-Anweisung, die eine ODBC-Anwendung für folgende Vorgänge aktivieren kann:  
  
-   Werte für Spalten in einer Tabelle effizient bereitstellen  
  
-   Benutzerinteraktion beim Aufstellen von Abfragekriterien verbessern  
  
-   Verwalten von **Text**, **Ntext**, und **Image** Daten und [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifischen C-Datentypen.  
  
 Z. B. eine **Teile** Tabelle enthält, Spalten, die mit dem Namen **PartID**, **Beschreibung**, und **Preis**. Um ein Teil ohne Parameter hinzuzufügen, ist eine SQL-Anweisung erforderlich. Beispiel:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Diese Anweisung ist zwar zum Einfügen einer Zeile in eine bekannte Menge von Werten akzeptabel, sie ist jedoch umständlich, wenn die Anwendung mehrere Zeilen einfügen muss. ODBC löst dieses Problem, indem eine Anwendung jeden Datenwert in einer SQL-Anweisung durch eine Parametermarkierung ersetzen kann. Diese wird durch ein Fragezeichen (?) angegeben. Im folgenden Beispiel werden drei Datenwerte durch Parametermarkierungen ersetzt:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Die Parametermarkierungen werden dann an Anwendungsvariablen gebunden. Um eine neue Zeile einzufügen, muss die Anwendung nur die Werte der Variablen festlegen und die Anweisung ausführen. Der Treiber ruft dann die aktuellen Werte der Variablen ab und sendet sie an die Datenquelle. Wenn die Anweisung mehrfach ausgeführt wird, kann die Anwendung den Prozess durch Vorbereiten der Anweisung noch effizienter gestalten.  
  
 Auf jede Parametermarkierung wird durch die entsprechende Ordnungszahl, die den Parametern von links nach rechts zugewiesen wurde, verwiesen. Die äußere linke Parametermarkierung in einer SQL-Anweisung besitzt den Ordnungswert 1, die nächste Markierung den Wert 2 usw.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Binden von Parametern](../../relational-databases/native-client-odbc-queries/using-statement-parameters-binding-parameters.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen von Abfragen &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
