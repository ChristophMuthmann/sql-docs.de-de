---
title: "Microsoft Connectors für Oracle und Teradata von Attunity (SSIS) | Microsoft Docs"
ms.date: 05/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 926c0c51b5a55a2869b73666f5620fa56e139cca
ms.openlocfilehash: fd8b0177227167f6caa3417029bb2acb974fe181
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="microsoft-connectors-for-oracle-and-teradata-by-attunity-for-integration-services-ssis"></a>Microsoft Connectors für Oracle und Teradata von Attunity für Integrationsservices (SSIS)

Sie können die Connectors für Integration Services von Attunity, die Leistung zu optimieren, beim Laden von Daten zu oder von Oracle oder Teradata in einem SSIS-Paket herunterladen.

## <a name="download-the-latest-attunity-connectors"></a>Herunterladen der neuesten Attunity-connectors

Die neueste Version der Connector hier abrufen:  
[Microsoft Connectors V5. 0 für Oracle- und Teradata](https://www.microsoft.com/download/details.aspx?id=55179)

## <a name="issue---the-attunity-connectors-arent-visible-in-the-ssis-toolbox"></a>Problem - verfügt nicht über die Attunity-Connectors in der SSIS-Toolbox

Um die Attunity-Connectors in der SSIS-Toolbox anzuzeigen, müssen Sie immer die Version der Connector installieren, dass Ziele die gleiche Version von SQL Server als die Version von SQL Server Data Tools (SSDT) auf Ihrem Computer installiert. (Sie müssen auch frühere Versionen der Connector installiert.) Dies gilt unabhängig von der Version von SQL Server, die in der SSIS-Projekte und Pakete ausgerichtet werden sollen.

Z. B., wenn Sie die neueste Version von SSDT installiert haben, müssen Sie 17-Version von SSDT mit einem Build-Nummer, die mit 14 beginnt. Diese Version von SSDT fügt Unterstützung für SQL Server-2017 hinzu. Anzeigen und verwenden die Attunity-Paket-Connectors in SSIS Development - auch dann, wenn Sie eine frühere Version von SQL Server möchten – Sie auch die neueste Version der Attunity Connectors, Version 5.0 installieren müssen. Diese Version der Connectors bietet nun auch Unterstützung für SQL Server-2017.

Überprüfen Sie die installierte Version von SSDT in Visual Studio aus **Hilfe** | **zu Microsoft Visual Studio**, oder im **Programme und Funktionen** in der Systemsteuerung. Befestigen Sie die entsprechende Version der Attunity Connectors aus der folgenden Tabelle aus.

|SSDT-version|SSDT-Buildnummer|SQL Server-Zielversion|Erforderliche Version von Connectors|
|---------|---------|---------|---------|
|17|Beginnt mit 14|SQL Server 2017|[Microsoft Connectors V5. 0 für Oracle- und Teradata](https://www.microsoft.com/download/details.aspx?id=55179)|
|16|Beginnt mit 13|SQL Server 2016|[Microsoft Connectors v4. 0 für Oracle und Teradata](https://www.microsoft.com/download/details.aspx?id=52950)|
||||

## <a name="download-the-latest-sql-server-data-tools-ssdt"></a>Herunterladen der neuesten SQL Server Data Tools (SSDT)

Erhalten Sie die neueste Version von SSDT hier:  
[Herunterladen von SQL Server Data Tools (SSDT)](..//ssdt/download-sql-server-data-tools-ssdt.md)

