---
title: Arbeiten mit SQL Server-Daten mithilfe von R (SQL und R deep Dive) | Microsoft Docs
ms.date: 12/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 5cd152ac5da350b216eaf3f517d5da2d1c415a4d
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/04/2018
---
# <a name="work-with-sql-server-data-using-r-sql-and-r-deep-dive"></a>Arbeiten Sie mit SQL Server-Daten mithilfe von R (SQL und R deep Dive)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Dieser Artikel ist Teil des Lernprogramms Data Science Deep Dive zur Verwendung von ["revoscaler"](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) mit SQL Server.

In dieser Lektion Einrichten der Umgebung und Hinzufügen von Daten, die Sie benötigen für das Trainieren der Modelle und einige schnellen Zusammenfassungen der Daten ausgeführt werden. Im Rahmen des Prozesses müssen Sie diese Aufgaben ausführen:
  
- Erstellen einer neuen Datenbank zum Speichern der Daten für das Training und die Bewertung von zwei R-Modellen.
  
- Erstellen eines Kontos (entweder ein Windows-Benutzer oder ein SQL-Anmeldename), das für die Kommunikation zwischen Ihrer Arbeitsstation und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Computer verwendet wird.
  
- Erstellen von Datenquellen in R für die Arbeit mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Daten und Datenbankobjekten.
  
- Verwenden von R-Datenquellen zum Laden von Daten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Verwenden von R zum Abrufen einer Liste von Variablen und zum Ändern der Metadaten der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabelle.
  
- Erstellen eines Computekontexts zum Aktivieren von Remoteausführungen von R-Code.
  
- (Optional) Aktivieren der Ablaufverfolgung für die remote-computekontext.
  
## <a name="create-the-database-and-user"></a>Erstellen Sie die Datenbank und die Benutzer

In dieser exemplarischen Vorgehensweise erstellen Sie eine neue Datenbank in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], und fügen Sie einen SQL-Anmeldenamen mit Berechtigungen zum Schreiben und Lesen von Daten sowie zum Ausführen von R-Skripts hinzu.

> [!NOTE]
> Wenn Sie Daten nur lesen, muss das Konto, das R-Skripts ausgeführt, SELECT-Berechtigungen (**"db_datareader"** Rolle "") für die angegebene Datenbank. In diesem Lernprogramm müssen Sie allerdings DDL-Administratorrechte vorbereiten die Datenbank und zum Erstellen von Tabellen zum Speichern der bewerteten Ergebnisse verfügen.
> 
> Wenn Sie nicht der Datenbankbesitzer sind, benötigen Sie die Berechtigung EXECUTE ANY EXTERNAL SCRIPT, um R-Skripts ausführen.

1. Wählen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]die Instanz aus, bei der [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] aktiviert ist. Führen Sie einen Rechtsklick auf **Datenbanken**aus, und wählen Sie **Neue Datenbank**aus.
  
2. Geben Sie einen Namen für die neue Datenbank ein. Sie können einen beliebigen Namen verwenden, denken Sie jedoch daran, alle [!INCLUDE[tsql](../../includes/tsql-md.md)] -Skripts und R-Skripts in dieser exemplarischen Vorgehensweise dementsprechend zu bearbeiten.
  
    > [!TIP]
    > Klicken Sie mit der rechten Maustaste auf **Datenbanken** , und wählen Sie **Aktualisieren** aus, um den aktualisierten Datenbanknamen anzuzeigen.
  
3. Klicken Sie auf **Neue Abfrage**, und legen Sie die Masterdatenbank als Datenbankkontext fest.
  
4. Führen Sie im Fenster **Abfrage** die folgenden Befehle aus, um die Benutzerkonten zu erstellen und sie der Datenbank zuzuweisen, die für dieses Tutorial verwendet wird. Achten Sie darauf, den Datenbanknamen falls nötig zu ändern.
  
**Windows-Benutzer**
  
```SQL
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[DeepDive]

 --Add the new user to tutorial database
USE [DeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL-Anmeldename**

```SQL
-- Create new SQL login
USE master
GO
CREATE LOGIN DDUser01 WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE [DeepDive]
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

5. Um zu bestätigen, dass der Benutzer erstellt wurde, wählen Sie die neue Datenbank aus, und erweitern Sie **Sicherheit**und **Benutzer**.

## <a name="troubleshooting"></a>Problembehandlung

Dieser Abschnitt enthält einige häufig auftretende Probleme, denen Sie möglicherweise während der Einrichtung der Datenbank gegenüber stehen.

- **Wie kann ich die Datenbankkonnektivität und SQL-Abfragen überprüfen?**
  
    Bevor Sie R-Code mithilfe des Servers ausführen, möchten Sie möglicherweise überprüfen, ob die Datenbank über Ihre R-Entwicklungsumgebung erreicht werden kann. Sowohl [Server-Explorer in Visual Studio](https://msdn.microsoft.com/library/x603htbk.aspx) als auch [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) sind kostenlose Tools mit leistungsstarker Datenbankkonnektivität und Verwaltungsfunktionen.
  
    Wenn Sie zusätzliche Datenbankverwaltungstools installieren möchten, können Sie eine Testverbindung zur SQL Server-Instanz erstellen, indem Sie den [ODBC-Datenquellen-Administrator](https://msdn.microsoft.com/library/ms714024.aspx) in der Systemsteuerung verwenden. Wenn die Datenbank ordnungsgemäß konfiguriert ist und Sie den richtigen Benutzernamen und das richtige Kennwort eingeben, sollten Sie die zuvor von Ihnen erstellte Datenbank sehen und diese als Ihre Standarddatenbank auswählen.
  
    Wenn Sie keine Verbindung mit der Datenbank herstellen können, überprüfen Sie ob die Remoteverbindungen für den Server aktiviert sind und ob das Named Pipes-Protokoll aktiviert ist. Weitere Tipps zur Problembehandlung finden Sie in diesem Artikel: [Problembehandlung beim Verbinden mit SQL Server-Datenbankmoduls](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **Mein Tabellenname wurde mit dem Präfix DataReader versehen – warum?**
  
    Wenn Sie angeben, das Standardschema für diesen Benutzer als **"db_datareader"**, alle Tabellen und andere neue Objekte, die von diesem Benutzer erstellte vorangestellt werden die *Schema* Name. Ein Schema ist wie ein Ordner, den Sie einer Datenbank hinzufügen können, um Objekte zu organisieren. Das Schema definiert außerdem die Berechtigungen eines Benutzers in der Datenbank.
  
    Wenn das Schema einen bestimmten Benutzernamen zugeordnet ist, wird der Benutzer die _schemabesitzer_. Wenn Sie ein Objekt erstellen, müssen Sie immer es immer in Ihrem eigenen Schema erstellen, außer Sie geben ausdrücklich an, dass es in einem anderen Schema erstellt werden soll.
  
    Angenommen, Sie erstellen eine Tabelle mit dem Namen `*`TestData`, and your default schema is **db\_datareader**, the table is created with the name `.db_datareader < Datenbankname >. TestData ".
  
    Aus diesem Grund kann eine Datenbank mehrere Tabellen mit dem gleichen Namen enthalten, solange die Tabellen zu unterschiedlichen Schemas gehören.
   
    Wenn Sie eine Tabelle suchen und ein Schema nicht angeben, sucht der Datenbankserver für ein Schema, das Ihnen gehört. Daher müssen Sie keinen Schemanamen angeben, wenn Sie auf Tabellen in einem Schema zugreifen, das mit Ihrem Login verknüpft sind.
  
- **Ich verfüge über keine DDL-Berechtigungen. Kann ich weiterhin das Tutorial ausführen?**
  
    Ja. Sie müssen jedoch jemanden bitten, die Daten vorab in die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Tabellen zu laden und die Abschnitte zu überspringen, in denen Sie neue Tabellen erstellen sollen. Die Funktionen, die DDL-Administratorrechte erfordern werden im Lernprogramm möglichst hingewiesen.

    Darüber hinaus bitten Sie Ihren Administrator um die Berechtigung EXECUTE ANY EXTERNAL SCRIPT zu gewähren. Erforderlich für die Ausführung des R-Skripts, ob remote oder mithilfe von `sp_execute_external_script`.

## <a name="next-step"></a>Nächster Schritt

[Erstellen von SQL Server-Datenobjekten mithilfe von RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>Übersicht

[Tieferer Einblick in Data Science: Verwenden der RevoScaleR-Pakete](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)



