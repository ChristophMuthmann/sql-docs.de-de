---
title: OData-Quelle | Microsoft-Dokumentation
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.DTS.DESIGNER.ODATASOURCE.F1
- sql13.dts.designer.odatasource.connection.f1
- sql13.dts.designer.odatasource.columns.f1
- sql13.dts.designer.odatasource.erroroutput.f1
ms.assetid: cc9003c9-638e-432b-867e-e949d50cec90
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9640bcc3af0bc8503ec0bdfaaf9116cc56aec3a1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="odata-source"></a>OData-Quelle
Verwenden Sie die OData-Quellkomponente in einem SSIS-Paket, um Daten aus einem Open Data Protocol (OData)-Dienst zu nutzen. Die Komponente unterstützt die OData v3 und v4-Protokolle.  
  
-   Für OData V3-Protokolle unterstützt die Komponente das ATOM- und das JSON-Datenformat.  
  
-   Für OData V4-Protokolle unterstützt die Komponente das JSON-Datenformat.  

Die OData-Quelle umfasst Unterstützung für die folgenden Datenquellen:
-   Microsoft Dynamics AX Online und Microsoft Dynamics CRM Online
-   SharePoint-Listen. Um alle Listen auf einem SharePoint-Server anzuzeigen, verwenden Sie die folgende URL: „http://\<Server>/_vti_bin/ListData.svc“. Weitere Informationen zu den URL-Konventionen in SharePoint finden Sie unter [SharePoint Foundation-REST-Schnittstelle](http://msdn.microsoft.com/library/ff521587.aspx).
  
## <a name="odata-format-and-performance"></a>OData-Format und Leistung
 Die meisten OData-Dienste können Ergebnisse in verschiedenen Formaten zurückgeben. Sie können das Format des Resultsets mithilfe der `$format`-Abfrageoption angeben. Formate wie JSON und JSON Light sind effizienter als ATOM oder XML und erzielen bei der Übertragung großer Datenmengen möglicherweise eine bessere Leistung. In der folgenden Tabelle sind Ergebnisse aus Beispieltests dargestellt. Wie Sie erkennen können, ergab der Wechsel von ATOM zu JSON einen Leistungszuwachs von 30-53% und der Wechsel von ATOM zum neuen JSON Light-Format (verfügbar in WCF Data Services 5.1) einen Leistungszuwachs von 67 %.  
  
|Zeilen|ATOM|JSON|JSON (Light)|  
|-|-|-|-|  
|10000|113 Sekunden|74 Sekunden|68 Sekunden|  
|1000000|1110 Sekunden|853 Sekunden|665 Sekunden|  
  
## <a name="related-topics-in-this-section"></a>Verwandte Themen in diesem Abschnitt  
  
-   [Lernprogramm: Verwenden der OData-Quelle](../../integration-services/data-flow/tutorial-using-the-odata-source.md)  
  
-   [Ändern einer OData-Quellabfrage zur Laufzeit](../../integration-services/data-flow/modify-odata-source-query-at-runtime.md)  
  
-   [OData-Quelleneigenschaften](../../integration-services/data-flow/odata-source-properties.md)  
  
## <a name="odata-source-editor-connection-page"></a>Quellen-Editor für OData (Seite 'Verbindung')
  Auf der Seite **Verbindung** des Dialogfelds **Quellen-Editor für OData** wählen Sie den OData-Verbindungs-Manager für die OData-Quelle aus. Auf dieser Seite können Sie außerdem eine Auflistung oder einen Ressourcenpfad sowie beliebige Abfrageoptionen angeben, mit denen die aus der OData-Quelle abzurufenden Daten bestimmt werden. 
  
### <a name="static-options"></a>Statische Optionen  
 **OData-Verbindungs-Manager**  
 Wählen Sie in der Liste einen vorhandenen Verbindungs-Manager aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu**klicken.  
  
 Nach dem Auswählen oder Erstellen eines Verbindungs-Managers wird im Dialogfeld die vom Verbindungs-Manager verwendete OData-Protokollversion angezeigt.  
  
 **Neu**  
 Erstellen Sie mithilfe des Dialogfelds **OData-Verbindungs-Manager-Editor** einen neuen Verbindungs-Manager.  
  
 **Auflistung oder Ressourcenpfad verwenden**  
 Geben Sie die Methode für die Auswahl von Daten aus der Quelle an.  
  
|Option|Description|  
|------------|-----------------|  
|Auflistung|Rufen Sie mithilfe eines Auflistungsnamens Daten aus der OData-Quelle ab.|  
|Ressourcenpfad|Rufen Sie mithilfe eines Ressourcenpfads Daten aus der OData-Quelle ab.|  
  
 **Abfrageoptionen**  
 Geben Sie Optionen für die Abfrage an. Beispiel: `$top=5` 
  
 **Feed-URL**  
 Zeigt die schreibgeschützte Feed-URL auf Grundlage der Optionen an, die Sie in diesem Dialogfeld ausgewählt haben.  
  
 **Vorschau**  
 Zeigt mithilfe des Dialogfelds **Vorschau** eine Vorschau der Ergebnisse an. In der**Vorschau** können bis zu 20 Zeilen angezeigt werden.  
  
### <a name="dynamic-options"></a>Dynamische Optionen  
  
#### <a name="use-collection-or-resource-path--collection"></a>Auflistung oder Ressourcenpfad verwenden = Auflistung  
 **Auflistung**  
 Wählen Sie eine Auflistung aus dem Dropdownlistenfeld aus.  
  
#### <a name="use-collection-or-resource-path--resource-path"></a>Auflistung oder Ressourcenpfad verwenden = Ressourcenpfad  
 **Resource path**  
 Geben Sie einen Ressourcenpfad ein. Beispiel: Mitarbeiter  
  
## <a name="odata-source-editor-columns-page"></a>Quellen-Editor für OData (Seite 'Spalten')
  Verwenden Sie die Seite **Spalten** im Dialogfeld **Quellen-Editor für OData**, um externe (Quell-)Spalten auszuwählen, die in der Ausgabe enthalten sein sollen, und um die Spalten und Ausgabespalten einander zuzuordnen.  
  
### <a name="options"></a>Tastatur  
 **Verfügbare externe Spalten**  
 Zeigt die Liste der in der Datenquelle verfügbaren Quellspalten an. Verwenden Sie Kontrollkästchen in der Liste, um in der Tabelle am Ende der Seite Spalten hinzuzufügen bzw. Spalten zu entfernen. Die ausgewählten Spalten werden der Ausgabe hinzugefügt.  
  
 **Externe Spalte**  
 Zeigt auswählbare Quellspalten an, die Sie in die Ausgabe einschließen können.  
  
 **Ausgabespalte**  
 Geben Sie für jede Ausgabespalte einen eindeutigen Namen an. Standardmäßig wird der Name der ausgewählten externen (Quell-)Spalte verwendet. Sie können jedoch auch einen beschreibenden Namen angeben, sofern dieser eindeutig ist.  
  
## <a name="odata-source-editor-error-output-page"></a>Quellen-Editor für OData (Seite 'Fehlerausgabe')
  Mithilfe der Seite **Fehlerausgabe** des Dialogfelds **Quellen-Editor für OData** können Sie Fehlerbehandlungsoptionen auswählen und Eigenschaften für Fehlerausgabespalten festlegen.  
  
### <a name="options"></a>Tastatur  
 **Eingabe/Ausgabe**  
 Zeigt den Namen der Datenquelle an.  
  
 **Column**  
 Zeigt die externen (Quell-)Spalten an, die im Dialogfeld **Quellen-Editor für OData** auf der Seite **Verbindungs-Manager** ausgewählt wurden.  
  
 **Fehler**  
 Gibt an, was bei Auftreten eines Fehlers geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Verwandte Themen:** [Fehlerbehandlung in Daten](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Abschneiden**  
 Gibt an, was im Falle einer Kürzung geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Beschreibung**  
 Zeigt die Beschreibung des Fehlers an.  
  
 **Diesen Wert für ausgewählte Zellen festlegen**  
 Gibt an, was im Falle eines Fehlers oder einer Kürzung mit den ausgewählten Zellen geschehen soll: den Fehler ignorieren, die Zeile umleiten oder die Komponente mit einem Fehler abbrechen.  
  
 **Anwenden**  
 Wendet die Fehlerbehandlungsoption auf die ausgewählten Zellen an.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OData-Verbindungs-Manager](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  
