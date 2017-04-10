---
title: "Transformations-Editor f&#252;r UNION ALL | Microsoft Docs"
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
  - "sql13.dts.designer.unionalltransformation.f1"
helpviewer_keywords: 
  - "Transformations-Editor für UNION ALL"
ms.assetid: 32fbc1c1-da83-4684-9479-31fc3e2df98c
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Transformations-Editor f&#252;r UNION ALL
  Mithilfe des Dialogfelds **Transformations-Editor für UNION ALL** können Sie mehrere Eingaberowsets zu einem einzigen Ausgaberowset zusammenführen. Durch das Einschließen der Transformation für UNION ALL in einen Datenfluss können Sie Daten aus mehreren Datenflüssen zusammenführen, komplexe Datasets durch Verschachteln der Transformationen für UNION ALL erstellen und Zeilen erneut zusammenführen, nachdem Sie Fehler in den Daten korrigiert haben.  
  
 Weitere Informationen zur Transformation für UNION ALL finden Sie unter [Union All Transformation](../../../integration-services/data-flow/transformations/union-all-transformation.md).  
  
## enthalten  
 **Name der Ausgabespalte**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte von der ersten (Referenz-)Eingabe verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Eingabe 1 für UNION ALL**  
 Wählen Sie eine Eingabespalte aus der Liste der verfügbaren Eingabespalten in der ersten (Referenz-)Eingabe aus. Die Metadaten der zugeordneten Spalten müssen übereinstimmen.  
  
 **Eingabe n für UNION ALL**  
 Wählen Sie eine Eingabespalte aus der Liste der verfügbaren Eingabespalten in den folgenden Eingaben aus. Die Metadaten der zugeordneten Spalten müssen übereinstimmen.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Zusammenführen von Daten mithilfe der Transformation für UNION ALL](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)   
 [Transformation für Zusammenführen](../../../integration-services/data-flow/transformations/merge-transformation.md)   
 [Transformation für Zusammenführungsjoin](../../../integration-services/data-flow/transformations/merge-join-transformation.md)  
  
  