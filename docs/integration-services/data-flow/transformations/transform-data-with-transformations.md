---
title: Transformieren von Daten mit Transformationen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data flow [Integration Services], transformations
- transformations [Integration Services], about transformations
- transforming data [Integration Services]
ms.assetid: e1340b6f-ef75-4b14-af6f-823586eff0ed
caps.latest.revision: "43"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 94d528e378d85709f8accc5526636d73d305d6a2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="transform-data-with-transformations"></a>Transformieren von Daten mit Transformationen
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] schließt drei verschiedene Arten von Datenflusskomponenten ein: Quellen, Transformationen und Ziele.  
  
 Im folgenden Diagramm wird ein einfacher Datenfluss mit einer Quelle, zwei Transformationen und einem Ziel dargestellt.  
  
 ![Data flow](../../../integration-services/data-flow/media/mw-dts-08.gif "Data flow")  
  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Transformationen stellen die folgende Funktionalität bereit:  
  
-   Teilen, Kopieren und Zusammenführen von Rowsets und Ausführen von Suchvorgängen.  
  
-   Aktualisieren von Spaltenwerten und Erstellen neuer Spalten durch Anwenden von Transformationen, wie z. B. das Ändern von Großbuchstaben in Kleinbuchstaben.  
  
-   Ausführen von Business Intelligence-Vorgängen, wie z. B. das Bereinigen von Daten, Text Mining oder das Ausführen von Data Mining-Vorhersageabfragen.  
  
-   Erstellen neuer Rowsets, die aus Aggregatwerten oder sortierten Werten, Stichprobendaten oder pivotierten bzw. entpivotierten Daten bestehen.  
  
-   Ausführen von Aufgaben, wie z. B. das Exportieren und Importieren von Daten, das Bereitstellen von Überwachungsinformationen sowie das Verwenden von langsam veränderlichen Dimensionen.  
  
 Weitere Informationen finden Sie unter [Integration Services Transformations](../../../integration-services/data-flow/transformations/integration-services-transformations.md).  
  
 Sie können auch benutzerdefinierte Transformationen erstellen. Weitere Informationen finden Sie unter [Entwickeln einer benutzerdefinierten Datenflusskomponente](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) und [Entwickeln bestimmter Arten von Datenflusskomponenten](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md).  
  
 Nachdem Sie dem Datenfluss-Designer die Transformation hinzugefügt haben, jedoch bevor Sie die Transformation konfigurieren, verbinden Sie die Transformation mit dem Datenfluss. Hierzu verbinden Sie die Ausgabe einer anderen Transformation oder Quelle im Datenfluss mit der Eingabe dieser Transformation. Der Konnektor zwischen den beiden Datenflusskomponenten wird als Pfad bezeichnet. Weitere Informationen zum Verbinden von Komponenten und zum Verwenden von Pfaden finden Sie unter [Verbinden von Komponenten mit Pfaden](http://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8).  
  
### <a name="to-add-a-transformation-to-a-data-flow"></a>So fügen Sie einem Datenfluss eine Transformation hinzu  
  
-   [Hinzufügen oder Löschen einer Komponente im Datenfluss](../../../integration-services/data-flow/add-or-delete-a-component-in-a-data-flow.md)  
  
### <a name="to-connect-a-transformation-to-a-data-flow"></a>So verbinden Sie eine Transformation mit einem Datenfluss  
  
-   [Verbinden von Komponenten in einem Datenfluss](../../../integration-services/data-flow/connect-components-in-a-data-flow.md)  
  
### <a name="to-set-the-properties-of-a-transformation"></a>So legen Sie die Eigenschaften einer Transformation fest  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Datenflusstask](../../../integration-services/control-flow/data-flow-task.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [Verbinden von Komponenten mit Pfaden](http://msdn.microsoft.com/library/05633e4c-1370-4b05-802b-f36b07dd71c8)   
 [Fehlerbehandlung in Daten](../../../integration-services/data-flow/error-handling-in-data.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)  
  
  
