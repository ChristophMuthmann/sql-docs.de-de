---
title: "Microsoft Connectors für Oracle und Teradata von Attunity (SSIS) | Microsoft-Dokumentation"
ms.date: 05/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d7e5ca02e2e4f7ee2e1a2e7044f522048a6fb196
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors für Oracle und Teradata von Attunity für Integration Services (SSIS)

Sie können Connectors von Attunity für Integration Services herunterladen, die die Leistung verbessern, wenn Daten in oder aus Oracle oder Teradata in ein SSIS-Paket geladen werden.

## <a name="download-the-latest-attunity-connectors"></a>Herunterladen der neuesten Attunity-Connectors

Laden Sie die neuesten Versionen der Connectors unter folgendem Link herunter:  
[Microsoft Connectors v5.0 for Oracle and Teradata (Microsoft Connectors Version 5.0 für Oracle und Teradata)](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problem: Die Attunity-Connectors werden in der SSIS-Toolbox nicht angezeigt

Damit die Attunity-Connectors in der SSIS-Toolbox angezeigt werden, müssen Sie stets die Version der Connectors installieren, die auf dieselbe SQL Server-Version ausgerichtet ist wie die auf Ihrem Computer installierten SQL Server Data Tools (SSDT). (Es dürfen auch frühere Versionen der Connectors installiert sein.) Diese Anforderung steht nicht mit der SQL Server-Version in Zusammenhang, auf die Ihre SSIS-Projekte und -Pakete ausgerichtet sind.

Wenn z.B. die neueste SSDT-Version installiert ist, ist Version 17 von SSDT mit einer Buildnummer installiert, die mit der Zahl 14 beginnt. In dieser Version von SSDT wird die SQL Server 2017-Unterstützung hinzugefügt. Sie müssen die neuste Version von Attunity-Connectors (Version 5.0) installieren, wenn Sie Attunity Connectors in der SSIS-Paketentwicklung abrufen und verwenden möchten, sogar wenn Sie diese auf eine frühere SQL Server-Version ausrichten möchten. In dieser Version der Connectors wird außerdem die SQL Server 2017-Unterstützung hinzugefügt.

Überprüfen Sie die in Visual Studio installierte Version von SSDT unter **Hilfe** | **Info zu Microsoft Visual Studio** oder unter **Programme und Funktionen** in den Einstellungen. Installieren Sie anschließend die zugehörige Version der Attunity-Connectors aus der folgenden Tabelle.

|SSDT-Version|SSDT-Buildnummer|Zielversion von SQL Server|Erforderliche Connectors-Version|
|---------|---------|---------|---------|
|17|Beginnt mit 14|SQL Server 2017|[Microsoft Connectors v5.0 for Oracle and Teradata (Microsoft Connectors Version 5.0 für Oracle und Teradata)](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Beginnt mit 13|SQL Server 2016|[Microsoft Connectors v4.0 for Oracle and Teradata (Microsoft Connectors Version 4.0 für Oracle und Teradata)](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Herunterladen der neuesten SQL Server Data Tools (SSDT)

Laden Sie die neueste Version von SSDT unter folgendem Link herunter:  
[Herunterladen von SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)
