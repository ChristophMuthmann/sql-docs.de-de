---
title: Datenquellen | Microsoft Docs
ms.custom: 
ms.date: 08/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data sources [Integration Services], about data sources
ms.assetid: 7ac81612-9822-470f-8d0f-a1dc96142fe3
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 77ca3b5849eb90d21da55989d2c9ec7ae94a53f6
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="data-sources"></a>Datenquellen
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] umfasst ein Entwurfszeitobjekt, das Sie in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen verwenden können: die Datenquelle.  
  
 Ein Datenquellenobjekt ist ein Verweis auf eine Verbindung und enthält zumindest eine Verbindungszeichenfolge und einen Datenquellenbezeichner. Außerdem können zusätzliche Metadaten enthalten sein, wie z. B. eine Beschreibung, ein Name, ein Benutzername und ein Kennwort.  
  
> **HINWEIS:** Sie können Datenquellen nur Projekten hinzufügen, die für die Verwendung des Paketbereitstellungsmodells konfiguriert wurden. Wenn ein Projekt für die Verwendung des Projektbereitstellungsmodells konfiguriert wurde, können Sie anstelle von Datenquellen Verbindungs-Manager verwenden, die auf Projektebene zur Freigabe von Verbindungen erstellt wurden.  
>   
>  Weitere Informationen zu Bereitstellungsmodellen finden Sie unter [Deployment of Projects and Packages](../packages/deploy-integration-services-ssis-projects-and-packages.md). Weitere Informationen zum Konvertieren eines Projekts in das Projektbereitstellungsmodell finden Sie unter [Deploy Projects to Integration Services Server](https://msdn.microsoft.com/library/hh231102.aspx).  
  
 Die Verwendung von Datenquellen in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paketen bietet folgende Vorteile:  
  
-   Eine Datenquelle besitzt einen Projektbereich. Das bedeutet, dass eine in einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt erstellte Datenquelle für alle Pakete im Projekt verfügbar ist. Eine Datenquelle kann einmal definiert werden, und Verbindungs-Manager können dann in mehreren Paketen darauf verweisen.  
  
-   Eine Datenquelle ermöglicht die Synchronisierung zwischen dem Datenquellenobjekt und den Paketverweisen. Falls sich die Datenquelle und die Pakete, die darauf verweisen, im selben Projekt befinden, wird die Eigenschaft der Verbindungszeichenfolge der Datenquellenverweise automatisch aktualisiert, wenn die Datenquelle geändert wird.  
  
## <a name="reference-data-sources"></a>Verweisdatenquellen  
 Um einem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Projekt ein Datenquellenobjekt hinzuzufügen, klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Datenquellen** , und klicken Sie dann auf **Neue Datenquelle**. Das Element wird dem Ordner **Datenquellen** hinzugefügt. Wenn Sie Datenquellenobjekte verwenden möchten, die in anderen Projekten erstellt wurden, müssen Sie diese zuerst dem Projekt hinzufügen.  
  
 Sie verwenden ein Datenquellenobjekt in einem Paket, indem Sie dem Paket einen Verbindungs-Manager hinzufügen, der auf das Datenquellenobjekt verweist. Sie können ihn dem Paket vor dem Erstellen der Paketablaufsteuerung und der Datenflüsse oder als Schritt beim Erstellen der Ablaufsteuerung oder des Datenflusses hinzufügen.  
  
 Ein Datenquellenobjekt stellt eine einfache Verbindung mit einer Datenquelle dar und ermöglicht den Zugriff auf die Objekte im Datenspeicher, auf die verwiesen wird. Beispielsweise enthält ein Datenquellenobjekt, das eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]AdventureWorks-Beispieldatenbank herstellt, alle 60 Tabellen aus der Datenbank.  
  
 Es gibt keine Abhängigkeit zwischen einer Datenquelle und den Verbindungs-Managern, die darauf verweisen. Falls eine Datenquelle nicht mehr zum Projekt gehört, sind die Pakete weiterhin gültig, weil Informationen zur Datenquelle, wie z. B. der Verbindungstyp und die Verbindungszeichenfolge, in der Paketdefinition enthalten sind.  
  
  

