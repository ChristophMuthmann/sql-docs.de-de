---
title: Was &#39; s in Integration Services in SQLServer 2017 | Microsoft Docs
ms.custom: 
ms.date: 09/28/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: e76675099ab290d29231d434eb74e92b613185b7
ms.openlocfilehash: 63aba0f64bc63a3a86e5aa07245375938acdf6e4
ms.contentlocale: de-de
ms.lasthandoff: 09/29/2017

---
# <a name="what39s-new-in-integration-services-in-sql-server-2017"></a>Was &#39; s in Integration Services in SQLServer 2017
Dieses Thema beschreibt die Funktionen, die in [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]hinzugefügt oder aktualisiert wurden.

>   [!NOTE]
> SQL Server-2017 enthält auch die Funktionen von SQL Server 2016 und die Funktionen in SQL Server 2016-Updates hinzugefügt. Informationen zu den neuen Funktionen von SSIS in SQL Server 2016 finden Sie unter [Neuigkeiten in Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="highlights-of-this-release"></a>Highlights von dieser Version

Hier sind die wichtigsten neuen Funktionen von Integration Services in SQL Server-2017.

-   **Horizontales Skalieren**. SSIS-paketausführung leichter auf mehrere Arbeitsthreads Computer verteilen und Verwalten von Ausführungen und Worker aus einem einzelnen Mastercomputer. Weitere Informationen finden Sie unter [Integration Services horizontal skalieren](../integration-services/scale-out/integration-services-ssis-scale-out.md).

-   **Integrationsservices unter Linux**. SSIS-Pakete auf Linux-Computern ausführen. Weitere Informationen finden Sie unter [extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS](../linux/sql-server-linux-migrate-ssis.md).

-   **Konnektivität Verbesserungen**. Verbinden Sie mit der OData-Feeds von Microsoft Dynamics AX Online und Microsoft Dynamics CRM Online mit den aktualisierten OData-Komponenten. 

## <a name="new-in-azure-data-factory"></a>Neues in Azure Data Factory

Mit der öffentlichen Vorschau von Azure Data Factory, Version 2 im September 2017 können Sie jetzt Folgendes tun:
-   Bereitstellen von Paketen zur SSIS-Katalogdatenbank (SSISDB) für Azure SQL-Datenbank.
-   Ausführen von Paketen, die in Azure auf der Azure-SSIS-Integrationslaufzeit, eine Komponente von Azure Data Factory, Version 2 bereitgestellt wird.

Weitere Informationen finden Sie unter [Lift- and -Shift SQL Serverintegration Services-arbeitsauslastungen in die Cloud](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

Diese neuen Funktionen benötigen SQL Server Data Tools (SSDT) Version 17.2 oder höher, aber keine 2017 von SQL Server oder SQL Server 2016 erfordern. Wenn Sie Pakete in Azure bereitstellen, aktualisiert der Paket-Bereitstellungs-Assistent die Pakete immer auf das aktuelle Paketformat.

## <a name="new-in-the-azure-feature-pack"></a>Neu in das Azure Feature Pack

Zusätzlich zu den Konnektivität-Verbesserungen in SQL Server hat den Integration Services Feature Pack für Azure-Unterstützung für Azure Data Lake-Speicher hinzugefügt. Weitere Informationen finden Sie im Blogbeitrag [neue Azure Feature Pack Version Stärkung ADLS Konnektivität](https://blogs.msdn.microsoft.com/ssis/2017/08/29/new-azure-feature-pack-release-strengthening-adls-connectivity/). Siehe auch [Azure Feature Pack für Integration Services (SSIS)](azure-feature-pack-for-integration-services-ssis.md).

## <a name="new-in-sql-server-data-tools-ssdt"></a>Neu in SQL Server Data Tools (SSDT)

Sie können jetzt entwickeln, SSIS-Projekte und Pakete, die auf Versionen von SQL Server 2012 bis 2017 in Visual Studio 2017 oder in Visual Studio 2015 abzielen. Weitere Informationen finden Sie unter [Herunterladen von SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md).

## <a name="new-in-ssis-in-sql-server-2017-rc1"></a>Neues in SSIS in SQL Server 2017 RC1

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Neue und geänderte Features in Horizontales Skalieren für SSIS

-   Scale Out-Master unterstützt jetzt die hohe Verfügbarkeit. Sie können Always On für SSISDB aktivieren und Einrichten von Windows Server-Failoverclustering für den Server, der als Host den Scale-Out-Master-Dienst. Diese Änderung auf Scale-Out-Master anwenden, müssen Sie eine einzelne Fehlerquelle vermeiden und bietet hohe Verfügbarkeit für die gesamte Bereitstellung horizontal skalieren.
-   Die Failoverbehandlung der Ausführungsprotokolle aus Scale-Out-Workern wurde verbessert. Für den Fall, dass die Skala Out Worker unerwartet beendet wird, werden die ausführungsprotokolle auf lokalem Datenträger beibehalten. Später beim Neustart der Arbeitsthread wird es lädt die persistente Protokolle und weiterhin SSISDB speichern möchten.
-   Der Parameter *runincluster* der gespeicherten Prozedur **[catalog].[create_execution]** wird hinsichtlich Konsistenz und Lesbarkeit in *runinscaleout* umbenannt. Diese Änderung des Parameternamens hat folgende Auswirkungen:
    -   Ggf. vorhandene Skripts zum Ausführen von Paketen in horizontal skalieren haben Sie so ändern Sie den Parameternamen von *Runincluster* auf *Runinscaleout* die Skripts funktionieren in RC1 vornehmen.
    -   SQL Server Management Studio (SSMS) 17.1 und früheren Versionen können nicht die Ausführung des Pakets in horizontal skalieren in RC1 ausgelöst. Die Fehlermeldung lautet: "*@runincluster* is not a parameter for procedure **create_execution** (ist kein Parameter für die Prozedur create_execution)." Dieses Problem wurde in der nächsten Version von SSMS, (Version 17.2) behoben. 17.2 und höher von SSMS unterstützt die neue Parameter und die Paket-Ausführung in horizontal skalieren. Bis SSMS Version 17,2, dieses Problem zu umgehen, verfügbar ist, können Sie die vorhandene Version von SSMS verwenden, um die paketausführungsskripts zu generieren und anschließend ändern Sie den Namen des der *Runincluster* Parameter *Runinscaleout* in das Skript, und führen Sie das Skript.
-   Der SSIS-Katalog verfügt über eine neue globale Eigenschaft, um den Standardmodus für das Ausführen von SSIS-Paketen anzugeben. Diese neue Eigenschaft gilt beim Aufrufen der **[Catalog]. [ Create_execution]** gespeicherte Prozedur mit der *Runinscaleout* Parameter auf null festgelegt ist. Dieser Modus gilt auch für SSIS SQL Agent-Aufträge. Sie können die neue globale Eigenschaft im Dialogfeld Eigenschaften für den SSISDB-Knoten in SSMS oder mit dem folgenden Befehl festlegen:
    ```sql
    EXEC [catalog].[configure_catalog] @property_name=N'DEFAULT_EXECUTION_MODE', @property_value=1
    ```

## <a name="new-in-ssis-in-sql-server-2017-ctp-21"></a>Neues in SSIS in 2.1 2017 CTP für SQL Server

### <a name="new-and-changed-features-in-scale-out-for-ssis"></a>Neue und geänderte Features in Horizontales Skalieren für SSIS

-   Sie können nun die **Use32BitRuntime** -Parameter, wenn Sie die Ausführung in horizontal skalieren auslösen.
-   Die Leistung der Protokollierung in SSISDB für paketausführungen in horizontal skalieren wurde verbessert. Die ereignismeldung und den Nachrichtenkontext Protokolle werden jetzt im Batchmodus statt einzeln in SSISDB geschrieben. Hier sind einige zusätzliche Hinweise zu dieser Verbesserung:        
    - Einige Berichte in der aktuellen Version von SQL Server Management Studio (SSMS) diese Protokolle für die Ausführung in horizontal skalieren nicht aktuell angezeigt werden. Wir erwarten, dass sie in der nächsten Version von SSMS unterstützt werden. Die betroffenen Berichte enthalten die *alle Verbindungen* Bericht, der *Fehlerkontext* Bericht, und die *Verbindungsinformationen* Abschnitt, in dem Integration Service-Dashboard.
    - Eine neue Spalte **Event_message_guid** hinzugefügt wurde. Verwenden Sie diese Spalte zum Verknüpfen der [Catalog]. [Event_message_context]-Sicht und der [Catalog]. [Event_messages] anzeigen, anstatt **Event_message_id** bei einer Abfrage diese Protokolle der Ausführungen in horizontal skalieren.
-   Zum Abrufen der verwaltungsanwendung für SSIS horizontal skalieren [Herunterladen von SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 17.1 oder höher.

## <a name="new-in-ssis-in-sql-server-2017-ctp-20"></a>Neues in SSIS in SQL Server 2017 CTP 2.0

Es sind keine neuen SSIS-Funktionen in SQL Server 2017 CTP 2.0.

## <a name="new-in-ssis-in-sql-server-2017-ctp-14"></a>Neues in SSIS in SQL Server 2017 CTP 1.4

Es sind keine neuen SSIS-Funktionen in SQL Server 2017 CTP 1.4.

## <a name="new-in-ssis-in-sql-server-2017-ctp-13"></a>Neues in SSIS in 1.3 2017 CTP für SQL Server

Es sind keine neuen SSIS-Funktionen in SQL Server 2017 CTP-Version 1.3.

## <a name="new-in-ssis-in-sql-server-2017-ctp-12"></a>Neues in SSIS im 2017-CTP für SQL Server 1.2

Es sind keine neuen SSIS-Funktionen in SQL Server 2017 CTP-Version 1.2.

## <a name="new-in-ssis-in-sql-server-2017-ctp-11"></a>Neues in SSIS im 2017-CTP für SQL Server 1.1

Es sind keine neuen SSIS-Funktionen in SQL Server 2017 CTP-Version 1.1.

## <a name="new-in-ssis-in-sql-server-2017-ctp-10"></a>Neues in SSIS in SQL Server 2017 CTP 1.0

### <a name="scale-out-for-ssis"></a>Horizontale Hochskalierung für SSIS

Die Funktion zum horizontalen Skalieren macht es viel einfacher, [!INCLUDE[ssIS_md](../includes/ssis-md.md)] auf mehreren Computern auszuführen. 
   
Nach dem Installieren des Masters und der Worker für horizontales Hochskalieren kann das Paket automatisch für die Ausführung auf verschiedenen Workern verteilt werden. Wenn die Ausführung unerwartet abbricht, wird sie automatisch wiederholt. Ferner können alle Ausführungen und Worker zentral mithilfe des Masters verwaltet werden.
   
Weitere Informationen finden Sie unter [Horizontale Hochskalierung für Integration Services (SSIS)](../integration-services/scale-out/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Unterstützung für Onlineressourcen von Microsoft Dynamics

Die OData-Quelle und der OData-Verbindungs-Manager unterstützen jetzt Verbindungen mit den OData-Feeds von Microsoft Dynamics AX Online und Microsoft Dynamics CRM Online.


