---
Title: 'Tutorial: Using Templates in SQL Server Management Studio'
description: Ein Tutorial zur Verwendung von Vorlagen in SSMS. zugreifen.
keywords: SQL Server, SSMS, SQL Server Management Studio, Vorlagen
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- templates [SQL Server], SQL Server Management Studio
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: 05a9883ff436991e5ee830ce1561ecced0fa9b60
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-using-templates-within-sql-server-management-studio"></a>Tutorial: Verwenden von Vorlagen in SQL Server Management Studio
In diesem Tutorial werden die vorgefertigten T-SQL-Vorlagen (Transact-SQL) vorgestellt, die in SQL Server Management Studio (SSMS) verfügbar sind. In diesem Artikel lernen Sie Folgendes:
    - Verwenden des Vorlagenbrowsers zum Generieren von T-SQL-Skripts
    - Bearbeiten einer vorhandenen Vorlage 
    - Suchen der Vorlagen auf dem Datenträger
    - Erstellen einer neuen Vorlage
   

## <a name="prerequisites"></a>Voraussetzungen
Zur Durchführung dieses Tutorials benötigen Sie SQL Server Management Studio und Zugriff auf einen SQL-Server. 

- Installieren Sie [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Installieren Sie die [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).

 

## <a name="using-the-template-browser"></a>Verwenden des Vorlagenbrowsers
In diesem Abschnitt erfahren Sie, wie Sie den **Vorlagenbrowser** suchen und verwenden. 

1. Starten Sie SQL Server Management Studio.
2. Über das Menü **Ansicht** > **Vorlagenbrowser** (Strg + Alt + T): 

    ![Vorlagenbrowser](media/templates-ssms/templatebrowser.png)
    - Im unteren Bereich des **Vorlagenbrowsers** können Sie auch aktuell verwendete Vorlagen sehen.

3. Erweitern Sie den Knoten, der für Sie von Interesse ist, und klicken Sie mit der rechten Maustaste auf „Vorlage“ > „Öffnen“:

    ![Vorlage öffnen](media/templates-ssms/opentemplate.png)
    - Ein Doppelklick auf die Vorlage hat den gleichen Effekt.

4. Hierdurch wird ein neues Abfragefenster geöffnet, in dem T-SQL bereits aufgefüllt wurde. 
5. Ändern Sie die Vorlage Ihren Anforderungen entsprechend, und klicken Sie anschließend bei der Abfrage auf **Ausführen**:
    
    ![Datenbankvorlage erstellen](media/templates-ssms/createdbtemplate.png)


## <a name="edit-an-existing-template"></a>Bearbeiten einer vorhandenen Vorlage
Sie können die vorhandenen Vorlagen auch im **Vorlagenbrowser** bearbeiten.  

1. Suchen Sie die gewünschte Vorlage im **Vorlagenbrowser**.
2. Klicken Sie mit der rechten Maustaste auf die Vorlage > **Bearbeiten**.

    ![Vorlage bearbeiten](media/templates-ssms/edittemplate.png)

3. Nehmen Sie in dem Abfragefenster, das geöffnet wird, die gewünschten Änderungen vor.
4. Speichern Sie die Vorlage, indem Sie zu **Datei** > **Speichern** (Strg + S) navigieren.
5. Schließen Sie das Abfragefenster.
6. Öffnen Sie die gespeicherte Vorlage erneut. Ihre neuen Bearbeitungen müssten nun darin enthalten sein.
 

## <a name="locate-the-templates-on-disk"></a>Suchen der Vorlagen auf dem Datenträger
Sobald eine Vorlage geöffnet wurde, können Sie diese anschließend auf dem Datenträger suchen.

1. Wählen Sie eine Vorlage im **Vorlagenbrowser** > **Bearbeiten** aus.
2. Klicken Sie mit der rechten Maustaste auf **Abfragetitel** > **Übergeordneten Ordner öffnen**. Dadurch müsste Ihr Explorer dort geöffnet werden, wo die Vorlagen auf dem Datenträger gespeichert sind: 

    ![Vorlagen auf dem Datenträger](media/templates-ssms/templatesondisk.png)
  

## <a name="create-a-new-template"></a>Erstellen einer neuen Vorlage
Sie können im **Vorlagenbrowser** auch neue Vorlagen erstellen. In den folgenden Schritten erfahren Sie, wie Sie einen neuen Ordner erstellen und anschließend innerhalb dieses Ordners eine neue Vorlage erstellen können. Mit diesen Schritten können Sie jedoch auch in den vorhandenen Ordnern eine benutzerdefinierte Vorlage erstellen. 

1. Öffnen Sie den **Vorlagenbrowser**.
2. Klicken Sie mit der rechten Maustaste auf „SQL Server-Vorlagen“ > **Neu** > **Ordner**. 
3. Geben Sie diesem Ordner den Namen **Benutzerdefinierte Vorlagen**.

    ![Erstellen benutzerdefinierter Vorlagen](media/templates-ssms/creatingcustomtemplate.png)

4. Klicken Sie mit der rechten Maustaste auf den neu erstellten Ordner **Benutzerdefinierte Vorlagen** > **Neu** > **Vorlage**, und geben Sie Ihrer Vorlage einen Namen. 
 
    ![Erstellen benutzerdefinierter Vorlagen](media/templates-ssms/createnewtemplate.png)
   
5. Klicken Sie mit der rechten Maustaste auf die gerade erstellte Vorlage > **Bearbeiten**. Dadurch wird ein **Neues Abfragefenster** geöffnet.
6. Geben Sie den T-SQL-Text ein, der gespeichert werden soll. 
7. Speichern Sie die Datei, indem Sie zum Menü **Datei** > **Speichern** navigieren.
8. Schließen Sie das vorhandene **Abfragefenster**, und öffnen Sie Ihre neue benutzerdefinierte Vorlage. 

    

## <a name="next-steps"></a>Nächste Schritte
Der nachfolgende Artikel enthält einige zusätzliche Tipps und Tricks zur Verwendung von SQL Server Management Studio. 

Für weitere Informationen zum nächsten Artikel blättern
> [!div class="nextstepaction"]
> [Nächste Schritte](ssms-tricks.md)
