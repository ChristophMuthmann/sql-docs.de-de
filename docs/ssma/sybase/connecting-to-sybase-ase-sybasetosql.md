---
title: Herstellen einer Verbindung mit der Sybase ASE (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Connecting to Sybase ASE
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
caps.latest.revision: "8"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 56a6b4fcfae030a265998b5deb9f0c2407d1e1e3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/05/2017
---
# <a name="connecting-to-sybase-ase-sybasetosql"></a>Herstellen einer Verbindung mit der Sybase ASE (SybaseToSQL)
Zum Migrieren von Datenbanken von Sybase Adaptive Server Enterprise (ASE) zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, Sie müssen die Verbindung mit dem Adaptive Server mit den Datenbanken, die Sie migrieren möchten. Wenn Sie eine Verbindung herstellen, SSMA Ruft Metadaten zu allen Datenbanken auf dem Adaptive Server ab, und Sie werden Datenbankmetadaten in der Sybase-Metadaten-Explorer-Bereich angezeigt. SSMA speichert Informationen über den Datenbankserver, aber die Kennwörter werden nicht gespeichert.  
  
Die Verbindung mit ASE bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie ASE wiederherstellen, wenn Sie möchten, dass eine aktive Verbindung mit dem Server.  
  
Metadaten zu den adaptiven Server wird nicht automatisch aktualisiert. Stattdessen, wenn Sie die Metadaten in Sybase-Metadaten-Explorer aktualisieren möchten, müssen Sie manuell die Metadaten aktualisieren wie im Abschnitt "Aktualisieren von Sybase ASE Metadaten" weiter unten in diesem Thema beschrieben.  
  
## <a name="required-ase-permissions"></a>ASE erforderliche Berechtigungen  
Das Konto, mit dem Herstellen einer ASE, benötigen mindestens **öffentlichen** Zugriff auf die master-Datenbank und alle Quelldatenbanken auf migriert werden [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Um Berechtigungen für Tabellen auswählen, die migriert werden, muss der Benutzer darüber hinaus SELECT-Berechtigungen für die folgenden Systemtabellen verfügen:  
  
-   [Source_db].dbo.sysobjects  
  
-   [Source_db].dbo.syscolumns  
  
-   [Source_db].dbo.sysusers  
  
-   [Source_db].dbo.systypes  
  
-   [Source_db].dbo.sysconstraints  
  
-   [Source_db].dbo.syscomments  
  
-   [Source_db].dbo.sysindexes  
  
-   [Source_db].dbo.sysreferences  
  
-   Master.dbo.sysdatabases an  
  
## <a name="establishing-a-connection-to-ase"></a>Herstellen einer Verbindung mit ASE  
Wenn Sie eine Adaptive Server verbinden, SSMA liest die Metadaten der Datenbank auf dem Datenbankserver und fügt dann diese Metadaten in die Projektdatei. Diese Metadaten werden von SSMA verwendet, wenn die Objekte konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure-Syntax, und wenn sie Daten migriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure. Sie können diese Metadaten im Bereich Sybase-Metadaten-Explorer durchsuchen und überprüfen Sie die Eigenschaften der einzelnen Datenbankobjekte.  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung mit dem Datenbankserver herstellen, stellen Sie sicher, dass der Datenbankserver ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit der Sybase ASE**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit der Sybase**.  
  
    Wenn Sie zuvor mit Sybase verbunden, wird der Befehlsname sein **eine erneute Verbindung zu Sybase**.  
  
2.  In der **Anbieter** wählen eine der installierten Anbieter für Sybase-Server die Verbindung auf dem Computer.  
  
3.  In der **Modus** wählen **Modus "Standard"** oder **im erweiterten Modus**.  
  
    Verwenden Sie Modus "standard", um den Servernamen, Port, Benutzername und Kennwort anzugeben. Verwenden Sie im erweiterten Modus, um eine Verbindungszeichenfolge zur Verfügung stellen. Dieser Modus ist in der Regel nur für die Problembehandlung oder während der Arbeit mit dem technischen Support verwendet.  
  
4.  Bei Auswahl des **Modus "Standard"**, geben Sie die folgenden Werte:  
  
    1.  In der **Servernamen** Feld eingeben oder auswählen den Namen oder IP-Adresse des Datenbankservers.  
  
    2.  Wenn der Datenbankserver nicht konfiguriert ist, um Verbindungen zuzulassen, auf die Standardeinstellung (5000) port verwenden, geben Sie die Portnummer für die Sybase-Verbindungen in verwendeten die **Serverport** Feld.  
  
    3.  In der **Benutzername** Geben Sie ein Sybase-Konto, das die erforderlichen Berechtigungen verfügt.  
  
    4.  In der **Kennwort** Geben Sie das Kennwort für den angegebenen Benutzernamen ein.  
  
5.  Bei Auswahl des **im erweiterten Modus**, geben Sie eine Verbindungszeichenfolge in der **Verbindungszeichenfolge** Feld.  
  
    Beispiele für verschiedene Verbindungszeichenfolgen sind wie folgt aus:  
  
    1.  **Verbindungszeichenfolgen für Sybase OLE DB-Anbieter:**  
  
        Für Sybase ASE OLE DB-12,5 sehen eine Beispielverbindungszeichenfolge wie folgt:  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Für Sybase ASE OLE DB-15 weist eine Beispielverbindungszeichenfolge Folgendes:  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2.  **Die Verbindungszeichenfolge für Sybase ODBC-Anbieter:**  
  
        `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3.  **Die Verbindungszeichenfolge für Sybase ADO.NET-Anbieter:**  
  
        `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    Weitere Informationen finden Sie unter [Herstellen einer Verbindung mit der Sybase &#40; SybaseToSQL &#41; ](../../ssma/sybase/connect-to-sybase-sybasetosql.md).  
  
## <a name="reconnecting-to-sybase-ase"></a>Wiederherstellen der Verbindung mit der Sybase ASE  
Die Verbindung mit dem Datenbankserver bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit dem Adaptive Server verwendet werden soll. Sie können offline arbeiten, bis Sie verwenden möchten, aktualisieren Sie Metadaten an, und laden die Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] oder SQL Azure, und Daten migrieren.  
  
## <a name="refreshing-sybase-ase-metadata"></a>Aktualisieren von Metadaten für Sybase ASE  
Metadaten zu den Datenbanken ASE wird nicht automatisch aktualisiert. Die Metadaten in Sybase-Metadaten-Explorer ist eine Momentaufnahme der Metadaten aus, wenn Sie zuerst, die Adaptive Server oder dem letzten verbunden, dass Sie manuell die Metadaten aktualisiert werden. Sie können die Metadaten für eine einzelne Datenbank in ein einzelnes Datenbankschema oder für alle Datenbanken manuell aktualisieren.  
  
**Aktualisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit dem Adaptive Server verbunden sind.  
  
2.  Wählen Sie in der Sybase-Metadaten-Explorer das Kontrollkästchen neben der Datenbank oder das Datenbankschema, die Sie aktualisieren möchten.  
  
3.  Mit der rechten Maustaste Datenbanken, die einzelne Datenbank oder Datenbankschema, und wählen Sie dann **aus der Datenbank aktualisieren**.  
  
4.  Wenn Sie gefragt werden, um das aktuelle Objekt zu überprüfen, klicken Sie auf **Ja**.  
  
## <a name="next-step"></a>Nächster Schritt  
  
-   Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit einer Instanz von SQL Server](http://msdn.microsoft.com/en-us/dd368a1a-45b0-40e9-b4d3-5cdb48c26606) / [Herstellen einer Verbindung mit einer Instanz von SQL Azure](http://msdn.microsoft.com/en-us/9e77e4b0-40c0-455c-8431-ca5d43849aa7)  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Sybase ASE-Datenbanken zu SQLServer - Azure SQL-Datenbank &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
