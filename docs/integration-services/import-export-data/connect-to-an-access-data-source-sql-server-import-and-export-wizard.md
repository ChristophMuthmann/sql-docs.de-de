---
title: Herstellen einer Verbindung mit einer Access-Datenquelle (SQL Server-Import / Export-Assistent) | Microsoft Docs
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: 71bb3914e31259bc95a1116c2db03708c0442e8c
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Access-Datenquelle (SQL Server-Import / Export-Assistent)
Dieses Thema veranschaulicht das Herstellen von Verbindungen ein **Microsoft Access** Datenquelle aus der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf der Seite der SQL Server-Import / Export-Assistenten.

Der folgende Screenshot zeigt eine Beispielverbindung mit einer Microsoft Access-Datenbank. In diesem Beispiel müssen Sie einen Benutzernamen und Kennwort eingeben, da die Zieldatenbank eine Informationsdatei nicht verwendet.

![Herstellen einer Verbindung mit Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Optionen zum Festlegen

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter sind identisch, ob der Zugriff auf die Quelle oder Ziel ist. D. h. die Optionen finden Sie unter sind für beide die **wählen Sie eine Datenquelle** und **wählen Sie ein Ziel** Seiten des Assistenten.

**Datenquelle**  
Die Liste der Datenanbieter kann mehrere Einträge für Microsoft Access enthalten. Wählen Sie die neueste installierte Version oder die Version, die der Access-Version entspricht, die die Datenbank erstellt.

|Datenquelle|Office-version|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Microsoft Access-Datenbankmodul)|Office 2010 und Office 2007|
|Microsoft Access (Microsoft Jet-Datenbankmodul)|Office-Versionen vor Office 2007|

> [!IMPORTANT]
> Sie müssen möglicherweise zusätzliche Dateien für die Verbindung mit Access-Datenbanken herunterladen und installieren. Finden Sie unter [erhalten Sie die Dateien müssen Sie für die Verbindung für den Zugriff auf](#officeDownloads) auf dieser Seite finden Sie weitere Informationen.

 **Dateiname**  
Geben Sie den Pfad und Namen für die Access-Datei. Beispielsweise **"c:"\\MyData.mdb** für eine Datei auf dem lokalen Computer oder  **\\ \\Sales\\Datenbank\\Northwind.mdb** für eine Datei auf einer Netzwerkfreigabe. Oder klicken Sie auf **Durchsuchen**. 

 >   [!NOTE] 
 > Wenn Sie auf **Durchsuchen** , suchen Sie die Access-Datei, die **öffnen** Dialogfeld Feld Filter für Dateien mit dem älteren. MDB-Format und Datei-Erweiterung standardmäßig. Der Datenanbieter kann jedoch auch Dateien mit der neueren öffnen. Formate ACCDB und Erweiterung.
  
 **Durchsuchen**  
 Suchen Sie die Datenbankdatei mithilfe des Dialogfelds **Öffnen**.  
  
 **Benutzername**  
Wenn eine Informationsdatei der Datenbank zugeordnet ist, geben Sie einen gültigen Benutzernamen ein.  
  
 **Kennwort**  
Wenn eine Informationsdatei der Datenbank zugeordnet ist, geben Sie das Kennwort des Benutzers hier ein.
 
Wenn die Datenbank mit einem einzigen Kennwort für alle Benutzer geschützt ist, finden Sie unter [wird die Datenbankdatei ein Kennwort geschützt?](#database_password).
  
 **Erweitert**  
Legen Sie erweiterte Optionen, z. B. das Datenbankkennwort oder eine nicht standardmäßige Informationsdatei der **Datenlinkeigenschaften** (Dialogfeld).  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Ich nicht Zugriff in der Liste der Datenquellen angezeigt.
Wenn Sie den Zugriff in der Liste der Datenquellen nicht angezeigt wird, werden Sie die 64-Bit-Assistent ausgeführt? Die Anbieter für Excel und Access sind in der Regel 32-Bit- und nicht in der 64-Bit-Assistent angezeigt. Führen Sie stattdessen den 32-Bit-Assistenten.

> [!NOTE]
> Um die 64-Bit-Version von den SQL Server-Import / Export-Assistenten verwenden zu können, müssen Sie SQL Server installieren. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen, und nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten installieren.

## <a name="officeDownloads"></a>Rufen Sie die Verbindung für den Zugriff auf benötigte Dateien ab  
Sie müssen möglicherweise herunterladen die Konnektivitätskomponenten für Microsoft Office-Datenquellen, einschließlich Access und Excel, sofern diese nicht bereits installiert sind. Die neueste Version der datenkonnektivitätskomponenten für Access und Excel-Dateien hier herunterladen: [Microsoft Access Database Engine 2016 Redistributable](https://www.microsoft.com/download/details.aspx?id=54920).
  
Die neueste Version der Komponenten kann von früheren Versionen von Access erstellte Dateien öffnen.

Verfügt der Computer eine 32-Bit-Version von Office, dann müssen Sie die 32-Bit-Version der Komponenten zu installieren, und außerdem müssen Sie sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie Access-Datenbank-Engine 2016 Redistributable und nicht die Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, sehen Sie eine Fehlermeldung angezeigt, dass Sie die Download-Seite-an-Seite mit den Office-Klick-und-Los-Komponenten installieren können. Um diese Fehlermeldung umgehen, führen Sie die Installation im stillen Modus, indem Sie ein Eingabeaufforderungsfenster öffnen und Ausführen der. EXE-Datei, die Sie heruntergeladen, mit der `/quiet` wechseln. Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a>Wird die Datenbankdatei ein Kennwort geschützt?
In einigen Fällen eine Access-Datenbank ein Kennwort geschützt ist, aber eine Informationsdatei ist nicht verwenden. Alle Benutzer müssen dasselbe Kennwort angeben, aber Sie müssen einen Benutzernamen eingeben. Um ein Datenbankkennwort bereitzustellen, führen Sie folgende Schritte aus.

1.  Auf der **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** auf die **erweitert** die Schaltfläche, um die **Datenlinkeigenschaften** (Dialogfeld).  
2.  In der **Datenlinkeigenschaften** wählen Sie im Dialogfeld die **alle** Registerkarte.  
3.  Wählen Sie in der Liste der Eigenschaften und Werte, **Jet OLEDB: Database Password**.   
    
    ![Geben Sie Zugriffskennwort, Bildschirm 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Klicken Sie auf **Wert bearbeiten** So öffnen die **Eigenschaftswert bearbeiten** (Dialogfeld).  
    
    ![Geben Sie Zugriffskennwort, (Bildschirm 2)](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  In der **Eigenschaftswert bearbeiten** Dialogfeld Geben Sie das Datenbankkennwort.
6.  Klicken Sie auf **OK** in jedem Dialogfeld, um wieder die **wählen Sie eine Datenquelle** oder **wählen Sie ein Ziel** Seite des Assistenten und den Vorgang fortzusetzen.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Behalten Sie beim Exportieren von Access AutoWert-Werten
Damit vorhandene Identity-Werte in den Quelldaten in eine Identity-Spalte in der Zieltabelle eingefügt werden können, wählen Sie die **IDENTITY_INSERT aktivieren** -Option in der **Spaltenzuordnungen** (Dialogfeld). Standardmäßig ist nicht die Identity-Zielspalte in der Regel vorhandene Werte einfügen kann. Zum Anzeigen der **Spaltenzuordnungen** wählen Sie im Dialogfeld **Zuordnungen bearbeiten** Sie beim Erreichen der **wählen Quelltabellen und-Sichten** Seite des Assistenten. Um diese Seiten anzuzeigen, finden Sie unter [wählen Quelltabellen und-Sichten](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) und [Spaltenzuordnungen](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Wenn Ihre vorhandenen Primärschlüssel in einer Identity-Spalte, einer automatisch nummerierten Spalte oder einem Äquivalent enthalten sind, müssen Sie diese Option auswählen, um die vorhandenen Primärschlüsselwerte beizubehalten. Andernfalls weist die Identity-Zielspalte in der Regel neue Werte zu.

## <a name="see-also"></a>Siehe auch
[Wählen Sie eine Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Wählen Sie ein Ziel](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


