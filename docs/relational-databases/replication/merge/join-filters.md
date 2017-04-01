---
title: "Joinfilter | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Filter [SQL Server-Replikation], verknüpfen"
  - "Veröffentlichungen [SQL Server-Replikation], Verknüpfungsfilter"
  - "Joinfilter für die Mergereplikation [SQL Server-Replikation]"
  - "Verknüpfungsfilter"
ms.assetid: dd78fd8f-56e3-4582-9abd-6bc25c91e075
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Joinfilter
  Durch einen Joinfilter kann eine Tabelle auf der Grundlage der Filterkriterien einer verknüpften Tabelle in der Veröffentlichung gefiltert werden. In der Regel wird eine übergeordnete Tabelle mithilfe eines parametrisierten Filters gefiltert. Anschließend werden ein oder mehrere Joinfilter auf dieselbe Weise definiert, wie Sie einen Join zwischen Tabellen definieren. Die Joinfilter erweitern den parametrisierten Filter so, dass die Daten in den zugehörigen Tabellen nur dann repliziert werden, wenn sie der Joinfilterklausel entsprechen.  
  
 Joinfilter folgen normalerweise den Beziehungen zwischen Primär- und Fremdschlüssel, die für die Tabellen, auf die sie angewendet werden, definiert wurden. Sie sind jedoch nicht streng auf diese Primär-/Fremdschlüssel-Beziehungen festgelegt. Joinfilter können auf jeder Logik basieren, die miteinander in Beziehung stehende Daten in zwei Tabellen vergleicht.  
  
 Nehmen wir als Beispiel die folgenden Tabellen in der [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] -Beispieldatenbank, die durch eine Primärschlüssel/Fremdschlüssel-Beziehung miteinander verbunden sind:  
  
-   **HumanResources.Employee**  
  
-   **Sales.SalesOrderHeader**  
  
-   **Sales.SalesOrderDetail**  
  
 Diese Tabellen könnten in einer Anwendung zur Unterstützung mobiler Außendienstmitarbeiter verwendet werden, müssen dabei aber gefiltert werden, damit jeder Mitarbeiter in der **HumanResources.Employee** -Tabelle nur die für die Aufträge seiner Kunden relevanten Daten erhält.  
  
 Dafür muss als Erstes ein parametrisierter Filter für die übergeordnete Tabelle definiert werden. In diesem Beispiel ist dies die **HumanResources.Employee** -Tabelle. Diese Tabelle enthält die Spalte **LoginID**, das die Anmeldung für jeden Mitarbeiter in der Form enthält *Domain\login*. Wenn Sie diese Tabelle so filtern möchten, dass jeder Mitarbeiter nur die Daten erhält, die für ihn relevant sind, geben Sie folgende parametrisierte Filterklausel an:  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 Dieser Filter stellt sicher, dass das Abonnement des jeweiligen Mitarbeiters enthält nur Daten aus der **HumanResources.Employee** Tabelle, die für diese Mitarbeiter sind (in diesem Fall eine einzelne Zeile). Weitere Informationen finden Sie unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-row-filters.md).  
  
 Als Nächstes wird dieser Filter auf jede einzelne der zugehörigen Tabellen erweitert. Die dazu verwendete Syntax ähnelt derjenigen, mit der Sie einen Join zwischen zwei Tabellen angeben können. Die erste Joinfilterklausel lautet:  
  
```  
Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
```  
  
 Diese Klausel stellt sicher, dass das Abonnement nur die Auftragsdaten enthält, die für den betreffenden Außendienstmitarbeiter relevant sind. Die zweite Joinfilterklausel lautet:  
  
```  
SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
```  
  
 Diese Klausel stellt sicher, dass das Abonnement nur die den Auftragsdaten zugehörigen Detaildaten des betreffenden Außendienstmitarbeiters enthält. Dieses Beispiel zeigt eine Einzeltabelle, die an jedem Punkt verknüpft ist. Es ist aber auch möglich, an jedem Punkt mehrere Tabellen zu verknüpfen.  
  
 Joinfilter können jeweils einzeln im Assistenten für neue Veröffentlichung und im Dialogfeld **Veröffentlichungseigenschaften** oder aber programmgesteuert hinzugefügt werden. Außerdem können Joinfilter über den Assistenten für neue Veröffentlichung automatisch generiert werden: Geben Sie dazu einen Zeilenfilter für eine Tabelle an, und die Joinfilter werden auf alle entsprechenden Tabellen angewendet. Weitere Informationen finden Sie unter [definieren und ändern Sie einen Join Filter zwischen Mergeveröffentlichungen](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md), [generiert automatisch ein Festlegen der Join Filter zwischen Merge Artikel und #40; SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/automatically generate join filters between merge articles.md), und [Definieren eines Artikels](../../../relational-databases/replication/publish/define-an-article.md).  
  
## Optimieren der Joinfilterleistung  
 Zur Optimierung der Leistung der Joinfilter sollten Sie die folgenden Hinweise beachten:  
  
-   Begrenzen Sie die Anzahl der Tabellen in der Joinsfilterhierarchie.  
  
     Joinfilter können zwar eine unbegrenzte Anzahl von Tabellen enthalten, Filter mit einer großen Tabellenanzahl wirken sich aber möglicherweise deutlich negativ auf die Leistung bei der Mergeverarbeitung aus. Wenn Sie Joinsfilter für fünf oder mehr Tabellen erstellen, sollten Sie andere Lösungen in Betracht ziehen: Kleinere Tabellen, Tabellen, die nicht geändert werden, oder Tabellen, bei denen es sich primär um Nachschlagetabellen handelt, sollten in diesem Fall nicht gefiltert werden. Verwenden Sie Joinsfilter nur zwischen Tabellen, für die eine Partitionierung auf Abonnements erfolgen muss.  
  
-   Legen Sie, sofern zutreffend, für **join unique key** den Wert **True** fest.  
  
     Im Mergeprozess sind besondere Leistungsoptimierungsmöglichkeiten verfügbar, wenn die verknüpfte Spalte in der übergeordneten Tabelle eindeutig ist. Wenn die Joinbedingung auf einer eindeutigen Spalte basiert, aktivieren Sie die Option **join unique key** für den Joinfilter. Informationen zum Festlegen dieser Option finden Sie in den im vorhergehenden Abschnitt genannten Vorgehensweise-Themen.  
  
-   Stellen Sie sicher, dass die Spalten, auf die in den Joinfiltern verwiesen wird, indiziert sind.  
  
     Wenn die Spalten, auf die im Filter verwiesen wird, indiziert sind, kann die Replikation die Filter effizienter verarbeiten.  
  
-   Erstellen Sie keine Zeilenfilter, die sich wie Joinfilter verhalten.  
  
     Mithilfe einer Unterabfrage in einer WHERE-Klausel ist es möglich, Zeilenfilter zu erstellen, die sich wie Joinfilter verhalten:  
  
    ```  
    WHERE Customer.SalesPersonID IN (SELECT EmployeeID FROM Employee WHERE LoginID = SUSER_SNAME())   
    ```  
  
     Es wird dringend empfohlen, eine solche Logik statt in einer Unterabfrage in einem Joinfilter auszudrücken. Wenn Ihre Anwendung für die Verwendung einer Unterabfrage einen Zeilenfilter benötigt, stellen Sie sicher, dass die Unterabfrage ausschließlich Daten in der Nachschlagetabelle referenziert, die sich nicht ändern.  
  
## Siehe auch  
 [Filtern veröffentlichter Daten für die Mergereplikation](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)   
 [Parametrisierte Zeilenfilter](../../../relational-databases/replication/merge/parameterized-row-filters.md)  
  
  