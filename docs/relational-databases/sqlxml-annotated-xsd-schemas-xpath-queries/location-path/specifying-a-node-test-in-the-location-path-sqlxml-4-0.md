---
title: Angeben eines Knotentests im Speicherortpfad (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e2c25b27a36a8505f0608ad8690ea13d6c60c197
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>Angeben eines Knotentests unter dem Speicherortpfad (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ein Knotentest gibt den vom Positionsschritt ausgewählten Knotentyp an. Jede Achse (**untergeordneten**, **übergeordneten**, **Attribut**, oder **self**) hat einen Hauptknotentyp. Für die **Attribut** Achse, der Hauptknotentyp ist  **\<Attribut >**. Für die **übergeordneten**, **untergeordneten**, und **self** Achsen, der Hauptknotentyp ist  **\<Element >**.  
  
> [!NOTE]  
>  Der Platzhalterknotentest * (z. B. `child::*`) wird nicht unterstützt.  
  
## <a name="node-test-example-1"></a>Knotentest: Beispiel 1  
 Der Pfad zum Speicherort `child::Customer` wählt  **\<Kunden >** untergeordneten-Elemente des Kontextknotens.  
  
 In diesem Beispiel ist `child` die Achse, und `Customer` ist der Knotentest. Der Hauptknotentyp für die **untergeordneten** Achse ist  **\<Element >**. Aus diesem Grund ist der Knotentest TRUE, wenn die  **\<Kunden >** Knoten ist ein  **\<Element >** Knoten. Wenn der Kontextknoten keine  **\<Kunden >** untergeordneter Elemente, wird ein leerer Satz Knoten zurückgegeben.  
  
## <a name="node-test-example-2"></a>Knotentest: Beispiel 2  
 Der Pfad zum Speicherort `attribute::CustomerID` wählt die **CustomerID** Attribut des Kontextknotens.  
  
 Im Beispiel ist `attribute` die Achse, und `CustomerID` ist der Knotentest. Der Hauptknotentyp für die **Attribut** Achse ist  **\<Attribut >**. Aus diesem Grund ist der Knotentest TRUE, wenn **CustomerID** ist ein  **\<Attribut >** Knoten. Wenn der Kontextknoten keine **CustomerID**, wird ein leerer Satz Knoten zurückgegeben.  
  
> [!NOTE]  
>  In dieser Implementierung von XPath zu schreiben, wenn ein speicherortschritt ein  **\<Element >** oder ein  **\<Attribut >** Typ, der nicht im Schema deklariert ist, wird ein Fehler generiert. Dies unterscheidet sich von der Implementierung von XPath in MSXML, bei der ein leerer Knotensatz zurückgegeben wird.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>Abgekürzte Syntax für die Achsen  
 Es wird die folgende abgekürzte Syntax für den Speicherortpfad unterstützt:  
  
-   `attribute::` kann als `@` abgekürzt werden.  
  
     Der Speicherortpfad `Customer[@CustomerID="ALFKI"]` entspricht `child::Customer[attribute::CustomerID="ALFKI"]`.  
  
-   `child::` kann von einem Speicherortschritt ausgelassen werden.  
  
     Folglich **untergeordneten** ist die Standardachse. Der Speicherortpfad `Customer/Order` entspricht `child::Customer/child::Order`.  
  
-   `self::node()` kann zu einem Punkt (.) abgekürzt werden, und `parent::node()` kann zu zwei Punkten (..) abgekürzt werden.  
  
  
