---
title: "Konfigurieren Sie freigegebene Datenträgercluster für SQL Server on Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 08/23/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: b6e6cc415b01c6021a4ba7c52433543dc58a4452
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Freigegebene Datenträgercluster für SQL Server on Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Sie können einen Hochverfügbarkeitscluster freigegebenem Speicher mit Linux zum Zulassen von SQL Server-Instanz auf Failover von einem Knoten zu einem anderen konfigurieren. In einem typischen Cluster sind mindestens zwei Server mit freigegebenem Speicher verbunden. Die Server sind die Clusterknoten. Failovercluster bieten Schutzebene Instanz, um die Wiederherstellungszeit von SQL Server erlaubt, für ein Failover zwischen zwei oder mehr Knoten zu verbessern. Konfigurationsschritte hängen davon ab, die Linux-Distribution und clustering-Lösungen. In der folgenden Tabelle identifiziert die spezielle Schritte für die überprüfte Clusterlösungen.  

|Distribution |Thema 
|----- |-----
|**Red Hat Enterprise Linux mit HA-Add-On** |[Konfigurieren](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Ausgeführt werden](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server mit HA-Add-On** |[Konfigurieren](sql-server-linux-shared-disk-cluster-sles-configure.md)

