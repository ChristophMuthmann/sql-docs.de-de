---
title: "Verweisen auf andere Assemblys in Scripting Lösungen | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
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
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3deb13c7e3aeb2e974ac6e6582555a617346a298
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="referencing-other-assemblies-in-scripting-solutions"></a>Verweisen auf andere Assemblys in Skriptlösungen
  Die [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] -Klassenbibliothek bietet Skriptentwicklern einen Satz leistungsstarker Tools zum Implementieren von benutzerdefinierten Funktionen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Pakete. In Skripttasks und Skriptkomponenten können ebenfalls benutzerdefinierte verwaltete Assemblys verwendet werden.  
  
> [!NOTE]  
>  Verwenden Sie zum Aktivieren der Pakete die Objekte und Methoden eines Webdienstes verwenden die **Webverweis hinzufügen** Befehl verfügbar in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). In früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mussten Sie eine Proxyklasse generieren, um einen Webdienst zu verwenden.  
  
## <a name="using-a-managed-assembly"></a>Verwenden einer verwalteten Assembly  
 Für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] um eine verwaltete Assembly zur Entwurfszeit findet, müssen Sie die folgenden Schritte aus:  
  
1.  Speichern Sie die verwaltete Assembly in einem beliebigen Ordner auf dem Computer.  
  
    > [!NOTE]  
    >  In früheren Versionen von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] konnten Sie nur einen Verweis auf eine verwaltete Assembly hinzufügen, die im Ordner %windir%\Microsoft.NET\Framework\vx.x.xxxxx oder unter %Programme%\Microsoft SQL Server\100\SDK\Assemblies gespeichert war.  
  
2.  Fügen Sie einen Verweis auf die verwaltete Assembly hinzu.  
  
     Der Verweis in VSTA im Hinzufügen der **Verweis hinzufügen** das Dialogfeld die **Durchsuchen** Registerkarte, suchen, und fügen Sie die verwaltete Assembly hinzu.  
  
 Damit [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] die verwaltete Assembly zur Laufzeit findet, müssen Sie die folgenden Schritte ausführen:  
  
1.  Signieren Sie die verwaltete Assembly mit einem starken Namen.  
  
2.  Installieren Sie die Assembly im globalen Assemblycache auf dem Computer, auf dem das Paket ausgeführt wird.  
  
     Weitere Informationen finden Sie unter [erstellen, bereitstellen und Debuggen von benutzerdefinierten Objekten](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="using-the-microsoft-net-framework-class-library"></a>Verwenden der Microsoft .NET Framework-Klassenbibliothek  
 Der Skripttask und die Skriptkomponente können alle anderen Objekte und Funktionen, die von der [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Klassenbibliothek bereitgestellt werden, nutzen. Durch Verwendung von [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] können Sie beispielsweise Informationen zu Ihrer Umgebung abrufen und mit dem Computer interagieren, der das Paket ausführt.  
  
 In dieser Liste werden einige der häufig verwendeten [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]-Klassen beschrieben:  
  
-   **"System.Data"** enthält die ADO.NET-Architektur.  
  
-   **System.IO** stellt eine Schnittstelle für das Dateisystem und Streams.  
  
-   **"System.Windows.Forms"** ermöglicht die formularerstellung.  
  
-   **System.Text.RegularExpressions** stellt Klassen zum Arbeiten mit regulären Ausdrücken bereit.  
  
-   **"System.Environment"** gibt Informationen über den lokalen Computer, den aktuellen Benutzer und die Computer- und benutzereinstellungen zurück.  
  
-   **System.Net** ermöglicht die Netzwerkkommunikation.  
  
-   **System.DirectoryServices** stellt Active Directory bereit.  
  
-   **"System.Drawing"** stellt umfangreiche bildbearbeitungsbibliotheken bereit.  
  
-   **System.Threading** aktiviert Multithreadprogrammierung.  
  
 Weitere Informationen über [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] finden Sie in der MSDN Library.  
  
## <a name="see-also"></a>Siehe auch  
 [Erweitern von Paketen mit Skripts](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
