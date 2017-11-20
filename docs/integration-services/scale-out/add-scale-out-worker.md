---
title: "Fügen Sie ein SSIS-Dezentrales Skalieren Worker mit Skalieren auf Unternehmensebene Manager | Microsoft Docs"
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
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b769236330941a107865a0b133961bce5bf6b85b
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="add-a-scale-out-worker-with-scale-out-manager"></a>Horizontales Worker mit Skalieren auf Unternehmensebene Manager hinzufügen

Integration Services-Scale Out Manager Infrastrukturkosten erheblich die Komplexität, um die vorhandene Umgebung horizontal skalieren Scale-Out-Worker hinzufügen. 

Die unten aufgeführten Schritten ermöglichen es Ihnen, eine Skalierung Out Worker der Topologie Horizontales Skalieren hinzufügen:

## <a name="1-install-scale-out-worker"></a>1. Dezentrales Skalieren Worker installieren
Wählen Sie im Installations-Assistenten von SQL Server Integration Services und Scale-Out-Worker auf die **Funktionsauswahl** Seite. 
![Komponentenauswahl Worker](media/feature-select-worker.PNG)

Auf der **Scale Out Konfiguration von Integration Services - Worker-Knoten** Seite, Sie können einfach klicken Sie auf "Weiter", um diese Konfiguration überspringen und verwenden **Scale-Out-Manager** , die Konfiguration nach der Installation auszuführen.

Beenden Sie den Installations-Assistenten.

## <a name="2-open-firewall-on-scale-out-master-computer"></a>2. Öffnen Sie die Firewall auf Scale-Out-Master-computer
Öffnen Sie den Port angegeben werden, während die Scale-Out-Master-Installation (standardmäßig 8391) und den Port des SQL Server (standardmäßig 1433) verwenden die Windows-Firewall auf dem Computer Scale-Out-Master.

## <a name="3-add-scale-out-worker-with-scale-out-manager"></a>3. Dezentrales Skalieren Worker mit Skalieren auf Unternehmensebene Manager hinzufügen
SQL Server Management Studio als Administrator ausführen, und Verbinden mit SQL Server-Instanz des Scale-Out-Master.

Mit der rechten Maustaste **SSISDB** im Objekt-Explorer, und wählen **verwalten horizontal skalieren...** . 

![Verwalten für horizontales Skalieren](media/manage-scale-out.PNG)

In der ausgelesene einrichten **Scale-Out-Manager**, wechseln Sie zur **Worker-Manager**. Klicken Sie auf "+" Schaltfläche und befolgen Sie die Anweisungen im Dialogfeld "Worker verbinden". Weitere Informationen finden Sie unter [Scale-Out-Manager](integration-services-ssis-scale-out-manager.md).

