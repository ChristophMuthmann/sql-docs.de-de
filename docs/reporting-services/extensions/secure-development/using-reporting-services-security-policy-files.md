---
title: Verwenden von Reporting Services-Sicherheitsrichtliniendateien | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- CodeGroup elements
- configuration files [Reporting Services]
- code access security [Reporting Services], security policies
- security policies [Reporting Services]
- security configuration files [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: 2280fff6-3de7-44b1-87da-5db0ec975928
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 490f32a022606157376f7c8402d11cd8f027bc04
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

---
# <a name="using-reporting-services-security-policy-files"></a>Verwenden von Reporting Services-Sicherheitsrichtliniendateien
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] speichert Informationen zu Komponentensicherheitsrichtlinien in drei Konfigurationsdateien, die bei der Installation in das Dateisystem kopiert werden. Diese Konfigurationsdateien können eine Kombination aus nur intern verwendeten und benutzerdefinierten Sicherheitsrichtlinien für Codeassemblys in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] enthalten. Die drei Konfigurationsdateien entsprechen drei sicherungsfähigen Komponenten in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]: Berichtsserver und Windows-Dienst, Berichts-Manager-Webanwendung und Vorschaufenster des Berichts-Designers.  
  
> [!NOTE]  
>  Es stehen zwei Vorschaumodi für den Berichts-Designer: Registerkarte "Vorschau" und das Popup-Vorschaufenster, das geöffnet wird, wenn der Start Ihres Berichtsprojekts im **DebugLocal** Modus. Die **Vorschau** Registerkarte "ist keine sicherungsfähige Komponente und gilt nicht sicherheitsrichtlinieneinstellungen. Im Vorschaufenster sollen die Berichtsserverfunktionen simuliert werden. Es enthält daher eine Richtlinienkonfigurationsdatei, die von Ihnen oder einem Administrator verändert werden muss, um benutzerdefinierte Assemblys und benutzerdefinierte Erweiterungen im Berichts-Designer zu verwenden.  
  
 Die Sicherheitsrichtlinien-Konfigurationsdateien enthalten Informationen zu Sicherheitsklassen, einige benannte Standardberechtigungssätze und die Codegruppen für Assemblys in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Die Richtlinien-Konfigurationsdateien von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] weisen Ähnlichkeiten mit der Security.config-Datei auf, in der die Codegruppenhierarchie und die Berechtigungssätze für Richtlinien auf Computer- und Unternehmensebene in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] festgelegt werden. Der Speicherort dieser Datei ist C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\CONFIG\security.config.  
  
## <a name="policy-files-in-reporting-services"></a>Richtliniendateien in Reporting Services  
 In der nachstehenden Tabelle werden die Richtlinienkonfigurationsdateien in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], ihre Speicherorte (bei einer Standardinstallation) und die entsprechenden Funktionen aufgelistet.  
  
|Dateiname|Speicherort (Standardinstallation)|Description|  
|---------------|---------------------------------------|-----------------|  
|rssrvpolicy.config|C:\Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer|Die Berichtsserverrichtlinien-Konfigurationsdatei. Diese Sicherheitsrichtlinien wirken sich vorwiegend auf Berichtsausdrücke und benutzerdefinierte Assemblys aus, nachdem ein Bericht für einen Berichtsserver bereitgestellt wurde. Diese Richtliniendatei beeinflusst auch benutzerdefinierte Daten, Übermittlung, Rendering und Sicherheitserweiterungen, die für den Berichtsserver bereitgestellt wurden.|  
|rsmgrpolicy.config|C:\Programme\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager|Richtlinienkonfigurationsdatei des Berichts-Managers. Diese Sicherheitsrichtlinien wirken sich auf alle Assemblys aus, die eine Erweiterung für den Berichts-Manager darstellen, wie zum Beispiel Abonnementbenutzeroberflächen-Erweiterungen für benutzerdefinierte Übermittlung.|  
|rspreviewpolicy.config|C:\Programme\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies|Der Berichts-Designer enthält eine eigenständige Vorschaurichtlinien-Konfigurationsdatei. Diese Sicherheitsrichtlinien wirken sich auf Berichtsausdrücke und benutzerdefinierte Assemblys aus, die während der Vorschau und der Entwicklung in Berichten verwendet werden. Diese Richtlinien beeinflussen auch benutzerdefinierte Erweiterungen, z. B. Datenverarbeitungserweiterungen, die für den Berichts-Designer bereitgestellt werden.|  
  
## <a name="modifying-configuration-files"></a>Ändern der Konfigurationsdateien  
 Konfigurationseinstellungen werden als XML-Elemente oder -Attribute angegeben. Wenn Sie sich mit XML und Konfigurationsdateien auskennen, können Sie mit einem Text- oder Code-Editor benutzerdefinierbare Einstellungen ändern. Sicherheitskonfigurationsdateien enthalten Informationen zur Codegruppenhierarchie und zu Berechtigungssätzen, die in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] einer Richtlinienebene zugeordnet sind. Es wird empfohlen, mithilfe des .NET Framework Configuration Utility (Mscorcfg.msc) oder des Sicherheitsrichtlinienhilfsprogramms für den Codezugriff (Caspol.exe) die Sicherheitsrichtlinie in der Security.config-Datei zuerst dahingehend zu ändern, dass Richtlinienänderungen gültigen XML-Konfigurationselementen für Richtliniendateien entsprechen. Anschließend können Sie die neuen Codegruppen und Berechtigungssätze aus Security.config ausschneiden und in die Richtliniendatei für die Komponente kopieren, der Sie Codeberechtigungen hinzufügen.  
  
> [!IMPORTANT]  
>  Erstellen Sie vor der Durchführung von Änderungen eine Sicherungskopie Ihrer Richtlinienkonfigurationsdateien.  
  
 Mit diesem Ansatz können Sie zwei Ziele verfolgen. Erstens: Sie können ein visuelles Tool zur Erstellung Ihrer Codegruppen und Berechtigungssätze für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] verwenden. Dies ist wesentlich einfacher als das Neuschreiben von XML-Konfigurationselementen. Zweitens wird sichergestellt, dass die Sicherheitsrichtlinien-Konfigurationsdateien nicht mit fehlerhaften XML-Elementen und Attributen beschädigt werden. Weitere Informationen über das Code Access Security Policy Utility entnehmen Sie dem Artikel zur Verwendung von Reporting Services-Sicherheitsrichtliniendateien auf MSDN.  
  
 Vor dem Ändern von Richtlinienkonfigurationsdateien empfiehlt es sich, alle in diesem Abschnitt und unter verwandten Themen vorhandenen Informationen zu lesen. Eine Veränderung der Richtlinienkonfiguration von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] kann sich erheblich auf die Sicherheit bei der Ausführung von externen Codemodulen durch [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Komponenten auswirken.  
  
## <a name="placement-of-codegroup-elements-for-extensions"></a>Platzierung von CodeGroup-Elementen für Erweiterungen  
 Die Platzierung von CodeGroup-Elementen in einer Sicherheitsrichtliniendatei ist wichtig. Für von Ihnen entwickelte Erweiterungen und benutzerdefinierte Assemblys sollten Sie nach Möglichkeit Ihre benutzerdefinierten Codegruppen direkt unter dem vorhandenen Eintrag für die URL-Mitgliedschaft "$CodeGen$/*" platzieren, wie im Folgenden angegeben:  
  
```  
<CodeGroup  
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust">  
    <IMembershipCondition   
        class="UrlMembershipCondition"  
        version="1"  
        Url="$CodeGen$/*"  
    />  
</CodeGroup>  
<CodeGroup   
    class="UnionCodeGroup"  
    version="1"  
    PermissionSetName="FullTrust"  
    Name="MyCustomCodeGroup"  
    Description="Code group for my custom extension">  
        <IMembershipCondition class="UrlMembershipCondition"  
        version="1"  
        Url="C:\Program Files\Microsoft SQL Server\MSSQL\Reporting Services\ReportServer\bin\MyAssembly.dll"  
        />  
</CodeGroup>  
```  
  
 Zusätzliche Codegruppen können nacheinander hinzugefügt werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Understanding Security Policies (Grundlegendes zu Sicherheitsrichtlinien)](../../../reporting-services/extensions/secure-development/understanding-security-policies.md)  
  
  
