---
title: "Erstellen einer Bibliothek für Übermittlungserweiterungen | Microsoft Docs"
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
- delivery extensions [Reporting Services], namespace assignments
- library [Reporting Services]
- assigning namespaces to extensions
ms.assetid: 63b32f93-4bab-4b07-bd72-39a47aca1cda
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: bcfb5b69df148108531e9e5b843f127af0e3fbb4
ms.contentlocale: de-de
ms.lasthandoff: 08/12/2017

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
  
 Wenn Sie eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]-Übermittlungserweiterung kompilieren, müssen Sie für den Compiler einen Verweis auf Microsoft.ReportingServices.Interfaces.dll angeben, da sich die Schnittstellen der Übermittlungserweiterungen und -klassen dort befinden. Der <xref:Microsoft.ReportingServices.Interfaces>-Namespace wird benötigt, um die <xref:Microsoft.ReportingServices.Interfaces.IExtension>-Schnittstelle, die <xref:Microsoft.ReportingServices.Interfaces.IDeliveryExtension>-Schnittstelle und mehr zu implementieren. Angenommen, wenn alle Dateien, die des Codes zum Implementieren einer [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] übermittlungserweiterung, die in c# geschrieben, die in einem Verzeichnis mit der Erweiterung .cs befänden, würde der folgende Befehl aus dem Verzeichnis, die in CompanyName.ExtensionName.dll gespeicherten Dateien zu kompilieren ausgegeben werden.  
  
```csharp  
csc /t:library /out:CompanyName.ExtensionName.dll *.cs /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
 Im folgenden Codebeispiel wird veranschaulicht, den Befehl, der für verwendet werden würde [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] Dateien mit der Erweiterung. vb dar.  
  
```vb  
vbc /t:library /out:CompanyName.ExtensionName.dll *.vb /r:System.dll   
/r:Microsoft.ReportingServices.Interfaces.dll  
```  
  
> [!NOTE]  
>  Sie können die Übermittlungserweiterung auch mit [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] entwerfen, entwickeln und erstellen. Weitere Informationen zum Entwickeln von Assemblys in [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] finden Sie in der Dokumentation zu [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Erweiterungen](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementing a Delivery Extension](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Reporting Services-Erweiterungsbibliothek](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

