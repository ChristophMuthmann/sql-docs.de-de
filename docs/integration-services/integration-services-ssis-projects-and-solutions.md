---
title: Integration Services-Projekte und -Projektmappen (SSIS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.importprojectwizard.f1
helpviewer_keywords:
- projects [Integration Services], creating
- folders [Integration Services], projects
- files [Integration Services], projects
- folders [Integration Services]
- projects [Integration Services], about projects
ms.assetid: 28ea8120-0a79-4029-93f0-07d521b32bee
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 57dd62cdd59b3ec571f2e9705e15ca64f3f18124
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="integration-services-ssis-projects-and-solutions"></a>SQL Server Integration Services-Projekte und Projektmappen (SSIS)
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] stellt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] für die Entwicklung von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Paketen bereit.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete werden in Projekten gespeichert. Sie müssen die [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Umgebung installieren, um [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] -Projekte zu erstellen und zu verwenden. Weitere Informationen finden Sie unter [Installieren von Integration Services](../integration-services/install-windows/install-integration-services.md).  
  
 Wenn Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]erstellen, enthält das Dialogfeld **Neues Projekt** die Vorlage **Integration Services-Projekt** . Diese Projektvorlage erstellt ein neues Projekt, das ein einzelnes Paket enthält.  
  
## <a name="projects-and-solutions"></a>Projekte und Projektmappen  
 Projekte werden in Projektmappen gespeichert. Sie können zuerst eine Projektmappe erstellen und dann ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzufügen. Falls keine Projektmappe vorhanden ist, erstellt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] automatisch eine Projektmappe für Sie, wenn Sie das Projekt erstellen. Eine Projektmappe kann mehrere Projekte unterschiedlichen Typs enthalten.  
  
> [!TIP]  
>  Wenn Sie in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] ein neues Projekt erstellen, wird die Projektmappe standardmäßig nicht im Bereich **Projektmappen-Explorer** angezeigt. Um dieses Standardverhalten zu ändern, klicken Sie im Menü **Extras** auf **Optionen**. Erweitern Sie im Dialogfeld **Optionen** den Eintrag **Projekte und Projektmappen**, und klicken Sie dann auf **Allgemein**. Wählen Sie auf der Seite **Allgemein** die Option **Projektmappe immer anzeigen**aus.  

## <a name="solutions-contain-projects"></a>Lösungen enthalten Projekte  
 Eine Projektmappe ist ein Container, in dem die Projekte gruppiert und verwaltet werden, die Sie zum Entwickeln von End-to-End-Unternehmenslösungen verwenden. Mithilfe einer Projektmappe können Sie mehrere Projekte als Einheit verwalten und zusammenhängende Projekte für eine Unternehmenslösung zusammenbringen.  
  
 Projektmappen können unterschiedliche Projekttypen enthalten. Wenn Sie [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer zum Erstellen eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakets verwenden, arbeiten Sie in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt in einer von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]bereitgestellten Projektmappe.  
  
 Wenn Sie eine neue Projektmappe erstellen, fügt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] dem Projektmappen-Explorer einen Projektmappenordner hinzu und erstellt Dateien mit den Dateierweiterungen „.sln“ und „.suo“.  
  
-   Die SLN-Datei enthält Informationen zur Projektmappenkonfiguration und führt die Projekte in der Projektmappe auf.  
  
-   Die SUO-Datei enthält Informationen zu Ihren Einstellungen für das Verwenden der Projektmappe.  
  
 Zwar wird von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] beim Erstellen eines neuen Projekts automatisch eine Projektmappe erstellt, jedoch können Sie auch eine leere Projektmappe erstellen und später Projekte hinzufügen.  
   
## <a name="integration-services-projects-contain-packages"></a>Integration Services-Projekte enthalten Pakete  
 Ein Projekt ist ein Container, in dem Sie [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Pakete entwickeln.  
  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]werden in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekten die mit dem Paket verknüpften Dateien gespeichert und gruppiert. Beispielsweise enthält ein Projekt die zum Erstellen einer bestimmten ETL-Projektmappe (Extract, Transfer, And Load) erforderlichen Dateien.  
  
 Vor dem Erstellen eines [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekts sollten Sie sich mit den grundlegenden Inhalten dieser Art von Projekten vertraut machen. Wenn Sie die Inhalte eines Projekts verstanden haben, können Sie ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt erstellen und verwenden.  
  
## <a name="folders-in-integration-services-projects"></a>Ordner in SQL Server Integration Services-Projekten  
 Im folgenden Diagramm werden die Ordner in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]veranschaulicht.  
  
 ![Ordner in einem Integration Services-Projekt](../integration-services/media/solutionexplorer.gif "Folders in an Integration Services project")  
  
 In der folgende Tabelle werden die Ordner in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt beschrieben.  
  
|Ordner|Description|  
|------------|-----------------|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] Pakete|Enthält Pakete. Weitere Informationen finden Sie unter [Integration Services-Pakete &#40;SSIS&#41;](../integration-services/integration-services-ssis-packages.md).|  
|Sonstiges|Enthält Dateien, die sich von Paketdateien unterscheiden.|  
  
## <a name="files-in-integration-services-projects"></a>Dateien in SQL Server Integration Services-Projekten  
 Wenn Sie einer Projektmappe ein neues oder vorhandenes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzufügen, erstellt [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] Projektdateien mit den Erweiterungen DTPROJ, DTPROJ.USER und DATABASE.  
  
-   Die DTPROJ-Datei enthält Informationen zu Projektkonfigurationen und Elementen wie Pakete.  
  
-   Die DTPROJ.USER-Datei enthält Informationen zu Ihren Einstellungen für das Verwenden dieses Projekts.  
  
-   Die DATABASE-Datei enthält Informationen, die [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] zum Öffnen des [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekts benötigt.  
  
## <a name="version-targeting-in-integration-services-projects"></a>Versionsauswahl in Integration Services-Projekten  
 In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]können Sie Pakete für SQL Server 2016, SQL Server 2014 oder SQL Server 2012 erstellen, verwalten und ausführen.  
  
 Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf ein Integration Services-Projekt, und wählen Sie **Eigenschaften** aus, um die Eigenschaftsseiten für das Projekt zu öffnen. Klicken Sie in der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie dann SQL Server 2016, 2014 oder 2012 aus.  
  
 ![TargetServerVersion-Eigenschaft im Dialogfeld „Projekteigenschaften“](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
 
## <a name="create-a-new-integration-services-project"></a>Erstellen eines neuen SQL Server Integration Services-Projekts  
  
1.  Öffnen Sie [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Zeigen Sie im Menü **Datei** auf **Neu**, und klicken Sie dann auf **Projekt**.  
  
3.  Wählen Sie im Dialogfeld **Neues Projekt** im Bereich **Vorlagen** die Vorlage **Integration Services-Projekt** aus.  
  
     Die **Integration Services-Projekt** -Vorlage erstellt ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt, das ein einzelnes, leeres Paket enthält.  
  
4.  (Optional) Bearbeiten Sie den Projektnamen und den Speicherort.  
  
     Der Projektmappenname wird automatisch aktualisiert und an den Projektnamen angepasst.  
  
5.  Um einen separaten Ordner für die Projektmappendatei zu erstellen, aktivieren Sie das Kontrollkästchen **Projektmappenverzeichnis erstellen**. Diese Option ist die Standardeinstellung.  
  
6.  Wenn die Software für die Quellcodeverwaltung auf dem Computer installiert ist, wählen Sie **Zur Quellcodeverwaltung hinzufügen**  aus, um das Projekt der Quellcodeverwaltung zuzuordnen.  
  
7.  Falls es sich bei der Software für die Quellcodeverwaltung um [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe handelt, wird das Dialogfeld **Visual SourceSafe-Anmeldung** geöffnet. Stellen Sie im Dialogfeld **Visual SourceSafe-Anmeldung**einen Benutzernamen, ein Kennwort und den Namen der [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe-Datenbank bereit. Klicken Sie auf **Durchsuchen** , um die Datenbank zu suchen.  
  
    > **HINWEIS:** Klicken Sie im Menü **Extras** auf **Optionen**, und erweitern Sie den Knoten **Quellcodeverwaltung**, um das ausgewählte Quellcodeverwaltungs-Plug-In anzuzeigen und zu ändern und um die Umgebung für die Quellcodeverwaltung zu konfigurieren.  
  
8.  Klicken Sie auf **OK** , um die Projektmappe dem **Projektmappen-Explorer** und das Projekt der Projektmappe hinzuzufügen.  
  
## <a name="choose-the-target-version-of-a-project-and-its-packages"></a>Wählen der Zielversion eines Projekt und der zugehörigen Pakete  
  
1.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf ein Integration Services-Projekt, und wählen Sie **Eigenschaften** aus, um die Eigenschaftsseiten für das Projekt zu öffnen.  
  
2.  Klicken Sie in der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie dann SQL Server 2016, 2014 oder 2012 aus.  
  
     ![TargetServerVersion-Eigenschaft im Dialogfeld „Projekteigenschaften“](../integration-services/media/targetserverversion2.png "TargetServerVersion property in project properties dialog box")  
  
 Sie können Pakete für SQL Server 2016, SQL Server 2014 oder SQL Server 2012 erstellen, verwalten und ausführen.  

## <a name="import-an-existing-project-with-the-import-project-wizard"></a>Importieren eines bestehenden Projekts mit dem Assistenten zum Importieren von Projekten
  
1.  Klicken Sie in [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]im Menü **Datei** > **auf** Neu **Projekt** .  
  
2.  Erweitern Sie im Bereich **Installierte Vorlagen** des Fensters **Neues Projekt** **Business Intelligence**, und klicken Sie auf **Integration Services**.  
  
3.  Wählen Sie **Integration Services-Assistent zum Importieren von Projekten** aus der Liste der Projekttypen aus.  
  
4.  Geben Sie einen Namen für das neu zu erstellende Projekt im Textfeld **Name** ein.  
  
5.  Geben Sie den Pfad oder Speicherort für das Projekt im Textfeld **Speicherort** ein, oder klicken Sie auf **Durchsuchen** , um ihn auszuwählen.  
  
6.  Geben Sie einen Namen für die Projektmappe im Textfeld **Projektmappenname** ein.  
  
7.  Klicken Sie auf **OK** , um das Dialogfeld **Integration Services-Assistent zum Importieren von Projekten** zu starten.  
  
8.  Klicken Sie auf **Weiter** , um zur Seite **Quelle auswählen** zu wechseln.  
  
9. Wenn Sie aus einer **ISPAC-Datei** importieren, geben Sie den Pfad einschließlich Dateinamen im Textfeld **Pfad** ein. Klicken Sie auf **Durchsuchen** , um zu dem Ordner zu navigieren, in dem die Projektmappe gespeichert werden soll. Geben Sie den Dateinamen im Textfeld **Dateiname** ein, und klicken Sie auf **Öffnen**.  
  
     Wenn Sie aus einem **Integration Services-Katalog**importieren, geben Sie den Datenbankinstanznamen im Textfeld **Servername** ein, oder klicken Sie auf **Durchsuchen** und wählen Sie die Datenbankinstanz aus, die den Katalog enthält.  
  
     Klicken Sie auf **Durchsuchen** neben dem Textfeld **Pfad** , erweitern Sie den Ordner im Katalog, wählen Sie das Projekt aus, das Sie importieren möchten, und klicken Sie auf **OK**.  
  
     Klicken Sie auf **Weiter** , um zur Seite **///Überprüfen** zu wechseln.  
  
10. Überprüfen Sie die Informationen, und klicken Sie auf **Importieren** , um ein Projekt auf Grundlage des vorhandenen Projekts zu erstellen, das Sie ausgewählt haben.  
  
11. Optional: Klicken Sie auf **Bericht speichern** , um die Ergebnisse in einer Datei zu speichern.  
  
12. Klicken Sie auf **Schließen** , um das Dialogfeld **Integration Services-Assistent zum Importieren von Projekten** zu schließen.  

## <a name="add-a-project-to-a-solution"></a>Hinzufügen eines Projekts zu einer Projektmappe 
 Beim Hinzufügen eines Projekts können Sie mit [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ein neues, leeres Projekt erstellen oder ein bereits für eine andere Projektmappe erstelltes Projekt hinzufügen. Sie können ein Projekt nur einer vorhandenen Projektmappe hinzufügen, wenn die Projektmappe in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]sichtbar ist.  
  
### <a name="add-a-new-project-to-a-solution"></a>Hinzufügen eines neuen Projekts zu einer Projektmappe  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]die Projektmappe, der Sie ein neues [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzufügen möchten, und führen Sie eine der folgenden Aktionen aus:  
  
    -   Klicken Sie mit der rechten Maustaste auf die Projektmappe, klicken Sie auf **Hinzufügen**, und klicken Sie dann auf **Neues Projekt**.  
  
    -   Zeigen Sie im Menü **Datei** auf **Hinzufügen**, und klicken Sie dann auf **Neues Projekt**.  
  
2.  Klicken Sie im Dialogfeld **Neues Projekt hinzufügen** im Fensterbereich **Vorlagen** auf **Integration Services-Projekt** .  
  
3.  Bearbeiten Sie optional den Projektnamen und den Speicherort.  
  
4.  Klicken Sie auf **OK**.  
  
### <a name="add-an-existing-project-to-a-solution"></a>Hinzufügen eines vorhandenen Projekts zu einer Projektmappe  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]die Projektmappe, der Sie ein vorhandenes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt hinzufügen möchten, und führen Sie eine der folgenden Aktionen aus:  
  
    -   Klicken Sie mit der rechten Maustaste auf die Projektmappe, zeigen Sie auf **Hinzufügen**, und klicken Sie dann auf **Vorhandenes Projekt**.  
  
    -   Klicken Sie im Menü **Datei** auf **Hinzufügen**, und klicken Sie dann auf **Vorhandenes Projekt**.  
  
2.  Suchen Sie im Dialogfeld **Vorhandenes Projekt hinzufügen** das Projekt, das Sie hinzufügen möchten, und klicken Sie dann auf **Öffnen**.  
  
3.  Das Projekt wird dem Projektmappenordner im **Projektmappen-Explorer**hinzugefügt.  
  
## <a name="remove-a-project-from-a-solution"></a>Entfernen eines Projekts aus einer Projektmappe
 Sie können ein Projekt aus einer Projektmappe nur entfernen, wenn die Projektmappe in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]sichtbar ist. Nachdem die Projektmappe sichtbar ist, können alle Projekte, außer einem Projekt, entfernt werden. Sobald nur ein Projekt verbleibt, wird der Projektmappenordner in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] nicht mehr angezeigt, und das Löschen des letzten Projekts ist nicht möglich.  
   
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]die Projektmappe, aus der Sie ein [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt entfernen möchten.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, und klicken Sie dann auf **Projekt entladen**.  
  
3.  Klicken Sie auf **OK** , um das Entfernen zu bestätigen.  

## <a name="add-an-item-to-a-project"></a>Hinzufügen eines Elements zu einem Projekt  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]die Projektmappe mit dem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt, dem Sie ein Element hinzufügen möchten.  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf das Projekt, zeigen Sie auf **Hinzufügen**, und führen Sie eine der folgenden Aktionen aus:  
  
    -   Klicken Sie auf **Neues Element**, und wählen Sie im Bereich **Vorlagen** im Dialogfeld **Neues Element hinzufügen** eine Vorlage aus.  
  
    -   Klicken Sie auf **Vorhandenes Element**, suchen Sie im Dialogfeld **Vorhandenes Element hinzufügen** nach dem Element, das Sie dem Projekt hinzufügen möchten, und klicken Sie dann auf **Hinzufügen**.  
  
3.  Das neue Element wird im Projektmappen-Explorer im entsprechenden Ordner angezeigt.  

## <a name="copy-project-items"></a>Kopieren von Projektelementen  
Sie können Objekte in einem [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt oder zwischen [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekten kopieren. Sie können Objekte auch zwischen anderen Typen von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] -Projekten, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] und [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]kopieren. Für den Kopiervorgang zwischen den Projekten müssen die Projekte Teil derselben [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] -Projektmappe sein.

1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt bzw. die Projektmappe, mit dem bzw. mit der Sie arbeiten möchten.  
  
2.  Erweitern Sie das Projekt und den Elementordner, aus dem Sie kopieren möchten.  
  
3.  Klicken Sie mit der rechten Maustaste auf das Element, und klicken Sie anschließend auf **Kopieren**.  
  
4.  Klicken Sie mit der rechten Maustaste auf das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Projekt, in das kopiert werden soll, und klicken Sie auf **Einfügen**.  
  
     Die Elemente werden automatisch in den richtigen Ordner kopiert. Wenn Sie in das [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Projekt Elemente kopieren, die keine Pakete darstellen, werden die Elemente in den Ordner **Sonstiges** kopiert.  
     
