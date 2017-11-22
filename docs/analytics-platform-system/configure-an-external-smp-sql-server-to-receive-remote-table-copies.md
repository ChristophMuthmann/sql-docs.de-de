---
title: Konfigurieren von externen SMP-SQL-Server zum Empfangen der Remotetabelle Kopien (PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bbd2ed6-064e-4b45-b67b-608dc0f2b2bc
caps.latest.revision: "13"
ms.openlocfilehash: 56ef4d9b75e8051a17c276556a321ed19ddcf2d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a>Konfigurieren Sie eine externe SMP-SQL-Server für den Empfang von Kopien der Remotetabelle
Beschreibt, wie eine externe SQL Server-Instanz zum Empfangen der Remotetabelle Kopien von SQL Server PDW konfiguriert.  
  
Dieses Thema beschreibt eine der Konfigurationsschritte zum Konfigurieren von remote-Tabelle kopieren. Eine Übersicht über die Konfigurationsschritte finden Sie unter [Remotekopie Tabelle](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Vorbereitungen  
Bevor Sie den externen SQL Server konfigurieren können, müssen Sie folgende Schritte ausführen:  
  
-   Haben Sie ein Windows-System mit SQL Server 2008 Enterprise Edition oder höher installiert oder installiert werden können. Das Windows-System muss bereits konfiguriert sein, gemäß der Anleitung in [konfigurieren Sie eine externe Windows System zum Empfangen Remote Tabelle Kopien mithilfe InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Ein Windows-Admin-Konto mit der Möglichkeit, SQL Server-Instanz und die Windows-System zu konfigurieren.  
  
-   Ein SQL Server Anmeldekonto (falls es sich um eine SQL Server bereits installiert ist) mit der Fähigkeit zum Erstellen von Anmeldenamen und Erteilen von Berechtigungen für die Ziel-Datenbanken.  
  
## <a name="HowToSQLServer"></a>Konfigurieren Sie eine externe SMP-SQL-Server für den Empfang von Kopien der Remotetabelle  
Die Funktion zum Kopieren der Remotetabelle kopiert Tabellen aus der SQL Server PDW-Anwendung mit einer externen SMP SQL Server-Datenbank, die auf einem Windows-Betriebssystem ausgeführt wird. Nach dem Konfigurieren der externen Windows-System um Remotetabelle Kopien zu erhalten, wird als Nächstes installieren und Konfigurieren von SQL Server auf dem Windows-System.  
  
Um SQL Server zu konfigurieren, verwenden Sie die folgenden Schritte aus:  
  
1.  Installieren Sie SQL Server 2008 Enterprise Edition oder höher auf dem Windows-System an. Dies wird als SMP SQL Server bezeichnet.  
  
2.  Konfigurieren von SQL Server TCP/IP-Verbindungen auf einem festen TCP-Port akzeptiert. Diese Konfiguration ist standardmäßig deaktiviert und muss aktiviert sein, um SQL Server PDW für die Verbindung mit dem SMP-SQL-Server zu ermöglichen.  
  
3.  Deaktivieren Sie die Windows-Firewall oder konfigurieren Sie den SMP SQL Server TCP-Port so, dass er mit aktivierter Windows-Firewall verwendet werden kann.  
  
4.  Konfigurieren Sie SQL Server für SQL Server-Authentifizierungsmodus zu. Die parallele Daten exportieren immer verwendet SQL Server-Konten für die Authentifizierung.  
  
5.  Bestimmen Sie eine SQL Server-Dienstkonto auf dem SMP-SQL-Server, die für die Authentifizierung verwendet werden. Erteilen Sie diesem Konto die Berechtigung zum Erstellen, löschen und Einfügen von Daten in Tabellen in der Zieldatenbank für den Exportvorgang parallel Daten.  
  
## <a name="BPSQLConfig"></a>Bewährte Methoden für SMP SQL Server-Konfiguration für die Remotetabelle kopieren  
Wenn Sie den SMP-SQL-Server zum Empfangen der Remotetabelle Kopien zu konfigurieren, verwenden Sie die folgenden bewährten Methoden zur Verbesserung der Leistung.  
  
1.  Führen Sie die bewährte Methoden, wie beschrieben in SQL Server-Produktdokumentation. Aktivieren Sie z. B. die Verschlüsselung von Daten. Weitere Informationen zum Sichern von SQL Server finden Sie unter [Sichern von SQL Server](../relational-databases/security/securing-sql-server.md) auf MSDN.  
  
2.  Verwenden Sie das massenprotokollierte oder einfache Wiederherstellungsmodell.  
  
    Während die Daten parallelen Exportvorgänge, beim Massenkopieren in die neu erstellte Zieltabelle eingefügt. Legen Sie zur Optimierung der Leistung während des masseneinfügungsvorgangs der Zieldatenbank, die massenprotokollierte Wiederherstellung verwenden oder das einfache Wiederherstellungsmodell.  
  
3.  Verwenden Sie die Batch_size-Option, um Protokollspeicherplatz freizugeben.  
  
    Obwohl die massenprotokollierte oder einfache Wiederherstellung verwenden, die minimale Protokollierung für eingelegt Massendaten modelliert, einige Protokollierung weiterhin ausgeführt. Um zu verhindern, dass die Protokolldateien zu umfangreich, verwenden Sie die SQL Server-Batch_size-Option, um in regelmäßigen Abständen wieder Protokollspeicherplatz freizugeben.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
