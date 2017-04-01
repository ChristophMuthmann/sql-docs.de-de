---
title: "Erstellen und Verwenden eingebetteter Datenquellen | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c38c2e8-7a29-4f79-a4a3-85ed2b13723b
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 10
---
# Erstellen und Verwenden eingebetteter Datenquellen
  Eine eingebettete Datenquelle wird in einer Berichtsdefinition definiert und nur von diesem Bericht verwendet.  
  
## So erstellen Sie eine eingebettete Datenquelle im Berichts-Designer  
  
1.  Klicken Sie im Berichtsdatenbereich auf der Symbolleiste auf **Neu** , und klicken Sie dann auf **Datenquelle**. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.  
  
    > [!NOTE]  
    >  Zum Anzeigen des Berichtsdatenbereichs klicken Sie im Menü **Ansicht** auf **Berichtsdaten**.  
  
2.  Geben Sie im Textfeld **Name** einen Namen für die Datenquelle ein, oder übernehmen Sie den Standardnamen. Der Name der Datenquelle wird intern für den Bericht verwendet. Zur Verdeutlichung sollte der Name der Datenquelle den Namen der Datenbank enthalten, die in der Verbindungszeichenfolge angegeben ist.  
  
3.  Überprüfen Sie, ob **Eingebettete Verbindung** aktiviert ist, und führen Sie folgende Schritte aus.  
  
    1.  Wählen Sie in der Dropdownliste **Typ** einen Datenquellentyp aus, zum Beispiel **Microsoft SQL Server** oder **OLE DB**.  
  
    2.  Geben Sie eine Verbindungszeichenfolge an, indem Sie eine der folgenden Alternativen verwenden:  
  
        -   Geben Sie die Verbindungszeichenfolge direkt in das Textfeld **Verbindungszeichenfolge** ein. Eine Liste der Beispiele für Verbindungszeichenfolgen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md) oder [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
        -   Klicken Sie auf die Ausdrucksschaltfläche (**fx)**, um einen Ausdruck zu erstellen, der als Verbindungszeichenfolge ausgewertet wird. Geben Sie den Ausdruck im Dialogfeld **Ausdruck** in den Bereich Ausdruck ein. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   Klicken Sie auf **Bearbeiten** , um das Dialogfeld **Verbindungseigenschaften** für den Datenquellentyp zu öffnen, den Sie in Schritt 2 gewählt haben.  
  
             Füllen Sie die Felder im Dialogfeld **Verbindungseigenschaften** gemäß dem jeweiligen Datenquellentyp aus. Verbindungseigenschaften enthalten den Typ der Datenquelle, den Namen der Datenquelle und die zu verwendenden Anmeldeinformationen. Nachdem Sie in diesem Dialogfeld Werte angegeben haben, klicken Sie auf **Verbindung testen** , um zu überprüfen, ob die Datenquelle verfügbar ist und die angegebenen Anmeldeinformationen richtig sind. Weitere Informationen zu bestimmten Datenquellentypen finden Sie unter [Hinzufügen von Daten aus externen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md).  
  
    3.  Klicken Sie auf **Anmeldeinformationen**.  
  
         Geben Sie die Anmeldeinformationen für diese Datenquelle an. Der Besitzer der Datenquelle wählt den Typ von Anmeldeinformationen aus, die unterstützt werden.  
  
4.  Die neue eingebettete Datenquelle wird im Berichtsdatenbereich angezeigt.  
  
## So erstellen Sie eine eingebettete Datenquelle im Berichts-Generator  
  
1.  Klicken Sie im Berichtsdatenbereich auf der Symbolleiste auf **Neu**und anschließend auf **Datenquelle**. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.  
  
2.  Geben Sie im Textfeld **Name** einen Namen für die Datenquelle ein, oder übernehmen Sie den Standardnamen.  
  
3.  Stellen Sie sicher, dass die Option **In Bericht eingebettete Verbindung verwenden** aktiviert ist.  
  
    1.  Wählen Sie in der Dropdownliste **Verbindungstyp auswählen** einen Datenquellentyp aus, zum Beispiel **Microsoft SQL Server** oder **OLE DB**.  
  
    2.  Geben Sie eine Verbindungszeichenfolge mit einer der folgenden Möglichkeiten an:  
  
        -   Geben Sie die Verbindungszeichenfolge direkt in das Textfeld **Verbindungszeichenfolge** ein. Eine Liste von Beispielen für Verbindungszeichenfolgen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md).  
  
        -   Klicken Sie auf die Ausdrucksschaltfläche (**fx)**, um einen Ausdruck zu erstellen, der als Verbindungszeichenfolge ausgewertet wird. Geben Sie den Ausdruck im Dialogfeld **Ausdruck** in den Bereich Ausdruck ein. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   Klicken Sie auf **Erstellen** , um das Dialogfeld **Verbindungseigenschaften** für den Datenquellentyp zu öffnen, den Sie in Schritt 2 gewählt haben.  
  
             Füllen Sie die Felder im Dialogfeld **Verbindungseigenschaften** gemäß dem jeweiligen Datenquellentyp aus. Verbindungseigenschaften enthalten den Typ der Datenquelle, den Namen der Datenquelle und die zu verwendenden Anmeldeinformationen. Nachdem Sie in diesem Dialogfeld Werte angegeben haben, klicken Sie auf **Verbindung testen** , um zu überprüfen, ob die Datenquelle verfügbar ist und die angegebenen Anmeldeinformationen richtig sind.  
  
4.  Klicken Sie auf **Anmeldeinformationen**.  
  
     Geben Sie die Anmeldeinformationen für diese Datenquelle an. Der Besitzer der Datenquelle wählt den Typ von Anmeldeinformationen aus, die unterstützt werden. Weitere Informationen finden Sie unter [Angeben von Anmeldeinformationen im Berichts-Generator](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Die Datenquelle wird im Berichtsdatenbereich angezeigt.  
  
## Siehe auch  
 [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Angeben von Anmeldeinformationen im Berichts-Generator](../Topic/Specify%20Credentials%20in%20Report%20Builder.md)  
  
  