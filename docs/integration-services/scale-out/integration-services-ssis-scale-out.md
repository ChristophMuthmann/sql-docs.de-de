---
title: "Horizontale Hochskalierung für Integration Services (SSIS) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dcfbd1c5-c001-4fb7-b9ae-916e49ab6a96
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0277d312ce4dab14e7ba64529e3eb2251a0d2d02
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="integration-services-ssis-scale-out"></a>Horizontale Hochskalierung für Integration Services (SSIS)
Horizontale Hochskalierung für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bietet eine äußerst leistungsfähige Paketausführung, indem Ausführungsvorgänge auf mehrere Computer verteilt werden. Sie können eine Anforderung für mehrere Paketausführungen in SQL Server Management Studio senden. Diese Pakete werden parallel in einem Modus für horizontale Hochskalierung ausgeführt.  

Horizontale Hochskalierung von [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] besteht aus einem Master für horizontales Hochskalieren für [!INCLUDE[ssIS_md](../../includes/ssis-md.md)] und mindestens einem Worker für horizontales Hochskalieren für [!INCLUDE[ssIS_md](../../includes/ssis-md.md)]. Der Master für horizontales Hochskalieren ist für die Verwaltung von horizontaler Hochskalierung verantwortlich und empfängt Paketausführungsanforderungen von Benutzern. Worker für horizontales Hochskalieren holen sich Ausführungsaufgaben vom Master für horizontales Hochskalieren und erledigen die Paketausführungsvorgänge. Weitere Informationen finden Sie unter [Master für horizontales Hochskalieren](integration-services-ssis-scale-out-master.md), [Worker für horizontales Hochskalieren](integration-services-ssis-scale-out-worker.md).

Horizontale Hochskalierung für [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] kann auf einem Computer konfiguriert werden, auf dem ein Master für horizontales Hochskalieren und ein Worker für horizontales Hochskalieren nebeneinander eingerichtet sind. Horizontale Hochskalierung kann auch auf mehreren Computern ausgeführt werden, wobei sich jeder Worker für horizontales Hochskalieren auf einem anderen Computer befindet.
- [Exemplarische Vorgehensweise: Einrichten von horizontaler Hochskalierung für Integration Services](walkthrough-set-up-integration-services-scale-out.md)

Horizontale Hochskalierung unterstützt mehrere Pakete im SSISDB-Katalog parallel. Weitere Informationen finden Sie unter [Ausführen von Paketen in horizontaler Hochskalierung](run-packages-in-integration-services-ssis-scale-out.md).
