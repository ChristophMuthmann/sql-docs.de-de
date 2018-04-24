---
title: Von parametrisierten Befehlen | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70049127949ecc4f0e5931339b951620b58784ce
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="operation-of-parameterized-commands"></a>Von parametrisierten Befehlen
Bei Verwendung mit einem großen untergeordneten **Recordset**, insbesondere auf die Größe des übergeordneten Elements verglichene **Recordset**, aber nur ein paar untergeordnete Kapitel zugreifen müssen Sie finden es vielleicht eine effizientere Verwendung eine parametrisierte Befehle.  
  
 Ein *nicht parametrisierten Befehl* Ruft die gesamte über- und untergeordneten **Recordsets**Fügt eine Kapitelspalte an der übergeordneten Tabelle und weist dann einen Verweis auf das zugehörige untergeordnete Kapitel für jede übergeordnete Zeile .  
  
 Ein *parametrisierten Befehl* Ruft das gesamte übergeordnete **Recordset**, jedoch nur im Kapitel über das ruft **Recordset** beim Zugriff auf die Kapitelspalte. Aus diesem Unterschied beim Abrufstrategie kann beachtliche Leistungsvorteile ergeben.  
  
 Beispielsweise können Sie Folgendes angeben:  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 Die über- und untergeordneten Tabellen haben einen Spaltennamen im Allgemeinen, Cust_id*.* Die *untergeordnete-Befehl* hat ein "?" Platzhalter, auf die die RELATE-Klausel verweist (d. h. "... PARAMETER 0").  
  
> [!NOTE]
>  Die PARAMETER-Klausel bezieht sich ausschließlich auf die Shape-Befehlssyntax. Es ist nicht verknüpft mit entweder dem ADO [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt oder die [Parameter](../../../ado/reference/ado-api/parameters-collection-ado.md) Auflistung.  
  
 Wenn der parametrisierten Form-Befehl ausgeführt wird, geschieht Folgendes:  
  
1.  Die *übergeordneten Befehl* wird ausgeführt und gibt ein übergeordnetes Element **Recordset** aus der Customers-Tabelle.  
  
2.  Eine Kapitelspalte wird an das übergeordnete Element angefügt **Recordset**.  
  
3.  Wenn der Kapitelspalte einer übergeordneten Zeile zugegriffen wird, die *untergeordneten Produktionsabfragen* ausgeführt wird, mit dem Wert von der Customer. cust_id als der Wert des Parameters.  
  
4.  Alle Zeilen in der in Schritt 3 erstellten Daten Anbieterrowset werden verwendet, um das untergeordnete Element Auffüllen **Recordset**. In diesem Beispiel werden alle Zeilen in der Orders-Tabelle, in der die Cust_id der Wert von Customer. cust_id entspricht, darstellt. Standardmäßig wird das untergeordnete Element **Recordset**s wird auf dem Client zwischengespeichert werden, bis alle Verweise auf das übergeordnete Element **Recordset** freigegeben werden. Um dieses Verhalten zu ändern, legen die **Recordset** [dynamische Eigenschaft](../../../ado/reference/ado-api/ado-dynamic-property-index.md) **Cache untergeordneten Zeilen** auf **"false"**.  
  
5.  Ein Verweis auf die abgerufenen untergeordneten Zeilen (d. h. im Kapitel über das untergeordnete Element **Recordset**) befindet sich in der aktuellen Zeile des übergeordneten Elements der Kapitelspalte **Recordset**.  
  
6.  Schritte 3 bis 5 werden wiederholt, wenn der Kapitelspalte mit einer anderen Zeile zugegriffen wird.  
  
 Die **Cache untergeordneten Zeilen** dynamische Eigenschaft auf festgelegt ist **"true"** standardmäßig. Das Cachingverhalten variiert abhängig von der Abfrage die Parameterwerte. In einer Abfrage mit einem einzelnen Parameter, die untergeordnete **Recordset** Wert wird für einen bestimmten Parameter zwischen den Anforderungen für ein untergeordnetes Element mit diesem Wert zwischengespeichert werden. Der folgende Code veranschaulicht dies:  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 In einer Abfrage mit zwei oder mehr Parameter wird ein zwischengespeichertes untergeordnetes Element verwendet, nur dann, wenn alle Parameterwerte, die zwischengespeicherten Werte übereinstimmen.  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>Parametrisierte Befehle und komplexe übergeordneten untergeordnete Beziehungen  
 Zusätzlich zur Verwendung parametrisierter Befehle zum Verbessern der Leistung einer Typhierarchie gleichheitsjoin, können parametrisierte Befehle verwendet werden, um komplexere über-und untergeordneten Beziehungen zu unterstützen. Betrachten Sie beispielsweise eine Datenbank nur wenig League mit zwei Tabellen: eine bestehend aus den Teams (Team_id, Teamname) und die andere Spiele (Date, Home_team, Visiting_team).  
  
 Verwenden eine Hierarchie nicht parametrisiert, besteht keine Möglichkeit zum Verknüpfen der Tabellen Teams und Spiele so, das untergeordnete Element **Recordset** für jedes Team Abständen vollständige enthält. Sie können Kapitel erstellen, die den eigenen Zeitplan oder die Road-Zeitplan, aber nicht beides enthalten. Dies ist, da die RELATE-Klausel Sie über-und untergeordneten Beziehungen des Formulars schränkt (pc1 cc1 =) und (pc2 pc2 =). Daher würde der Befehl "RELATE Team_id TO Home_team, Team_id TO Visiting_team" enthalten, Sie nur Spiele abrufen, wobei wurde ein Team selbst wiedergeben. Was soll ist "(team_id=home_team) oder (Team_id = Visiting_team)", die Shape-Anbieter unterstützt jedoch nicht den OR-Klausel.  
  
 Um das gewünschte Ergebnis zu erhalten, können Sie einen parametrisierten Befehl verwenden. Beispiel:  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 Dieses Beispiel nutzt die größere Flexibilität für die SQL-WHERE-Klausel, um das Ergebnis zu erhalten, das Sie benötigen.  
  
> [!NOTE]
>  Wenn mit WHERE-Klauseln, Parameter können nicht verwenden die SQL-Datentypen für Text-, ntext- und Image oder einem Fehler führt, die enthält der folgenden Beschreibung: `Invalid operator for data type`.  
  
## <a name="see-also"></a>Siehe auch  
 [Daten strukturiert werden, Beispiel](../../../ado/guide/data/data-shaping-example.md)   
 [Formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md)   
 [Shape-Befehle im Allgemeinen](../../../ado/guide/data/shape-commands-in-general.md)
