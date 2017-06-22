---
title: Berechtigungserteilung in benutzerdefinierten Assemblys | Microsoft Docs
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
- secure calls [Reporting Services]
- custom assemblies [Reporting Services], permissions
- permission sets [Reporting Services]
- asserting permissions
- permissions [Reporting Services], custom assemblies
- limited permission sets
- security configuration files [Reporting Services]
ms.assetid: 3afb9631-f15e-405e-990b-ee102828f298
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 12e12b61a6b2a2a6a58bb88dd3c4f47c2a6eab22
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="asserting-permissions-in-custom-assemblies"></a>Berechtigungserteilung in benutzerdefinierten Assemblys
  Standardmäßig benutzerdefiniertem Assemblycode ausgeführt wird, mit dem eingeschränkten **Ausführung** Berechtigungssatz. In einigen Fällen möchten Sie vielleicht eine benutzerdefinierte Assembly implementieren, die gesicherte Aufrufe an geschützte Ressourcen innerhalb Ihres Sicherheitssystems durchführt (z. B. an Dateien oder die Registrierung). Hierzu müssen Sie folgende Schritte durchführen:  
  
1.  Identifizieren Sie die genauen Berechtigungen, die der Code benötigt, um den gesicherten Aufruf zu machen. Wenn diese Methode Teil ist eine [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Bibliothek, diese Informationen in der Dokumentation der Methode eingeschlossen werden soll.  
  
2.  Ändern Sie die Dateien für die Berichtsserver-Richtlinienkonfiguration, um der benutzerdefinierten Assembly die erforderlichen Berechtigungen zu erteilen. Weitere Informationen zu den Sicherheitsrichtlinien-Konfigurationsdateien, finden Sie unter [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md).  
  
3.  Erteilen Sie die erforderlichen Berechtigungen als ein Teil der Methode, in der der gesicherte Aufruf gemacht wird. Dies ist erforderlich, da der benutzerdefinierten Assembly-Code, die vom Berichtsserver aufgerufen wird Teil der berichtsausdrucks-Hostassembly,, die ausgeführt wird ist und **Ausführung** Berechtigung standardmäßig. Die **Ausführung** Satz von Datenbankberechtigungen, kann der Code ausgeführt, aber nicht für die geschützten Ressourcen verwendet.  
  
4.  Markieren Sie die benutzerdefinierte Assembly mit **AllowPartiallyTrustedCallersAttribute** Wenn sie mit einem starken Namen signiert ist. Dies ist erforderlich, da benutzerdefinierte Assemblys von einem berichtsausdruck aufgerufen werden, die Teil der berichtsausdrucks-Hostassembly, ist, die nicht standardmäßig erteilt **FullTrust**; es handelt sich daher ein "teilweise vertrauenswürdig" Aufrufer. Weitere Informationen finden Sie unter [Verwenden von benutzerdefinierten Assemblys](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md).  
  
## <a name="implementing-a-secure-call"></a>Implementieren sicherer Aufrufe  
 Sie können die Dateien für die Richtlinienkonfiguration ändern, um der Assembly bestimmte Berechtigungen zu erteilen. Wenn Sie beispielsweise eine benutzerdefinierte Assembly für die Währungsumrechnung schreiben, kann es nötig sein, dass die aktuellen Wechselkurse aus einer Datei gelesen werden müssen. Um die Rate Informationen abzurufen, müssen Sie zum Hinzufügen einer Berechtigung Sicherheitsvorkehrungen **FileIOPermission**, zum Berechtigungssatz der Assembly. Sie können folgenden zusätzlichen Eintrag in der Datei für die Richtlinienkonfiguration vornehmen:  
  
```  
<PermissionSet class="NamedPermissionSet"  
   version="1"  
   Name="CurrencyRatesFilePermissionSet"  
   Description="A special permission set that grants read access to my currency rates file.">  
      <IPermission class="FileIOPermission"  
         version="1"  
         Read="C:\CurrencyRates.xml"/>  
      <IPermission class="SecurityPermission"  
         version="1"  
         Flags="Execution, Assertion"/>  
</PermissionSet>  
```  
  
 Sie fügen dann eine Codegruppe hinzu, die auf diesen Berechtigungssatz verweist:  
  
```  
<CodeGroup class="UnionCodeGroup"  
   version="1"  
   PermissionSetName="CurrencyRatesFilePermissionSet"  
   Name="MyNewCodeGroup"  
   Description="A special code group for my custom assembly.">  
   <IMembershipCondition class="UrlMembershipCondition"  
      version="1"  
      Url="C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\MSSQL\Reporting Services\ReportServer\bin\CurrencyConversion.dll"/>  
</CodeGroup>  
```  
  
 Damit Ihr Code die entsprechende Berechtigung erhält, müssen Sie diese Berechtigung im Code der benutzerdefinierten Assembly erteilen. Wenn Sie beispielsweise Lesezugriff zur XML-Datei, C:\CurrencyRates.xml, hinzufügen möchten, müssen Sie folgenden Code zu Ihrer Methode hinzufügen:  
  
```  
// C#  
FileIOPermission permission = new FileIOPermission(FileIOPermissionAccess.Read, @"C:\CurrencyRates.xml");  
try  
{  
   permission.Assert();  
   // Load the XML currency rates file  
   XmlDocument doc = new XmlDocument();  
   doc.Load(@"C:\CurrencyRates.xml");  
...  
```  
  
 Sie können diese Erteilung auch als Methodenattribut hinzufügen:  
  
```  
[FileIOPermissionAttribute(SecurityAction.Assert, Read=@"C:\CurrencyRates.xml")]  
```  
  
 Weitere Informationen finden Sie in der .NET Framework-Sicherheit im .NET Framework Developer's Guide.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwenden von benutzerdefinierten Assemblys mit Berichten](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
