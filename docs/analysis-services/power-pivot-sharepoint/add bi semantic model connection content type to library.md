---
title: "Hinzuf&#252;gen eines BI-Semantikmodell-Verbindungs-Inhaltstyps zu einer Bibliothek (PowerPivot f&#252;r SharePoint) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 145505ed-50bc-4528-912b-2a5cd2566011
caps.latest.revision: 13
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Hinzuf&#252;gen eines BI-Semantikmodell-Verbindungs-Inhaltstyps zu einer Bibliothek (PowerPivot f&#252;r SharePoint)
  Eine BI-Semantikmodellverbindung wird in SharePoint erstellt und stellt eine Umleitung zu den Business Intelligence-Semantikmodelldaten in einer [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappe oder einer Datenbank für ein tabellarisches Modell der Analysis Services auf einem Netzwerkserver bereit. Vor dem Erstellen einer BI-Semantikmodellverbindung in SharePoint müssen Sie eine Dokumentbibliothek erweitern, um das Erstellen einer BISM-Datei zu ermöglichen. Dieser Schritt muss nur einmal für jede Bibliothek ausgeführt werden, jedoch für jede Bibliothek wiederholt werden, aus der BISM-Dateien erstellt werden sollen. Als bewährte Methode wird empfohlen, eine zentrale Bibliothek zum Speichern von BISM-Dateien zu erstellen, damit die Berechtigungen zentral verwaltet werden können.  
  
> [!NOTE]  
>  Wenn Sie bereits SharePoint-Datenverbindungsbibliotheken verwenden, wird der BI-Semantikmodell-Verbindungsinhaltstyp dieser Bibliotheksvorlage automatisch hinzugefügt. Sie können die Schritte in diesem Abschnitt überspringen, wenn Sie eine Datenverbindungsbibliothek verwenden, mit der Sie bereits neue BI-Semantikmodell-Verbindungsdokumente erstellen können.  
  
##  <a name="bkmk_addtype"></a> Hinzufügen des Inhaltstyps zu einer Dokumentbibliothek  
 Sie müssen mindestens über die Listenverwaltungsberechtigung verfügen, um einen Inhaltstyp hinzuzufügen und zu konfigurieren. Diese Berechtigung ist in die Berechtigungsebene "Entwerfen" und höher integriert.  
  
 Die Website, die die Dokumentbibliothek enthält, muss eine Funktionsaktivierung für [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint aufweisen. Weitere Informationen finden Sie unter [Activate Power Pivot Feature Integration for Site Collections in Central Administration](../../analysis-services/power-pivot-sharepoint/activate power pivot integration for site collections in ca.md).  
  
1.  Öffnen Sie die Dokumentbibliothek, für die Sie den BI-Semantikmodell-Verbindungsinhaltstyp aktivieren möchten.  
  
2.  Klicken Sie im SharePoint-Menüband in den Bibliothekstools auf **Bibliothek**.  
  
3.  Klicken Sie auf **Bibliothekeinstellungen**.  
  
4.  Klicken Sie unter Allgemeine Einstellungen auf **Erweiterte Einstellungen**.  
  
5.  Klicken Sie unter Inhaltstypen im Abschnitt Verwaltung von Inhaltstypen zulassen? auf **Ja**.  
  
6.  Klicken Sie auf **OK**.  
  
7.  Klicken Sie im Abschnitt Inhaltstypen auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**. Falls diese Seite nicht angezeigt wird, wechseln Sie zurück zur Website und klicken unter Bibliothekstools auf **Bibliothek** und dann auf **Bibliothekseinstellungen**.  
  
8.  Klicken Sie unter Inhaltstypen auf **Aus vorhandenen Websiteinhaltstypen hinzufügen**.  
  
9. Wählen Sie unter Websiteinhaltstypen auswählen aus: die Option **Business Intelligence**aus.  
  
10. Klicken Sie in der Liste Verfügbare Websiteinhaltstypen auf BI-Semantikmodell-Verbindungsdatei, und klicken Sie dann auf **Hinzufügen**, um den ausgewählten Inhaltstyp in die Liste **Hinzuzufügende Inhaltstypen** zu verschieben.  
  
11. Klicken Sie auf **OK**.  
  
12. Um zu überprüfen, ob Sie den Inhaltstyp hinzugefügt haben, navigieren Sie zurück zur Bibliothek, und klicken Sie im Bereich zu den Dokumenten des Bibliotheksmenübands auf **Neues Dokument** . Sie sollten **BI-Semantikmodell-Verbindungsdatei** in der Liste "Neue Dokumente" sehen.  
  
     ![Untermenü "Neues Dokument" in einer SharePoint-Bibliothek](../../analysis-services/power-pivot-sharepoint/media/ssas-bismconnection-new.gif "Untermenü "Neues Dokument" in einer SharePoint-Bibliothek")  
  
 Nachdem Sie den Inhaltstyp für die BI-Semantikmodellverbindung für eine Bibliothek aktiviert haben, können Sie eine Verbindung erstellen, die Umleitung für Geschäftssemantikmodelldaten bereitstellt, die von Excel- oder [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] -Berichten verwendet werden können. Wählen Sie die folgenden Links, um mehr über diesen nächsten Schritt zu erfahren:  
  
 [Erstellen einer BI-Semantikmodellverbindung zu einer PowerPivot-Arbeitsmappe](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
 [Erstellen einer BI-Semantikmodellverbindung mit einer tabellarischen Modelldatenbank](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
## Siehe auch  
 [PowerPivot-BI-Semantikmodell-Verbindung &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Verwenden einer BI-Semantikmodellverbindung in Excel oder Reporting Services](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)  
  
  