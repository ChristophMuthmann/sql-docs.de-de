---
title: Angeben einer Achse (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], axes
- XPath queries [SQLXML], location paths
- self axis
- attribute axis [SQLXML]
- axis [SQLXML]
- child axis
- parent axis
- location path for XPath query
- axes [SQLXML]
ms.assetid: 65631795-3389-40cf-90ea-85e9438956c5
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8659d8187042b0c40d2890e5a4feaf367efc7203
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-an-axis-sqlxml-40"></a>Angeben einer Achse (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
-   Die Achse gibt die Strukturbeziehung zwischen den vom Positionsschritt ausgewählten Knoten und dem Kontextknoten an. Die folgenden Achsen werden unterstützt: **untergeordneten**  
  
     Enthält das untergeordnete Element des Kontextknotens.  
  
     Der folgende XPath-Ausdruck (Speicherortpfad) Wählt alle aktuellen Kontextknotens aus der  **\<Kunden >** untergeordneten Elemente:  
  
    ```  
    child::Customer  
    ```  
  
     In der folgenden XPath-Abfrage ist `child` die Achse. `Customer` ist der Knotentest.  
  
-   **parent**  
  
     Enthält das übergeordnete Element des Kontextknotens.  
  
     Der folgende XPath-Ausdruck wählt alle dem  **\<Kunden >** übergeordneten Elementen von der  **\<Reihenfolge >** untergeordneten Elemente:  
  
    ```  
    child::Customer/child::Order[parent::Customer/@customerID="ALFKI"]  
    ```  
  
     Dies entspricht exakt der Angabe `child::Customer`. In dieser XPath-Abfrage sind `child` und `parent` die Achsen. `Customer` und `Order` sind die Knotentests.  
  
-   **attribute**  
  
     Enthält das Attribut des Kontextknotens.  
  
     Der folgende XPath-Ausdruck wählt den **CustomerID** Attribut des Kontextknotens:  
  
    ```  
    attribute::CustomerID  
    ```  
  
-   **Self-Service**  
  
     Enthält den Kontextknoten selbst.  
  
     Der folgende XPath-Ausdruck wählt den aktuellen Knoten wird jedoch die  **\<Reihenfolge >** Knoten:  
  
    ```  
    self::Order  
    ```  
  
     In dieser XPath-Abfrage ist `self` die Achse und `Order` der Knotentest.  
  
  
