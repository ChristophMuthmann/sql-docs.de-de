---
title: Exportieren eine Access-Inventur (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
caps.latest.revision: "18"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5d4c6fb051f37d02875070eeef6709cba84ae452
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Exportieren eine Access-Inventur (AccessToSQL)
Wenn Sie mehrere Access-Datenbanken verfügen und Sie nicht sicher, welche Informationen zum Migrieren sind in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], können Sie ein Inventar aller Access-Datenbanken in einem Projekt exportieren. Sie können anschließend überprüfen und Fragen Sie die Metadaten Inventar, um zu bestimmen, welche Datenbanken und Objekte innerhalb dieser Datenbanken migrieren. Diese Inventur können Sie schnell beantwortet Fragen, wie die folgenden:  
  
-   Was sind die größten Datenbanken?  
  
-   Wer besitzt die meisten Datenbanken?  
  
-   Welche Datenbanken enthalten die gleichen Tabellen?  
  
-   Welche Datenbanken in den letzten sechs Monaten nicht geändert wurden?  
  
-   Welche Datenbanken private Informationen enthalten?  
  
Beispiele für Abfragen, die verwendet werden, zum Beantworten dieser Fragen werden am Ende dieses Themas bereitgestellt.  
  
## <a name="exported-metadata"></a>Exportierten Metadaten  
SSMA exportiert Metadaten über die Access-Datenbanken, Tabellen, Spalten, Indizes, Fremdschlüssel, Abfragen, Berichte, Formulare, Makros und Module. Metadaten zu jeder dieser Kategorien von Elementen wird in einer separaten Tabelle exportiert. Schemas dieser Tabellen finden Sie unter [Zugriff Inventur Schemas](http://msdn.microsoft.com/en-us/fdd3cff2-4d62-4395-8acf-71ea8f17f524).  
  
## <a name="exporting-inventory-data"></a>Exportieren von Inventurdaten  
Um eine Inventur Zugriff zu exportieren, müssen Sie zum ersten Mal öffnen oder erstellen SSMA-Projekt und fügen Sie dann auf die Access-Datenbank, die Sie analysieren möchten. Nachdem Sie Datenbanken zu einem SSMA-Projekt hinzugefügt haben, exportieren Sie Metadaten zu diesen Datenbanken mit einem angegebenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank und Schema. Bei Bedarf erstellt SSMA Tabellen zum Speichern der Metadaten. SSMA fügt dann die Metadaten über die Access-Datenbanken, um die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Datenbank.  
  
> [!NOTE]  
> Eine Access-Datenbank kann in mehrere Dateien aufgeteilt werden: ein Back-End-Datenbank, die Tabellen und Front-End-Datenbanken, Abfragen, Formulare, Berichte, Makros, Module und Verknüpfungen enthalten, enthält. Wenn Sie eine Teilung Datenbank migrieren möchten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA die Front-End-Datenbank hinzufügen.  
  
Im folgenden wird beschrieben, wie Sie ein Projekt erstellen, Datenbanken zum Projekt hinzufügen, Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und klicken Sie dann Inventardaten.  
  
**Zum Erstellen eines Projekts**  
  
1.  Öffnen Sie SSMA für Access.  
  
2.  Wählen Sie im Menü **Datei** die Option **Neues Projekt** aus.  
  
    Das Dialogfeld **Neues Projekt** wird angezeigt.  
  
3.  In der **Namen** Geben Sie einen Namen für das Projekt.  
  
4.  In der **Speicherort** Feld, geben Sie ein oder wählen Sie einen Ordner für das Projekt.  
  
5.  In der **Migrieren zu** Kombinationsfeld wählen die Zielversion, die Sie migrieren, und klicken Sie dann auf möchten **OK**.  
  
Weitere Informationen zum Erstellen von Projekten finden Sie unter [erstellen und Verwalten von Projekten](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7).  
  
**Suchen und Hinzufügen von Datenbanken**  
  
1.  Auf der **Datei** Menü klicken Sie auf **Datenbanken suchen**.  
  
2.  Geben Sie im Assistenten Datenbanken finden Sie das Laufwerk, Dateipfad oder den UNC-Pfad, den Sie suchen möchten. Klicken Sie alternativ auf **Durchsuchen** auf den Laufwerk oder Ordner auswählen.  
  
3.  Klicken Sie auf **hinzufügen** auf den Speicherort in das Listenfeld hinzufügen.  
  
    Wiederholen Sie die vorherigen beiden Schritte zum Hinzufügen von zusätzlichen Speicherorten.  
  
4.  Fügen Sie Suchkriterien, um die Liste der Datenbanken zu optimieren, die zurückgegeben werden.  
  
    > [!IMPORTANT]  
    > Die **alle oder einen Teil des Dateinamens** Textfeld unterstützt keine Platzhalterzeichen enthalten.  
  
5.  Klicken Sie auf **Scan**.  
  
    Die Seite "Überprüfung" wird angezeigt. Dies zeigt die Datenbanken, die gefunden wurden, und den Fortschritt der Suche. Um die Suche zu beenden, klicken Sie auf **beenden**.  
  
6.  Wählen Sie auf der Seite "Dateien auswählen" die jede Datenbank, die Sie dem Projekt hinzufügen möchten.  
  
    Können Sie die **Alles markieren** und **alle löschen** Schaltflächen am oberen Rand der Liste aktivieren oder deaktivieren Sie alle Datenbanken. Sie können die STRG-Taste gedrückt, um mehrere Zeilen auswählen, oder halten Sie die UMSCHALTTASTE gedrückt abwärts bis zu einem Bereich von Zeilen.  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Klicken Sie auf der Seite "Überprüfen" auf **Fertig stellen**.  
  
Weitere Informationen zum Hinzufügen von Datenbanken zu Projekten finden Sie unter [hinzufügen und Entfernen von Access-Datenbankdateien](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
**Verbindung mit SQL Server**  
  
1.  Auf der **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit SQL Server**.  
  
2.  Klicken Sie im Dialogfeld "Verbindung" eingeben, oder wählen Sie den Namen der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf dem lokalen Computer herstellen, geben Sie **"localhost"** oder einen Punkt (**.**).  
  
    -   Wenn Sie eine Verbindung mit der Standardinstanz auf einem anderen Computer herstellen, geben Sie den Namen des Computers aus.  
  
    -   Wenn Sie eine Verbindung mit einer benannten Instanz herstellen, geben Sie den Computernamen, einen umgekehrten Schrägstrich und den Instanznamen. Zum Beispiel: MyServer\MyInstance.  
  
3.  In der **Datenbank** Geben Sie den Namen der Zieldatenbank für die exportierten Metadaten.  
  
4.  Wenn die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] konfiguriert ist auf einen nicht standardmäßigen Port Clientverbindungen akzeptiert werden, geben die Portnummer für die verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Verbindungen in der **Serverport** Feld. Für die Standardinstanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], die Standardportnummer ist 1433. Für benannte Instanzen SSMA versucht, erhalten die Portnummer der [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Browser-Dienst.  
  
5.  In der **Authentifizierung** Dropdown-Menü Wählen Sie den Authentifizierungstyp, der für die Verbindung verwendet. Um die aktuelle Windows-Konto verwenden möchten, wählen **Windows-Authentifizierung**. Verwenden einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Anmeldung wählen **SQL Server-Authentifizierung**, und geben Sie dann einen Benutzernamen und ein Kennwort.  
  
Weitere Informationen zum Verbinden mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], finden Sie unter [Herstellen einer Verbindung mit SQL Server &#40; AccessToSQL &#41; ](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**So exportieren Sie Inventurinformationen**  
  
1.  Erweitern Sie im Metadaten-Explorer für den Zugriff, **Zugriff Metabasis**.  
  
2.  Aktivieren Sie das Kontrollkästchen neben **Datenbanken**.  
  
    Um einzelne Datenbanken oder Datenbankobjekte weglassen, erweitern Sie die **Datenbanken** Ordner, und deaktivieren Sie dann das Kontrollkästchen neben der Datenbank oder ein Datenbankobjekt.  
  
3.  Mit der rechten Maustaste **Datenbanken** , und wählen Sie **Schema exportieren**.  
  
4.  In der **Schema auswählen, für den Export** (Dialogfeld), wählen Sie das Zielschema für die exportierten Metadaten, und klicken Sie dann auf **OK**.  
  
Bei jedem Exportieren von Metadaten, die Daten mit dem Bestand SSMA angefügt. Vorhandene Daten bei der Inventur nicht aktualisiert oder gelöscht wird.  
  
## <a name="querying-the-exported-metadata"></a>Die exportierte Metadaten Abfragen  
Nachdem Sie Metadaten über die Access-Datenbanken exportiert haben, können Sie die Metadaten Abfragen. Die folgenden Anweisungen beschreiben das Abfrage-Editor-Fenster in Verwendung [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] zum Ausführen von Abfragen.  
  
**Zum Abfragen von Metadaten**  
  
1.  Aus der **starten** Startmenü nacheinander auf **Programme**, zeigen Sie auf **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005** oder **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008** oder **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012**, und klicken Sie dann auf **SQL Server Management Studio**.  
  
2.  In der **Verbindung mit Server herstellen** (Dialogfeld), überprüfen Sie die Einstellungen, und klicken Sie dann auf **verbinden**.  
  
3.  Klicken Sie auf der Symbolleiste von Management Studio auf **neue Abfrage** Abfrage-Editor geöffnet.  
  
4.  Geben Sie im Fenster Abfrage-Editor eine Abfrage aus. Im folgenden Abschnitt werden einige Beispiele gezeigt.  
  
5.  Drücken Sie die F5-Taste, um die Abfrage auszuführen.  
  
## <a name="query-examples"></a>Beispiele für Abfragen  
Bevor Sie einen der folgenden Abfragen ausführen, führen Sie eine Verwendung *Database_name* Abfrage, um sicherzustellen, dass für die Datenbank, die die exportierte Metadaten enthält die Abfragen ausgeführt werden. Z. B. Wenn Sie Metadaten in einer Datenbank mit dem Namen MyAccessMetadata exportiert, Hinzufügen der folgenden am Anfang der [!INCLUDE[tsql](../../includes/tsql_md.md)] Code:  
  
```  
USE MyAccessMetadata;  
GO  
```  
Verwenden Sie die folgenden Beispiele, die alle die **Dbo** Schema. Wenn Sie die Metadaten in ein anderes Schema exportiert haben, stellen Sie sicher, das Schema zu ändern, wenn Sie diese Abfragen ausführen.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>Welche Tabellen und Spalten sind in diesen Datenbanken?  
Die folgende Abfrage verknüpft die Tabellen, die Spalten, Tabellen- und Datenbank-Metadaten enthalten, und klicken Sie dann die Namen aller Datenbanken, Tabellen und Spalten, sortiert nach dem Spaltennamen zurückgegeben:  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>Was sind die größten Datenbanken?  
Die folgende Abfrage gibt den Datenbanknamen, die Dateigröße und die Anzahl von Tabellen in jeder Access-Datenbank, sortiert nach Größe:  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>Wer ist der Besitzer der meisten Datenbanken?  
Die folgende Abfrage gibt den Datenbanknamen und den Besitzer der einzelnen Access-Datenbanken, sortiert nach Besitzer an.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>Welche Datenbanken enthalten die gleichen Tabellen?  
Die folgende Abfrage wird eine Unterabfrage verwendet, um alle Tabellennamen zu finden, die mehr als einmal in der Liste der Tabellen angezeigt werden, und klicken Sie dann diese Liste von Tabellen verwendet, um den Datenbanknamen abzurufen. Die Ergebnisse werden als Name der Datenbank, und klicken Sie dann den Tabellennamen zurückgegeben und anhand des Tabellennamens sortiert werden.  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>Welche Datenbanken in den letzten sechs Monaten nicht geändert wurden?  
Die folgende Abfrage ruft das aktuelle Datum ab, ruft den Wert des Monats für sechs Monate vor und gibt dann eine Liste von Datenbanken mit einem Änderungsdatum von mehr als sechs Monaten vor.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>Welche Datenbanken private Informationen enthalten?  
Access-Datenbanken möglicherweise vertrauliche oder persönliche Informationen enthalten. Möglicherweise möchten Sie diese Datenbanken verschieben [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] seine Sicherheitsfunktionen zu nutzen. Wenn Sie wissen, dass Spalten mit vertraulichen Daten einen bestimmten Namen haben, oder Sonderzeichen enthalten, können Sie eine Abfrage, um alle Spalten zu suchen, die diese Informationen enthalten. Beispielsweise finden Sie alle Spalten, die die Zeichenfolge "Gehalt".  Die Abfrage gibt dann den Datenbanknamen, Tabellennamen und Spaltennamen.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
Wenn Sie den Spaltennamen nicht kennen, können Sie eine Abfrage aus, um alle Spalten zurückgeben schreiben. Entfernen Sie zu diesem Zweck die WHERE-Klausel aus der vorherigen Abfrage.  
  
## <a name="see-also"></a>Siehe auch  
[Access-Datenbanken vorbereitet für die Migration.](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
