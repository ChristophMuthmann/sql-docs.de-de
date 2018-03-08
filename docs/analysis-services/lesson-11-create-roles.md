---
title: 'Lektion 12: Erstellen von Rollen | Microsoft Docs'
ms.custom: 
ms.date: 03/27/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 984face4-00fc-46d3-8ae1-9755bf737bdf
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 12a11fce82fbb0ec3e75ee9908f07372e5cbb086
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/08/2018
---
# <a name="lesson-11-create-roles"></a>Lektion 11: Erstellen von Rollen
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

In dieser Lektion erstellen Sie Rollen. Rollen stellen Modelldatenbankobjekt- und Datensicherheit bereit, indem sie den Zugriff auf die Windows-Benutzer einschränken, die Rollenmitglieder sind. Jede Rolle wird mit einer einzelnen Berechtigung definiert: Keine, Lesen, Lesen und verarbeiten, Verarbeiten oder Administrator. Rollen können während der Modellerstellung mithilfe des Rollen-Manager definiert werden. Nachdem ein Modell bereitgestellt wurde, können Sie mit [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]Rollen verwalten. Weitere Informationen finden Sie unter [Rollen](../analysis-services/tabular-models/roles-ssas-tabular.md)während der Modellerstellung im Dialogfeld Rollen-Manager definiert werden.  
  
> [!NOTE]  
> Das Erstellen von Rollen ist zum Abschließen dieses Lernprogramms nicht erforderlich. Das Konto, über das Sie derzeit angemeldet sind, verfügt standardmäßig über Administratorberechtigungen für das Modell. Allerdings müssen Sie damit andere Benutzer in Ihrer Organisation zum Durchsuchen des Modells mit einem berichtserstellungsclient wird, erstellen mindestens eine Rolle mit Berechtigungen und diese Benutzer als Mitglieder hinzufügen.  
  
Sie erstellen drei Rollen:  
  
-   **Vertriebsleiter** – diese Rolle kann Benutzer umfassen, in Ihrer Organisation, die für die Leseberechtigung für alle Modellobjekte und Daten haben sollen.  
  
-   **Sales Analyst US** – diese Rolle kann Benutzer umfassen, in Ihrer Organisation, die für die Sie nur Daten zum Vertrieb in den Vereinigten Staaten durchsuchen können möchten. Für diese Rolle definieren Sie mit einer DAX-Formel einen *Zeilenfilter*, der Mitgliedern der Rolle lediglich das Durchsuchen von Daten in den USA ermöglicht.  
  
-   **Administrator** – diese Rolle kann auch Benutzer, die für die Administrator-Berechtigung verfügen, die uneingeschränkten Zugriff und Berechtigungen zum Ausführen von Verwaltungsaufgaben in der Model-Datenbank ermöglicht werden soll.  
  
Da Windows-Benutzer- und -Gruppenkonten in der Organisation eindeutig sind, können Sie Mitgliedern Konten aus Ihrer Organisation hinzufügen. In diesem Lernprogramm können Sie die Angaben zu den Mitgliedern auch weglassen. Sie können die Auswirkungen der einzelnen Rollen immer noch in "Lektion 12: Analysieren in Excel" testen.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Voraussetzungen  
Dieses Thema ist Teil eines Lernprogramms zur Tabellenmodellierung, das in der entsprechenden Reihenfolge bearbeitet werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 10: Erstellen von Partitionen](../analysis-services/lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Erstellen von Rollen  
  
#### <a name="to-create-a-sales-manager-user-role"></a>So erstellen Sie die Benutzerrolle "Sales Manager"  
  
1.  Im tabellarischen Modell-Explorer mit der Maustaste **Rollen** > **Rollen**.  
  
2.  Klicken Sie im Rollen-Manager auf **neu**.  
  
3.  Klicken Sie auf die neue Rolle, und klicken Sie dann in der **Namen** Spalte, benennen Sie die Rolle auf **Sales Manager**.  
  
4.  Klicken Sie in der Spalte **Berechtigungen** auf die Dropdownliste, und wählen Sie anschließend die Berechtigung **Lesen** aus. 

    ![als tabellarische-lesson11-neuen-Rolle](../analysis-services/media/as-tabular-lesson11-new-role.png) 
  
5.  Optional: Klicken Sie auf die **Elemente** Registerkarte, und klicken Sie dann auf **hinzufügen**. Geben Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder -Gruppen in Ihrer Organisation ein, die Sie der Rolle hinzufügen möchten.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>So erstellen Sie die Benutzerrolle "Sales Analyst US"  
  
1.  Klicken Sie im Rollen-Manager auf **neu**.    
  
2.  Benennen Sie die Rolle auf **Sales Analyst US**.  
  
3.  Diese Funktion **lesen** Berechtigung.  
  
4.  Klicken Sie auf die Registerkarte Zeilenfilter, und klicken Sie dann für die **DimGeography** Tabelle nur in der Spalte DAX-Filter geben Sie die folgende Formel:  
  
    ```
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Eine Zeilenfilterformel muss in einen booleschen Wert (TRUE/FALSE) aufgelöst werden. Mit dieser Formel legen Sie fest, dass nur Zeilen mit dem Länder-/Regionscode (Country Region Code) "US" für den Benutzer sichtbar sind.  
    ![als tabellarische-lesson11-Rolle-filter](../analysis-services/media/as-tabular-lesson11-role-filter.png) 
  
6.  Optional: Klicken Sie auf die Registerkarte **Mitglieder** und anschließend auf **Hinzufügen**. Geben Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder -Gruppen in Ihrer Organisation ein, die Sie der Rolle hinzufügen möchten.  
  
#### <a name="to-create-an-administrator-user-role"></a>So erstellen eine Administrator-Benutzerrolle "  
  
1.  Klicken Sie auf **Neu**.  
  
2.  Benennen Sie die Rolle auf **Administrator**.  
  
3.  Diese Funktion **Administrator** Berechtigung.  
  
4.  Optional: Klicken Sie auf die Registerkarte **Mitglieder** und anschließend auf **Hinzufügen**. Geben Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder -Gruppen in Ihrer Organisation ein, die Sie der Rolle hinzufügen möchten. 
  
  
## <a name="whats-next"></a>Wie geht es weiter?
Wechseln Sie zur nächsten Lektion: [Lektion 12: Analysieren in Excel](../analysis-services/lesson-12-analyze-in-excel.md).

  
  
