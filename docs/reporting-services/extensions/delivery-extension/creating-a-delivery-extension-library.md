---
title: "Erstellen einer Bibliothek für Übermittlungserweiterungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: extensions
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
caps.latest.revision: "36"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8f057b2aff58d5e8d6022d2c7560e03412312e22
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="creating-a-delivery-extension-library"></a>Erstellen einer Bibliothek für Übermittlungserweiterungen
  Jede von Ihnen erstellte [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung sollte einen eindeutigen Namespace erhalten und in eine Bibliothek oder Assemblydatei integriert werden. Der exakte Name des Namespace ist unerheblich, er muss jedoch eindeutig sein und darf nicht zusammen mit einer anderen Erweiterung verwendet werden. Sie sollten eigene eindeutige Namespaces für die Übermittlungserweiterungen Ihres Unternehmens erstellen.  
  
 Folgendes Beispiel zeigt den Code, mit dem Sie eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung beginnen sollten. Der Code verwendet die Namespaces, welche die Übermittlungsschnittstellen und jegliche Hilfsprogrammklassen enthalten.  
  
```vb  
Imports System  
Imports Microsoft.ReportingServices.Interfaces  
  
Namespace CompanyName.ExtensionName  
   ...  
```  
  
```csharp  
using System;  
using Microsoft.ReportingServices.Interfaces;  
  
namespace CompanyName.ExtensionName  
{  
   ...  
```  
  
 Wenn Sie eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung kompilieren, müssen Sie für den Compiler einen Verweis auf Microsoft.ReportingServices.Interfaces.dll angeben, da sich die Schnittstellen der Übermittlungserweiterungen und -klassen dort befinden. Der <xref:Microsoft.ReportingServices.Interfaces>-Namespace wird benötigt, um die <xref:Microsoft.ReportingServices.Interfaces.IExtension>-Schnittstelle, die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>-Schnittstelle und mehr zu implementieren. Beispiel: Wenn sich alle Dateien, die den Code für die Implementierung einer in C# geschriebenen [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung enthalten, in einem Verzeichnis mit der Erweiterung .cs befinden, würde folgender Befehl von diesem Verzeichnis ausgegeben, um die in „CompanyName.ExtensionName.dll“ gespeicherten Dateien zu kompilieren.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 Im folgenden Codebeispiel wird der Befehl gezeigt, der für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]-Dateien mit der Erweiterung .vb verwendet werden würde.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  Sie können die Übermittlungserweiterung auch mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] entwerfen, entwickeln und erstellen. Weitere Informationen zum Entwickeln von Assemblys in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] finden Sie in der Dokumentation zu [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erweiterungen für Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementieren von Übermittlungserweiterungen](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services Extension Library (Reporting Services-Erweiterungsbibliothek)](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
