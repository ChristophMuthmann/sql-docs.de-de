---
title: Installieren von Integration Services-Versionen nebeneinander | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 114e51f111e4b3dfece42c9510a35bb9be5d5652
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="installing-integration-services-versions-side-by-side"></a>Paralleles Installieren von Integration Services-Versionen
  Sie können   
      [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Integration Services (SSIS) Seite-an-Seite mit früheren Versionen von SSIS. Dieses Thema beschreibt einige Einschränkungen der parallelen Installationen.  
  
## <a name="designing-and-maintaining-packages"></a>Entwerfen und Verwalten von Paketen  
 Verwenden Sie SQL Server Data Tools (SSDT) für Visual Studio 2015, um Pakete zu entwerfen und zu verwalten, die auf SQL Server 2016, SQL Server 2014 oder SQL Server 2012 ausgerichtet sind. Die neuesten SSDT können Sie unter [Download der neuesten SQL Server-Datatools](../../ssdt/download-sql-server-data-tools-ssdt.md)herunterladen.  
  
 Klicken Sie auf der Eigenschaftsseite eines Integration Services-Projekts auf der Registerkarte **Allgemein** in den **Konfigurationseigenschaften**auf die Eigenschaft **TargetServerVersion** , und wählen Sie SQL Server 2016, 2014 oder 2012 aus.  
  
|Zielversion von SQL Server|Entwicklungsumgebung für SSIS-Pakete|  
|----------------------------------|-----------------------------------------------|  
|2016|SQL Server Data Tools für Visual Studio 2015|  
|2014|SQL Server Data Tools für Visual Studio 2015<br /><br /> oder<br /><br /> SQL Server Data Tools - Business Intelligence für Visual Studio 2013|  
|2012|SQL Server Data Tools für Visual Studio 2015<br /><br /> oder<br /><br /> SQL Server Data Tools – Business Intelligence für Visual Studio 2012|  
|2008|Business Intelligence Development Studio von SQL Server 2008|  
  
 Wenn Sie ein vorhandenes Paket einem bestehenden Projekt hinzufügen, wird das Paket in das Format des Projekts konvertiert.  
  
## <a name="running-packages"></a>Ausführen von Paketen  
 Sie können die [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Version des **dtexec** -Hilfsprogramms oder des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents verwenden, um die mit früheren Versionen der Entwicklungstools erstellten Integration Services-Pakete auszuführen. Wenn diese [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Tools ein Paket laden, das mit einer früheren Version der Entwicklungstools erstellt wurde, wird das Paket im Arbeitsspeicher vorübergehend in das von [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] verwendete Paketformat konvertiert. Wenn das Paket Probleme verursacht, die eine erfolgreiche Konvertierung verhindern, kann das [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] -Tool das Paket erst ausführen, wenn diese Probleme behoben wurden. Weitere Informationen finden Sie unter [Aktualisieren von Integration Services-Paketen](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
  
