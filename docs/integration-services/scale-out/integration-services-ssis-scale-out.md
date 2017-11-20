---
title: "SQL Serverintegration Services (SSIS) für horizontales Skalieren | Microsoft Docs"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: ce7fb96901e8af4da74392fe0a0a85c6e2ec05a4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="integration-services-ssis-scale-out"></a>Horizontale Hochskalierung für Integration Services (SSIS)
Horizontale Hochskalierung für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bietet eine äußerst leistungsfähige Paketausführung, indem Ausführungsvorgänge auf mehrere Computer verteilt werden. Sie können eine Anforderung für mehrere paketausführungen in SQL Server Management Studio senden. Diese Pakete werden parallel in einem Modus für horizontale Hochskalierung ausgeführt.  

[!INCLUDE[ssIS_md](../../includes/ssis-md.md)]Horizontales Skalieren besteht aus einem [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale-Out-Master und einen oder mehrere [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] Scale-Out-Worker. Der Master für horizontales Hochskalieren ist für die Verwaltung von horizontaler Hochskalierung verantwortlich und empfängt Paketausführungsanforderungen von Benutzern. Worker für horizontales Hochskalieren holen sich Ausführungsaufgaben vom Master für horizontales Hochskalieren und erledigen die Paketausführungsvorgänge. Weitere Informationen finden Sie unter [Master für horizontales Hochskalieren](integration-services-ssis-scale-out-master.md), [Worker für horizontales Hochskalieren](integration-services-ssis-scale-out-worker.md).

[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]Horizontales Skalieren kann auf einem Computer konfiguriert werden, in einem Masterauftrag für den Out-Skalierung und eine Skala, Worker Seite-an-Seite auf dem Computer eingerichtet sind. Horizontale Hochskalierung kann auch auf mehreren Computern ausgeführt werden, wobei sich jeder Worker für horizontales Hochskalieren auf einem anderen Computer befindet.
- [Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung für Integration Services](walkthrough-set-up-integration-services-scale-out.md)

Horizontale Hochskalierung unterstützt mehrere Pakete im SSISDB-Katalog parallel. Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung](run-packages-in-integration-services-ssis-scale-out.md).

