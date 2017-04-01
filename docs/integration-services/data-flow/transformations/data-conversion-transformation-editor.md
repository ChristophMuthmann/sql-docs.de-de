---
title: "Transformations-Editor f&#252;r Datenkonvertierung | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.dataconversiontransformation.f1"
helpviewer_keywords: 
  - "Transformations-Editor für Datenkonvertierung"
ms.assetid: 7b4e4873-e8fe-4549-a965-65bebdb270bc
caps.latest.revision: 28
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 28
---
# Transformations-Editor f&#252;r Datenkonvertierung
  Im Dialogfeld **Transformations-Editor für Datenkonvertierung** können Sie die zu konvertierenden Spalten und den Datentyp, in den die Spalte konvertiert werden soll, auswählen und Konvertierungsattribute festlegen.  
  
> [!NOTE]  
>  Die **FastParse** -Eigenschaft der Ausgabespalten der Transformation für Datenkonvertierung ist im **Transformations-Editor für Datenkonvertierung**nicht verfügbar, kann aber mithilfe des **erweiterten Editors**festgelegt werden. Weitere Informationen zu dieser Eigenschaft finden Sie im Abschnitt "Transformation für Datenkonvertierung" von [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Weitere Informationen zur Transformation für Datenkonvertierung finden Sie unter [Data Conversion Transformation](../../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
## enthalten  
 **Verfügbare Eingabespalten**  
 Wählen Sie mithilfe der Kontrollkästchen die zu konvertierenden Spalten aus. Durch Ihre Auswahl werden der nachfolgenden Tabelle Eingabespalten hinzugefügt.  
  
 **Eingabespalte**  
 Wählen Sie zu konvertierende Spalten aus der Liste der verfügbaren Eingabespalten aus. Ihre Auswahl wird entsprechend in der Auswahl der Kontrollkästchen oben deutlich.  
  
 **Ausgabealias**  
 Geben Sie einen Alias für jede neue Spalte ein. Der Standard lautet **Copy of** , gefolgt vom Namen der Eingabespalte. Sie können jedoch auch einen eindeutigen, beschreibenden Namen auswählen.  
  
 **Datentyp**  
 Wählen Sie einen verfügbaren Datentyp aus der Liste aus. Weitere Informationen finden Sie unter [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 **Länge**  
 Legt für Zeichenfolgendaten die Spaltenlänge fest.  
  
 **Genauigkeit**  
 Legt für numerische Daten die Genauigkeit fest.  
  
 **Dezimalstellen**  
 Legt für numerische Daten die Dezimalstellen fest.  
  
 **Codepage**  
 Wählen Sie die geeignete Codepage für Spalten vom Typ DT_STR aus.  
  
 **Fehlerausgabe konfigurieren**  
 Geben Sie mithilfe des Dialogfelds [Fehlerausgabe konfigurieren](../Topic/Configure%20Error%20Output.md) an, wie Fehler auf Zeilenebene behandelt werden sollen.  
  
## Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Konvertieren von Daten in einen anderen Datentyp mithilfe der Transformation für Datenkonvertierung](../../../integration-services/data-flow/transformations/convert-data-type-by-using-data-conversion-transformation.md)  
  
  