---
title: MERGE in Integration Services-Paketen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: control-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5df41c86f2d1eb8daa0fa29f066e16f6b0dc5e73
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="merge-in-integration-services-packages"></a>MERGE in Integration Services-Paketen
  In der aktuellen Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]kann die SQL-Anweisung in einem Task „SQL ausführen“ eine MERGE-Anweisung enthalten. Diese MERGE-Anweisung ermöglicht es Ihnen, in einer einzelnen Anweisung mehrere INSERT-, UPDATE- und DELETE-Vorgänge auszuführen.  
  
 Um die MERGE-Anweisung in einem Paket zu verwenden, führen Sie folgende Schritte aus:  
  
-   Erstellen Sie einen Datenflusstask, der die Quelldaten in eine temporäre oder Stagingtabelle lädt, transformiert und speichert.  
  
-   Erstellen Sie einen Task "SQL ausführen", der die MERGE-Anweisung enthält.  
  
-   Verbinden Sie den Datenflusstask mit der Aufgabe "SQL ausführen", und verwenden Sie die Daten in der Stagingtabelle als Eingabe für die MERGE-Anweisung.  
  
    > [!NOTE]  
    >  Obwohl eine MERGE-Anweisung in diesem Szenario normalerweise eine Stagingtabelle erfordert, übersteigt die Leistung der MERGE-Anweisung normalerweise die Leistung der von der Transformation für Suche ausgeführten zeilenweisen Suche. Die MERGE-Anweisung ist außerdem nützlich, wenn die Größe einer Suchtabelle den Speicher testen würde, der der Transformation für Suche zum Zwischenspeichern der entsprechenden Verweistabelle zur Verfügung steht.  
  
 Ein Beispiel für eine Zielkomponente, die die Verwendung der MERGE-Anweisung unterstützt, finden Sie im CodePlex-Communitybeispiel [MERGE Destination](http://go.microsoft.com/fwlink/?LinkId=141215).  
  
## <a name="using-merge"></a>Verwenden von MERGE  
 In der Regel verwenden Sie die MERGE-Anweisung, wenn Sie Änderungen, die Einfügungen, Updates und Löschungen umfassen, von einer Tabelle in die andere Tabelle übernehmen möchten. Vor [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]erforderte dieser Prozess sowohl eine Transformation für Suche als auch mehrere Transformationen für OLE DB-Befehl. Die Transformation für Suche hat eine zeilenweise Suche ausgeführt, um zu bestimmen, ob jede Zeile neu war oder geändert wurde. Die Transformationen für OLE DB-Befehl haben anschließend die notwendigen INSERT-, UPDATE- und DELETE-Vorgänge ausgeführt. Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]kann eine einzelne MERGE-Anweisung sowohl die Transformation für Suche als auch die entsprechenden Transformationen für OLE DB-Befehl ersetzen.  
  
### <a name="merge-with-incremental-loads"></a>MERGE mit inkrementellem Laden  
 Die neue Change Data Capture-Funktion in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] erleichtert es, inkrementelles Laden in ein Data Warehouse zuverlässig auszuführen. Als Alternative zu parametrisierten Transformationen für OLE DB-Befehl zur Durchführung von Einfügungen und Updates können Sie die MERGE-Anweisung verwenden, um beide Vorgänge zu kombinieren.  
  
 Weitere Informationen finden Sie unter [Anwenden der Änderungen auf das Ziel](../../integration-services/change-data-capture/apply-the-changes-to-the-destination.md).  
  
#### <a name="merge-in-other-scenarios"></a>MERGE in anderen Szenarios  
 In den folgenden Szenarios können Sie die MERGE-Anweisung entweder außerhalb oder innerhalb eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets verwenden. Häufig ist jedoch ein [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket erforderlich, um diese Daten aus mehreren heterogenen Quellen zu laden und sie anschließend zu kombinieren und zu bereinigen. Deshalb könnten Sie erwägen, die MERGE-Anweisung in einem Paket zu verwenden, um die Wartung zu erleichtern.  
  
##### <a name="track-buying-habits"></a>Nachverfolgen von Kaufgewohnheiten  
 Die FactBuyingHabits-Tabelle im Data Warehouse erfasst das letzte Datum, an dem ein Kunde ein bestimmtes Produkt gekauft hat. Die Tabelle besteht aus den Spalten ProductID, CustomerID und PurchaseDate. Jede Woche generiert die Transaktionsdatenbank eine PurchaseRecords-Tabelle, in der die während dieser Woche getätigten Käufe enthalten sind. Das Ziel ist, mit einer einzigen MERGE-Anweisung die Informationen der PurchaseRecords-Tabelle in die FactBuyingHabits-Tabelle einzufügen. Für Produkt/Kunde-Paare, die nicht vorhanden sind, fügt die MERGE-Anweisung neue Zeilen ein. Für Produkt/Kunde-Paare, die vorhanden sind, aktualisiert die MERGE-Anweisung das letzte Kaufdatum.  
  
###### <a name="track-price-history"></a>Nachverfolgen der Preisentwicklung  
 Die DimBook-Tabelle repräsentiert die Liste der Bücher im Bestand eines Buchhändlers und identifiziert die Preisentwicklung für jedes Buch. Diese Tabelle enthält folgende Spalten: ISBN, ProductID, Price, Shelf und IsCurrent. Außerdem enthält die Tabelle eine Zeile für jeden Preis des Buchs in der Vergangenheit. Eine dieser Zeilen enthält den aktuellen Preis. Um anzugeben, welche Zeile den aktuellen Preis enthält, wird der Wert der "IsCurrent"-Spalte für diese Zeile auf 1 gesetzt.  
  
 Jede Woche generiert die Datenbank eine WeeklyChanges-Tabelle, in der Preisänderungen und neue Bücher, die während der Woche in den Bestand aufgenommen wurden, enthalten sind. Mit einer einzigen MERGE-Anweisung können Sie die Änderungen der WeeklyChanges-Tabelle in die DimBook-Tabelle übernehmen. Die MERGE-Anweisung fügt neue Zeilen für neu hinzugefügte Bücher hinzu und aktualisiert die IsCurrent-Spalte für Zeilen vorhandener Bücher, deren Preis sich geändert hat, auf 0. Außerdem fügt die MERGE-Anweisung neue Zeilen für Bücher hinzu, deren Preis sich geändert hat, und legt den Wert der IsCurrent-Spalte für diese neuen Zeilen auf 1 fest.  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>Zusammenführen einer Tabelle mit neuen Daten aus der alten Tabelle  
 Die Datenbank formt die Eigenschaften eines Objekts mit einem "offenen Schema", das heißt, eine Tabelle enthält Name/Wert-Paare für jede Eigenschaft. Die Properties-Tabelle enthält drei Spalten: EntityID,  PropertyID und Value. Eine NewProperties-Tabelle, bei der es sich um eine neuere Version der Tabelle handelt, muss mit der Properties-Tabelle synchronisiert werden. Um diese beiden Tabellen zu synchronisieren, können Sie eine einzelne MERGE-Anweisung verwenden, um die folgenden Vorgänge auszuführen:  
  
-   Löschen Sie Eigenschaften aus der Properties-Tabelle, wenn sie in der NewProperties-Tabelle fehlen.  
  
-   Aktualisieren Sie Werte für Eigenschaften in der Properties-Tabelle mit neuen Werten aus der NewProperties-Tabelle.  
  
-   Fügen Sie neue Eigenschaften für Eigenschaften hinzu, die in der NewProperties-Tabelle vorhanden sind, jedoch in der Properties-Tabelle fehlen.  
  
 Dieser Ansatz ist in Szenarios nützlich, die Replikationsszenarios ähneln, deren Ziel darin besteht, Daten in zwei Tabellen auf zwei Servern synchronisiert zu halten.  
  
### <a name="track-inventory"></a>Bestandsnachverfolgung  
 Die Inventory-Datenbank umfasst eine ProductsInventory-Tabelle mit den Spalten ProductID und StockOnHand. In einer Shipments-Tabelle mit den Spalten ProductID, CustomerID und Quantity werden Produktlieferungen an Kunden verfolgt. Die ProductInventory-Tabelle muss täglich auf Basis der Informationen der Shipments-Tabelle aktualisiert werden. Mit einer einzigen MERGE-Anweisung kann der Bestand in der ProductInventory-Tabelle auf Grundlage der erfolgten Lieferungen reduziert werden. Wenn der Bestand für ein Produkt auf 0 reduziert wurde, kann diese MERGE-Anweisung die entsprechende Produktzeile auch in der ProductInventory-Tabelle löschen.  
  
  
