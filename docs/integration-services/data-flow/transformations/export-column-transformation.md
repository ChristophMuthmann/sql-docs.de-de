---
title: Exportieren Sie Spaltentransformation | Microsoft Docs
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
- sql13.dts.designer.exportcolumntrans.f1
helpviewer_keywords:
- exporting data
- append options [Integration Services]
- Export Column transformation [Integration Services]
- columns [Integration Services], exporting
- inserting data
- truncate options [Integration Services]
ms.assetid: 678d2dfc-e40c-4fbb-b2cc-42fffc44478a
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e7e611452f931d049c63c822587dc7610bf1eb25
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="export-column-transformation"></a>Transformation für das Exportieren von Spalten
  Die Transformation für das Exportieren von Spalten liest Daten in einem Datenfluss und fügt sie in eine Datei ein. Wenn z. B. der Datenfluss Produktinformationen enthält, wie z. B. ein Image jedes Produkts, könnten Sie mithilfe der Transformation für das Exportieren von Spalten die Bilder in Dateien speichern.  
  
## <a name="append-and-truncate-options"></a>Optionen zum Anfügen und Abschneiden  
 In der folgenden Tabelle wird beschrieben, wie die Einstellungen für die Optionen zum Anfügen und Abschneiden die Ergebnisse beeinflussen.  
  
|Anfügen|Abschneiden|Die Datei ist vorhanden|Ergebnisse|  
|------------|--------------|-----------------|-------------|  
|False|False|Nein|Die Transformation erstellt eine neue Datei und schreibt die Daten in die Datei.|  
|Wahr|False|Nein|Die Transformation erstellt eine neue Datei und schreibt die Daten in die Datei.|  
|False|Wahr|Nein|Die Transformation erstellt eine neue Datei und schreibt die Daten in die Datei.|  
|Wahr|Wahr|Nein|Zur Entwurfszeit tritt bei der Überprüfung der Transformation ein Fehler auf. Beide Eigenschaften dürfen nicht auf **true**festgelegt werden.|  
|False|False|Ja|Ein Laufzeitfehler tritt auf. Die Datei ist vorhanden, aber die Transformation kann nicht in diese schreiben.|  
|False|Wahr|Ja|Die Transformation löscht die Datei und erstellt sie neu und schreibt die Daten in diese Datei.|  
|Wahr|False|Ja|Die Transformation öffnet die Datei und fügt die Daten am Dateiende an.|  
|Wahr|Wahr|Ja|Zur Entwurfszeit tritt bei der Überprüfung der Transformation ein Fehler auf. Beide Eigenschaften dürfen nicht auf **true**festgelegt werden.|  
  
## <a name="configuration-of-the-export-column-transformation"></a>Konfiguration der Transformation für das Exportieren von Spalten  
 Es gibt folgende Möglichkeiten, um die Transformation für das Exportieren von Spalten zu konfigurieren:  
  
-   Geben Sie die Datenspalten und die Spalten an, die den Pfad von Dateien enthalten, in die die Daten geschrieben werden sollen.  
  
-   Geben Sie an, ob der Vorgang zum Einfügen von Daten an vorhandene Dateien anfügt oder diese abschneidet.  
  
-   Geben Sie an, ob eine Bytereihenfolgemarke (BOM, Byte-Order Mark) in die Datei geschrieben wird.  
  
    > [!NOTE]  
    >  Eine BOM wird nur geschrieben, wenn die Daten nicht an eine vorhandene Datei angefügt werden und die Daten vom DT_NTEXT-Datentyp sind.  
  
 Die Transformation verwendet Eingabespaltenpaare: Eine Spalte enthält einen Dateinamen, die andere Spalte enthält Daten. In jeder Zeile des Datasets kann eine andere Datei angegeben sein. Beim Verarbeiten einer Zeile durch die Transformation werden die Daten in die angegebene Datei eingefügt. Zur Laufzeit erstellt die Transformation die Dateien, falls sie noch nicht vorhanden sind. Anschließend schreibt die Transformation die Daten in die Dateien. Die zu schreibenden Daten müssen den Datentyp DT_TEXT, DT_NTEXT oder DT_IMAGE aufweisen. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 Diese Transformation weist eine Eingabe, eine Ausgabe und eine Fehlerausgabe auf.  
  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Weitere Informationen zu den Eigenschaften, die Sie im Dialogfeld **Transformations-Editor für das Exportieren von Spalten** festlegen können, finden Sie unter [Transformations-Editor für das Exportieren von Spalten &#40;Seite Spalten&#41;](../../../integration-services/data-flow/transformations/export-column-transformation-editor-columns-page.md).  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften von Transformationen](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Informationen zum Festlegen von Eigenschaften finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
  
