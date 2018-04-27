---
title: Flatfileziel | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.flatfiledest.f1
- sql13.dts.designer.flatfiledestadapter.connection.f1
- sql13.dts.designer.flatfiledestadapter.mappings.f1
helpviewer_keywords:
- flat files
- Flat File destination
- text file writing [Integration Services]
- destinations [Integration Services], Flat File
ms.assetid: e0d6e356-8db4-48aa-ba66-029397f98f61
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: c649a4d31129d3719a3a648547b2139c767b6e61
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="flat-file-destination"></a>Flatfileziel
  Das Flatfileziel schreibt Daten in eine Textdatei. Die Textdatei kann in verschiedenen Formaten vorliegen: mit Trennzeichen, mit fester Breite, mit fester Breite mit Zeilentrennzeichen oder mit rechtem Flatterrand.  
  
 Es gibt folgende Möglichkeiten, um das Flatfileziel zu konfigurieren:  
  
-   Geben Sie einen Textblock an, der in die Datei eingefügt wird, bevor Daten geschrieben werden. Der Text kann Informationen bereitstellen, wie z. B. Spaltenüberschriften.  
  
-   Geben Sie an, ob Daten in einer gleichnamigen Zieldatei überschrieben werden sollen.  
  
 Dieses Ziel verwendet für den Zugriff auf die Textdatei einen Verbindungs-Manager für Flatfiles. Durch Festlegen von Eigenschaften im Verbindungs-Manager für Flatfiles, der vom Flatfileziel verwendet wird, können Sie angeben, wie das Flatfileziel die Textdatei formatiert und schreibt. Wenn Sie den Verbindungs-Manager für Flatfiles konfigurieren, geben Sie Informationen zur Datei und zu jeder Spalte in der Datei an. Beispielsweise können Sie die Zeichen angeben, mit denen Spalten und Zeilen in der Datei getrennt werden, sowie den Datentyp und die Länge jeder Spalte. Weitere Informationen finden Sie unter [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
 Das Flatfileziel schließt die benutzerdefinierte Header-Eigenschaft ein. Diese Eigenschaft kann beim Laden des Pakets mithilfe eines Eigenschaftsausdrucks aktualisiert werden. Weitere Informationen finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md) und [Benutzerdefinierte Eigenschaften der Flatfile](../../integration-services/data-flow/flat-file-custom-properties.md).  
  
 Das Ziel weist eine Ausgabe auf. Eine Fehlerausgabe wird nicht unterstützt.  
  
## <a name="configuration-of-the-flat-file-destination"></a>Konfiguration des Flatfileziels  
 Sie können Eigenschaften mit dem [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designer oder programmgesteuert festlegen.  
  
 Das Dialogfeld **Erweiterter Editor** enthält die Eigenschaften, die programmgesteuert festgelegt werden können. Klicken Sie auf eines der folgenden Themen, um weitere Informationen zu den Eigenschaften zu erhalten, die Sie im Dialogfeld **Erweiterter Editor** oder programmgesteuert festlegen können:  
  
-   [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Benutzerdefinierte Eigenschaften der Flatfile](../../integration-services/data-flow/flat-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Informationen zum Festlegen der Eigenschaften einer Datenflusskomponente finden Sie unter [Festlegen der Eigenschaften einer Datenflusskomponente](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="flat-file-destination-editor-connection-manager-page"></a>Ziel-Editor für Flatfiles (Seite Verbindungs-Manager)
  Mithilfe der Seite **Verbindungs-Manager** des Dialogfelds **Ziel-Editor für Flatfiles** können Sie die Flatfile-Verbindung für das Ziel auswählen und angeben, ob die vorhandene Zieldatei überschrieben werden soll oder ob die Daten an die vorhandene Datei angehängt werden sollen. Das Flatfileziel schreibt Daten in eine Textdatei. Als Format für diese Textdatei können Trennzeichen, feste Breite, feste Breite mit Zeilentrennzeichen oder rechter Flatterrand gewählt werden.  
  
### <a name="options"></a>Tastatur  
 **Verbindungs-Manager für Flatfiles**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus dem Listenfeld aus, oder erstellen Sie durch Klicken auf **Neu**eine neue Verbindung.  
  
 **Neu**  
 Erstellen Sie eine neue Verbindung mithilfe der Dialogfelder **Flatfileformat** und **Verbindungs-Manager-Editor für Flatfiles** .  
  
 Neben den standardmäßigen Flatfileformaten mit Trennzeichen, fester Breite oder rechtem Flatterrand verfügt das Dialogfeld **Flatfileformat** über eine vierte Option, **Feste Breite mit Zeilentrennzeichen**. Diese Option stellt einen Sonderfall des Formats mit rechtem Flatterrand dar, bei dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] eine Pseudospalte als letzte Datenspalte hinzufügt. Diese Pseudospalte stellt sicher, dass die letzte Spalte über eine feste Breite verfügt.  
  
 Die Option **Feste Breite mit Zeilentrennzeichen** ist im **Verbindungs-Manager-Editor für Flatfiles**nicht verfügbar. Sofern erforderlich, können Sie diese Option im Editor emulieren. Um diese Option zu emulieren, wählen Sie im **Verbindungs-Manager-Editor für Flatfiles** auf der Seite **Allgemein**für **Format**die Option **Rechter Flatterrand**aus. Fügen Sie dann im Editor auf der Seite **Erweitert** eine neue Pseudospalte als letzte Datenspalte hinzu.  
  
 **Daten in der Datei überschreiben**  
 Gibt an, ob eine vorhandene Datei überschrieben, oder ob Daten angehängt werden sollen.  
  
 **Header**  
 Geben Sie einen in die Datei einzufügenden Textblock ein, bevor Daten geschrieben werden. Mithilfe dieser Option können Sie zusätzliche Informationen wie Spaltenüberschriften hinzufügen.  
  
 **Vorschau**  
 Zeigen Sie mithilfe des Dialogfelds **Datenansicht** eine Vorschau der Ergebnisse an. In der Vorschau können bis zu 200 Zeilen angezeigt werden.  
  
## <a name="flat-file-destination-editor-mappings-page"></a>Ziel-Editor für Flatfiles (Seite Zuordnungen)
  Auf der Seite **Zuordnungen** des Dialogfelds **Ziel-Editor für Flatfiles** können Sie eine Zuordnung von Eingabe- zu Zielspalten vornehmen.  
  
### <a name="options"></a>Tastatur  
 **Verfügbare Eingabespalten**  
 Zeigt die Liste der verfügbaren Eingabespalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Eingabespalten den Zielspalten zuordnen.  
  
 **Verfügbare Zielspalten**  
 Zeigt die Liste der verfügbaren Zielspalten an. Mithilfe eines Drag-und-Drop-Vorgangs können Sie verfügbare Zielspalten den Eingabespalten zuordnen.  
  
 **Eingabespalte**  
 Zeigt die zu einem früheren Zeitpunkt in diesem Thema ausgewählten Eingabespalten an. Die Zuordnungen können Sie mithilfe der Liste **Verfügbare Eingabespalten**ändern. Wählen Sie **\<ignore>** aus, um die Spalte von der Ausgabe auszuschließen.  
  
 **Zielspalte**  
 Zeigt alle verfügbaren Zielspalten an, und ob sie zugeordnet sind.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Flatfilequelle](../../integration-services/data-flow/flat-file-source.md)   
 [Datenfluss](../../integration-services/data-flow/data-flow.md)  
  
  
