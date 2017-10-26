---
title: "Optimieren der Komprimierung für die Verfügbarkeitsgruppe | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/22/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7632769c-b246-4766-886f-7c60ec540be8
caps.latest.revision: 12
author: MikeRayMSFT
ms.author: v-saume
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: d7eed64649188267eafb4a555fa811d8c9d27f0e
ms.contentlocale: de-de
ms.lasthandoff: 09/27/2017

---
# <a name="tune-compression-for-availability-group"></a>Optimieren der Komprimierung für die Verfügbarkeitsgruppe

Standardmäßig werden Datenströme für Verfügbarkeitsgruppen gegebenenfalls von SQL Server komprimiert. Die Komprimierung reduziert den Netzwerkverkehr, steigert die CPU-Auslastung und kann die Latenz erhöhen. Sie müssen Mitglied der festen Serverrolle „sysadmin“ sein, um die Komprimierung zu aktivieren. Die folgende Tabelle zeigt, wann SQL Server Protokolldatenströme von Verfügbarkeitsgruppen komprimiert:

| Szenario | Komprimierungseinstellung
| ---- | ----
| Replikat für synchrone Commits | Nicht komprimiert
| Replikat für asynchrone Commits | Compressed
| Während des automatischen Seedings | Nicht komprimiert

## <a name="trace-flags-for-availability-group-compression"></a>Ablaufverfolgungsflags für Verfügbarkeitsgruppenkomprimierung 

In den meisten Szenarien empfiehlt Microsoft, diese Einstellungen nicht zu ändern. Sie können globale Ablaufverfolgungsflags verwenden, um Änderungen an diesen Einstellungen zu testen. SQL Server wendet globale Ablaufverfolgungsflags auf die gesamte Instanz an. Alle Verfügbarkeitsgruppen in der Instanz sind von diesen Einstellungen betroffen.  

Die folgende Tabelle zeigt Ablaufverfolgungsflags, die das Standardkomprimierungsverhalten für SQL Server ändern. 

Ablaufverfolgungsflag | Description
------------- | -------------
1462          | Deaktiviert die Protokolldatenstrom-Komprimierung für Verfügbarkeitsgruppen mit asynchronen Replikaten. Dieses Feature ist für asynchrone Replikate standardmäßig aktiviert, um die Netzwerkbandbreite zu optimieren.
9567          | Aktiviert die Komprimierung des Datenstroms für Verfügbarkeitsgruppen während des automatischen Seedings. Während des automatischen Seedings kann die Übertragungszeit durch die Komprimierung erheblich reduziert und die Arbeitslast für den Prozessor erhöht werden.
9592          | Aktiviert die Protokolldatenstrom-Komprimierung für Verfügbarkeitsgruppen mit synchronen Replikaten. Dieses Feature ist für synchrone Replikate standardmäßig deaktiviert, da die Komprimierung die Latenz erhöht. Für asynchrone Replikate ist die Protokolldatenstrom-Komprimierung standardmäßig aktiviert.


## <a name="resources"></a>Ressourcen


[Startoptionen für das Datenbankmodul](../../../database-engine/configure-windows/database-engine-service-startup-options.md)

[Automatisches Seeding](https://msdn.microsoft.com/library/mt735149(SQL.130).aspx)

[Voraussetzungen für Always On](prereqs-restrictions-recommendations-always-on-availability.md) 

