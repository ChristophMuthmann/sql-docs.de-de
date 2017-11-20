---
title: Azure Resource Manager-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd1dbf668bf3ac24d9d6598b0ff9e2256d897c42
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager-Verbindungs-Manager
Die **Azure Resource Manager-Verbindungs-Manager** ermöglicht einem SSIS-Paket zum Verwalten von Azure-Ressourcen mithilfe einer [Dienstprinzipal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).

Die **Azure Resource Manager-Verbindungs-Manager** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Zum Erstellen und Konfigurieren einer **Azure Resource Manager-Verbindungs-Manager**, befolgen Sie die folgenden Schritte aus:

1. In der **SSIS-Verbindungs-Manager hinzufügen** wählen Sie im Dialogfeld **AzureResourceManager**, und klicken Sie auf **hinzufügen**.
2. In der **Azure Resource Manager-Verbindungs-Manager-Editor** Dialogfeld geben die **Anwendungs-ID**, **Anwendungsschlüssel**, und **Mandanten-ID** für den Dienstprinzipal. Einzelheiten zu diesen Eigenschaften finden Sie auf [dies](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) Artikel.
3. Klicken Sie auf **OK** , um das Dialogfeld zu schließen.
4. Die Eigenschaften des Verbindungs-Managers, die Sie im Fenster **Eigenschaften** erstellt haben, werden angezeigt.

