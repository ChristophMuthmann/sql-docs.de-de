---
title: Integration Services (SSIS)-Paket und Projektparametern | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.parameter.f1
- sql13.dts.designer.paramterwindow.f1
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 59c7e1cc3c31f77652acb21d375e1294bdc93397
ms.openlocfilehash: eb3b444f7cc248e89d21970d174d9792711dfbc6
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="integration-services-ssis-package-and-project-parameters"></a>Integration Services (SSIS)-Paket und Projektparametern
  Mit[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -(SSIS-)Parametern können Sie Eigenschaften in Paketen zur Zeit der Paketausführung Werte zuweisen. Sie können *Projektparameter* auf Projektebene und *Paketparameter* auf Paketebene erstellen. Projektparameter werden verwendet, um jegliche externen Eingaben bereitzustellen, die das Projekt für ein oder mehrere Pakete im Projekt empfängt. Mit Paketparametern können Sie die Paketausführung ändern, ohne das Paket bearbeiten und erneut bereitstellen zu müssen.  
  
 In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] können Sie im Fenster **Project.params** Projektparameter erstellen, ändern oder löschen. Sie erstellen, ändern und löschen Paketparameter mit der Registerkarte **Parameter** im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer. Im Dialogfeld **Parametrisieren** können Sie einen neuen oder vorhandenen Parameter einer Taskeigenschaft zuordnen. Weitere Informationen zum Verwenden des Fensters **Project.params** und der Registerkarte **Parameter** finden Sie unter [Create Parameters](http://msdn.microsoft.com/library/cd5d675b-dd5d-49cc-8b1f-dc717a973f99). Weitere Informationen zum Dialogfeld **Parametrisieren** finden Sie unter [Parameterize Dialog Box](http://msdn.microsoft.com/library/fac02b6d-d247-447a-8940-e8700c7ac350).  
  
## <a name="parameters-and-package-deployment-model"></a>Parameter und Paketbereitstellungsmodell  
 Im Allgemeinen sollten Sie beim Bereitstellen eines Pakets mit dem Paketbereitstellungsmodell Konfigurationen anstelle von Parametern verwenden.  
  
 Wenn Sie mithilfe des Paketbereitstellungsmodells ein Paket bereitstellen, das Parameter enthält, und dann das Paket ausführen, werden die Parameter während der Ausführung nicht aufgerufen. Wenn das Paket Paketparameter und Ausdrücke innerhalb des Pakets enthält, verwenden Sie die Parameter, die resultierenden Werte werden zur Laufzeit übernommen. Wenn das Paket Projektparameter enthält, tritt bei der Paketausführung möglicherweise ein Fehler auf.  
  
## <a name="parameters-and-project-deployment-model"></a>Parameter und Projektbereitstellungsmodell  
 Wenn Sie ein Projekt auf dem Integration Services-Server (SSIS) bereitstellen, verwenden Sie Sichten, gespeicherte Prozeduren und die [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] -Benutzeroberfläche zum Verwalten von Projekt- und Paketparametern. Weitere Informationen finden Sie in den nachfolgenden Themen.  
  
-   [Sichten &#40; Integration Services-Katalog &#41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [Gespeicherte Systemprozeduren &#40; Integration Services-Katalog &#41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [Dialogfeld "konfigurieren"](../integration-services/service/configure-dialog-box.md)  
  
-   [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog)  
  
### <a name="parameter-values"></a>Parameterwerte  
 Sie können einem Parameter bis zu drei verschiedene Werttypen zuweisen. Wenn eine Paketausführung gestartet wird, wird ein einzelner Wert für den Parameter verwendet, und der Parameter wird in seinen abschließenden Literalwert aufgelöst.  
  
 In der folgenden Tabelle sind die Werttypen aufgeführt.  
  
|Wertname|Beschreibung|Werttyp|  
|----------------|-----------------|-------------------|  
|Ausführungswert|Der Wert, der einer bestimmten Instanz der Paketausführung zugewiesen wird. Diese Zuweisung überschreibt alle anderen Werte, gilt aber nur für eine einzelne Instanz der Paketausführung.|Literal|  
|Serverwert|Der Wert, der dem Parameter innerhalb des Projektbereichs zugewiesen wird, nachdem das Projekt auf dem Integration Services-Server bereitgestellt wurde. Dieser Wert überschreibt den Entwurfsstandard.|Literaler oder Umgebungsvariablenverweis|  
|Entwurfswert|Der Wert, der dem Parameter zugewiesen wird, wenn das Projekt in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]erstellt oder bearbeitet wird. Dieser Wert bleibt im Projekt erhalten.|Literal|  
  
 Sie können mehreren Paketeigenschaften mithilfe eines einzelnen Parameters einen Wert zuweisen. Einer einzelnen Paketeigenschaft kann nur ein Wert aus einem einzelnen Parameter zugewiesen werden.  
  
###  <a name="executions"></a> Ausführungen und Parameterwerte  
 Die *Ausführung* ist ein Objekt, das eine einzelne Instanz der Paketausführung darstellt. Wenn Sie eine Ausführung erstellen, geben Sie alle Details an, die zum Ausführen eines Pakets erforderlich sind, z. B. Ausführungsparameterwerte. Sie können die Parameterwerte vorhandener Ausführungen auch ändern.  
  
 Wenn Sie einen Ausführungsparameterwert explizit festlegen, ist dieser Wert nur auf diese spezielle Instanz der Ausführung anwendbar. Der Ausführungswert wird anstelle eines Serverwerts oder eines Entwurfswerts verwendet. Wenn Sie keinen Ausführungswert explizit festlegen und ein Serverwert angegeben wurde, wird der Serverwert verwendet.  
  
 Wenn ein Parameter entsprechend markiert ist, muss für diesen Parameter ein Serverwert oder ein Ausführungswert angegeben werden. Andernfalls wird das entsprechende Paket nicht ausgeführt. Obwohl der Parameter zur Entwurfszeit über einen Standardwert verfügt, wird er nie verwendet, nachdem das Projekt bereitgestellt wurde.  
  
#### <a name="environment-variables"></a>Umgebungsvariablen  
 Wenn ein Parameter auf eine Umgebungsvariable verweist, wird der Literalwert dieser Variable durch den angegebenen Umgebungsverweis aufgelöst und auf den Parameter angewendet. Der finale Literalparameterwert, der für die Paketausführung verwendet wird, wird als Ausführungsparameterwert bezeichnet. Sie geben den Umgebungsverweis für eine Ausführung im Dialogfeld **Ausführen** an.  
  
 Wenn ein Projektparameter auf eine Umgebungsvariable verweist und der Literalwert in der Variablen bei der Ausführung nicht aufgelöst werden kann, wird der Entwurfswert verwendet. Der Serverwert wird nicht verwendet.  
  
 Um die Umgebungsvariablen anzuzeigen, die Parameterwerten zugewiesen werden, fragen Sie die catalog.object_parameters-Sicht ab. Weitere Informationen finden Sie unter [Catalog. object_parameters &#40; SSISDB-Datenbank &#41; ](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
#### <a name="determining-execution-parameter-values"></a>Bestimmen von Ausführungsparameterwerten  
 Die folgenden Transact-SQL-Sichten und die gespeicherte Prozedur können verwendet werden, um Parameterwerte anzuzeigen und festzulegen.  
  
 [Catalog. execution_parameter_values &#40; SSISDB-Datenbank &#41; ](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)(view)  
 Zeigt die tatsächlichen Parameterwerte an, die von einer bestimmten Ausführung verwendet werden.  
  
 [Catalog. get_parameter_values &#40; SSISDB-Datenbank &#41; ](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (gespeicherte Prozedur)  
 Löst die tatsächlichen Werte für das angegebene Paket und den Umgebungsverweis auf und zeigt diese an.  
  
 [Catalog. object_parameters &#40; SSISDB-Datenbank &#41; ](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (view)  
 Zeigt die Parameter und Eigenschaften für alle Pakete und Projekte im [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Katalog an, einschließlich der Entwurfsstandard- und Serverstandardwerte.  
  
 [Catalog. set_execution_parameter_value &#40; SSISDB-Datenbank &#41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Legt den Wert eines Parameters für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] -Katalog fest.  
  
 Sie können den Parameterwert auch im Dialogfeld **Paket ausführen** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ändern. Weitere Informationen finden Sie unter [Execute Package Dialog Box](../integration-services/packages/run-integration-services-ssis-packages.md#execute_package_dialog).  
  
 Sie können einen Parameterwert auch mit der dtexec-Option **/Parameter** ändern. Weitere Informationen finden Sie unter [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
### <a name="parameter-validation"></a>Parameterüberprüfung  
 Wenn Parameterwerte nicht aufgelöst werden können, schlägt die entsprechende Paketausführung fehl. Zur Fehlervermeidung können Sie Projekte und Pakete im Dialogfeld **Überprüfen** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]überprüfen. Mit der Überprüfung stellen Sie sicher, dass alle Parameter über die notwendigen Werte verfügen oder die notwendigen Werte mit bestimmten Umgebungsverweisen auflösen können. Mit der Überprüfung können auch andere häufig auftretende Paketprobleme überprüft werden.  
  
 Weitere Informationen finden Sie unter [Validate Dialog Box](../integration-services/service/validate-dialog-box.md).  
  
### <a name="parameter-example"></a>Parameterbeispiel  
 In diesem Beispiel wird ein Parameter mit dem Namen **pkgOptions** beschrieben, der für die Angabe von Optionen für das Paket verwendet wird, in dem er sich befindet.  
  
 Während der Entwurfszeit, als der Parameter in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]erstellt wurde, wurde dem Parameter der Standardwert 1 zugewiesen. Dieser Standardwert wird als Entwurfsstandard bezeichnet. Wenn das Projekt im SSISDB-Katalog bereitgestellt wurde und diesem Parameter keine anderen Werte zugewiesen wurden, würde der Paketeigenschaft, die dem **pkgOptions** -Parameter entspricht, während der Paketausführung der Wert 1 zugewiesen werden. Der Entwurfsstandard bleibt während des gesamten Lebenszyklus des Projekts erhalten.  
  
 Während der Vorbereitung einer bestimmten Instanz der Paketausführung wird dem **pkgOptions** -Parameter der Wert 5 zugewiesen. Dieser Wert wird als Ausführungswert bezeichnet, da es für den Parameter nur für diese spezifische Instanz der Ausführung gilt. Wenn die Ausführung startet, wird der dem **pkgOptions** -Parameter entsprechenden Paketeigenschaft der Wert 5 zugewiesen.  
  
## <a name="create-parameters"></a>Create Parameters
Sie verwenden [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , um Projektparameter und Paketparameter zu erstellen. Die folgenden Prozeduren stellen schrittweise Anweisungen zum Erstellen von Paket-/Projektparametern bereit.  
  
> **HINWEIS:** Wenn Sie ein Projekt, das Sie mit einer früheren Version von [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] erstellt haben, in das Projektbereitstellungsmodell konvertieren, können Sie mit dem **Assistent für die Konvertierung von Integration Services-Projekten** Parameter auf Grundlage von Konfigurationen erstellen. Weitere Informationen finden Sie unter [Bereitstellen von Integration Services (SSIS)-Projekten und Paketen](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
### <a name="create-package-parameters"></a>Erstellen Sie Paketparameter  
  
1.  Öffnen Sie das Paket in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], und klicken Sie dann auf die Registerkarte **Parameter** im SSIS-Designer.  
  
     ![Registerkarte "Parameter"-Paket](../integration-services/media/denali-package-parameters.gif "Registerkarte "Parameter"-Paket")  
  
2.  Klicken Sie auf die Schaltfläche **Parameter hinzufügen** auf der Symbolleiste.  
  
     ![Symbolleistenschaltfläche "hinzufügen"](../integration-services/media/denali-parameter-add.gif "hinzufügen (Symbolleistenschaltfläche)")  
  
3.  Geben Sie Werte für die Eigenschaften **Name**, **Datentyp**, **Wert**, **Vertraulich**und **Erforderlich** in der Liste selbst oder im Fenster **Eigenschaften** ein. In der folgenden Tabelle werden diese Eigenschaften beschrieben.  
  
    |Eigenschaft|Description|  
    |--------------|-----------------|  
    |Name|Der Name des Parameters.|  
    |Datentyp|Der Datentyp des Parameters.|  
    |Standardwert|Der Standardwert für den zur Entwurfszeit zugewiesenen Parameter. Dieser wird auch als Entwurfsstandard bezeichnet.|  
    |Vertraulich|Vertrauliche Parameterwerte werden im Katalog verschlüsselt und in Transact-SQL oder SQL Server Management Studio als NULL-Wert angezeigt.|  
    |Required|Dazu muss ein anderer als der Entwurfsstandardwert angegeben werden, bevor das Paket ausgeführt werden kann.|  
    |Description|Die Beschreibung des Parameters für bessere Verwaltbarkeit. Legen Sie im Visual Studio-Eigenschaftenfenster von [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]die Parameterbeschreibung fest, wenn der Parameter im entsprechenden Parameterfenster ausgewählt wurde.|  
  
    > **HINWEIS:** Wenn Sie im Katalog ein Projekt bereitstellen, werden dem Projekt einige weitere Eigenschaften zugeordnet. Um alle Eigenschaften für alle Parameter im Katalog anzuzeigen, verwenden Sie die Sicht [catalog.object_parameters &#40;SSISDB-Datenbank&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
4.  Speichern Sie das Projekt, um Änderungen an Parametern zu speichern. Parameterwerte werden in der Projektdatei gespeichert.  
  
    > **WARNUNG!!** Nehmen Sie Bearbeitungen direkt in der Liste vor, oder verwenden Sie das Fenster **Eigenschaften**, um die Werte von Parametereigenschaften zu ändern. Sie können mit der Symbolleistenschaltfläche **Löschen (X)** einen Parameter löschen. Über die letzte Symbolleistenschaltfläche können Sie einen Wert für einen Parameter angeben, der nur verwendet wird, wenn Sie das Paket in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]ausführen.  
  
    > **HINWEIS:** Wenn Sie die Paketdatei erneut öffnen, ohne das Projekt in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] zu öffnen, ist die Registerkarte **Parameter** leer und deaktiviert.  
  
### <a name="create-project-parameters"></a>Erstellen von Projektparametern  
  
1.  Öffnen Sie das Projekt in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
2.  Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Project.params**, und klicken Sie auf **Öffnen**. Oder doppelklicken auf **Project.params**, um das Projekt zu öffnen.  
  
     ![Projekt Parameterfenster](../integration-services/media/denali-project-parameters.gif "Projekt Parameterfenster")  
  
3.  Klicken Sie auf die Schaltfläche **Parameter hinzufügen** auf der Symbolleiste.  
  
     ![Symbolleistenschaltfläche "hinzufügen"](../integration-services/media/denali-parameter-add.gif "hinzufügen (Symbolleistenschaltfläche)")  
  
4.  Geben Sie Werte für die Eigenschaften **Name**, **Datentyp**, **Wert**, **Vertraulich**und **Erforderlich** ein.  
  
    |Eigenschaft|Description|  
    |--------------|-----------------|  
    |Name|Der Name des Parameters.|  
    |Datentyp|Der Datentyp des Parameters.|  
    |Standardwert|Der Standardwert für den zur Entwurfszeit zugewiesenen Parameter. Dieser wird auch als Entwurfsstandard bezeichnet.|  
    |Vertraulich|Vertrauliche Parameterwerte werden im Katalog verschlüsselt und in Transact-SQL oder SQL Server Management Studio als NULL-Wert angezeigt.|  
    |Required|Dazu muss ein anderer als der Entwurfsstandardwert angegeben werden, bevor das Paket ausgeführt werden kann.|  
    |Description|Die Beschreibung des Parameters für bessere Verwaltbarkeit. Legen Sie im Visual Studio-Eigenschaftenfenster von [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]die Parameterbeschreibung fest, wenn der Parameter im entsprechenden Parameterfenster ausgewählt wurde.|  
  
5.  Speichern Sie das Projekt, um Änderungen an Parametern zu speichern. Parameterwerte werden in Konfigurationen in der Projektdatei gespeichert. Speichern Sie die Projektdatei, um alle Änderungen in den Parameterwerten in einem Commit an den Datenträger zu übergeben.  
  
    > **WARNUNG FEHLERHAFT SIND.** Nehmen Sie Bearbeitungen direkt in der Liste vor, oder verwenden Sie das Fenster **Eigenschaften**, um die Werte von Parametereigenschaften zu ändern. Sie können mit der Symbolleistenschaltfläche **Löschen (X)** einen Parameter löschen. Über die letzte Symbolleistenschaltfläche können Sie das Dialogfeld **Parameterwerte verwalten** öffnen, um einen Wert für einen Parameter anzugeben, der nur verwendet wird, wenn Sie das Paket in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]ausführen.  
    
## <a name="parameterize-dialog-box"></a>Parameterize Dialog Box
Die **parametrisieren** Dialogfeld können Sie einen neuen oder vorhandenen Parameter einer Eigenschaft eines Tasks zuordnen. Sie öffnen das Dialogfeld, indem Sie mit der rechten Maustaste auf einen Task oder die Registerkarte „Ablaufsteuerung“ im [!INCLUDE[ssIS](../includes/ssis-md.md)]-Designer klicken und dann auf **Parametrisieren** klicken. Die folgende Liste beschreibt Benutzeroberflächenelemente im Dialogfeld. Weitere Informationen zu Parametern finden Sie unter [Integration Services-Parameter (SSIS)](https://msdn.microsoft.com/library/hh213214.aspx).
  
### <a name="options"></a>enthalten  
 **Eigenschaft**  
 Wählen Sie die Eigenschaft der Aufgabe aus, der Sie einem Parameter zuordnen möchten. Diese Liste wird mit allen Eigenschaften aufgefüllt, die parametrisiert werden können.  
  
 **Verwenden Sie vorhandene parameter**  
 Aktivieren Sie diese Option, um die Eigenschaft der Aufgaben einem vorhandenen Parameter zuzuordnen und dann den Parameter aus Dropdownliste auszuwählen.  
  
 **Parameter nicht verwenden**  
 Wählen Sie diese Option aus, um einen Verweist auf einen Parameter zu entfernen. Der Parameter wurde nicht gelöscht.  
  
 **Neuen Parameter erstellen**  
 Aktivieren Sie diese Option, um einen neuen Parameter zu erstellen, den Sie der Eigenschaft der Aufgabe zuordnen möchten.  
  
 **Name**  
 Geben Sie den Namen des Parameters an, den Sie erstellen möchten.  
  
 **Description**  
 Geben Sie die Beschreibung für den Parameter an.  
  
 **Wert**  
 Geben Sie den Standardwert für den Parameter an. Dies wird auch als der Entwurfsstandard bezeichnet, der später zur Bereitstellungszeit überschrieben werden kann.  
  
 **Scope**  
 Geben Sie den Bereich des Parameters an, indem Sie die Option **Projekt** oder die Option **Paket** aktivieren. Projektparameter werden verwendet, um jegliche externen Eingaben bereitzustellen, die das Projekt für ein oder mehrere Pakete im Projekt empfängt. Mit Paketparametern können Sie die Paketausführung ändern, ohne das Paket bearbeiten und erneut bereitstellen zu müssen.  
  
 **Vertrauliche**  
 Geben Sie an, ob der Parameter vertraulich ist, indem Sie das Kontrollkästchen aktivieren oder deaktivieren. Vertrauliche Parameterwerte werden im Katalog verschlüsselt und in Transact-SQL oder SQL Server Management Studio als NULL-Wert angezeigt.  
  
 **Erforderlich**  
 Geben Sie an, ob für den Parameter ein anderer als der Entwurfsstandardwert angegeben werden muss, bevor das Paket ausgeführt werden kann.  
 
## <a name="set-parameter-values-after-the-project-is-deployed"></a>Festlegen von Parameterwerten nach der Bereitstellung des Projekts
Mit dem Bereitstellungs-Assistenten können Sie Serverstandardparameterwerte festlegen, wenn Sie das Projekt im Katalog bereitstellen. Nachdem das Projekt dem Katalog hinzugefügt worden ist, Sie können Serverstandardwerte mithilfe von SQL Server Management Studio (SSMS)-Objekt-Explorer oder Transact-SQL festlegen.  
  
### <a name="set-server-defaults-with-ssms-object-explorer"></a>Festlegen von Serverstandards mit SSMS-Objekt-Explorer  
  
1.  Wählen Sie das Projekt unter dem Knoten **Integration Services** aus, und klicken Sie mit der rechten Maustaste darauf.  
  
2.  Klicken Sie auf **Eigenschaften** , um das Dialogfeld **Projekteigenschaften** zu öffnen.  
  
3.  Öffnen Sie die Parameterseite, indem Sie unter **Seite auswählen** auf **Parameter**klicken.  
  
4.  Wählen Sie in der Liste **Parameter** den gewünschten Parameter aus. Hinweis: Anhand der Spalte **Container** können Projektparameter leichter von Paketparametern unterschieden werden.  
  
5.  Geben Sie in der Spalte **Wert** den gewünschten Serverstandardparameterwert an.  

### <a name="set-server-defaults-with-transact-sql"></a>Festlegen von Serverstandards mit Transact-SQL  
 Verwenden Sie zum Festlegen von Serverstandardwerten mit Transact-SQL die gespeicherte Prozedur [catalog.set_object_parameter_value &#40;SSISDB-Datenbank&#41;](../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md). Verwenden Sie zum Anzeigen der aktuellen Serverstandards die Abfrage [catalog.object_parameters &#40;SSISDB-Datenbank&#41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md). Verwenden Sie zum Löschen von Serverstandardwerten die gespeicherte Prozedur [catalog.clear_object_parameter_value &#40;SSISDB-Datenbank&#41;](../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md).  
  
## <a name="related-content"></a>Verwandte Inhalte  
 Blogeintrag [SSIS-Quicktipp: Erforderliche Parameter](http://go.microsoft.com/fwlink/?LinkId=239781)auf mattmasson.com.  
  
  

