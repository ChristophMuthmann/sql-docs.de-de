---
title: "Horizontale Hochskalierung f&#252;r Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 6
---
# Horizontale Hochskalierung f&#252;r Integration Services (SSIS)
Horizontale Hochskalierung für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] bietet eine äußerst leistungsfähige Paketausführung, indem Ausführungsvorgänge auf mehrere Computer verteilt werden. Sie können eine Anforderung für mehrere Paketausführungen in SQL Server Management Studio senden. Diese Pakete werden parallel in einem Modus für horizontale Hochskalierung ausgeführt.  


## <a name="ssis-scale-out-master-and-scale-out-worker"></a>Master für horizontales Hochskalieren und Worker für horizontales Hochskalieren für SSIS
Horizontale Hochskalierung von [!INCLUDE[ssIS_md](../includes/ssis-md.md)] besteht aus einem Master für horizontales Hochskalieren für [!INCLUDE[ssIS_md](../includes/ssis-md.md)] und mehreren Worker für horizontales Hochskalieren für [!INCLUDE[ssIS_md](../includes/ssis-md.md)]. Der Master für horizontales Hochskalieren ist für die Verwaltung von horizontaler Hochskalierung verantwortlich und empfängt Paketausführungsanforderungen von Benutzern. Worker für horizontales Hochskalieren holen sich Ausführungsaufgaben vom Master für horizontales Hochskalieren und erledigen die Paketausführungsvorgänge. Weitere Informationen finden Sie unter [Master für horizontales Hochskalieren](../integration-services/integration-services-ssis-scale-out-master.md), [Worker für horizontales Hochskalieren](../integration-services/integration-services-ssis-scale-out-worker.md).


## <a name="how-to-set-up-scale-out"></a>So richten Sie horizontale Hochskalierung ein
Horizontale Hochskalierung für [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] kann auf einem Computer ausgeführt werden, auf dem ein Master für horizontales Hochskalieren und ein Worker für horizontales Hochskalieren nebeneinander eingerichtet sind. Horizontale Hochskalierung kann auch auf mehreren Computern ausgeführt werden, wobei sich jeder Worker für horizontales Hochskalieren auf einem anderen Computer befindet.
- [Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung für Integration Services](../integration-services/walkthrough-set-up-integration-services-scale-out.md)


## <a name="run-packages-in-scale-out"></a>Ausführen von Paketen in horizontaler Hochskalierung
Horizontale Hochskalierung unterstützt mehrere Pakete im SSISDB-Katalog parallel. Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung](../integration-services/run-packages-in-integration-services-ssis-scale-out.md).

