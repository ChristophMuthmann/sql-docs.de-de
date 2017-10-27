---
title: Binary Large Object (BLOB)-Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-blob
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a9291aa99091d1b44e4b829af803637250bd333
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="binary-large-object-blob-data-sql-server"></a>Binary Large Object (BLOB)-Daten (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Lösungen zum Speichern von Dateien und Dokumenten in der Datenbank oder auf Remotespeichergeräten bereit.  
  
##  <a name="section"></a> In diesem Abschnitt  
 [Vergleichen von Optionen zum Speichern von Blobs &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md)  
 Vergleichen Sie die Vorteile von FILESTREAM, FileTables und Remote Blob Store.  
  
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
 FILESTREAM ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-basierten Anwendungen, nicht strukturierte Daten wie beispielsweise Dokumente und Bilder im Dateisystem zu speichern. Anwendungen können die umfassenden Streaming-APIs und die Leistung des Dateisystems nutzen und dabei die Transaktionskonsistenz zwischen den nicht strukturierten Daten und den entsprechenden strukturierten Daten erhalten.  
  
 [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
 Die FileTable-Funktion bietet für die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeicherten Dateidaten Unterstützung für den Windows-Dateinamespace und die Kompatibilität mit Windows-Anwendungen. Mit FileTable können das Speichersystem und die Datenverwaltungskomponenten einer Anwendung integriert werden. Zudem werden integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste (z. B. Volltextsuche und semantische Suche) über unstrukturierte Daten und Metadaten bereitgestellt.  
  
 So können Sie Dateien und Dokumente in besonderen Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichern, die als FileTables bezeichnet werden, und auf diese über Windows-Anwendungen zugreifen, so als ob sie im Dateisystem gespeichert wären, ohne Clientanwendungen ändern zu müssen.  
  
 [Remoteblobspeicher &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
 Der Remote BLOB-Speicher (RBS) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht Datenbankadministratoren, Binary Large Objects (BLOBS) in Speicherlösungen statt auf dem Server direkt zu speichern. Dies spart bedeutend Platz und vermeidet Aufwand für teure Serverhardwareressourcen. RBS stellt einen Satz von API-Bibliotheken bereit, die ein standardisiertes Modell für Anwendungen definieren, um auf BLOB-Daten zuzugreifen. Außerdem umfasst RBS Wartungstools wie die automatische Speicherbereinigung, um die Verwaltung von BLOB-Remotedaten zu unterstützen.  
  
 RBS ist nicht auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsmedien enthalten. Er wird auch nicht über das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setupprogram installiert.  
  
  

