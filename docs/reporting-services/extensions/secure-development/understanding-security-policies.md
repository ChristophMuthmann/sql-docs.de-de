---
title: Grundlegendes zu Sicherheitsrichtlinien | Microsoft Docs
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
- code access security [Reporting Services], security policies
- Execution permission set
- custom assemblies [Reporting Services], security
- permission sets [Reporting Services]
- expressions [Reporting Services], security
- evidence [Reporting Services]
- FullTrust permission set
- security policies [Reporting Services]
- named permission sets [Reporting Services]
ms.assetid: a9bf043a-139a-4929-9a58-244815323df0
caps.latest.revision: 32
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4cb028a3034ddd4dbee5ee3d1b10f696bbe995f3
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="understanding-security-policies"></a>Grundlegendes zu Sicherheitsrichtlinien
  Jeder Code, der von einem Berichtsserver ausgeführt wird, muss Teil einer bestimmten Codezugriff-Sicherheitsrichtlinie sein. Diese Sicherheitsrichtlinien bestehen aus Codegruppen, die einem Satz von benannten Berechtigungen Beweise zuordnen. Häufig sind Codegruppen einem benannten Berechtigungssatz zugeordnet, der die zulässigen Berechtigungen für Code in dieser Gruppe angibt. Die Laufzeit bestimmt anhand von Beweisen, die von einem vertrauenswürdigen Host oder dem Ladeprogramm bereitgestellt werden, zu welchen Codegruppen der Code gehört und welche Berechtigungen ihm daher zuzuweisen sind. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]dieser Sicherheitsrichtlinien-Architektur unterliegen gemäß der [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] common Language Runtime (CLR). In den nachfolgenden Abschnitten werden die verschiedenen Codetypen in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] sowie die damit verknüpften Richtlinienregeln aufgeführt.  
  
## <a name="report-server-assemblies"></a>Berichtsserverassemblys  
 Berichtsserverassemblys sind Assemblys mit Code, der zu [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] gehört. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] wurde mit verwalteten Codeassemblys geschrieben. Alle diese Assemblys verfügen über starke Namen (sind digital signiert). Die Codegruppen für diese Assemblys werden definiert über die **StrongNameMembershipCondition**, basierend auf Informationen des öffentlichen Schlüssels für den starken Namen der Assembly Beweis stellt. Die Codegruppe erhält die **FullTrust** Berechtigungssatz.  
  
## <a name="report-server-extensions-rendering-data-delivery-and-security"></a>Berichtsservererweiterungen (Rendering, Daten, Übermittlung und Sicherheit)  
 Berichtsservererweiterungen sind benutzerdefinierte Erweiterungen für Daten, Übermittlung, Rendering und Sicherheit, die Sie selbst oder Drittanbieter zur Erweiterung der Funktionen von [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] erstellen. Sie gewähren müssen **FullTrust** diesen Erweiterungen oder die Assembly Code in den Konfigurationsdateien der Richtlinie zugeordneten der [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Komponente, die Sie erweitern. Erweiterungen im Lieferumfang des [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] werden mit dem öffentlichen Schlüssel des Berichtsservers signiert und erhalten die **FullTrust** Berechtigungssatz.  
  
> [!IMPORTANT]  
>  Müssen Sie ändern die [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Richtlinienkonfigurationsdateien ermöglichen **FullTrust** für alle Erweiterungen von Drittanbietern. Wenn Sie keine Codegruppe mit hinzufügen **FullTrust** für Ihre benutzerdefinierten Erweiterungen nicht verwendet werden vom Berichtsserver.  
  
 Weitere Informationen über die Richtlinienkonfigurationsdateien in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], finden Sie unter [Using Reporting Services Security Policy Files](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
## <a name="expressions-used-in-reports"></a>In Berichten verwendete Ausdrücke  
 Berichtsausdrücke sind inlinecodeausdrücke oder benutzerdefinierte Methoden, die als Bestandteil der **Code** Element von einer Berichtsdefinitions-Sprachdatei. Es wird eine Codegruppe, die in den Richtliniendateien bereits konfiguriert ist, die diese Ausdrücke gewährt der **Ausführung** standardmäßig festgelegte Berechtigung. Die Codegruppe sieht wie folgt aus:  
  
```  
<CodeGroup  
   class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="Execution"  
   Name="Report_Expressions_Default_Permissions"  
   Description="This code group grants default permissions for code in report expressions and Code element. ">  
    <IMembershipCondition  
       class="StrongNameMembershipCondition"  
       version="1"  
       PublicKeyBlob="002400..."  
    />  
</CodeGroup>  
```  
  
 **Ausführung** Berechtigung kann der Code zum Ausführen (execute), jedoch nicht um die geschützten Ressourcen verwendet. Alle in einem Bericht gefundenen Ausdrücke werden in einer Assembly kompiliert ("Ausdruckshostassembly"), die als Teil des kompilierten Berichts gespeichert wird. Beim Ausführen des Berichts lädt der Berichtsserver die Ausdruckshostassembly und führt Aufrufe für diese Assembly zum Ausführen von Berechtigungen durch. Ausdruckshostassemblys werden mit einem bestimmten Schlüssel signiert, der zum Definieren der Codegruppe für alle Ausdruckshosts verwendet wird.  
  
 Berichtsausdrücke beziehen sich auf Berichtsobjekt-Modellauflistungen (Felder, Parameter usw.) und führen einfache Aufgaben wie arithmetische und Zeichenfolgenoperationen aus. Code, der diese einfachen Vorgänge ausführt, erfordert nur **Ausführung** Berechtigung. Standardmäßig wird benutzerdefinierten Methoden in der **Code** Element und alle benutzerdefinierten Assemblys gewährt werden **Ausführung** -Berechtigung für [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Daher muss bei den meisten Ausdrücken die aktuelle Konfiguration nicht in den Sicherheitsrichtliniendateien geändert werden. Um Ausdruckshostassemblys weitere Berechtigungen gewähren zu können, muss ein Administrator die Riechlinienkonfigurationsdateien des Berichtsservers und des Berichts-Designers anpassen sowie die Berichtsausdruck-Codegruppe ändern. Da es sich um eine globale Einsstellung handelt, wirkt sich eine Änderung der Standardberechtigungen für den Ausdruckshost auf alle Berichte aus. Aus diesem Grund wird empfohlen, jeglichen Code, der zusätzliche Sicherheit erfordert, in einer benutzerdefinierten Assembly zu speichern. Nur dieser Assembly werden die benötigten Berechtigungen gewährt.  
  
> [!IMPORTANT]  
>  Code, der externe Assemblys oder geschützte Ressourcen aufruft, muss zur Verwendung in Berichten in eine benutzerdefinierte Assembly einbezogen werden. Auf diese Weise können Sie die vom Code angeforderten und durchgesetzten Berechtigungen besser steuern. Sie sollten keine Aufrufe von sicheren Methoden im vornehmen der **Code** Element. Auf diese Weise müssen Sie erteilen **FullTrust** berichtsausdruckshost und alle benutzerdefinierten Code Vollzugriff auf die CLR gewährt.  
  
> [!CAUTION]  
>  Erteilen Sie keine **FullTrust** der Codegruppe für einen berichtsausdruckshost. Ansonsten können alle Berichtsausdrücke geschützte Systemaufrufe ausführen.  
  
## <a name="custom-assemblies-referenced-in-reports"></a>In Berichten referenzierte benutzerdefinierte Assemblys  
 Einige Berichtsausdrücke können Codeassemblys von Drittanbietern aufrufen, die in [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] auch als benutzerdefinierte Assemblys bezeichnet werden. Der Berichtsserver erwartet, dass diese Assemblys mindestens **Ausführung** -Berechtigung für die Richtlinien-Konfigurationsdateien. Standardmäßig Richtliniendateien die im Lieferumfang [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] gewähren **Ausführung** Berechtigung auf alle Assemblys, die aus der Zone 'Arbeitsplatz' ab. Sie können benutzerdefinierten Assemblys nach Bedarf zusätzliche Berechtigungen gewähren.  
  
 In einigen Fällen müssen Sie einen Vorgang ausführen, der bestimmte Codeberechtigungen in einem Berichtsausdruck erfordert. In der Regel bedeutet dies, dass ein Berichtsausdruck einen Aufruf einer sicheren CLR-Bibliotheksmethode (z. B. einer Methode, die auf Dateien oder die Systemregistrierung zugreift) durchführen muss. In der Dokumentation zu [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] werden die Codeberechtigungen beschrieben, die zum Durchführen dieses sicheren Aufrufs notwendig sind. Um den Aufruf ausführen zu können, müssen dem aufrufenden Code diese speziellen, sicheren Berechtigungen gewährt werden. Wenn Sie den Aufruf von einem berichtsausdruck vornehmen oder die **Code** -Element, die Ausdruckshostassembly muss werden die erforderlichen Berechtigungen erteilt. Nachdem Sie dem Ausdruckshost jedoch die Berechtigung gewährt haben, gilt diese spezielle Berechtigung für jeglichen Code, der in einem Ausdruck eines beliebigen Berichts ausgeführt wird. Es ist sicher, diesen Aufruf von einer benutzerdefinierten Assembly auszuführen und dieser benutzerdefinierten Assembly die speziellen Berechtigungen zuzuweisen.  
  
## <a name="see-also"></a>Siehe auch  
 [Codezugriffssicherheit in Reporting Services](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)   
 [Sichere Entwicklung &#40; Reporting Services &#41;](../../../reporting-services/extensions/secure-development/secure-development-reporting-services.md)  
  
  
