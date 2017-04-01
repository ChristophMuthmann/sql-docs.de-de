---
title: "Integration Services (SSIS)-Paket und Projektparameter | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.designer.parameter.f1"
  - "sql13.dts.designer.paramterwindow.f1"
ms.assetid: 9ed9ca8e-8b1e-48d9-907d-285516d6562b
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 22
---
# Integration Services (SSIS)-Paket und Projektparameter
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)-Parameter können Sie Eigenschaften in Paketen zur Zeit der paketausführung Werte zuweisen. Sie können *Projektparameter* auf Projektebene und *Paketparameter* auf Paketebene erstellen. Projektparameter werden verwendet, um jegliche externen Eingaben bereitzustellen, die das Projekt für ein oder mehrere Pakete im Projekt empfängt. Mit Paketparametern können Sie die Paketausführung ändern, ohne das Paket bearbeiten und erneut bereitstellen zu müssen.  
  
 In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] können Sie im Fenster **Project.params** Projektparameter erstellen, ändern oder löschen. Sie erstellen, ändern und löschen Paketparameter mit der Registerkarte **Parameter** im [!INCLUDE[ssIS](../includes/ssis-md.md)] -Designer. Im Dialogfeld **Parametrisieren** können Sie einen neuen oder vorhandenen Parameter einer Taskeigenschaft zuordnen. Weitere Informationen zum Verwenden des Fensters **Project.params** und der Registerkarte **Parameter** finden Sie unter [Create Parameters](../Topic/Create%20Parameters.md). Weitere Informationen zum Dialogfeld **Parametrisieren** finden Sie unter [Parameterize Dialog Box](../Topic/Parameterize%20Dialog%20Box.md).  
  
## Parameter und Paketbereitstellungsmodell  
 Im Allgemeinen sollten Sie beim Bereitstellen eines Pakets mit dem Paketbereitstellungsmodell Konfigurationen anstelle von Parametern verwenden.  
  
 Wenn Sie mithilfe des Paketbereitstellungsmodells ein Paket bereitstellen, das Parameter enthält, und dann das Paket ausführen, werden die Parameter während der Ausführung nicht aufgerufen. Wenn das Paket Paketparameter und Ausdrücke innerhalb des Pakets enthält, verwenden Sie die Parameter, die resultierenden Werte werden zur Laufzeit übernommen. Wenn das Paket Projektparameter enthält, tritt bei der Paketausführung möglicherweise ein Fehler auf.  
  
## Parameter und Projektbereitstellungsmodell  
 Wenn Sie ein Projekt mit dem Server Integration Services (SSIS) bereitstellen, verwenden Sie Sichten, gespeicherte Prozeduren und [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Benutzeroberfläche zum Verwalten von Projekt- und Paketparametern. Weitere Informationen finden Sie in den nachfolgenden Themen.  
  
-   [Ansichten & #40; Integration Services-Katalog & #41;](../integration-services/system-views/views-integration-services-catalog.md)  
  
-   [Gespeicherte Prozeduren und #40; Integration Services-Katalog & #41;](../integration-services/system-stored-procedures/stored-procedures-integration-services-catalog.md)  
  
-   [Konfigurieren (Dialogfeld)](../integration-services/service/configure-dialog-box.md)  
  
-   [Paket ausführen (Dialogfeld)](../integration-services/packages/execute-package-dialog-box.md)  
  
### Parameterwerte  
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
  
#### Umgebungsvariablen  
 Wenn ein Parameter auf eine Umgebungsvariable verweist, wird der Literalwert dieser Variable durch den angegebenen Umgebungsverweis aufgelöst und auf den Parameter angewendet. Der finale Literalparameterwert, der für die Paketausführung verwendet wird, wird als Ausführungsparameterwert bezeichnet. Sie geben den Umgebungsverweis für eine Ausführung im Dialogfeld **Ausführen** an.  
  
 Wenn ein Projektparameter auf eine Umgebungsvariable verweist und der Literalwert in der Variablen bei der Ausführung nicht aufgelöst werden kann, wird der Entwurfswert verwendet. Der Serverwert wird nicht verwendet.  
  
 Um die Umgebungsvariablen anzuzeigen, die Parameterwerten zugewiesen werden, fragen Sie die catalog.object_parameters-Sicht ab. Weitere Informationen finden Sie unter [object_parameters & #40; SSISDB-Datenbank & #41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md).  
  
#### Bestimmen von Ausführungsparameterwerten  
 Die folgenden Transact-SQL-Sichten und die gespeicherte Prozedur können verwendet werden, um Parameterwerte anzuzeigen und festzulegen.  
  
 [Catalog. execution_parameter_values & #40; SSISDB-Datenbank & #41;](../integration-services/system-views/catalog-execution-parameter-values-ssisdb-database.md)(Ansicht)  
 Zeigt die tatsächlichen Parameterwerte an, die von einer bestimmten Ausführung verwendet werden.  
  
 [Catalog. get_parameter_values & #40; SSISDB-Datenbank & #41;](../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md) (gespeicherte Prozedur)  
 Löst die tatsächlichen Werte für das angegebene Paket und den Umgebungsverweis auf und zeigt diese an.  
  
 [object_parameters & #40; SSISDB-Datenbank & #41;](../integration-services/system-views/catalog-object-parameters-ssisdb-database.md) (Ansicht)  
 Zeigt die Parameter und Eigenschaften für alle Pakete und Projekte im [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalog an, einschließlich der Entwurfsstandard- und Serverstandardwerte.  
  
 [set_execution_parameter_value & #40; SSISDB-Datenbank & #41;](../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Legt den Wert eines Parameters für eine Instanz der Ausführung im [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalog fest.  
  
 Sie können den Parameterwert auch im Dialogfeld **Paket ausführen** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ändern. Weitere Informationen finden Sie unter [Execute Package Dialog Box](../integration-services/packages/execute-package-dialog-box.md).  
  
 Sie können auch die Dtexec **/Parameter** Option, um einen Parameterwert ändern. Weitere Informationen finden Sie unter [dtexec Utility](../integration-services/packages/dtexec-utility.md).  
  
### Parameterüberprüfung  
 Wenn Parameterwerte nicht aufgelöst werden können, schlägt die entsprechende Paketausführung fehl. Zur Fehlervermeidung können Sie Projekte und Pakete im Dialogfeld **Überprüfen** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]überprüfen. Mit der Überprüfung stellen Sie sicher, dass alle Parameter über die notwendigen Werte verfügen oder die notwendigen Werte mit bestimmten Umgebungsverweisen auflösen können. Mit der Überprüfung können auch andere häufig auftretende Paketprobleme überprüft werden.  
  
 Weitere Informationen finden Sie unter [Validate Dialog Box](../integration-services/service/validate-dialog-box.md).  
  
### Parameterbeispiel  
 In diesem Beispiel wird ein Parameter mit dem Namen **pkgOptions** beschrieben, der für die Angabe von Optionen für das Paket verwendet wird, in dem er sich befindet.  
  
 Während der Entwurfszeit, als der Parameter in [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]erstellt wurde, wurde dem Parameter der Standardwert 1 zugewiesen. Dieser Standardwert wird als Entwurfsstandard bezeichnet. Wenn das Projekt im SSISDB-Katalog bereitgestellt wurde und diesem Parameter keine anderen Werte zugewiesen wurden, würde der Paketeigenschaft, die dem **pkgOptions** -Parameter entspricht, während der Paketausführung der Wert 1 zugewiesen werden. Der Entwurfsstandard bleibt während des gesamten Lebenszyklus des Projekts erhalten.  
  
 Während der Vorbereitung einer bestimmten Instanz der Paketausführung wird dem **pkgOptions** -Parameter der Wert 5 zugewiesen. Dieser Wert wird als Ausführungswert bezeichnet, da es für den Parameter nur für diese spezifische Instanz der Ausführung gilt. Wenn die Ausführung startet, wird der dem **pkgOptions** -Parameter entsprechenden Paketeigenschaft der Wert 5 zugewiesen.  
  
## Verwandte Aufgaben  
 [Erstellen von Parametern](../Topic/Create%20Parameters.md)  
  
 [Festlegen von Parameterwerten nach der Bereitstellung des Projekts](../Topic/Set%20Parameter%20Values%20After%20the%20Project%20Is%20Deployed.md)  
  
## Verwandte Inhalte  
 Blogeintrag [SSIS-Quicktipp: Erforderliche Parameter](http://go.microsoft.com/fwlink/?LinkId=239781)auf mattmasson.com.  
  
  