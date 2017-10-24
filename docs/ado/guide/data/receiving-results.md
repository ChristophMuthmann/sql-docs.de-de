---
title: Empfangen von Ergebnissen | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5768404342f76eb8c5999678e6c1a4aa4a3bcd42
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="receiving-results"></a>Empfangen von Ergebnissen
Führen in ADO die meisten Befehle in einige Informationen, die an den Aufrufer zurückgegeben. Für Befehle Rowset zurückgeben, werden die Ergebnisse im Empfangen einer **Recordset** -Objekt, das vermutlich der am häufigsten verwendeten ADO-Objekt ist.  
  
 Es gibt mehrere Möglichkeiten zum Empfangen von Daten in einem **Recordset** Objekt aus einer Datenquelle, einschließlich des Aufrufens Folgendes:  
  
-   [Connection.Execute-Methode](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open-Methode](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Recordset.Open-Methode](../../../ado/guide/data/creating-and-executing-a-simple-command.md)  
  
-   [Connection.NamedCommand](../../../ado/guide/data/named-commands.md)  
  
-   [Connection.StoredProcedure](../../../ado/guide/data/calling-a-stored-procedure-as-a-method-on-a-connection-object.md)  
  
 Empfangen von Daten in eine **Recordset** Objekt endet den Prozess des Abrufens von Daten, wobei der Beteiligung des eine **Verbindung** Objekt und ein **Befehl** -Objekts können implizit oder explizit. In einem typischen Client/Server-Anwendung-System, erfordert der gesamte Prozess des Abrufens von Daten einen Roundtrip über das Netzwerk für die einzelnen gefüllt **Recordset**.  
  
 Mehrere Resultsets empfangen bedeutet, müssen Sie mehrere, Netzwerkroundtrips über das Netzwerk, eine für jedes Dataset gekapselt, die einem **Recordset** Objekt. Für Netzwerke langsam oder überlastet kann die Anzahl der Roundtrips reduziert verbessern die Anwendung beeinflusst. Aus diesem Grund bieten alle Anbieter an Support, um mehrere Empfangsports **Recordset**s in einem einzelnen Roundtrip. Dies wird im folgenden Thema erörtert:  
  
-   [Mehrere Recordsets empfangen](../../../ado/guide/data/receiving-multiple-recordsets.md)

