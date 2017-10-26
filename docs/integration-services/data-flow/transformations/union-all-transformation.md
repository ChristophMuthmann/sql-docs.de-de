---
title: Union All-Transformation | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.unionalltrans.f1
- sql13.dts.designer.unionalltransformation.f1
helpviewer_keywords:
- merging datasets [Integration Services]
- combining datasets
- Union All transformation
- datasets [Integration Services], merging
ms.assetid: 942e4b90-9c41-4e9c-a6f3-80b3afe57f2f
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: e947aa8b3d079830b9433ba1b01450fda699904a
ms.contentlocale: de-de
ms.lasthandoff: 08/19/2017

---
# <a name="union-all-transformation"></a>Transformation für UNION ALL
  Die Transformation für UNION ALL kombiniert mehrere Eingaben zu einer einzigen Ausgabe. Beispielsweise können die Ausgaben von fünf verschiedenen Flatfilequellen Eingaben für die Transformation für UNION ALL sein und zu einer einzigen Ausgabe kombiniert werden.  
  
## <a name="inputs-and-outputs"></a>Eingaben und Ausgaben  
 Die Transformationseingaben werden der Transformationsausgabe nacheinander hinzugefügt. Die Zeilen werden nicht neu angeordnet. Falls das Paket eine sortierte Ausgabe erfordert, sollten Sie anstelle der Transformation für UNION ALL die Transformation für Zusammenführen verwenden.  
  
 Die erste Eingabe, die Sie mit der Transformation für UNION ALL verbinden, ist die Eingabe, von der die Transformation die Transformationsausgabe erstellt. Die Spalten in den Eingaben, die Sie anschließend mit der Transformation verbinden, werden den Spalten in der Transformationsausgabe zugeordnet.  
  
 Um Eingaben zusammenzuführen, ordnen Sie Eingabespalten Ausgabespalten zu. Eine Spalte von mindestens einer Eingabe muss jeder Ausgabespalte zugeordnet werden. Für die Zuordnung von zwei Spalten müssen die Metadaten der Spalten übereinstimmen. Beispielsweise müssen die zugeordneten Spalten denselben Datentyp aufweisen.  
  
 Wenn die zugeordneten Spalten Zeichenfolgendaten enthalten und die Ausgabespalte kürzer als die Eingabespalte ist, wird die Ausgabespalte automatisch verlängert, damit die Eingabespalten Platz haben. Für Eingabespalten, die keinen Ausgabespalten zugeordnet werden, werden in den Ausgabespalten NULL-Werte festgelegt.  
  
 Diese Transformation weist mehrere Eingaben und eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="configuration-of-the-union-all-transformation"></a>Konfiguration der Transformation für UNION ALL  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie programmgesteuert festlegen können, finden Sie unter [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zum Festlegen von Eigenschaften anzuzeigen:  
  
-   [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="union-all-transformation-editor"></a>Transformations-Editor für UNION ALL
  Mithilfe des Dialogfelds **Transformations-Editor für UNION ALL** können Sie mehrere Eingaberowsets zu einem einzigen Ausgaberowset zusammenführen. Durch das Einschließen der Transformation für UNION ALL in einen Datenfluss können Sie Daten aus mehreren Datenflüssen zusammenführen, komplexe Datasets durch Verschachteln der Transformationen für UNION ALL erstellen und Zeilen erneut zusammenführen, nachdem Sie Fehler in den Daten korrigiert haben.  
  
### <a name="options"></a>enthalten  
 **Name der Ausgabespalte**  
 Geben Sie einen Alias für jede Spalte ein. Standardmäßig wird der Name der Eingabespalte von der ersten (Referenz-)Eingabe verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
 **Eingabe 1 für UNION ALL**  
 Wählen Sie eine Eingabespalte aus der Liste der verfügbaren Eingabespalten in der ersten (Referenz-)Eingabe aus. Die Metadaten der zugeordneten Spalten müssen übereinstimmen.  
  
 **Eingabe n für UNION ALL**  
 Wählen Sie eine Eingabespalte aus der Liste der verfügbaren Eingabespalten in den folgenden Eingaben aus. Die Metadaten der zugeordneten Spalten müssen übereinstimmen.  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
 [Zusammenführen von Daten mithilfe der Transformation für UNION ALL](../../../integration-services/data-flow/transformations/merge-data-by-using-the-union-all-transformation.md)  
  
  

