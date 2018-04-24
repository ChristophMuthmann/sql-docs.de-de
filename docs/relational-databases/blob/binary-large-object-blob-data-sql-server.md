---
title: Binary Large Object (BLOB)-Daten (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], design and implementation
ms.assetid: 97509274-c3f8-43e5-a37c-52f1ffe0961a
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 7a7584b5ccc191a11cdc82ece7be9d6fb426da1e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="binary-large-object-blob-data-sql-server"></a>Binary Large Object (BLOB)-Daten (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] stellt Lösungen zum Speichern von Dateien und Dokumenten in der Datenbank oder auf Remotespeichergeräten bereit.  
  
## <a name="compare-options-for-storing-blobs-in-sql-server"></a>Vergleichen von Optionen zum Speichern von Blobs (SQL Server)

Vergleichen Sie die Vorteile von FILESTREAM, FileTables und Remote Blob Store. Weitere Informationen finden Sie unter [Vergleichen von Optionen zum Speichern von Blobs &#40;SQL Server&#41;](../../relational-databases/blob/compare-options-for-storing-blobs-sql-server.md).
  
##  <a name="options-for-storing-blobs"></a>Optionen zum Speichern von Blobs  

### <a name="filestream-40sql-server41relational-databasesblobfilestream-sql-servermd"></a>[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  

FILESTREAM ermöglicht es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-basierten Anwendungen, nicht strukturierte Daten wie beispielsweise Dokumente und Bilder im Dateisystem zu speichern. Anwendungen können die umfassenden Streaming-APIs und die Leistung des Dateisystems nutzen und dabei die Transaktionskonsistenz zwischen den nicht strukturierten Daten und den entsprechenden strukturierten Daten erhalten.  
  
### <a name="filetables-40sql-server41relational-databasesblobfiletables-sql-servermd"></a>[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  

Die FileTable-Funktion bietet für die in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]gespeicherten Dateidaten Unterstützung für den Windows-Dateinamespace und die Kompatibilität mit Windows-Anwendungen. Mit FileTable können das Speichersystem und die Datenverwaltungskomponenten einer Anwendung integriert werden. Zudem werden integrierte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienste (z. B. Volltextsuche und semantische Suche) über unstrukturierte Daten und Metadaten bereitgestellt.  
  
 So können Sie Dateien und Dokumente in besonderen Tabellen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] speichern, die als FileTables bezeichnet werden, und auf diese über Windows-Anwendungen zugreifen, so als ob sie im Dateisystem gespeichert wären, ohne Clientanwendungen ändern zu müssen.  
  
### <a name="remote-blob-store-40rbs41-40sql-server41relational-databasesblobremote-blob-store-rbs-sql-servermd"></a>[Remoteblobspeicher &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  

Der Remote BLOB-Speicher (RBS) für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht Datenbankadministratoren, Binary Large Objects (BLOBS) in Speicherlösungen statt auf dem Server direkt zu speichern. Dies spart bedeutend Platz und vermeidet Aufwand für teure Serverhardwareressourcen. RBS stellt einen Satz von API-Bibliotheken bereit, die ein standardisiertes Modell für Anwendungen definieren, um auf BLOB-Daten zuzugreifen. Außerdem umfasst RBS Wartungstools wie die automatische Speicherbereinigung, um die Verwaltung von BLOB-Remotedaten zu unterstützen.  
  
 RBS ist nicht auf den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Installationsmedien enthalten. Er wird auch nicht über das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setupprogram installiert.  
  
  
