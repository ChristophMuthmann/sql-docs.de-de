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
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b2a5deb6e6ec95e6f6707abe9ad85374b2334e05
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
> Sie müssen möglicherweise zum Herunterladen und installieren zusätzliche Dateien für die Verbindung der Access-Version, die Sie auswählen. Finden Sie unter [erhalten Sie die Dateien müssen Sie für die Verbindung für den Zugriff auf](#officeDownloads) auf dieser Seite finden Sie weitere Informationen.

Wenn Sie ein Problem bei der Angabe einer Version haben, geben Sie eine andere Version, auch eine frühere Version. Beispielsweise können Sie nicht in der Lage, Office 2016-Datenanbieter installiert werden, da Sie ein Microsoft Office 365-Abonnement besitzen. Sie können den Datenanbieter für 2016 Access und Excel 2016 nur mit einer desktop-Version von Microsoft Office installieren. In diesem Fall können Sie Access 2013 statt Zugriff 2016 angeben. Die beiden Versionen des Anbieters sind funktional äquivalent. Diese Einschränkung von der Laufzeit Office 2016 gemäß [diesem Blogbeitrag](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

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
  
## <a name="officeDownloads"></a>Rufen Sie die Verbindung für den Zugriff auf benötigte Dateien ab  
Sie müssen möglicherweise herunterladen die Konnektivitätskomponenten für Microsoft Office-Datenquellen, einschließlich Excel- und Access, sofern diese nicht bereits installiert sind.

Spätere Versionen der Komponenten dienen zum Öffnen von Dateien, die in früheren Versionen der Programme erstellt wurden. In vielen Fällen können frühere Versionen der Komponenten auch höhere Versionen der Programme erstellte Dateien öffnen. Z. B. Wenn Sie die Office 2016-Komponenten installieren können, verwenden Sie die Office 2013-Komponenten stattdessen. Die beiden Versionen des Anbieters sind funktional äquivalent. Diese Einschränkung von der Laufzeit Office 2016 gemäß [diesem Blogbeitrag](https://blogs.office.com/2015/12/16/access-2016-runtime-is-now-available-for-download/).

Wenn der Computer eine 32-Bit-Version von Office hat-dies normal, selbst auf 64-Bit-Computer ist – müssen Sie die 32-Bit-Version der Komponenten zu installieren. Sie müssen auch sicherstellen, dass Sie den 32-Bit-Assistenten ausführen, oder führen Sie das SQL Server Integration Services-Paket, das der Assistent im 32-Bit-Modus erstellt.

|Microsoft Office-Version|Herunterladen|  
|------------------------------|--------------|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2007|[2007 Office System-Treiber: Datenkonnektivitätskomponenten](https://www.microsoft.com/download/details.aspx?id=23734)|    

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


