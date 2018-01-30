---
title: Erstellen von benutzerdefinierten Vorlagen | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- tql
- templates [Transact-SQL], creating
- templates [Transact-SQL]
ms.assetid: 41098e78-b482-410e-bfe8-2ac10769ac4a
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 757a6b2aebe68dc32ddc493c3e6649a8b589be3e
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/17/2018
---
# <a name="lesson-3-2---create-custom-templates"></a>Lektion 3-2: Erstellen von benutzerdefinierten Vorlagen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] kommt mit einer Reihe von Vorlagen für viele häufig ausgeführte Aufgaben. Der größte Vorteil von Vorlagen besteht jedoch darin, dass Sie für ein komplexes Skript, das Sie häufig erstellen müssen, eine benutzerdefinierte Vorlage anlegen können. Sie werden nun ein einfaches Skript mit wenigen Parametern erstellen. Vorlagen sind jedoch auch bei umfangreichen Skripts mit vielen Wiederholungen nützlich.  
  
## <a name="using-custom-templates"></a>Verwenden benutzerdefinierter Vorlagen  
  
#### <a name="to-create-a-custom-template"></a>So erstellen Sie eine benutzerdefinierte Vorlage  
  
1.  Erweitern Sie **SQL Server-Vorlagen**im Vorlagen-Explorer, klicken Sie mit der rechten Maustaste auf **Gespeicherte Prozedur**, zeigen Sie auf **Neu**, und klicken Sie anschließend auf **Ordner**.  
  
2.  Geben Sie **Custom** als Namen für den neuen Vorlagenordner ein, und drücken Sie anschließend die EINGABETASTE.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Custom**, zeigen Sie auf **Neu**, und klicken Sie anschließend auf **Vorlage**.  
  
4.  Geben Sie **WorkOrdersProc** als Namen für die neue Vorlage ein, und drücken Sie anschließend die **EINGABETASTE**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **WorkOrdersProc**und anschließend auf **Bearbeiten**.  
  
6.  Überprüfen Sie im Dialogfeld **Verbindung mit Datenbankmodul herstellen** die Verbindungseinstellungen, und klicken Sie anschließend auf **Verbinden**.  
  
7.  Geben Sie im Abfrage-Editor das folgende Skript ein, um eine gespeicherte Prozedur zu erstellen, über die Bestellungen für ein bestimmtes Teil gesucht werden. In diesem Fall handelt es sich um Klingen (Blade). (Sie können den Code im Fenster des Lernprogramms kopieren und dann einfügen.)  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersForBlade')  
       DROP PROCEDURE dbo.WorkOrdersForBlade;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersForBlade  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = 'Blade';  
    GO  
    ```  
  
8.  Drücken Sie F5, um das Skript auszuführen. Damit wird die Prozedur **WorkOrdersForBlade** erstellt.  
  
9. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf Ihren Server und anschließend auf **Neue Abfrage**. Ein neues Abfrage-Editorfenster wird geöffnet.  
  
10. Geben Sie im Abfrage-Editor **EXECUTE dbo.WorkOrdersForBlade**ein, und drücken Sie anschließend F5, um die Abfrage auszuführen. Überprüfen Sie, ob im Bereich **Ergebnisse** eine Liste mit Bestellungen für Klingen zurückgegeben wird.  
  
11. Bearbeiten Sie das Vorlagenskript (das Skript von Schritt 7), und ersetzen Sie dabei den Produktnamen „Blade“ an vier Stellen durch den Parameter ***\<*product_name**, **nvarchar(50)**, **name*>***.  
  
    > [!NOTE]  
    > Für Parameter sind drei Elemente erforderlich: der Name des zu ersetzenden Parameters, der Datentyp des Parameters und ein Standardwert für den Parameter.  
  
12. Das Skript sollte nun wie folgt aussehen:  
  
    ```  
    USE AdventureWorks20012;  
    GO  
    IF EXISTS (  
    SELECT *   
       FROM INFORMATION_SCHEMA.ROUTINES   
       WHERE SPECIFIC_NAME = 'WorkOrdersFor<product_name, nvarchar(50), name>')  
       DROP PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>;  
    GO  
    CREATE PROCEDURE dbo.WorkOrdersFor<product_name, nvarchar(50), name>  
    AS  
    SELECT Name, WorkOrderID   
    FROM Production.WorkOrder AS WO  
    JOIN Production.Product AS Prod  
    ON WO.ProductID = Prod.ProductID  
    WHERE Name = '<product_name, nvarchar(50), name>';  
    GO  
    ```  
  
13. Klicken Sie im Menü **Datei** auf **WorkOrdersProc.sql speichern** , um Ihre Vorlage zu speichern.  
  
#### <a name="to-test-the-custom-template"></a>So testen Sie die benutzerdefinierte Vorlage  
  
1.  Erweitern Sie im Vorlagen-Explorer **Gespei6cherte Prozeduren**, erweitern Sie **Benutzerdefiniert**, und doppelklicken Sie anschließend auf **WorkOrderProc**.  
  
2.  Vervollständigen Sie im Dialogfeld **Verbindung mit Datenbankmodul herstellen** die Verbindungseinstellungen, und klicken Sie anschließend auf **Verbinden**. Ein neues Fenster des Abfrage-Editors wird geöffnet, in dem der Inhalt der Vorlage **WorkOrderProc** angezeigt wird.  
  
3.  Klicken Sie im Menü **Abfrage** auf **Werte für Vorlagenparameter angeben**.  
  
4.  Geben Sie im Dialogfeld **Werte für Vorlagenparameter angeben** für den Wert **product_name** die Eingabe **FreeWheel** ein (Sie überschreiben dabei den Standardinhalt). Klicken Sie auf **OK** , um das Dialogfeld **Werte für Vorlagenparameter angeben** zu schließen und das Skript im Abfrage-Editor zu ändern.  
  
5.  Drücken Sie F5, um das Skript auszuführen. Damit wird die Prozedur erstellt.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in der Lektion  
[Speichern von Skripts als Projekte oder Lösungen](../../tools/sql-server-management-studio/lesson-3-3-save-scripts-as-projects-or-solutions.md)  
  
  
  
