---
title: "Konfigurieren Sie freigegebene Datenträgercluster für SQL Server on Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 31c8c92e-12fe-4728-9b95-4bc028250d85
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 92b4cb2500d4fd8a1643488593c40e97b1ff6454
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---

# <a name="shared-disk-cluster-for-sql-server-on-linux"></a>Freigegebene Datenträgercluster für SQL Server on Linux

Sie können einen Hochverfügbarkeitscluster freigegebenem Speicher mit Linux zum Zulassen von SQL Server-Instanz auf Failover von einem Knoten zu einem anderen konfigurieren. In einem typischen Cluster sind mindestens zwei Server mit freigegebenem Speicher verbunden. Die Server sind die Clusterknoten. Failovercluster bieten Schutzebene Instanz, um die Wiederherstellungszeit von SQL Server erlaubt, für ein Failover zwischen zwei oder mehr Knoten zu verbessern. Konfigurationsschritte hängen davon ab, die Linux-Distribution und clustering-Lösungen. In der folgenden Tabelle identifiziert die spezielle Schritte für die überprüfte Clusterlösungen.  

|Distribution |Thema 
|----- |-----
|**Red Hat Enterprise Linux mit HA-Add-On** |[Konfigurieren](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Ausgeführt werden](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server mit HA-Add-On** |[Konfigurieren](sql-server-linux-shared-disk-cluster-sles-configure.md)

## <a name="next-steps"></a>Nächste Schritte


