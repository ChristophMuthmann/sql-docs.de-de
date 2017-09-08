---
title: "Vorgehensweise: Bereitstellen eine Datenverarbeitungserweiterung für Berichts-Designer | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- assemblies [Reporting Services], data processing extension deployments
ms.assetid: 3614e601-004e-4a16-8388-836ffd67e9dd
caps.latest.revision: 41
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e5e309ee7092bdc64efa89fa27579e9e8944da14
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="deploying-a-data-processing-extension-to-report-designer"></a>Deploying a Data Processing Extension um Designer zu melden.
  Beim Entwerfen von Berichten verwendet der Berichts-Designer Datenverarbeitungserweiterungen zum Abruf und zur Verarbeitung von Daten. Sie sollten Ihre Assembly für Datenverarbeitungserweiterungen auf dem Berichts-Designer als private Assembly bereitstellen. Sie müssen auch einen Eintrag in der Konfigurationsdatei des Berichts-Designers RSReportDesigner.config vornehmen.  
  
#### <a name="to-deploy-a-data-processing-extension-assembly"></a>So stellen Sie eine Assembly für Datenverarbeitungserweiterungen bereit  
  
1.  Kopieren Sie die Assembly aus dem Bereitstellungsverzeichnis in das Verzeichnis „Berichts-Designer“. Das Standardverzeichnis für den Berichts-Designer ist C:\Programme\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
2.  Nachdem die Assemblydatei kopiert wurde, öffnen Sie die Datei RSReportDesigner.config. Die Datei RSReportDesigner.config befindet sich auch im Verzeichnis „Berichts-Designer“. Sie müssen einen Eintrag in der Konfigurationsdatei für die Datei Ihrer Datenverarbeitungserweiterungsassembly vornehmen. Sie können die Konfigurationsdatei mit öffnen [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] oder mit einem einfachen Text-Editor, z. B. Notepad.  
  
3.  Suchen Sie das **Data** -Element in der Datei RSReportDesigner.config. In folgendem Verzeichnis muss ein Eintrag für Ihre neu erstellte Datenverarbeitungserweiterung erstellt werden:  
  
    ```  
    <Extensions>  
       <Data>  
          <Your extension configuration information goes here>  
       </Data>  
    </Extensions>  
    ```  
  
4.  Fügen Sie einen Eintrag für Ihre datenverarbeitungserweiterung enthält ein **Erweiterung** Element mit Werten für die **Namen**, **Typ**, und **Visible** Attribute. Der Eintrag könnte folgendermaßen aussehen:  
  
    ```  
    <Extension Name="ExtensionName" Type="CompanyName.ExtensionName.MyConnectionClass, AssemblyName" />  
    ```  
  
     Der Wert für **Namen** ist der eindeutige Name der datenverarbeitungserweiterung. Der Wert für **Typ** ist eine durch Trennzeichen getrennte Liste, die einen Eintrag für den vollqualifizierten Namespace der Klasse enthält, implementiert die <xref:Microsoft.ReportingServices.Interfaces.IExtension> und <xref:Microsoft.ReportingServices.DataProcessing.IDbConnection> Schnittstellen, gefolgt vom Namen Assembly (ohne die Dateierweiterung .dll). Standardmäßig sind Datenverarbeitungserweiterungen sichtbar. Eine Erweiterung in Benutzeroberflächen wie dem Berichts-Designer auszublenden Hinzufügen einer **sichtbar** -Attribut auf die **Erweiterung** Element, und legen Sie dafür **"false"**.  
  
5.  Schließlich fügen Sie eine Codegruppe für die benutzerdefinierte Assembly, die gewährt **FullTrust** Berechtigung für die Erweiterung. Hierzu fügen Sie die Codegruppe zur Datei rspreviewpolicy.config hinzu, die sich standardmäßig im Verzeichnis C:\Programme\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies befindet. Die Codegruppe kann folgendermaßen aussehen:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="MyExtensionCodeGroup"  
       Description="Code group for my data processing extension">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url="C:\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\MyExtensionAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 Die URL-Mitgliedschaft ist eine der vielen Mitgliedschaftsbedingungen, die Sie für die Datenverarbeitungserweiterung auswählen können. Weitere Informationen zur Codezugriffssicherheit in [!INCLUDE[ssRSversion2005](../../../includes/ssrsversion2005-md.md)], finden Sie unter [sichere Entwicklung &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
## <a name="generic-query-designer"></a>Standardabfrage-Designer  
 Der Berichts-Designer enthält einen Standardabfrage-Designer, den Sie zusammen mit den benutzerdefinierten Datenverarbeitungserweiterungen verwenden können. Dieser Designer besteht aus zwei Bereichen: dem Abfragebereich und dem Ergebnisbereich. Sie können den Standard-Designer verwenden, um Abfragen zu schreiben, die nicht von der grafischen Oberfläche unterstützt werden. Im Gegensatz zum grafischen Abfrage-Designer wird die Abfragesyntax vom Standardabfrage-Designer nicht überprüft und die Abfrage nicht umstrukturiert.  
  
#### <a name="to-enable-the-generic-query-designer-for-a-custom-extension"></a>So aktivieren Sie den Standardabfrage-Designer für eine benutzerdefinierte Erweiterung  
  
-   Fügen Sie den folgenden Eintrag zur Datei RSReportDesigner.config unter der **Designer** Element, und Ersetzen Sie dabei die **Name** Attribut mit dem Namen, den Sie in vorhergehenden Einträgen angegeben.  
  
    ```  
    <Extension Name="ExtensionName" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
## <a name="verifying-the-deployment"></a>Überprüfen der Bereitstellung  
 Sie können die Bereitstellung erst überprüfen, wenn Sie alle Instanzen von [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] auf Ihrem lokalen Computer geschlossen haben. Wenn Sie alle aktuellen Sitzungen beendet haben, können Sie überprüfen, ob die Datenverarbeitungserweiterung erfolgreich für den Berichts-Designer bereitgestellt wurde, indem Sie in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] ein neues Berichtsprojekt erstellen. Die Erweiterung sollte beim Erstellen eines neuen Datasets für den Bericht in der Liste der verfügbaren Datenquellentypen aufgeführt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Deploying a Data Processing Extension](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Data Processing Extension](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
