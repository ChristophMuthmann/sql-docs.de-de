---
title: Importieren und Exportieren von Wissen | Microsoft-Dokumentation
ms.custom: 
ms.date: 07/31/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: 
ms.component: data-quality-services
ms.reviewer: 
ms.suite: sql
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 12537c9d-31e4-40b0-a411-cb343abbe96a
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 13ca99cdb38d8fced0eae2b655f1d1b2df7b9b03
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="importing-and-exporting-knowledge"></a>Importieren und Exportieren von Wissen
  Sie können Wissensdatenbanken und Domänen direkt in der [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Anwendung erstellen, oder Sie können Wissen in eine Wissensdatenbank importieren oder daraus exportieren. In der [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Anwendung können Sie eine Datendatei für Import- und Exportvorgänge, oder eine Excel-Datei für Importvorgänge, verwenden. Die verwendete Datendatei ist eine verschlüsselte Datei, die von [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) mit einer DQS-Erweiterung erstellt wird. Die von Microsoft Excel erstellten Dateien können die Erweiterung .xlsx, .xls oder .csv haben. Diese Vorgänge geben Ihnen mehr Flexibilität bei der Erstellung und Freigabe des Wissens, mit dem Sie Datenbereinigung und Datenabgleich durchführen.  
  
> [!IMPORTANT]  
>  Sie können sofort *alle* Wissensdatenbanken auf dem [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] durch das Ausführen der Datei DQSInstaller.exe von der Eingabeaufforderung in eine DQS-Sicherungsdatei (.dqsb) exportieren. Auf ähnliche Weise können Sie sofort *alle* Wissensdatenbanken aus einer DQS-Sicherungsdatei (.dqsb) durch das Ausführen der DQSInstaller.exe von der Eingabeaufforderung auf den [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] importieren. Informationen hierzu finden Sie unter [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md) im DQS-Installationshandbuch.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 Sie können folgende Import- und Exportvorgänge ausführen:  
  
|||  
|-|-|  
|Exportieren einer Domäne in einer Wissensdatenbank in eine DQS-Datendatei|[Exportieren einer Domäne in eine DQS-Datei](../data-quality-services/export-a-domain-to-a-dqs-file.md)|  
|Importieren einer Domäne aus einer DQS-Datendatei in eine vorhandene Wissensdatenbank|[Importieren einer Domäne aus einer DQS-Datei](../data-quality-services/import-a-domain-from-a-dqs-file.md)|  
|Exportieren einer ganzen Wissensdatenbank in eine DQS-Datendatei|[Exportieren einer Wissensdatenbank in eine DQS-Datei](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)|  
|Importieren einer ganzen Wissensdatenbank in eine DQS-Datendatei|[Importieren einer Wissensdatenbank aus einer DQS-Datei](../data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)|  
|Importieren von Werten aus einer Excel-Datei in eine Domäne|[Import Values from an Excel File into a Domain](../data-quality-services/import-values-from-an-excel-file-into-a-domain.md)|  
|Importieren von Domänen aus einer Excel-Datei in eine Wissensdatenbank|[Importieren von Domänen aus einer Excel-Datei in eine Wissensermittlung](../data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)|  
|Importieren von Wissen, das während der Bereinigung gesammelt wurde, in eine Wissensdatenbank|[Importieren von Bereinigungsprojektwerten in eine Domäne](../data-quality-services/import-cleansing-project-values-into-a-domain.md)|  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Erstellen einer Wissensdatenbank durch das Ausführen der Wissensermittlung und interaktives Verwalten von Wissen|[Aufbau einer Wissensdatenbank](../data-quality-services/building-a-knowledge-base.md)|  
|Erstellen einer einzelnen Domäne und Hinzufügen von Wissen zur Domäne.|[Verwalten einer Domäne](../data-quality-services/managing-a-domain.md)|  
|Erstellen einer Verbunddomäne und Hinzufügen von Wissen zur Domäne.|[Verwalten einer Verbunddomäne](../data-quality-services/managing-a-composite-domain.md)|  
  
  
