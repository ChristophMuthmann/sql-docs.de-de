---
title: Empfangen von Ergebnissen | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- receiving results [ADO]
- Recordset object [ADO], receiving results
ms.assetid: 791aa26e-7aae-477e-9f05-5cd46e1de095
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a13be909891455c21b3409ea53072a5f2c9268e3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
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
