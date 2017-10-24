---
title: ADO-Objekte und Sammlungen | Microsoft Docs
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
- ADO, objects and collections
ms.assetid: 7a745aae-9372-49b6-8dae-b9c93e5f3216
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ec860c8e4d3766b983e38589418637c1d4eb3cc9
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="ado-objects-and-collections"></a>ADO-Objekte und Sammlungen
ADO besteht aus den folgenden neun Objekte und vier Sammlungen.  
  
|Objekt oder einer Auflistung|Description|  
|--------------------------|-----------------|  
|**Verbindung** Objekt|Stellt eine eindeutige Sitzung mit einer Datenquelle dar. Im Fall von einem Client/Server-Datenbanksystem kann es entspricht eine tatsächliche Netzwerk-Verbindung mit dem Server sein. Abhängig von den Funktionen, die vom Anbieter, einige Auflistungen, Methoden oder Eigenschaften des unterstützt eine **Verbindung** Objekt möglicherweise nicht zur Verfügung.|  
|**Command** -Objekt|Dient zum Definieren eines bestimmten Befehls wie z. B. eine SQL-Abfrage für eine Datenquelle ausgeführt werden soll.|  
|**Recordset** Objekt|Stellt die gesamte Gruppe von Datensätzen aus einer Basistabelle oder die Ergebnisse eines ausgeführten Befehls dar. Alle **Recordset** Objekte bestehen aus Datensätzen (Zeilen) und Feldern (Spalten).|  
|**Datensatz** Objekt|Stellt eine einzelne Zeile mit Daten aus einer **Recordset** oder vom Anbieter. Dieser Datensatz könnte Datensatzes in einer Datenbank oder einem anderen Typ des Objekts, z. B. einer Datei oder eines Verzeichnisses, abhängig von Ihrem Anbieter darstellen.|  
|**Stream** Objekt|Stellt einen Datenstrom von Binär oder Text-Daten dar. Beispielsweise kann ein XML-Dokument in einen Stream für Befehl Eingabe- oder von bestimmten Anbietern zurückgegeben wird, da sich die Ergebnisse einer Abfrage geladen werden. Ein **Stream** Objekt kann verwendet werden, um Felder oder Datensätze, enthält diese Datenströme zu bearbeiten.|  
|**Parameter** Objekt|Stellt einen Parameter oder das zugeordnete Argument eine **Befehl** Objekt anhand einer parametrisierten Abfrage oder gespeicherte Prozedur.|  
|**Feld** Objekt|Stellt eine Spalte von Daten mit einem gemeinsamen Datentyp. Jede **Feld** -Objekt entspricht einer Spalte in der **Recordset**.|  
|**Eigenschaft** Objekt|Stellt ein Merkmal eines ADO-Objekts, das vom Anbieter definiert ist. ADO-Objekte sind zwei Eigenschaften: integrierte und dynamische. Integrierte Eigenschaften sind diese Eigenschaften implementiert in ADO und für alle neuen Objekte sofort verfügbar. Die **Eigenschaft** Objekt ist ein Container für die dynamischen Eigenschaften, die vom zugrunde liegenden Anbieter definiert.|  
|**Error** -Objekt|Enthält Details über Data Access-Fehlern, die auf einem einzelnen Vorgang im Zusammenhang mit dem Anbieter beziehen.|  
|**Felder** Auflistung|Enthält alle der **Feld** Objekte von einem **Recordset** oder **Datensatz** Objekt.|  
|**Eigenschaften** Auflistung|Enthält alle der **Eigenschaft** Objekte für eine bestimmte Instanz eines Objekts.|  
|**Parameter** Auflistung|Enthält alle der **Parameter** Objekte von einem **Befehl** Objekt.|  
|**Fehler** Auflistung|Enthält alle der **Fehler** in Reaktion auf einen einzelnen anbieterbezogenen Fehler erstellten Objekte.|  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Objektmodell](../../../ado/reference/ado-api/ado-object-model.md)

