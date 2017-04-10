---
title: "R-Interoperabilit&#228;t in SQL Server-R-Dienste | Microsoft Docs"
ms.custom: ""
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0506b950-34b3-4f11-8e2f-d067a58015bd
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# R-Interoperabilit&#228;t in SQL Server-R-Dienste

Dieses Thema konzentriert sich auf den Mechanismus zum Ausführen für R in [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], und beschreibt die Unterschiede zwischen Microsoft R und open-Source-R. Informationen über zusätzliche Komponenten finden Sie unter [neue Komponenten in SQL Server](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md).

### Open-Source-R-Komponenten

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] enthält eine vollständige Verteilung Basis R-Pakete und Tools. Weitere Informationen, was die Basis-Verteilung enthalten ist finden Sie unter der Dokumentation, die während der Installation die folgenden standardmäßigen Speicherort installiert:
`C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES\doc\manual`

Im Rahmen der Installation von [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], müssen Sie die Begriffe der öffentlichen GNU-Lizenz bekommen. Anschließend können Sie standard-R-Pakete ohne weitere Änderung ausführen, wie in anderen open-Source-Verteilung von R.

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] die R-Runtime in keiner Weise werden nicht geändert werden. Die R-Laufzeit ausgeführt wird, außerhalb von den [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] verarbeitet und kann ausgeführt werden, unabhängig von [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Jedoch wird dringend empfohlen, diese Tools verwenden, während Sie nicht ausgeführt werden [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R, verwendet wird, um Ressourcenkonflikte zu vermeiden.

Der R-Basispaket-Verteilung, die mit einem bestimmten verknüpft ist [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Instanz finden Sie in den Ordner mit der Instanz verknüpft. Z. B. Wenn Sie R-Dienste auf der Standardinstanz installiert haben, die R-Bibliotheken befinden sich im `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`.

Auf ähnliche Weise die R-Tools, die die Standardinstanz zugeordnet würde in befinden `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`,

Weitere Informationen über die Basis-Verteilung finden Sie unter [in Microsoft R Open installierte Pakete](https://mran.revolutionanalytics.com/rro/installed/)

### Zusätzliche R-Pakete

Neben der Basis R-Verteilung [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] umfasst einige proprietären R-Pakete sowie ein Framework für die parallele Ausführung von R und Bibliotheken, die Ausführung von R in remote Compute Kontexten zu unterstützen. 

Diese kombinierte Funktionssatz R - R-Basis-Verteilung sowie verbesserte R-Funktionen und Pakete - genannt wird **Microsoft R**. Wenn Sie Microsoft-R-Server (eigenständig) installieren, erhalten Sie genau den gleichen Satz von Paketen, die mit SQL Server-R-Services (In der Datenbank), aber in einem anderen Ordner installiert werden. 

Microsoft R enthält eine Verteilung von Intel Math Kernel-Bibliothek, die nach Möglichkeit für schnellere mathematische Verarbeitung verwendet wird. Beispielsweise ist die einfache lineare Algebra (BLAS)-Bibliothek für viele der Add-on-Pakete als auch von R selbst verwendet. Weitere Informationen finden Sie in diesen Artikeln:

+ [Wie Sie R beschleunigt der Intel mathematische Kernel](http://blog.revolutionanalytics.com/2014/10/revolution-r-open-mkl.html)
+ [Die Leistungsvorteile von R multithreaded mathematische Bibliotheken verknüpfen](http://blog.revolutionanalytics.com/2010/06/performance-benefits-of-multithreaded-r.html)

Zu den wichtigsten Ergänzungen zu Microsoft R gehören die **RevoScaleR** und **RevoPemaR** Pakete. Dies sind die R-Pakete, die für eine bessere Leistung größtenteils in C oder C++ geschrieben wurden.

+ **RevoScaleR.** Enthält eine Reihe von APIs für die Bearbeitung von Daten und Analyse. Die APIs wurden optimiert, um Datensätze zu analysieren, die zu groß, um in den Arbeitsspeicher passen und Berechnungen über mehrere Kerne oder Prozessoren verteilt auszuführen sind.

   Die RevoScaleR-APIs unterstützen auch arbeiten mit Teilmengen von Daten für größere Skalierbarkeit. Anders gesagt können die meisten RevoScaleR Funktionen für Segmente der Daten und die verwenden Algorithmen so aggregieren Sie Ergebnisse aktualisieren ausgeführt werden. Daher R Projektmappen auf Grundlage der RevoScaleR Funktionen können mit sehr großen Datenmengen arbeiten und nicht durch den lokalen Arbeitsspeicher gebunden sind.

  Das RevoScaleR-Paket unterstützt auch die. XDF-Dateiformat für schnellere Bewegung und Speicherung von Daten, die für die Analyse verwendet. Das Format XDF spaltenweise Speicherung verwendet, ist übertragbar und laden und ändern dann Daten aus verschiedenen Quellen, z. B. Text, SPS oder eine ODBC-Verbindung verwendet werden kann. Ein Beispiel zum Verwenden der XDF-Format finden Sie in diesem Lernprogramm: [Data Science Deep Dive](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)


+ **RevoPemaR.** PEMA steht für parallelen Algorithmus für den externen Speicher. Die **RevoPemaR** bietet APIs, die Sie verwenden können, um eigene parallelen Algorithmen zu entwickeln. Weitere Informationen finden Sie unter [RevoPemaR Getting Started Guide](https://msdn.microsoft.com/microsoft-r/rserver/rserver-pemar-getting-started).

## Siehe auch
[Übersicht über die Architektur](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)

[Neue Komponenten in SQLServer zur Unterstützung von R-Dienste](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md)

[Sicherheitsübersicht](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md)
