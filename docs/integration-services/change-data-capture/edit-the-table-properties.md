---
title: "Bearbeiten der Tabelleneigenschaften | Microsoft Docs"
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
  - "editTabProps"
ms.assetid: 95ea72ba-8e40-4177-a963-0fb4d10c56e3
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Bearbeiten der Tabelleneigenschaften
  Verwenden Sie dieses Dialogfeld, um die spezifischen Spalten der ausgewählten Tabelle zu bearbeiten, in der Änderungen aufgezeichnet werden. Sie können auch die Informationen unter **Security Role** und **Capture Instance** bearbeiten.  
  
### So bearbeiten Sie die Spalten, die in die CDC-Instanz eingeschlossen werden sollen  
  
1.  Führen Sie einen oder beide der folgenden Schritte aus:  
  
    -   Aktivieren Sie das Kontrollkästchen neben einer beliebigen zusätzlichen Spalte, die Sie einschließen möchten.  
  
    -   Deaktivieren Sie das Kontrollkästchen neben den Spalten, die nicht mehr enthalten sein sollen.  
  
### So bearbeiten Sie die Sicherheitsrolle  
  
1.  Geben Sie im Feld **Security Role** einen neuen Namen ein, oder bearbeiten Sie den Namen.  
  
### So erstellen Sie eine neue Aufzeichnungsinstanz  
  
1.  Geben Sie im Abschnitt **Security Role** im Feld **Name** einen Namen für die Aufzeichnungsinstanz ein. Standardmäßig entspricht der Name im Feld dem Namen der aktuellen Aufzeichnungsinstanz mit dem Zusatz **_NEW** (z.B. **alte_instanz_NEW**).  
  
2.  Speichern Sie die Aufzeichnungsinstanz wie folgt:  
  
    -   **New Capture Instance**: In diesem Fall wird eine neue Aufzeichnungsinstanz gespeichert und die alte Aufzeichnungsinstanz nicht gelöscht.  
  
         **Hinweis**: Sie können pro Tabelle nicht mehr als zwei Aufzeichnungsinstanzen verwenden. Falls bereits zwei Aufzeichnungsinstanzen vorhanden sind, ist diese Option nicht verfügbar.  
  
    -   **Replace Existing**: In diesem Fall wird die aktuelle Aufzeichnungsinstanz gelöscht und durch die erstellte Aufzeichnungsinstanz ersetzt. Wenn für die Tabelle zwei Aufzeichnungsinstanzen definiert sind, müssen Sie eine Instanz auswählen, die ersetzt werden soll.  
  
 **Hinweis**: Sie können eine Aufzeichnungsinstanz aus der Liste der Tabellen auf der Registerkarte **Tabelle** entfernen.  
  
 Klicken Sie auf **OK** , nachdem Sie die Informationen in diesem Dialogfeld eingegeben haben, um die Änderungen zu übernehmen.  
  
## Siehe auch  
 [Bearbeiten der CDC-Instanzeigenschaften](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Vornehmen von Änderungen an den zum Aufzeichnen von Änderungen ausgewählten Tabellen](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md)  
  
  