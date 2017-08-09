---
title: "Lektion 2: Definieren einer Datenverbindung und einer Datentabelle für den übergeordneten Bericht | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: adc2cc7d329586bae6fb85edb08d71fe51aaaef8
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lektion 2: Definieren einer Datenverbindung und einer Datentabelle für den übergeordneten Bericht
Nachdem Sie ein neues Websiteprojekt mithilfe der ASP.NET-Websitevorlage für Visual C# erstellt haben, erstellen Sie im nächsten Schritt eine Datenverbindung und eine Datentabelle für den übergeordneten Bericht. In diesem Tutorial wird eine Datenverbindung mit der AdventureWorks2014-Datenbank hergestellt.  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>So definieren Sie eine Datenverbindung und eine Datentabelle durch Hinzufügen eines Datasets (für den übergeordneten Bericht)  
  
1.  Wählen Sie im Menü **Website** die Option **Neues Element hinzufügen**aus.  
  
2.  Wählen Sie im Dialogfeld **Neues Element hinzufügen** die Option **DataSet** aus, und klicken Sie auf **Hinzufügen**. Sobald Sie dazu aufgefordert werden, fügen Sie das Element dem Ordner **App_Code** hinzu, indem Sie **Ja**auswählen.  
  
    Dadurch wird dem Projekt die neue XSD-Datei **DataSet1.xsd** hinzugefügt und der DataSet-Designer geöffnet.  
  
3.  Ziehen Sie ein **[TableAdapter](http://msdn.microsoft.com/library/bz9tthwx.aspx)** -Steuerelement aus der Toolbox auf die Entwurfsoberfläche. Dadurch wird der Konfigurations-Assistent **TableAdapter** gestartet.  
  
4.  Wählen Sie auf der Seite **Wählen Sie Ihre Datenverbindung aus** die Option **Neue Verbindung**aus.  
  
5.  Wenn Sie erstmalig eine Datenquelle in Visual Studio erstellen, wird die Seite **Datenquelle auswählen** angezeigt. Wählen Sie im Feld **Datenquelle** die Option **Microsoft SQL Server**aus.  
  
6.  Führen Sie im Dialogfeld **Verbindung hinzufügen** die folgenden Schritte aus:  
  
    1.  Geben Sie im Feld **Servername** den Server ein, auf dem sich die Datenbank **AdventureWorks2014** befindet.  
  
        Die SQL Server Express-Standardinstanz lautet **(local)\sqlexpress**.  
  
    2.  Wählen Sie im Abschnitt **Am Server anmelden** die Option aus, die Ihnen den Zugriff auf die Daten ermöglicht. Die Standardeinstellung ist**Windows-Authentifizierung verwenden** .  
  
    3.  Wählen Sie aus **AdventureWorks2014** aus der Dropdownliste **Datenbanknamen eingeben oder auswählen**aus.  
  
    4.  Wählen Sie **OK**, und wählen Sie anschließend **Weiter**aus.  
  
7.  Wenn Sie in Schritt 6 (b) **SQL Server-Authentifizierung verwenden** ausgewählt haben, legen Sie fest, ob die vertraulichen Daten in die Zeichenfolge eingeschlossen oder ob die Informationen im Anwendungscode festgelegt werden sollen.  
  
8.  Geben Sie auf der Seite **Verbindungszeichenfolge in der Anwendungskonfigurationsdatei speichern** den Namen der Verbindungszeichenfolge ein, oder übernehmen Sie den Standardwert **AdventureWorks2014ConnectionString**. Wählen Sie **Weiter**aus.  
  
9. Wählen Sie auf der Seite **Wählen Sie einen Befehlstyp aus** die Option **SQL-Anweisungen verwenden**aus, und klicken Sie anschließend auf **Weiter**.  
  
10. Geben Sie auf der Seite **SQL-Anweisung eingeben** die folgende Transact-SQL-Abfrage ein, um Daten aus der Datenbank **AdventureWorks2014** abzurufen, und klicken Sie anschließend auf **Weiter**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    Sie können die Abfrage auch erstellen, indem Sie den **Abfrage-Generator**auswählen. Überprüfen Sie anschließend die Abfrage, indem Sie **Abfrage ausführen**auswählen. Wenn die Abfrage nicht die erwarteten Daten zurückgibt, verwenden Sie möglicherweise eine frühere Version von AdventureWorks. Weitere Informationen zum Abrufen der **AdventureWorks2014** -Beispieldatenbank, finden Sie unter [Microsoft SQL Server Database Product Samples](http://msftdbprodsamples.codeplex.com/).  
  
11. Deaktivieren Sie auf der Seite **Zu generierende Methode auswählen** in jedem Fall die Option **Methoden erstellen, um Updates direkt an die Datenbank zu senden (GenerateDBDirectMethods)**, und wählen Sie anschließend **Fertig stellen**aus.  
  
    > [!WARNING]  
    > Deaktivieren Sie in jedem Fall die Option **Methoden erstellen, um Updates direkt an die Datenbank zu senden (GenerateDBDirectMethods)**  
  
    Die Konfiguration des ADO.NET DataTable-Objekts als Datenquelle für Ihren Bericht ist jetzt abgeschlossen. Auf der DataSet-Designer-Seite in Visual Studio sollte das hinzugefügte DataTable-Objekt jetzt mit den in der Abfrage angegebenen Spalten aufgeführt werden. DataSet1 enthält die Daten aus der Product-Tabelle basierend auf der Abfrage.  
  
12. Speichern Sie die Datei.  
  
13. Wählen Sie im Menü **Daten** die Option **Datenvorschau** aus, und klicken Sie anschließend auf **Vorschau**.  
  
## <a name="next-task"></a>Nächste Aufgabe  
Sie haben erfolgreich eine Datenverbindung und eine Datentabelle für den übergeordneten Bericht erstellt. Als Nächstes erstellen Sie den übergeordneten Bericht mithilfe des Berichts-Assistenten. Weitere Informationen finden Sie unter [Lektion 3: Entwerfen des übergeordneten Berichts mithilfe des Berichts-Assistenten](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md).  
  


