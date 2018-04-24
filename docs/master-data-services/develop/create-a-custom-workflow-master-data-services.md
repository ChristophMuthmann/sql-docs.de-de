---
title: Erstellen eines benutzerdefinierten Workflows (Master Data Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: develop
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 8e4403e9-595c-4b6b-9d0c-f6ae1b2bc99d
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e9068bb0564b0b4f0635175efb1a1805bcd2f4e5
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2018
---
# <a name="create-a-custom-workflow-master-data-services"></a>Erstellen eines benutzerdefinierten Workflows (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] verwendet Geschäftsregeln, um auf Basis der von Ihnen festgelegten Bedingungen grundlegende Workflowlösungen zu erstellen, beispielsweise das automatische Update und Validieren von Daten sowie das Senden von E-Mail-Benachrichtigungen. Wenn Sie Verarbeitungsfunktionen benötigen, die komplexer als die anhand der integrierten Workflowaktionen bereitgestellten Funktionen sind, verwenden Sie einen benutzerdefinierten Workflow. Ein benutzerdefinierter Workflow ist eine .NET-Assembly, die Sie erstellen. Wenn die Workflowassembly aufgerufen wird, kann der Code jede Aktion ausführen, die in Ihrer Situation erforderlich ist. Erfordert Ihr Workflow beispielsweise eine komplexe Ereignisverarbeitung wie Genehmigungen mit mehreren Ebenen oder komplizierte Entscheidungsstrukturen, können Sie [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] so konfigurieren, dass ein benutzerdefinierter Workflow gestartet wird, der die Daten analysiert und den Empfänger der Daten für die Genehmigung bestimmt.  
  
## <a name="how-custom-workflows-are-processed"></a>Verarbeitung von benutzerdefinierten Workflows  
 Es gibt drei Hauptkomponenten für die Verarbeitung von benutzerdefinierten Workflows: die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]-Webanwendung, den SQL Server MDS Workflow Integration Service und die Workflowhandlerassembly. Diese Komponenten verarbeiten einen benutzerdefinierten Workflow folgendermaßen:  
  
1.  Sie verwenden [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], um eine Entität zu validieren, die einen Workflow startet.  
  
2.  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] sendet Elemente, die die Geschäftsregelbedingungen für eine Service Broker-Warteschlange in der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank erfüllen.  
  
3.  In regelmäßigen Abständen ruft der SQL Server MDS Workflow Integration Service eine gespeicherte Prozedur in der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank auf.  
  
4.  Wenn diese gespeicherte Prozedur Datensätze in der Service Broker-Warteschlange findet, gibt sie diese an den SQL Server MDS Workflow Integration Service zurück.  
  
5.  Der SQL Server-MDS Workflow Integration Service leitet die Daten an die Workflowhandlerassembly weiter.  
  
> [!NOTE]  
>  Hinweis: Der SQL Server MDS Workflow Integration Service ist für das Auslösen von einfachen Prozessen konzipiert. Wenn der benutzerdefinierte Code komplexe Verarbeitungsvorgänge erfordert, führen Sie die Verarbeitung entweder in einem separaten Thread oder außerhalb des Workflowprozesses aus.  
  
## <a name="configure-master-data-services-for-custom-workflows"></a>Konfigurieren von Master Data Services für benutzerdefinierte Workflows  
 Das Erstellen eines benutzerdefinierten Workflows erfordert das Schreiben von benutzerdefiniertem Code sowie das Konfigurieren von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] zur Übergabe von Workflowdaten an den Workflowhandler. Gehen Sie folgendermaßen vor, um die Verarbeitung von benutzerdefinierten Workflows zu aktivieren:  
  
1.  Erstellen Sie eine .NET-Assembly, die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender> implementiert.  
  
2.  Konfigurieren Sie den SQL Server MDS Workflow Integration Service, um eine Verbindung mit der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank herzustellen und dem Workflowhandler ein Tag zuzuordnen.  
  
3.  Starten Sie den SQL Server MDS Workflow Integration Service.  
  
4.  Erstellen Sie in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] eine Geschäftsregel zum Starten eines Workflows, der mit dem Namen des Workflowhandlers gekennzeichnet ist.  
  
5.  Wenden Sie die Geschäftsregel auf ein Element an, das den benutzerdefinierten Workflow auslöst.  
  
### <a name="create-the-workflow-handler-assembly"></a>Erstellen der Workflowhandlerassembly  
 Ein benutzerdefinierter Workflow ist eine .NET-Klassenbibliotheksassembly, die die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>-Schnittstelle implementiert. Der SQL Server MDS Workflow Integration Service ruft zum Ausführen des Codes die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>-Methode auf. Beispielcode, der <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> implementiert, finden Sie unter [Beispiel für einen benutzerdefinierten Workflow &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md).  
  
 Gehen Sie wie folgt vor, um mit Visual Studio 2010 eine Assembly zu erstellen, die der SQL Server MDS Workflow Integration Service aufrufen kann, um einen benutzerdefinierten Workflow zu behandeln:  
  
1.  Erstellen Sie in Visual Studio 2010 ein neues **Klassenbibliotheksprojekt**, das Ihre gewünschte Sprache verwendet. Um eine C#-Klassenbibliothek zu erstellen, wählen Sie die **Visual C#\Windows**-Projekttypen sowie die **Klassenbibliotheksvorlage** aus. Geben Sie einen Namen für das Projekt ein, z.B. **MDSWorkflowTest**, und klicken Sie auf **OK**.  
  
2.  Fügen Sie einen Verweis auf Microsoft.MasterDataServices.WorkflowTypeExtender.dll hinzu. Diese Assembly befindet sich unter \<Ihr Installationsordner>\Master Data Services\WebApplication\bin.  
  
3.  Fügen Sie "using Microsoft.MasterDataServices.Core.Workflow;" der C#-Codedatei hinzu.  
  
4.  Erben Sie in der Klassendeklaration von <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>. Die Klassendeklaration sollte in etwa wie folgt aussehen: "public class WorkflowTester : IWorkflowTypeExtender".  
  
5.  Implementieren Sie die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender>-Schnittstelle. Die <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>-Methode wird vom SQL Server MDS Workflow Integration Service aufgerufen, um den Workflow zu starten.  
  
6.  Legen Sie eine Kopie der Assembly am Speicherort der ausführbaren Datei des SQL Server MDS Workflow Integration Service ab, die sich „Microsoft.MasterDataServices.Workflow.exe“ nennt (unter \<Ihr Installationsordner>\Master Data Services\WebApplication\bin).  
  
### <a name="configure-sql-server-mds-workflow-integration-service"></a>Konfigurieren des SQL Server MDS Workflow Integration Service  
 Bearbeiten Sie die [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Konfigurationsdatei, um Verbindungsinformationen für die [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank einzubinden und der Workflowhandlerassembly wie folgt ein Tag zuzuordnen:  
  
1.  Suchen Sie nach der Datei „Microsoft.MasterDataServices.Workflow.exe.config“ unter \<Ihr Installationsordner>\Master Data Services\WebApplication\bin.  
  
2.  Fügen Sie der Einstellung "ConnectionString" die Verbindungsinformationen der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank hinzu. Wenn die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Installation eine Sortierung mit Berücksichtigung der Groß-/Kleinschreibung verwendet, muss der Name der Datenbank in der gleichen Schreibweise wie in der Datenbank eingegeben werden. Beispielsweise kann das vollständige Einstellungstag wie folgt aussehen:  
  
    ```xml  
    <setting name="ConnectionString" serializeAs="String">  
        <value>Server=myServer;Database=myDatabase;Integrated Security=True</value>  
    </setting>  
    ```  
  
3.  Fügen Sie unter der Einstellung "ConnectionString" eine WorkflowTypeExtenders-Einstellung hinzu, um der Workflowhandlerassembly einen Tagnamen zuzuordnen. Zum Beispiel:  
  
    ```xml  
    <setting name="WorkflowTypeExtenders" serializeAs="String">  
        <value>TEST=MDSWorkflowTestLib.WorkflowTester, MDSWorkflowTestLib</value>  
    </setting>  
    ```  
  
     Der innere Text des Tags \<Wert> hat das Format \<Workflowtag>=\<durch die Assembly qualifizierter Workflowtypname>. \<Workflowtag> ist ein Name, mit dem Sie die Workflowhandlerassembly identifizieren, wenn Sie in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] eine Geschäftsregel erstellen. \<durch die Assembly qualifizierter Workflowtypname> entspricht dem durch einen Namespace qualifizierten Namen der Workflowklasse, gefolgt von einem Komma und dem Anzeigenamen der Assembly. Verfügt die Assembly über einen starken Namen, binden Sie zudem Versionsinformationen und sowie das zugehörige PublicKeyToken ein. Sie können mehrere \<Einstellungstags> einbinden, wenn Sie mehrere Workflowhandler für andere Arten von Workflows erstellt haben.  
  
> [!NOTE]  
>  Je nach Serverkonfiguration wird möglicherweise der Fehler "Der Zugriff wurde verweigert" angezeigt, wenn Sie versuchen, die Datei "Microsoft.MasterDataServices.Workflow.exe.config" zu speichern. Tritt dieser Fehler auf, deaktivieren Sie vorübergehend die Benutzerkontensteuerung (UAC) auf dem Server. Öffnen Sie dazu die Systemsteuerung, und klicken Sie auf **System und Sicherheit**. Klicken Sie unter **Wartungscenter** auf **Einstellungen der Benutzerkontensteuerung ändern**. Schieben Sie im Dialogfeld **Einstellungen zur Benutzerkontensteuerung** den Balken nach unten, damit Sie keine Benachrichtigung erhalten. Starten Sie den Computer neu, und wiederholen Sie die vorherigen Schritte, um die Konfigurationsdatei zu bearbeiten. Setzen Sie nach dem Speichern der Datei die UAC-Einstellungen auf die Standardebene zurück.  
  
### <a name="start-sql-server-mds-workflow-integration-service"></a>Starten des SQL Server MDS Workflow Integration Service  
 Standardmäßig ist SQL Server MDS Workflow Integration Service nicht installiert. Sie müssen den Dienst installieren, bevor er verwendet werden kann. Erstellen Sie für eine maximale Sicherheit einen lokalen Benutzer für den Dienst, und weisen Sie diesem Benutzer nur die zum Ausführen von Workflowvorgängen erforderlichen Berechtigungen zu. Gehen Sie wie folgt vor, um einen Benutzer zu erstellen sowie den Dienst zu installieren und zu starten:  
  
1.  Erstellen Sie mit dem Manager für lokale Benutzer und Gruppen einen lokalen Benutzer, beispielsweise mit dem Namen "mds_workflow_service".  
  
2.  Weisen Sie mithilfe von SQL Server Management Studio dem Benutzer "mds_workflow_service" die Berechtigung zum Ausführen der gespeicherten Prozedur "[mdm].[udpExternalActionsGet]" zu. Erstellen Sie dazu eine neue Anmeldung für das Konto "mds_workflow_service", erstellen Sie in der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank einen neuen Benutzer, ordnen Sie diesen Benutzer der Anmeldung "mds_workflow_service" zu, und gewähren Sie dem Benutzer die EXECUTE-Berechtigung für die gespeicherte Prozedur "[mdm].[udpExternalActionsGet]".  
  
3.  Gewähren Sie dem Benutzer "mds_workflow_service" die Berechtigung zum Ausführen der Workflowhandlerassembly. Fügen Sie dazu den Benutzer „mds_workflow_service“ der Registerkarte **Sicherheit** im Bereich **Eigenschaften** der Workflowhandlerassembly hinzu, und gewähren Sie dem Benutzer „mds_workflow_service“ die READ- und EXECUTE-Berechtigung.  
  
4.  Gewähren Sie dem Benutzer "mds_workflow_service" die Berechtigung zum Ausführen der ausführbaren Datei des SQL Server MDS Workflow Integration Service. Fügen Sie dazu den Benutzer „mds_workflow_service“ der Registerkarte **Sicherheit** im Bereich **Eigenschaften** der Datei „Microsoft.MasterDataServices.Workflow.exe“ hinzu, die unter \<Ihr Installationsordner>\Master Data Services\WebApplication\bin gespeichert ist, und gewähren Sie dem Benutzer „mds_workflow_service“ die READ- und EXECUTE-Berechtigung.  
  
5.  Installieren Sie SQL Server MDS Workflow Integration Service mithilfe des .NET-Installationshilfsprogramms (InstallUtil.exe). Die Datei „InstallUtil.exe“ befindet sich im .NET-Installationsordner, z.B. unter C:\Windows\Microsoft.NET\Framework\v4.0.30319\\\. Installieren Sie den SQL Server MDS Workflow Integration Service durch folgende Eingabe in einer Eingabeaufforderung für erhöhte Rechte:  
  
    ```  
    C:\Windows\Microsoft.NET\Framework\v4.0.30319\InstallUtil Microsoft.MasterDataServices.Workflow.exe  
    ```  
  
     Geben Sie während der Installation bei entsprechender Aufforderung den Benutzer "mds_workflow_service" an.  
  
6.  Starten Sie SQL Server MDS Workflow Integration Service mithilfe des Dienst-Snap-Ins. Suchen Sie dazu SQL Server MDS Workflow Integration Service im Dienst-Snap-In, wählen Sie den Dienst aus, und klicken Sie auf den Link **Starten**.  
  
### <a name="create-a-workflow-business-rule"></a>Erstellen einer Workflowgeschäftsregel  
 Erstellen und veröffentlichen Sie mithilfe von [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] eine Geschäftsregel, die bei Anwendung den Workflow startet. Die Geschäftsregel muss Aktionen enthalten, die Attributwerte ändern, damit die Regel den Wert "false" ergibt, nachdem sie einmal übernommen wurde. Beispielsweise kann die Geschäftsregel den Wert "true" ergeben, wenn ein Preisattributwert größer als 500 und der Approved-Attributwert leer ist. Die Regel kann dann zwei Aktionen umfassen, und zwar eine zum Festlegen des Approved-Attributwerts auf "Ausstehend" und eine zum Starten des Workflows. Sie können alternativ eine Regel erstellen, die auf die Bedingung "has changed" (wurde geändert) zurückgreift, und Ihre Attribute hinzufügen, um die Nachverfolgungsgruppen zu ändern. Weitere Informationen finden zu Geschäftsregeln Sie unter [Geschäftsregeln &#40;Master Data Services&#41;](../../master-data-services/business-rules-master-data-services.md).  
  
 Erstellen Sie wie folgt eine Geschäftsregel, mit der ein benutzerdefinierter Workflow in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] gestartet wird:  
  
1.  Ziehen Sie im Geschäftsregel-Editor von [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] nach der Angabe der Bedingungen für die Geschäftsregel die Aktion **Workflow starten** von der Liste für **externe Aktionen** zur Bezeichnung **Aktion** des Bereichs **THEN**.  
  
2.  Geben Sie im Bereich **Aktion bearbeiten** im Feld **Workflowtyp** das Tag ein, mit dem die Workflowhandlerassembly identifiziert wird. Hierbei handelt es sich um das Tag, das Sie in der Konfigurationsdatei für die Assembly angegeben haben, beispielsweise TEST.  
  
3.  Aktivieren Sie optional das Kontrollkästchen zum **Einschließen von Elementdaten**. Wählen Sie diese Option aus, um Attributnamen und Werte in der XML einzuschließen, die an den Workflowhandler übergeben wird.  
  
4.  Geben Sie im Feld **Workflowsite** den Namen einer Website ein. Dies gilt u. U. nicht für den benutzerdefinierten Workflow, kann jedoch für zusätzlichen Kontext angewendet werden.  
  
5.  Geben Sie im Feld **Workflowname** den Namen des Workflows von Visual Studio ein. Dies gilt u. U. nicht für den benutzerdefinierten Workflow, kann jedoch für zusätzlichen Kontext angewendet werden.  
  
6.  Speichern und veröffentlichen Sie die Geschäftsregel.  
  
### <a name="apply-business-rules-to-start-a-workflow"></a>Anwenden von Geschäftsregeln zum Starten eines Workflows  
 Wenden Sie zum Starten des Workflows die Geschäftsregel auf die Daten an. Bearbeiten Sie dazu mithilfe von [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] die Entität mit den zu validierenden Elementen. Klicken Sie auf **Geschäftsregeln anwenden**. Als Reaktion auf die Geschäftsregel füllt [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] die Service Broker-Warteschlange der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank auf. Überprüft der SQL Server MDS Workflow Integration Service die Warteschlange, werden die Daten an die angegebene Workflowhandlerassembly gesendet, und die Warteschlange wird geleert. Die Workflowhandlerassembly führt die Aktionen aus, die Sie darin codiert haben.  
  
## <a name="troubleshoot-custom-workflows"></a>Beheben von Fehlern bei benutzerdefinierten Workflows  
 Wenn die Workflowhandlerassembly keine Daten empfängt, versuchen Sie, SQL Server MDS Workflow Integration Service zu debuggen oder die Service Broker-Warteschlange anzuzeigen.  
  
### <a name="debug-sql-server-mds-workflow-integration-service"></a>Debuggen von SQL Server MDS Workflow Integration Service  
 So debuggen Sie SQL Server Workflow Integration Service:  
  
1.  Verwenden Sie das Dienst-Snap-In, um den Dienst zu beenden.  
  
2.  Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Speicherort des Diensts, und führen Sie den Dienst im Konsolenmodus aus. Geben Sie dazu Folgendes ein: Microsoft.MasterDataServices.Workflow.exe -console.  
  
3.  Aktualisieren Sie in [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] das Element, und wenden Sie erneut Geschäftsregeln an. Ausführliche Protokolle werden im Konsolenfenster angezeigt.  
  
### <a name="view-the-service-broker-queue"></a>Anzeigen der Service Broker-Warteschlange  
 Die Service Broker-Warteschlange, die die als Teil des Workflows übergebenen Masterdaten enthält, lautet folgendermaßen: mdm.microsoft/mdm/queue/externalaction. Warteschlangen befinden sich im **Objekt-Explorer** von SQL Management Studio unter dem Service Broker-Knoten der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]-Datenbank. Wenn der Dienst die Warteschlange ordnungsgemäß geleert hat, ist diese Warteschlange leer.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Beispiel für einen benutzerdefinierten Workflow &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-example.md)   
 [Benutzerdefinierte Workflow-XML-Beschreibung &#40;Master Data Services&#41;](../../master-data-services/develop/create-a-custom-workflow-xml-description.md)  
  
  
