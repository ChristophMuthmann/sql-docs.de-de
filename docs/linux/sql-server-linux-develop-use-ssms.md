---
title: Verwalten von SQLServer on Linux mit SSMS | Microsoft Docs
description: "Dieses Lernprogramm zeigt, wie SQL Server Management Studio unter Windows zur Verbindung mit SQL Server auf dem Linux ausgeführt wird."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 30cc4564-f389-4707-9b25-8ba782cc5150
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: b4e70106782541d771a2539d025a0a6dd75c34d9
ms.contentlocale: de-de
ms.lasthandoff: 10/02/2017

---
# <a name="use-sql-server-management-studio-ssms-on-windows-to-manage-sql-server-on-linux"></a>Verwenden Sie SQL Server Management Studio (SSMS) zum Verwalten von SQL Server on Linux unter Windows

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

In diesem Thema zeigt, wie [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) zur Verbindung mit SQL Server-2017 unter Linux. SSMS ist eine Windows-Anwendung, daher SSMS verwenden, wenn Sie einen Windows-Computer verfügen, der mit einer SQL Server-Remoteinstanz unter Linux eine Verbindung herstellen können.

Nachdem die Verbindung erfolgreich hergestellt, führen Sie eine einfache Transact-SQL (T-SQL)-Abfrage, um die Kommunikation mit der Datenbank zu überprüfen.

## <a name="install-the-newest-version-of-sql-server-management-studio"></a>Installieren Sie die neueste Version von SQL Server Management Studio

Bei der Arbeit mit SQL Server sollten Sie immer die neueste Version von SQL Server Management Studio (SSMS) verwenden. Die neueste Version von SSMS wird laufend aktualisiert und optimiert und arbeitet zurzeit mit SQLServer 2017 on Linux. Zum Herunterladen und installieren Sie die neueste Version, finden Sie unter [Herunterladen von SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Um auf dem neuesten Stand zu bleiben, die neueste Version von SSMS werden Sie aufgefordert, wenn eine neue Version für den download verfügbaren vorhanden ist. 

## <a name="connect-to-sql-server-on-linux"></a>Herstellen einer Verbindung mit SQLServer on Linux

Die folgenden Schritte zeigen, Herstellen einer Verbindung mit SQL Server-2017 unter Linux mit SSMS.

1. Starten Sie SSMS, geben Sie **Microsoft SQL Server Management Studio** in Windows-Suchfeld ein, und klicken Sie dann auf den desktop-app.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png)

2. In der **Verbindung mit Server herstellen** Fenster, geben Sie die folgenden Informationen (wenn SSMS bereits ausgeführt wird, klicken Sie auf **verbinden > Datenbankmodul** öffnen die **Verbindung mit Server herstellen** Fenster):

   | Einstellung | Description |
   |-----|-----|
   | **Servertyp** | Der Standardwert ist-Datenbankmoduls. Ändern Sie diesen Wert nicht. |
   | **Servername** | Geben Sie den Namen des Ziel-Linux SQL Server-Computer oder die IP-Adresse ein. |
   | **Authentifizierung** | Verwenden Sie für SQL Server 2017 unter Linux **SQL Server-Authentifizierung**. |
   | **Anmeldename** | Geben Sie den Namen eines Benutzers mit Zugriff auf eine Datenbank auf dem Server (z. B. die Standardeinstellung **SA** Konto während des Setups erstellt). |
   | **Kennwort** | Geben Sie das Kennwort für den angegebenen Benutzer (für die **SA** Konto Sie dies beim Setup erstellt wurde). |

    ![SQL Server Management Studio: Eine Verbindung mit SQL-Datenbankserver](./media/sql-server-linux-develop-use-ssms/connect.png)

3. Klicken Sie auf **Verbinden**.

    > [!TIP]
    > Wenn Sie einen Verbindungsfehler erhalten, versuchen Sie zunächst das Problem aus der Fehlermeldung zu ermitteln. Überprüfen Sie anschließend die [Empfehlungen zur Verbindungsproblembehandlung](sql-server-linux-troubleshooting-guide.md#connection).
 
5. Nach der erfolgreichen verbindungsherstellung mit Ihrem SQL Sever **Objekt-Explorer** wird geöffnet, und Sie können jetzt die Datenbank für administrative Aufgaben oder Abfragen von Daten zugreifen.
 
     ![Objekt-explorer](./media/sql-server-linux-develop-use-ssms/object-explorer.png)
     
## <a name="run-sample-queries"></a>Führen Sie Beispielabfragen

Nachdem Sie eine Verbindung mit dem Server herstellen, können Sie mit einer Datenbank verbinden und eine Beispielabfrage ausführen. Wenn Sie zum Schreiben von Abfragen nicht vertraut sind, finden Sie unter [Schreiben von Transact-SQL-Anweisungen](../t-sql/tutorial-writing-transact-sql-statements.md).

1. Identifizieren Sie eine Datenbank zu verwenden, um eine Abfrage auszuführen. Dies ist möglicherweise eine neue Datenbank, die Sie erstellt, in haben der [Transact-SQL-Lernprogramm](../t-sql/tutorial-writing-transact-sql-statements.md). Oder es ist möglicherweise die **AdventureWorks** Beispiel-Datenbank, die Sie [heruntergeladen und wiederhergestellt](sql-server-linux-migrate-restore-database.md).
2. In **Objekt-Explorer**, navigieren Sie in die Zieldatenbank auf dem Server.
2. Mit der rechten Maustaste in der Datenbank, und wählen Sie dann **neue Abfrage**:

    ![Neue Abfrage. Herstellen einer Verbindung mit SQL-Datenbankserver: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/new-query.png)

3. Schreiben Sie in das Abfragefenster ein eine Transact-SQL-Abfrage zur Auswahl von Daten aus einer der Tabellen ein. Das folgende Beispiel wählt Daten aus der **Production.Product** Tabelle mit den **AdventureWorks** Datenbank.

        SELECT TOP 10 Name, ProductNumber
        FROM Production.Product
        ORDER BY Name ASC

4. Klicken Sie auf die **Execute** Schaltfläche:

    ![Erfolg. Herstellen einer Verbindung mit SQL-Datenbankserver: SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/execute-query.png)

## <a name="next-steps"></a>Nächste Schritte

Zusätzlich zu Abfragen können Sie T-SQL-Anweisungen zum Erstellen und Verwalten von Datenbanken.

Wenn Sie noch nicht in T-SQL vertraut sind, finden Sie unter [Lernprogramm: Schreiben von Transact-SQL-Anweisungen](../t-sql/tutorial-writing-transact-sql-statements.md) und [Transact-SQL-Referenz (Datenbankmodul)](https://msdn.microsoft.com/library/bb510741.aspx).

Weitere Informationen zum Verwenden von SSMS finden Sie unter [Verwenden von SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx).

