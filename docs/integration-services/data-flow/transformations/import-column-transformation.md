---
title: "Transformation f&#252;r das Importieren von Spalten | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.importcolumntrans.f1"
helpviewer_keywords: 
  - "Transformation für das Importieren von Spalten [Integration Services]"
  - "Spalten [Integration Services], importieren"
  - "Importieren von Daten, SSIS-Pakete"
  - "Einfügen von Daten"
ms.assetid: ac3b74c1-ef54-4297-8062-1734324fffcc
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Transformation f&#252;r das Importieren von Spalten
  Die Transformation für das Importieren von Spalten liest Daten aus Dateien und fügt die Daten Spalten in einem Datenfluss hinzu. Mit dieser Transformation kann ein Paket einem Datenfluss Text und Bilder hinzufügen, die in separaten Dateien gespeichert sind. Beispielsweise können in einem Datenfluss, der Daten in eine Tabelle mit Produktinformationen lädt, mit der Transformation für das Importieren von Spalten Kundenbeurteilungen für jedes Produkt aus Dateien importiert und die Beurteilungen dem Datenfluss hinzugefügt werden.  
  
 Es gibt folgende Möglichkeiten, um die Transformation für das Importieren von Spalten zu konfigurieren:  
  
-   Geben Sie die Tabelle an, der die Transformation Daten hinzufügt.  
  
-   Geben Sie an, ob die Transformation eine Bytereihenfolgemarke (BOM, Byte-Order Mark) erwartet.  
  
    > [!NOTE]  
    >  Eine BOM wird nur bei Daten vom DT_NTEXT-Datentyp erwartet.  
  
 Eine Spalte in der Transformationseingabe enthält die Namen von Dateien, in denen die Daten gespeichert sind. In jeder Zeile des Datasets kann eine andere Datei angegeben sein. Wenn die Transformation für das Importieren von Spalten eine Zeile verarbeitet, wird der Dateiname gelesen, die entsprechende Datei im Dateisystem geöffnet und der Dateiinhalt in eine Ausgabespalte geladen. Die Ausgabespalte muss den Datentyp DT_TEXT, DT_NTEXT oder DT_IMAGE aufweisen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Diese Transformation weist eine Eingabe, eine Ausgabe und eine Fehlerausgabe auf.  
  
## Konfiguration der Transformation für das Importieren von Spalten  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Verwandte Aufgaben  
 Informationen zum Festlegen der Eigenschaften dieser Komponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Siehe auch  
 [Transformation für das Exportieren von Spalten](../../../integration-services/data-flow/transformations/export-column-transformation.md)   
 [Datenfluss](../../../integration-services/data-flow/data-flow.md)   
 [SQL Server Integration Services-Transformationen](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  