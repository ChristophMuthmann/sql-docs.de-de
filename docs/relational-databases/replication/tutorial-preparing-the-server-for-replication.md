---
title: "Tutorial: Vorbereiten des Servers für die Replikation | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3f7055cc15673a5dfd4564f26c4d314ccc0f5180
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="tutorial-preparing-the-server-for-replication"></a>Lernprogramm: Vorbereiten des Servers für die Replikation
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Es ist wichtig, einen Sicherheitsplan zu erstellen, bevor Sie die Replikationstopologie konfigurieren. In diesem Lernprogramm erfahren Sie, wie Sie eine Replikationstopologie besser sichern und die Verteilung konfigurieren können. Dieser Vorgang stellt den ersten Schritt für die Replikation von Daten dar. Es ist erforderlich, dieses Lernprogramm vor allen anderen Lernprogrammen abzuschließen.  
  
> [!NOTE]  
> Für das sichere Replizieren von Daten zwischen Servern empfiehlt es sich, alle Empfehlungen unter [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md)zu implementieren.  
  
## <a name="what-you-will-learn"></a>Lernziele  
In diesem Lernprogramm erfahren Sie, wie Sie einen Server vorbereiten, sodass die Replikation sicher und mit den geringsten Privilegien ausgeführt werden kann. In der ersten Lektion wird veranschaulicht, wie Sie die Windows-Dienstkonten erstellen können, die zur Ausführung von Replikations-Agents verwendet werden. In der zweiten Lektion erfahren Sie, wie der Ordner konfiguriert wird, in dem Momentaufnahmeveröffentlichungen generiert und gespeichert werden. In der dritten Lektion wird das Konfigurieren der Verteilung und das Festlegen der Berechtigungen erläutert.  
  
## <a name="requirements"></a>Anforderungen  
Dieses Lernprogramm ist für Benutzer vorgesehen, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Erfahrungen in Bezug auf die Replikation verfügen.  
  
Ihr System muss die folgenden installierten Komponenten aufweisen, damit dieses Lernprogramm verwendet werden kann:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mit der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank.  
  
**Geschätzte Zeit zum Bearbeiten dieses Lernprogramms: 30 Minuten**  
  
## <a name="lessons-in-this-tutorial"></a>Lektionen in diesem Lernprogramm  
  
-   [Lektion 1: Erstellen von Windows-Konten für die Replikation](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lektion 2: Vorbereiten des Momentaufnahmeordners](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lektion 3: Konfigurieren der Verteilung](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[Lernprogramm starten](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)  
[Sicherheit und Schutz &#40;Replikation&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  
