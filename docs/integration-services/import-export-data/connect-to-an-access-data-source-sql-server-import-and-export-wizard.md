---
title: Herstellen einer Verbindung mit einer Access-Datenquelle (SQL Server-Import/Export-Assistent) | Microsoft-Dokumentation
ms.custom: 
ms.date: 06/20/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b44c159a-c33d-4f3c-bdb8-9832f35317c8
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bfecde5790f25c254428d53ec613b968d7d3efd9
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-an-access-data-source-sql-server-import-and-export-wizard"></a>Herstellen einer Verbindung mit einer Access-Datenquelle (SQL Server-Import/Export-Assistent)
In diesem Artikel wird erläutert, wie Sie eine Verbindung mit einer **Microsoft Access**-Datenquelle über die Seiten **Datenquelle auswählen** oder **Ziel auswählen** des SQL Server-Import/Export-Assistenten herstellen.

Der folgende Screenshot zeigt eine Beispielverbindung mit einer Microsoft Access-Datenbank. In diesem Beispiel müssen Sie keinen Benutzernamen und kein Kennwort eingeben, da die Zieldatenbank keine Informationsdatei für die Arbeitsgruppe verwendet.

![Herstellen einer Verbindung mit Access](../../integration-services/import-export-data/media/connect-to-access.jpg)

## <a name="options-to-specify"></a>Anzugebende Optionen

> [!NOTE]
> Die Verbindungsoptionen für diesen Datenanbieter bleiben stets unverändert – egal, ob Access die Quelle oder das Ziel ist. Das bedeutet, dass die angezeigten Optionen auf den Seiten **Datenquelle auswählen** und **Ziel auswählen** des Assistenten gleich sind.

**Datenquelle**  
Die Liste der Datenanbieter kann mehrere Einträge für Microsoft Access enthalten. Wählen Sie die neueste installierte Version oder die Version aus, die der Version von Access entspricht, mit der die Datenbankdatei erstellt wurde.

|Datenquelle|Office-Version|
|-------|-------|
|Microsoft Access (Microsoft.ACE.OLEDB.16.0)|Office 2016|
|Microsoft Access (Microsoft.ACE.OLEDB.15.0)|Office 2013|
|Microsoft Access (Microsoft Access-Datenbankmodul)|Office 2010 und Office 2007|
|Microsoft Access (Microsoft Jet-Datenbankmodul)|Office-Versionen vor Office 2007|

> [!IMPORTANT]
> Sie müssen möglicherweise zusätzliche Dateien herunterladen und installieren, um eine Verbindung mit Access-Datenbanken herzustellen. Weitere Informationen finden Sie im Abschnitt [Herunterladen von Dateien zum Herstellen einer Verbindung mit Access](#officeDownloads) weiter unten auf dieser Seite.

 **Dateiname**  
Geben Sie den Pfad und den Dateinamen für die Access-Datei an. Beispielsweise **C:\\MyData.mdb** für eine Datei auf dem lokalen Computer oder **\\\\Sales\\Database\\Northwind.mdb** für eine Datei auf einer Netzwerkfreigabe. Oder klicken Sie auf **Durchsuchen**. 

 >   [!NOTE] 
 > Wenn Sie auf **Durchsuchen** klicken, um die Access-Datei zu suchen, filtert das Dialogfeld **Öffnen** standardmäßig automatisch nach Dateien mit dem älteren Format bzw. der älteren Erweiterung MDB. Der Datenanbieter kann jedoch auch Dateien mit dem neueren Format bzw. der neueren Erweiterung ACCDB öffnen.
  
 **Durchsuchen**  
 Suchen Sie die Datenbankdatei mithilfe des Dialogfelds **Öffnen**.  
  
 **Benutzername**  
Wenn eine Informationsdatei für die Arbeitsgruppe der Datenbank zugeordnet ist, geben Sie einen gültigen Benutzernamen ein.  
  
 **Kennwort**  
Wenn eine Informationsdatei für die Arbeitsgruppe der Datenbank zugeordnet ist, geben Sie ein Benutzerkennwort ein.
 
Wenn die Datenbank mit einem einzigen Kennwort für alle Benutzer geschützt ist, finden Sie weitere Informationen unter [Ist die Datenbankdatei kennwortgeschützt?](#database_password).
  
 **Erweitert**  
Geben Sie im Dialogfeld **Datenlinkeigenschaften** erweiterte Optionen an, z.B. das Datenbankkennwort oder eine nicht dem Standard entsprechende Informationsdatei für die Arbeitsgruppe.  

## <a name="i-dont-see-access-in-the-list-of-data-sources"></a>Access wird in der Liste der Datenquellen nicht angezeigt
Wenn Access nicht in der Liste der Datenquellen angezeigt wird, sollten Sie überprüfen, ob Sie die 64-Bit-Version des Assistenten verwenden. Die Anbieter für Excel und Access sind in der Regel 32-Bit-Versionen und werden in der 64-Bit-Version des Assistenten nicht angezeigt. Führen Sie stattdessen die 32-Bit-Version des Assistenten aus.

> [!NOTE]
> Sie müssen SQL Server installieren, um die 64-Bit-Version des Import/Export-Assistenten von SQL Server verwenden zu können. SQL Server Data Tools (SSDT) und SQL Server Management Studio (SSMS) sind 32-Bit-Anwendungen und installieren daher auch nur 32-Bit-Dateien, einschließlich der 32-Bit-Version des Assistenten.

## <a name="officeDownloads"></a>Herunterladen von Dateien zum Herstellen einer Verbindung mit Access  
Sie müssen möglicherweise die Konnektivitätskomponenten für Microsoft Office-Datenquellen (einschließlich Access und Excel) herunterladen, wenn diese nicht bereits installiert sind. Laden Sie die neueste Version der Konnektivitätskomponenten für Access- und Excel-Dateien hier herunter: [Microsoft Access Database Engine 2016 – Weitervertreibbare Komponente](https://www.microsoft.com/download/details.aspx?id=54920).
  
Die aktuelle Version der Komponenten dient zum Öffnen von Dateien, die in früheren Versionen von Access erstellt wurden.

Wenn der Computer über eine 32-Bit-Version von Office verfügt, müssen Sie die 32-Bit-Version der Komponenten installieren. Sie müssen zudem sicherstellen, dass Sie das Paket im 32-Bit-Modus ausführen.

Wenn Sie über ein Office 365-Abonnement verfügen, stellen Sie sicher, dass Sie die weitervertreibbare Komponente von Access Database Engine 2016 und nicht Microsoft Access 2016 Runtime herunterladen. Wenn Sie das Installationsprogramm ausführen, wird möglicherweise eine Fehlermeldung angezeigt, dass Sie den Download nicht parallel mit Klick-und-Los-Komponenten von Office installieren können. Führen Sie die Installation zur Umgehung dieser Fehlermeldung im stillen Modus durch, indem Sie ein Eingabeaufforderungsfenster öffnen und die EXE-Datei, die Sie heruntergeladen haben, mit der Befehlszeilenoption `/quiet` ausführen. Beispiel:

`C:\Users\<user name>\Downloads\AccessDatabaseEngine.exe /quiet`

## <a name="database_password"></a> Ist die Datenbankdatei kennwortgeschützt?
In einigen Fällen ist eine Access-Datenbank kennwortgeschützt, verwendet jedoch keine Informationsdatei für die Arbeitsgruppe. Alle Benutzer müssen das gleiche Kennwort angeben, es muss jedoch kein Benutzername eingegeben werden. Führen Sie zum Bereitstellen eines Datenbankkennworts die folgenden Schritte aus:

1.  Klicken Sie auf der Seite **Datenquelle auswählen** oder **Ziel auswählen** auf die Schaltfläche **Erweitert**, um das Dialogfeld **Datenlinkeigenschaften** zu öffnen.  
2.  Klicken Sie im Dialogfeld **Datenlinkeigenschaften** auf die Registerkarte **Alle**.  
3.  Klicken Sie in der Liste der Eigenschaften und Werte auf **Jet OLEDB:Database Password** (Jet-OLEDB: Datenbankkennwort).   
    
    ![Access-Kennwort festlegen, Screenshot 1](../../integration-services/import-export-data/media/specify-access-password-screen-1.jpg) 
4.  Klicken Sie auf **Wert bearbeiten**, um das Dialogfeld **Eigenschaftswert bearbeiten** zu öffnen.  
    
    ![Access-Kennwort festlegen, Screenshot 2](../../integration-services/import-export-data/media/specify-access-password-screen-2.jpg)
5.  Geben Sie im Dialogfeld **Eigenschaftswert bearbeiten** das Datenbankkennwort ein.
6.  Klicken Sie in jedem Dialogfeld auf **OK**, um zur Seite **Datenquelle auswählen** oder **Ziel auswählen** des Assistenten zurückzukehren und fortzufahren.

## <a name="keep-your-autonumber-values-when-you-export-from-access"></a>Beibehalten der automatisch nummerierten Werte beim Exportieren aus Access
Wählen Sie die Option **IDENTITY_INSERT aktivieren** im Dialogfeld **Spaltenzuordnungen** aus, um zu ermöglichen, dass in den Quelldaten vorhandene Identitätswerte in eine Identitätsspalte in der Zieltabelle eingefügt werden können. Standardmäßig ist das Eingeben von vorhandenen Werten in der Identitätsspalte des Ziels nicht zulässig. Klicken Sie auf **Zuordnungen bearbeiten**, wenn Sie die Seite **Quelltabellen und -sichten auswählen** des Assistenten erreichen, um das Dialogfeld **Spaltenzuordnungen** anzuzeigen. Weitere Informationen dazu, wie Sie diese Seiten anzeigen können, finden Sie unter [Select Source Tables and Views (Quelltabellen und -sichten auswählen)](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) und [Column Mappings (Spaltenzuordnungen)](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).

Wenn Ihre vorhandenen Primärschlüssel in einer Identity-Spalte, einer automatisch nummerierten Spalte oder einem Äquivalent enthalten sind, müssen Sie diese Option auswählen, um die vorhandenen Primärschlüsselwerte beizubehalten. Andernfalls weist die Identity-Zielspalte in der Regel neue Werte zu.

## <a name="see-also"></a>Siehe auch
[Auswählen einer Datenquelle](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Auswählen eines Ziels](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

