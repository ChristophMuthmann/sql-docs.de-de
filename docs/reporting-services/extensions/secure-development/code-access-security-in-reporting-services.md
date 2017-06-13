---
title: Codezugriffssicherheit in Reporting Services | Microsoft Docs
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
- code groups [Reporting Services]
- code access security [Reporting Services]
- permission sets [Reporting Services]
- evidence [Reporting Services]
- code access security [Reporting Services], about code access security
- named permission sets [Reporting Services]
ms.assetid: 97480368-1fc3-4c32-b1b0-63edfb54e472
caps.latest.revision: 30
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: bbb9ee191cf97b7b61e99b049faa0753034e9b9e
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="code-access-security-in-reporting-services"></a>Codezugriffssicherheit in Reporting Services
  Die Codezugriffssicherheit dreht sich um diese Kernbegriffe: Beweise, Codegruppen und benannte Berechtigungssätze. In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] haben die Komponenten Berichts-Manager, Berichts-Designer und Berichtsserver jeweils eine Richtliniendatei, die die Codezugriffssicherheit für benutzerdefinierte Assemblys sowie für die Daten-, Übermittlungs-, Rendering- und Sicherheitserweiterung konfiguriert. Die folgenden Abschnitte enthalten eine Übersicht über die Codezugriffssicherheit. Ausführlichere Informationen zu den Themen in diesem Abschnitt finden Sie unter "Sicherheitsrichtlinienmodell" in der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK-Dokumentation.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verwendet Codezugriffssicherheit, da ein großer Unterschied zwischen einer typischen [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]-Anwendung und dem Berichtsserver besteht, obwohl der Berichtsserver auf [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]-Technologie beruht. Eine typische [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)]-Anwendung führt keinen Benutzercode aus. Im Gegensatz dazu [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verwendet eine offene und erweiterbare Architektur, die Benutzern ermöglicht, Programmieren Berichtsdefinitionsdateien, die mithilfe der **Code** Element der Berichtsdefinitionssprache und um spezielle Funktionen in einer benutzerdefinierten Assembly für die Verwendung in Berichten zu entwickeln. Weiterhin können Entwickler leistungsstarke Erweiterungen entwerfen und bereitstellen, die die Funktionen des Berichtsservers verbessern. Diese Leistungsstärke und Flexibilität bringt auch die Notwendigkeit mit sich, so viel Schutz und Sicherheit wie möglich zu bieten.  
  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Entwickler können eine beliebige [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]-Assembly in ihren Berichten verwenden und alle Funktionen der Assemblys abrufen, die für den globalen Assemblycache bereitgestellt wurden. Der Berichtsserver kann lediglich steuern, welche Berechtigungen für Berichtsausdrücke und geladene benutzerdefinierte Assemblys gelten. In [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], benutzerdefinierte Assemblys **Execute**-standardmäßig nur Berechtigungen.  
  
## <a name="evidence"></a>Beweise  
 Beweise sind Informationen, die die Common Language Runtime (CLR) zum Ermitteln einer Sicherheitsrichtlinie für Codeassemblys verwendet. Beweise geben der Laufzeit an, dass der Code ein bestimmtes Merkmal besitzt. Zu üblichen Formen von Beweisen zählen digitale Signaturen und der Speicherort einer Assembly. Beweise können auch benutzerdefiniert sein, um andere Informationen darzustellen, die für die Anwendung sinnvoll sind.  
  
 Sowohl Assemblys als auch Anwendungsdomänen werden Berechtigungen auf der Grundlage von Beweisen gewährt. Der Speicherort einer Assembly, auf die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] versucht zuzugreifen, ist eine übliche Form des Beweises für Assemblys mit schwachen Namen. Sie wird auch als URL-Beweis bezeichnet. Der URL-Beweis für eine benutzerdefinierte Datenverarbeitungserweiterung, die für einen Berichtsserver bereitgestellt wird, kann folgendermaßen lauten: "C:\Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll". Der starke Name oder die digitale Signatur einer Assembly ist eine andere übliche Form für einen Beweis. In diesem Fall ist der Beweis der öffentliche Schlüssel für eine Assembly.  
  
## <a name="code-groups"></a>Codegruppen  
 Eine Codegruppe ist eine logische Gruppierung von Code mit einer angegebenen Bedingung für die Mitgliedschaft. Jeglicher Code, der die Mitgliedschaftsbedingung erfüllt, ist in der Gruppe enthalten. Administratoren konfigurieren eine Sicherheitsrichtlinie durch Verwaltung von Codegruppen und ihren zugeordneten Berechtigungssätzen.  
  
 Eine Mitgliedschaftsbedingung für eine Codegruppe basiert auf Beweisen. Zum Beispiel basiert eine URL-Mitgliedschaft für eine Codegruppe auf URL-Beweisen. Die Common Language Runtime (CLR) verwendet beschreibende Merkmale, wie z. B. URL-Beweise, mit denen Code beschrieben wird und ermittelt wird, ob die Bedingungen einer Gruppenmitgliedschaft erfüllt werden. Die Mitgliedschaftsbedingung für eine Codegruppe ist z. B. "Code in der Assembly C:\Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll". Die Laufzeit untersucht die Beweise, um zu ermitteln, ob der Code aus diesem Speicherort stammt. Ein Beispiel für einen Konfigurationseintrag für diesen Typ der Codegruppe könnte wie folgt aussehen:  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="FullTrust"  
   Name="MyCodeGroup"  
   Description="Code group for my data processing extension">  
      <IMembershipCondition class="UrlMembershipCondition"  
         version="1"  
         Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\Microsoft.Samples.ReportingServices.FsiDataExtension.dll"  
       />  
</CodeGroup>  
```  
  
 Sie sollten mit Ihrem Systemadministrator oder Experten für die Anwendungsbereitstellung zusammenarbeiten, um den Typ der Codezugriffssicherheit und Codegruppen zu ermitteln, die für Ihre benutzerdefinierten Assemblys oder [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Erweiterungen erforderlich sind.  
  
## <a name="named-permission-sets"></a>Benannte Berechtigungssätze  
 Ein benannter Berechtigungssatz ist ein Satz von Berechtigungen, den Administratoren einer Codegruppe zuordnen können. Die meisten benannten Berechtigungssätze bestehen aus mindestens einer Berechtigung, einem Namen und einer Beschreibung für den Berechtigungssatz. Administratoren können benannte Berechtigungssätze verwenden, um die Sicherheitsrichtlinien für Codegruppen zu erstellen oder zu ändern. Es ist möglich, einen benannten Berechtigungssatz mehreren Codegruppen zuzuordnen. Die CLR stellt integrierte benannte Berechtigungssätze bereit; zu diesen zählen **nichts**, **Ausführung**, **Internet**, **LocalIntranet**, **alles**, und **FullTrust**.  
  
> [!NOTE]  
>  Benutzerdefinierte Erweiterungen für Daten, Übermittlung, Rendering und Sicherheit im [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] muss ausgeführt werden die **FullTrust** Berechtigungssatz. Arbeiten Sie mit Ihrem Systemadministrator zusammen, um die geeigneten Codegruppen- und Mitgliedschaftsbedingungen für Ihre [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Erweiterungen hinzuzufügen.  
  
 Sie können Ihre eigenen benutzerdefinierten Ebenen von Berechtigungen benutzerdefinierten Assemblys zuordnen, die Sie mit Berichten verwenden. Wenn Sie z. B. möchten, dass eine Assembly auf eine bestimmte Datei zugreift, können Sie einen neuen benannten Berechtigungssatz mit einem bestimmten Datei-E/A-Zugriff erstellen und den Berechtigungssatz dann Ihrer Codegruppe zuordnen. Der folgende Berechtigungssatz gewährt schreibgeschützten Zugriff auf die Datei MyFile.xml:  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="MyNewFilePermissionSet"  
   Description="A special permission set that grants read access to my file.">  
    <IPermission class="FileIOPermission"  
       version="1"  
       Read="C:\MyFile.xml"/>  
    <IPermission class="SecurityPermission"  
       version="1"  
       Flags="Assertion, Execution"/>  
</PermissionSet>  
```  
  
 Eine Codegruppe, der Sie diesen Berechtigungssatz zuordnen, könnte wie folgt aussehen:  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="MyNewFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\MyCustomAssembly.dll"/>  
</CodeGroup>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sichere Entwicklung &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
