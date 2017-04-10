---
title: "Flatfileziel | Microsoft Docs"
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
  - "sql13.dts.designer.flatfiledest.f1"
helpviewer_keywords: 
  - "Flatfiles"
  - "Flatfileziel"
  - "Schreiben von Textdateien [Integration Services]"
  - "Ziele [Integration Services], Flatfile"
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 49
---
# Flatfileziel
  Das Flatfileziel schreibt Daten in eine Textdatei. Die Textdatei kann in verschiedenen Formaten vorliegen: mit Trennzeichen, mit fester Breite, mit fester Breite mit Zeilentrennzeichen oder mit rechtem Flatterrand.  
  
 Es gibt folgende Möglichkeiten, um das Flatfileziel zu konfigurieren:  
  
-   Geben Sie einen Textblock an, der in die Datei eingefügt wird, bevor Daten geschrieben werden. Der Text kann Informationen bereitstellen, wie z. B. Spaltenüberschriften.  
  
-   Geben Sie an, ob Daten in einer gleichnamigen Zieldatei überschrieben werden sollen.  
  
 Dieses Ziel verwendet für den Zugriff auf die Textdatei einen Verbindungs-Manager für Flatfiles. Durch Festlegen von Eigenschaften im Verbindungs-Manager für Flatfiles, der vom Flatfileziel verwendet wird, können Sie angeben, wie das Flatfileziel die Textdatei formatiert und schreibt. Wenn Sie den Verbindungs-Manager für Flatfiles konfigurieren, geben Sie Informationen zur Datei und zu jeder Spalte in der Datei an. Beispielsweise können Sie die Zeichen angeben, mit denen Spalten und Zeilen in der Datei getrennt werden, sowie den Datentyp und die Länge jeder Spalte. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Das Flatfileziel schließt die benutzerdefinierte Header-Eigenschaft ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften der Flatfile](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Das Ziel weist eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## Konfiguration des Flatfileziels  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Quellen-Editor für Flatfiles** festlegen können:  
  
-   [Ziel-Editor für Flatfiles &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/flat-file-destination-editor-connection-manager-page.md)  
  
-   [Ziel-Editor für Flatfiles &#40;Seite „Zuordnungen“&#41;](../../integration-services/data-flow/flat-file-destination-editor-mappings-page.md)  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Allgemeine Eigenschaften](../Topic/Common%20Properties.md)  
  
-   [Benutzerdefinierte Eigenschaften der Flatfile](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## Verwandte Aufgaben  
 Informationen zum Festlegen der Eigenschaften einer Datenflusskomponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Siehe auch  
 [Flatfilequelle](../../integration-services/data-flow/flat-file-source.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  