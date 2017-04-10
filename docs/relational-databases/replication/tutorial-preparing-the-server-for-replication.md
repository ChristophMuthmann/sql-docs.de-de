---
title: "Lernprogramm: Vorbereiten des Servers f&#252;r die Replikation | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "Replikation [SQL Server], Tutorials"
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# Lernprogramm: Vorbereiten des Servers f&#252;r die Replikation
Es ist wichtig, einen Sicherheitsplan zu erstellen, bevor Sie die Replikationstopologie konfigurieren. In diesem Lernprogramm erfahren Sie, wie Sie eine Replikationstopologie besser sichern und die Verteilung konfigurieren können. Dieser Vorgang stellt den ersten Schritt für die Replikation von Daten dar. Es ist erforderlich, dieses Lernprogramm vor allen anderen Lernprogrammen abzuschließen.  
  
> [!NOTE]  
> Für das sichere Replizieren von Daten zwischen Servern empfiehlt es sich, alle Empfehlungen unter [Bewährte Methoden für die Replikationssicherheit](../../relational-databases/replication/security/replication-security-best-practices.md) zu implementieren.  
  
## Lernziele  
In diesem Lernprogramm erfahren Sie, wie Sie einen Server vorbereiten, sodass die Replikation sicher und mit den geringsten Privilegien ausgeführt werden kann. In der ersten Lektion wird veranschaulicht, wie Sie die Windows-Dienstkonten erstellen können, die zur Ausführung von Replikations-Agents verwendet werden. In der zweiten Lektion erfahren Sie, wie der Ordner konfiguriert wird, in dem Momentaufnahmeveröffentlichungen generiert und gespeichert werden. In der dritten Lektion wird das Konfigurieren der Verteilung und das Festlegen der Berechtigungen erläutert.  
  
## Anforderungen  
Dieses Lernprogramm ist für Benutzer vorgesehen, die mit grundlegenden Datenbankvorgängen vertraut sind, aber nur über begrenzte Erfahrungen in Bezug auf die Replikation verfügen.  
  
Ihr System muss die folgenden installierten Komponenten aufweisen, damit dieses Lernprogramm verwendet werden kann:  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] mit der [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Datenbank.  
  
**Geschätzte Zeit zum Bearbeiten dieses Lernprogramms: 30 Minuten**  
  
## Lektionen in diesem Lernprogramm  
  
-   [Lektion 1: Erstellen von Windows-Konten für die Replikation](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [Lektion 2: Vorbereiten des Momentaufnahmeordners](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [Lektion 3: Konfigurieren der Verteilung](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[Lernprogramm starten](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## Siehe auch  
[Konfigurieren der Verteilung](../../relational-databases/replication/configure-distribution.md)  
[Sicherheit und Schutz &#40;Replikation&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  
