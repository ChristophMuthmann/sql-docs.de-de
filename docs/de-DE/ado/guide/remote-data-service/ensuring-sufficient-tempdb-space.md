---
title: Sicherstellen von ausreichend Speicherplatz für TempDB | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- TempDB space in RDS [ADO]
ms.assetid: 09130db1-6248-4234-a1e5-a9c8e1622c06
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b80874fcb1f6be96e6e8c7f1a87916ac69f2517
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="ensuring-sufficient-tempdb-space"></a>Sicherstellen, dass ausreichend Speicherplatz für TempDB
Wenn Fehler, während der Behandlung auftreten [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) Objekte, die Verarbeitung von Speicherplatz auf Microsoft SQL Server 6.5 benötigen, müssen Sie möglicherweise die Größe des TempDB-erhöhen. (Einige Abfragen erfordern temporäre Verarbeitungskapazitäten; z. B. eine Abfrage mit einer ORDER BY-Klausel erfordert eine Sortierung von der **Recordset**, wofür die temporären Speicherplatz.)  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
> [!IMPORTANT]
>  Lesen Sie dieses Verfahren vor dem Ausführen der Aktionen aus, da es ist nicht so einfach, ein Gerät zu verkleinern, nachdem es vergrößert wurde.  
  
> [!NOTE]
>  Standard-InMicrosoft ist SQLServer 7.0 und höher, TempDB festgelegt, bei Bedarf automatisch erweitert. Daher kann dieses Verfahren nur auf Servern mit Versionen vor 7.0 erforderlich.  
  
### <a name="to-increase-the-tempdb-space-on-sql-server-65"></a>Um die TempDB-Speicherplatz in SQL Server 6.5 zu erhöhen.  
  
1.  Starten Sie Microsoft SQL Server Enterprise Manager, öffnen Sie die Struktur für den Server, und öffnen Sie dann auf die Datenbankmedien-Struktur.  
  
2.  Wählen Sie ein Gerät (physisches), zu erweitern, z. B. Master, und doppelklicken Sie auf das Gerät zu öffnen die **Datenbankmedium bearbeiten** (Dialogfeld).  
  
     Dieses Dialogfeld zeigt, wie viel Speicherplatz die aktuellen Datenbanken verwenden.  
  
3.  In der **Größe** Feld, erhöhen Sie das Gerät in die gewünschte Anzahl (z. B. 50 Megabyte (MB) Festplattenspeicher).  
  
4.  Klicken Sie auf **jetzt ändern** um den Umfang des Speicherplatzes zu erhöhen, der (logische) TempDB erweitern kann.  
  
5.  Öffnen Sie die Struktur der Datenbanken auf dem Server, und doppelklicken Sie dann auf **TempDB** So öffnen die **Datenbank bearbeiten** (Dialogfeld). Die **Datenbank** Registerkarte zeigt den Umfang an Speicherplatz für TempDB (**Datengröße**). Standardmäßig ist dies 2 MB.  
  
6.  Klicken Sie unter der **Größe** zu gruppieren, klicken Sie auf **erweitern**. Die Diagramme zeigen die verfügbaren und den reservierten Speicherplatz auf jedem physischen Geräte. Die Balken Dunkelrot repräsentieren verfügbaren Speicherplatz.  
  
7.  Wählen Sie eine **Protokolliergerät**, z. B. Master, um die verfügbare Größe in anzuzeigen die **Größe (MB)** Feld.  
  
8.  Klicken Sie auf **jetzt erweitern** diesen Speicherplatz in der TempDB-Datenbank zu reservieren.  
  
     Die **Datenbank bearbeiten** Dialogfeld zeigt auf die neue Größe für TempDB belegt.  
  
 Weitere Informationen zu diesem Thema durchsuchen Sie die Microsoft SQL Server Enterprise Manager-Hilfe-Datei für "Datenbank erweitern (Dialogfeld)."  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


