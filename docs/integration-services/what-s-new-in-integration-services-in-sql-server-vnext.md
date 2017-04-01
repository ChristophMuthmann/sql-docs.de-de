---
title: "Neuigkeiten in Integration Services in SQL Server vNext | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e26d7884-e772-46fa-bfdc-38567fe976a1
caps.latest.revision: 4
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 3
---
# Neuigkeiten in Integration Services in SQL Server vNext
Dieses Thema beschreibt die Funktionen, die in [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] hinzugefügt oder aktualisiert wurden.

>   [!NOTE] SQL Server vNext umfasst auch die Funktionen von SQL Server 2016 sowie die bei Updates von SQL Server 2016 hinzugekommenen Funktionen. Informationen zu den neuen Funktionen von SSIS in SQL Server 2016 finden Sie unter [Neuigkeiten in Integration Services in SQL Server 2016](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md).

## <a name="new-in-ssis-in-sql-server-vnext-ctp-11"></a>Neuigkeiten in SSIS in SQL Server vNext CTP 1.1

In SQL Server vNext CTP 1.1 gibt es keine neuen Funktionen von SSIS.

## <a name="new-in-ssis-in-sql-server-vnext-ctp-10"></a>Neuigkeiten in SSIS in SQL Server vNext CTP 1.0

### <a name="scale-out-for-ssis"></a>Horizontale Hochskalierung für SSIS

Die Funktion zum horizontalen Skalieren macht es viel einfacher, [!INCLUDE[ssIS_md](../includes/ssis-md.md)] auf mehreren Computern auszuführen. 
   
Nach dem Installieren des Masters und der Worker für horizontales Hochskalieren kann das Paket automatisch für die Ausführung auf verschiedenen Workern verteilt werden. Wenn die Ausführung unerwartet abbricht, wird sie automatisch wiederholt. Ferner können alle Ausführungen und Worker zentral mithilfe des Masters verwaltet werden.
   
Weitere Informationen finden Sie unter [Horizontale Hochskalierung für Integration Services (SSIS)](../integration-services/integration-services-ssis-scale-out.md).
   
### <a name="support-for-microsoft-dynamics-online-resources"></a>Unterstützung für Onlineressourcen von Microsoft Dynamics

Die OData-Quelle und der OData-Verbindungs-Manager unterstützen jetzt Verbindungen mit den OData-Feeds von Microsoft Dynamics AX Online und Microsoft Dynamics CRM Online.
