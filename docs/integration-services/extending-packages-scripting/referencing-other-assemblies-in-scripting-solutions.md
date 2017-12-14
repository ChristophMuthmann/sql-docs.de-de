---
title: "Verweisen auf andere Assemblys in Skriptlösungen | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs: VB
helpviewer_keywords:
- SSIS Script task, .NET Framework
- Script task [Integration Services], adding references
- referencing custom assemblies
- SSIS Script task, VisualBasic namespace
- assemblies [Integration Services]
- VisualBasic namespace
- Script task [Integration Services], VisualBasic namespace
- Microsoft.VisualBasic namespace
- Script task [Integration Services], .NET Framework
- .NET Framework [Integration Services]
- referencing Web services
ms.assetid: 9b655bcd-19f6-43d8-9f89-1b4d299c6380
caps.latest.revision: "68"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1e90784bab93fa79b02add5223bebea08113a70c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Verweisen auf andere Assemblys in Skriptlösungen
  Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassenbibliothek bietet Skriptentwicklern leistungsfähige Tools zur Implementierung von benutzerdefinierten Funktionen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]-Paketen. In Skripttasks und Skriptkomponenten können ebenfalls benutzerdefinierte verwaltete Assemblys verwendet werden.  
  
> [!NOTE]  
>  Damit Ihre Pakete die Objekte und Methoden eines Webdienstes verwenden können, setzen Sie den Befehl **Webverweis hinzufügen** in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) ein. In früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mussten Sie eine Proxyklasse generieren, um einen Webdienst zu verwenden.  
  
## <a name="using-a-managed-assembly"></a>Verwenden einer verwalteten Assembly  
 Damit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die verwaltete Assembly zur Entwurfszeit findet, müssen Sie die folgenden Schritte ausführen:  
  
1.  Speichern Sie die verwaltete Assembly in einem beliebigen Ordner auf dem Computer.  
  
    > [!NOTE]  
    >  In früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] konnten Sie nur einen Verweis auf eine verwaltete Assembly hinzufügen, die im Ordner %windir%\Microsoft.NET\Framework\vx.x.xxxxx oder unter %Programme%\Microsoft SQL Server\100\SDK\Assemblies gespeichert war.  
  
2.  Fügen Sie einen Verweis auf die verwaltete Assembly hinzu.  
  
     Um den Verweis hinzuzufügen, klicken Sie in VSTA im Dialogfeld **Verweis hinzufügen** auf die Registerkarte **Durchsuchen**. Wenn Sie die verwaltete Assembly gefunden haben, fügen Sie sie hinzu.  
  
 Damit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die verwaltete Assembly zur Laufzeit findet, müssen Sie die folgenden Schritte ausführen:  
  
1.  Signieren Sie die verwaltete Assembly mit einem starken Namen.  
  
2.  Installieren Sie die Assembly im globalen Assemblycache auf dem Computer, auf dem das Paket ausgeführt wird.  
  
     Weitere Informationen finden Sie unter [Building, Deploying, and Debugging Custom Objects](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md) (Erstellen, Bereitstellen und Debuggen von benutzerdefinierten Objekten).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Verwenden der Microsoft .NET Framework-Klassenbibliothek  
 Der Skripttask und die Skriptkomponente können alle anderen Objekte und Funktionen, die von der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Klassenbibliothek bereitgestellt werden, nutzen. Durch Verwendung von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] können Sie beispielsweise Informationen zu Ihrer Umgebung abrufen und mit dem Computer interagieren, der das Paket ausführt.  
  
 In dieser Liste werden einige der häufig verwendeten [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassen beschrieben:  
  
-   **System.Data** enthält die ADO.NET-Architektur.  
  
-   **System.IO** eine Schnittstelle zum Dateisystem und den Datenströmen bereit.  
  
-   **System.Windows.Forms** ermöglicht die Formularerstellung.  
  
-   **System.Text.RegularExpressions** stellt Klassen zum Arbeiten mit regulären Ausdrücken bereit.  
  
-   **System.Environment** gibt Informationen über den lokalen Computer, den aktuellen Benutzer sowie die Computer- und Benutzereinstellungen zurück.  
  
-   **System.Net** ermöglicht die Netzwerkkommunikation.  
  
-   **System.DirectoryServices** stellt Active Directory bereit.  
  
-   **System.Drawing** stellt umfangreiche Bildbearbeitungsbibliotheken bereit.  
  
-   **System.Threading** aktiviert Multithreadprogrammierung.  
  
 Weitere Informationen über [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] finden Sie in der MSDN Library.  
  
## <a name="see-also"></a>Siehe auch  
 [Erweitern von Paketen mit Skripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
