---
title: "Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für untergeordnete Berichte | Microsoft-Dokumentation"
ms.custom: 
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
caps.latest.revision: "7"
author: guyinacube
ms.author: asaxton
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e46012de6473dcbfec2ff03ec16150fe6a81230a
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lektion 4: Definieren einer Datenverbindung und einer Datentabelle für den untergeordneten Bericht
Nachdem Sie den übergeordneten Bericht entworfen haben, erstellen Sie im nächsten Schritt eine Datenverbindung und eine Datentabelle für den untergeordneten Bericht. In diesem Tutorial wird eine Datenverbindung mit der AdventureWorks2014-Datenbank hergestellt.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>So definieren Sie eine Datenverbindung und eine Datentabelle durch Hinzufügen eines Datasets (für den untergeordneten Bericht)  
  
1.  Wählen Sie im Menü **Website** die Option **Neues Element hinzufügen**aus.  
  
2.  Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option **DataSet** und anschließend **Hinzufügen**aus. Sobald Sie dazu aufgefordert werden, fügen Sie das Element dem Ordner **App_Code** hinzu, indem Sie **Ja**auswählen.  
  
    Dadurch wird dem Projekt die neue XSD-Datei **DataSet2.xsd** hinzugefügt und der DataSet-Designer geöffnet.  
  
3.  Ziehen Sie ein **TableAdapter** -Steuerelement aus der Toolbox auf die Entwurfsoberfläche. Dadurch wird der Konfigurations-Assistent **TableAdapter** gestartet.  
  
4.  Auf der Seite **Wählen Sie Ihre Datenverbindung** können Sie die Verbindung auswählen, die Sie in Lektion 2 erstellt haben. Wenn Sie ausgewählt haben, wählen Sie **Weiter** und fahren Sie mit Schritt 8 fort. Wählen Sie andernfalls **Neue Verbindung**.  
  
5.  Führen Sie im Dialogfeld **Verbindung hinzufügen** die folgenden Schritte aus:  
  
    1.  Geben Sie im Feld **Servername** den Server ein, auf dem sich die Datenbank **AdventureWorks2014** befindet.  
  
        Die SQL Server Express-Standardinstanz lautet **(local)\sqlexpress**.  
  
    2.  Wählen Sie im Abschnitt **Am Server anmelden** die Option aus, die Ihnen den Zugriff auf die Daten ermöglicht. Die Standardeinstellung ist**Windows-Authentifizierung verwenden** .  
  
    3.  Wählen Sie aus **AdventureWorks2014** aus der Dropdownliste **Datenbanknamen eingeben oder auswählen**aus.  
  
    4.  Wählen Sie **OK**, und wählen Sie anschließend **Weiter**aus.  
  
6.  Wenn Sie in Schritt 5 (b) **SQL Server-Authentifizierung verwenden** ausgewählt haben, legen Sie fest, ob die vertraulichen Daten in die Zeichenfolge eingeschlossen oder ob die Informationen im Anwendungscode festgelegt werden sollen.  
  
7.  Geben Sie auf der Seite **Verbindungszeichenfolge in der Anwendungskonfigurationsdatei speichern** den Namen der Verbindungszeichenfolge ein, oder übernehmen Sie den Standardwert **AdventureWorks2014ConnectionString**. Wählen Sie **Weiter**aus.  
  
8.  Wählen Sie auf der Seite **Wählen Sie einen Befehlstyp aus** die Option **SQL-Anweisungen verwenden**aus, und klicken Sie anschließend auf **Weiter**.  
  
9. Geben Sie auf der Seite **SQL-Anweisung eingeben** die folgende Transact-SQL-Abfrage ein, um Daten aus der Datenbank **AdventureWorks2014** abzurufen, und klicken Sie anschließend auf **Weiter**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
    Sie können die Abfrage auch erstellen, indem Sie den **Abfrage-Generator**auswählen. Überprüfen Sie anschließend die Abfrage, indem Sie die Schaltfläche **Abfrage ausführen** auswählen. Wenn die Abfrage nicht die erwarteten Daten zurückgibt, verwenden Sie möglicherweise eine frühere Version von AdventureWorks. Weitere Informationen zum Abrufen der **AdventureWorks2014**-Beispieldatenbank finden Sie in den [AdventureWorks-Beispieldatenbanken](https://github.com/Microsoft/sql-server-samples/releases).  
  
10. Deaktivieren Sie auf der Seite **Zu generierende Methode auswählen** die Option **Methoden erstellen, um Updates direkt an die Datenbank zu senden (GenerateDBDirectMethods)**und wählen Sie **Fertig stellen**.  
  
    > [!WARNING]  
    > Deaktivieren Sie in jedem Fall die Option **Methoden erstellen, um Updates direkt an die Datenbank zu senden (GenerateDBDirectMethods)**  
  
    Die Konfiguration der ADO.NET [DataTable](http://msdn.microsoft.com/library/system.data.datatable.aspx) als Datenquelle für Ihren Bericht ist jetzt abgeschlossen. Auf der DataSet-Designer-Seite in Visual Studio sollte die hinzugefügte **DataTable** jetzt mit den in der Abfrage angegebenen Spalten aufgeführt werden. DataSet2 enthält die auf der Abfrage basierenden Daten aus der PurchaseOrderDetail-Tabelle.  
  
11. Speichern Sie die Datei.  
  
12. Wählen Sie im Menü **Daten** die Option **Datenvorschau** aus, und klicken Sie anschließend auf **Vorschau**.  
  
## <a name="next-task"></a>Nächste Aufgabe  
Sie haben erfolgreich eine Datenverbindung und eine Datentabelle für den untergeordneten Bericht erstellt. Als Nächstes entwerfen Sie den untergeordneten Bericht mithilfe des Berichts-Assistenten. Siehe [Lektion 5: Entwerfen des untergeordneten Berichts mithilfe des Berichts-Assistenten](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md).  
  

