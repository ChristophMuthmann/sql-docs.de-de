---
title: "Verwalten von Rollen mit SSMS (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 652faac0-1cfc-438b-8119-2f4b090a2381
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Verwalten von Rollen mit SSMS (SSAS – tabellarisch)
  Sie können Rollen für ein bereitgestelltes tabellarisches Modell mit [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]erstellen, bearbeiten und verwalten.  
  
 Aufgaben in diesem Thema:  
  
-   [So erstellen Sie eine neue Rolle](#bkmk_new_role)  
  
-   [So kopieren Sie eine Rolle](#bkmk_copy_role)  
  
-   [So bearbeiten Sie eine Rolle](#bkmk_edit_role)  
  
-   [So löschen Sie eine Rolle](#bkmk_deletet_role)  
  
> [!CAUTION]  
>  Wenn ein tabellarisches Modellprojekt, dessen Rollen mithilfe des Rollen-Managers in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] definiert wurden, erneut bereitgestellt wird, dann werden die in einem bereitgestellten tabellarischen Modell definierten Rollen überschrieben.  
  
> [!CAUTION]  
>  Wenn Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] verwenden, um eine Arbeitsbereichsdatenbank für tabellarische Modelle zu verwalten, während das Modellprojekt in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] geöffnet ist, kann die Datei Model.bim beschädigt werden. Wenn Sie Rollen für eine Arbeitsbereichsdatenbank für tabellarische Modelle erstellen und verwalten, verwenden Sie den Rollen-Manager in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
###  <a name="bkmk_new_role"></a> So erstellen Sie eine neue Rolle  
  
1.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die tabellarische Modelldatenbank, für die Sie eine neue Rolle erstellen möchten, klicken Sie mit der rechten Maustaste auf **Rollen**, und klicken Sie dann auf **Neue Rolle**.  
  
2.  Klicken Sie im Dialogfeld **Rolle erstellen** im Fenster "Seite auswählen" auf **Allgemein**.  
  
3.  Geben Sie im Fenster für allgemeine Einstellungen im Feld **Name** einen Namen für die Rolle ein.  
  
     Der Name der Standardrolle wird für jede neue Rolle automatisch inkrementell erhöht. Es wird empfohlen, einen Namen einzugeben, durch den der Elementtyp eindeutig identifiziert wird, beispielsweise "Finance Managers" oder "Human Resources Specialists".  
  
4.  Aktivieren Sie in **Legen Sie die Datenbankberechtigung für diese Rolle fest**eine der folgenden Berechtigungsoptionen:  
  
    |Berechtigung|Description|  
    |----------------|-----------------|  
    |**Vollzugriff (Administrator)**|Mitglieder können Änderungen am Modellschema vornehmen und alle Daten anzeigen.|  
    |**Datenbank verarbeiten**|Mitglieder können die Vorgänge Verarbeiten und Alles verarbeiten ausführen. Sie können weder das Modellschema ändern noch Daten anzeigen.|  
    |**Lesen**|Mitglieder dürfen Daten (basierend auf Zeilenfiltern) anzeigen, doch sie können keine Änderungen am Modellschema vornehmen.|  
  
5.  Klicken Sie im Dialogfeld **Rolle erstellen** im Fenster "Seite auswählen" auf **Mitgliedschaft**.  
  
6.  Klicken Sie im Mitgliedschaftseinstellungen-Fenster auf **Hinzufügen**, und fügen Sie dann im Dialogfeld **Benutzer oder Gruppen auswählen** die Windows-Benutzer oder die Gruppen hinzu, die Sie als Elemente hinzufügen möchten.  
  
7.  Wenn die Rolle, die Sie erstellen, Leseberechtigungen aufweist, können Sie Zeilenfilter für jede beliebige Tabelle hinzufügen, in der eine DAX-Formel verwendet wird. Klicken Sie zum Hinzuzufügen von Zeilenfiltern im Dialogfeld **Rolleneigenschaften – \<Rollenname>** unter **Seite auswählen** auf **Zeilenfilter**.  
  
8.  Wählen Sie im Zeilenfilter-Fenster eine Tabelle aus. Klicken Sie anschließend auf das Feld **DAX-Filter**, und geben Sie im Feld **DAX-Filter – \<Tabellenname>** eine DAX-Formel ein.  
  
    > [!NOTE]  
    >  Das Feld „DAX-Filter – \<Tabellenname>“ enthält keinen Abfrage-Editor mit AutoVervollständigen-Funktion und keine Option zum Einfügen von Funktionen. Um beim Schreiben einer DAX-Formel die Funktion zum AutoVervollständigen verwenden zu können, müssen Sie in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]einen DAX-Formel-Editor verwenden.  
  
9. Klicken Sie auf **OK** , um die Rolle zu speichern.  
  
###  <a name="bkmk_copy_role"></a> So kopieren Sie eine Rolle  
  
1.  Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die tabellarische Modelldatenbank, die die Rolle enthält, die Sie kopieren möchten, und erweitern Sie dann **Rollen**. Klicken Sie mit der rechten Maustaste auf die Rolle, und klicken Sie dann auf **Duplizieren**.  
  
###  <a name="bkmk_edit_role"></a> So bearbeiten Sie eine Rolle  
  
-   Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die tabellarische Modelldatenbank, die die Rolle enthält, die Sie bearbeiten möchten, und erweitern Sie dann **Rollen**. Klicken Sie mit der rechten Maustaste auf die Rolle, und klicken Sie dann auf **Eigenschaften**.  
  
     Im Dialogfeld „**Rolleneigenschaften** \<Rollenname>“ können Sie Berechtigungen ändern, Mitglieder hinzufügen oder entfernen und Zeilenfilter hinzufügen oder bearbeiten.  
  
###  <a name="bkmk_deletet_role"></a> So löschen Sie eine Rolle  
  
-   Erweitern Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die tabellarische Modelldatenbank, die die Rolle enthält, die Sie löschen möchten, und erweitern Sie dann **Rollen**. Klicken Sie mit der rechten Maustaste auf die Rolle, und klicken Sie dann auf **Löschen**.  
  
## Siehe auch  
 [Rollen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  