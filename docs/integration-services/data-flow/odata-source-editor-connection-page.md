---
title: "Quellen-Editor f&#252;r OData (Seite &#39;Verbindung&#39;) | Microsoft Docs"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.odatasource.connection.f1"
ms.assetid: 20bcd347-4547-4fad-b182-9571030101df
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Quellen-Editor f&#252;r OData (Seite &#39;Verbindung&#39;)
  Auf der Seite **Verbindung** des Dialogfelds **Quellen-Editor für OData** wählen Sie den OData-Verbindungs-Manager für die OData-Quelle aus. Auf dieser Seite können Sie außerdem eine Auflistung oder einen Ressourcenpfad sowie beliebige Abfrageoptionen angeben, mit denen die aus der OData-Quelle abzurufenden Daten bestimmt werden. Weitere Informationen zur OData-Quelle finden Sie unter [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## Statische Optionen  
 **OData-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Verbindungs-Manager aus der Liste aus, oder erstellen Sie eine neue Verbindung, indem Sie auf **Neu** klicken.  
  
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
 Geben Sie Optionen für die Abfrage an.  Beispiel: $top=5  
  
 **Feed-URL**  
 Zeigt die schreibgeschützte Feed-URL auf Grundlage der Optionen an, die Sie in diesem Dialogfeld ausgewählt haben.  
  
 **Vorschau**  
 Zeigt mithilfe des Dialogfelds **Vorschau** eine Vorschau der Ergebnisse an. In der**Vorschau** können bis zu 20 Zeilen angezeigt werden.  
  
## Dynamische Optionen  
  
### Auflistung oder Ressourcenpfad verwenden = Auflistung  
 **Auflistung**  
 Wählen Sie eine Auflistung aus dem Dropdownlistenfeld aus.  
  
### Auflistung oder Ressourcenpfad verwenden = Ressourcenpfad  
 **Ressourcenpfad**  
 Geben Sie einen Ressourcenpfad ein. Beispiel: Mitarbeiter  
  
## Siehe auch  
 [Quellen-Editor für OData &#40;Seite „Spalten“&#41;](../../integration-services/data-flow/odata-source-editor-columns-page.md)   
 [Quellen-Editor für OData &#40;Seite „Fehlerausgabe“&#41;](../../integration-services/data-flow/odata-source-editor-error-output-page.md)   
 [OData-Verbindungs-Manager](../../integration-services/connection-manager/odata-connection-manager.md)  
  
  