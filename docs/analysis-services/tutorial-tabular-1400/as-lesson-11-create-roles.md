---
title: 'Analysis Services Tutorial Lektion 11: Erstellen von Rollen | Microsoft Docs'
description: Beschreibt, wie Rollen in der Analysis Services Tutorial-Projekt zu erstellen.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: 
author: Minewiskan
manager: kfile
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 02/20/2018
ms.author: owend
ms.openlocfilehash: b3ed6028a02b117fb6cdb87a8097d1e1eab48b0f
ms.sourcegitcommit: 7ed8c61fb54e3963e451bfb7f80c6a3899d93322
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="create-roles"></a>Erstellen von Rollen

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In dieser Lektion erstellen Sie Rollen. Rollen bieten Model-Datenbank und datensicherheit durch das Beschränken des Zugriffs auf Benutzer, die Rollenmitglieder sind. Jede Rolle wird mit einer einzelnen Berechtigung definiert: Keine, Lesen, Lesen und verarbeiten, Verarbeiten oder Administrator. Rollen können während der Modellerstellung mithilfe des Rollen-Manager definiert werden. Nachdem ein Modell bereitgestellt wurde, können Sie Rollen mithilfe von SQL Server Management Studio (SSMS) verwalten. Weitere Informationen finden Sie unter [Rollen](../tabular-models/roles-ssas-tabular.md).
  
> [!NOTE]  
> Das Erstellen von Rollen ist zum Abschließen dieses Lernprogramms nicht erforderlich. Standardmäßig verfügt das Konto, dem Sie zurzeit angemeldet sind über Administratorrechte für das Modell an. Allerdings müssen Sie für andere Benutzer in Ihrer Organisation mit einem berichtserstellungsclient durchsucht werden, erstellen mindestens eine Rolle mit Berechtigungen und diese Benutzer als Mitglieder hinzufügen.  
  
Sie erstellen drei Rollen:  
  
-   **Vertriebsleiter** – diese Rolle kann Benutzer umfassen, in Ihrer Organisation, die für die Leseberechtigung für alle Modellobjekte und Daten haben sollen.  
  
-   **Sales Analyst US** – diese Rolle kann Benutzer umfassen, in Ihrer Organisation, die für die Sie nur Daten zum Vertrieb in den Vereinigten Staaten durchsuchen können möchten. Für diese Rolle verwenden Sie eine DAX-Formel definiert eine *Zeilenfilter*, der Mitgliedern Durchsuchen von Daten nur für die USA.  
  
-   **Administrator** – diese Rolle kann auch Benutzer, die für die Administrator-Berechtigung verfügen, die uneingeschränkten Zugriff und Berechtigungen zum Ausführen von Verwaltungsaufgaben in der Model-Datenbank ermöglicht werden soll.  
  
Da Windows-Benutzer- und -Gruppenkonten in der Organisation eindeutig sind, können Sie Mitgliedern Konten aus Ihrer Organisation hinzufügen. In diesem Lernprogramm können Sie die Angaben zu den Mitgliedern auch weglassen. Sie testen der Auswirkungen der jeweiligen Rolle später in Lektion 12: in Excel analysieren.  
  
Geschätzte Zeit zum Bearbeiten dieser Lektion: **15 Minuten**  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  

Dieser Artikel ist Teil eines Lernprogramms zur tabellenmodellierung, das in Reihenfolge absolviert werden sollte. Vor dem Ausführen der Aufgaben in dieser Lektion, Sie sollten haben die vorherige Lektion abgeschlossen: [Lektion 10: Erstellen von Partitionen](../tutorial-tabular-1400/as-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Erstellen von Rollen  
  
#### <a name="to-create-a-sales-manager-user-role"></a>So erstellen Sie die Benutzerrolle "Sales Manager"  
  
1.  Im tabellarischen Modell-Explorer mit der Maustaste **Rollen** > **Rollen**.  
  
2.  Klicken Sie im Rollen-Manager auf **neu**.  
  
3.  Klicken Sie auf die neue Rolle, und klicken Sie dann in der **Namen** Spalte, benennen Sie die Rolle auf **Sales Manager**.  
  
4.  Klicken Sie in der Spalte **Berechtigungen** auf die Dropdownliste, und wählen Sie anschließend die Berechtigung **Lesen** aus. 

    ![as-lesson11-new-role](../tutorial-tabular-1400/media/as-lesson11-new-role.png) 
  
5.  Optional: Klicken Sie auf die **Elemente** Registerkarte, und klicken Sie dann auf **hinzufügen**. Geben Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder -Gruppen in Ihrer Organisation ein, die Sie der Rolle hinzufügen möchten.  
  
#### <a name="to-create-a-sales-analyst-us-user-role"></a>So erstellen Sie die Benutzerrolle "Sales Analyst US"  
  
1.  Klicken Sie im Rollen-Manager auf **neu**.    
  
2.  Benennen Sie die Rolle auf **Sales Analyst US**.  
  
3.  Diese Funktion **lesen** Berechtigung.  
  
4.  Klicken Sie auf die Registerkarte Zeilenfilter, und klicken Sie dann für die **DimGeography** Tabelle nur in der Spalte DAX-Filter geben Sie die folgende Formel:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Eine Zeilenfilterformel muss in einen booleschen Wert (TRUE/FALSE) aufgelöst werden. Mit dieser Formel legen Sie fest, dass nur Zeilen mit dem Wert Länder-/ Regionscode "US" für den Benutzer sichtbar sind.  
    ![as-lesson11-role-filter](../tutorial-tabular-1400/media/as-lesson11-role-filter.png) 
  
6.  Optional: Klicken Sie auf die **Elemente** Registerkarte, und klicken Sie dann auf **hinzufügen**. Geben Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder -Gruppen in Ihrer Organisation ein, die Sie der Rolle hinzufügen möchten.  
  
#### <a name="to-create-an-administrator-user-role"></a>So erstellen eine Administrator-Benutzerrolle "  
  
1.  Klicken Sie auf **Neu**.  
  
2.  Benennen Sie die Rolle auf **Administrator**.  
  
3.  Diese Funktion **Administrator** Berechtigung.  
  
4.  Optional: Klicken Sie auf die **Elemente** Registerkarte, und klicken Sie dann auf **hinzufügen**. Geben Sie im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder -Gruppen in Ihrer Organisation ein, die Sie der Rolle hinzufügen möchten. 
  
  
## <a name="whats-next"></a>Wie geht es weiter?

[Lektion 12: In Excel analysieren](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).

  
  
