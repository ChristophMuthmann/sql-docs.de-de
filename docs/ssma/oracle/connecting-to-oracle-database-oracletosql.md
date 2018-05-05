---
title: Herstellen einer Verbindung mit Oracle-Datenbank (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Refreshing Oracle Metadata
ms.assetid: e276cdbf-3ebc-4ba8-b40d-a7a42befa2b6
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 93814b7d1b40a14d76dbc2548c128f382131d98e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-oracle-database-oracletosql"></a>Herstellen einer Verbindung mit Oracle-Datenbank (OracleToSQL)
Zum Migrieren von Oracle-Datenbanken zu [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], Sie müssen die Verbindung mit der Oracle-Datenbank, die Sie migrieren möchten. Wenn Sie eine Verbindung herstellen, SSMA Ruft Metadaten zu allen Oracle-Schemas ab und zeigt ihn dann in der Oracle-Metadaten-Explorer-Bereich an. SSMA speichert Informationen über den Datenbankserver, aber die Kennwörter werden nicht gespeichert.  
  
Die Verbindung mit der Datenbank bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit der Datenbank verwendet werden soll.  
  
Metadaten für die Oracle-Datenbank wird nicht automatisch aktualisiert. Stattdessen, wenn Sie die Metadaten in Oracle-Metadaten-Explorer aktualisieren möchten, müssen Sie manuell es aktualisieren. Weitere Informationen finden Sie im Abschnitt "Aktualisieren von Oracle-Metadaten" weiter unten in diesem Thema.  
  
## <a name="required-oracle-permissions"></a>Erforderliche Oracle-Berechtigungen  
Das Konto, das verwendet wird, für die Verbindung zur Oracle-Datenbank muss zumindest **verbinden** Berechtigungen. Dies ermöglicht der SSMA zum Abrufen von Metadaten aus Schemas im Besitz des Benutzers eine Verbindung herstellt. Zum Abrufen von Metadaten für Objekte in anderen Schemas, und klicken Sie dann konvertiert die Objekte in diesen Schemas, muss das Konto über die folgenden Berechtigungen verfügen:  
  
-   ERSTELLEN EINER PROZEDUR  
  
-   FÜHREN SIE EINE PROZEDUR  
  
-   WÄHLEN SIE EINE TABELLE  
  
-   WÄHLEN SIE EINE BELIEBIGE SEQUENZ  
  
-   ERSTELLEN SIE EINEN BELIEBIGEN TYP  
  
-   CREATE ANY TRIGGER  
  
-   WÄHLEN SIE ALLE WÖRTERBUCH  
  
## <a name="establishing-a-connection-to-oracle"></a>Herstellen einer Verbindung mit Oracle  
Wenn Sie eine Verbindung mit einer Datenbank herstellen, SSMA liest die Datenbankmetadaten und fügt dann diese Metadaten in die Projektdatei. Diese Metadaten werden von SSMA verwendet, wenn Objekte konvertiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Syntax, und wenn sie Daten migriert [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Sie können Durchsuchen dieser Metadaten in der Oracle-Metadaten-Explorer-Bereich und überprüfen Sie die Eigenschaften der einzelnen Datenbankobjekte.  
  
> [!IMPORTANT]  
> Bevor Sie versuchen, eine Verbindung herstellen, stellen Sie sicher, dass der Datenbankserver ausgeführt wird und Verbindungen akzeptieren kann.  
  
**Verbindung mit Oracle**  
  
1.  Auf der **Datei** klicken Sie im Menü **Connect to Oracle**.  
  
    Wenn Sie zuvor mit Oracle verbunden, wird der Befehlsname sein **eine erneute Verbindung mit Oracle**.  
  
2.  In der **Anbieter** wählen Sie im **Oracle-Client-Anbieter** oder **OLE DB-Anbieter**, je nachdem, welcher Anbieter installiert ist. Der Standardwert ist die Oracle-Client.  
  
3.  In der **Modus** wählen **Modus "Standard"**, **TNSNAME Modus**, oder **Zeichenfolge Verbindungsmodus**.  
  
    Verwenden Sie Modus "standard", um den Servernamen und den Port angeben. Verwenden Sie Namen Dienstmodus, um den Oracle-Dienstnamen manuell anzugeben. Verwenden Sie Zeichenfolge Verbindungsmodus, um eine vollständige Verbindungszeichenfolge bereitzustellen.  
  
4.  Bei Auswahl des **Modus "Standard"**, geben Sie die folgenden Werte:  
  
    1.  In der **Servernamen** Feld eingeben oder auswählen den Namen oder IP-Adresse des Datenbankservers.  
  
    2.  Wenn der Datenbankserver nicht konfiguriert ist, um Verbindungen zuzulassen, auf die Standardeinstellung (1521) port verwenden, geben Sie die Portnummer für die Oracle-Verbindungen in verwendeten die **Serverport** Feld.  
  
    3.  In der **Oracle SID** Geben Sie den Systembezeichner.  
  
    4.  In der **Benutzername** Geben Sie ein Oracle-Konto, das die erforderlichen Berechtigungen verfügt.  
  
    5.  In der **Kennwort** Geben Sie das Kennwort für den angegebenen Benutzernamen ein.  
  
5.  Bei Auswahl des **TNSNAME Modus**, geben Sie die folgenden Werte:  
  
    1.  In der **verbinden Bezeichner** Geben Sie Bezeichner (TNS Alias) der Datenbank herstellen.  
  
    2.  In der **Benutzername** Geben Sie ein Oracle-Konto, das die erforderlichen Berechtigungen verfügt.  
  
    3.  In der **Kennwort** Geben Sie das Kennwort für den angegebenen Benutzernamen ein.  
  
6.  Bei Auswahl des **Zeichenfolge Verbindungsmodus**, geben Sie eine Verbindungszeichenfolge in der **Verbindungszeichenfolge** Feld.  
  
    Das folgende Beispiel zeigt eine OLE DB-Verbindungszeichenfolge:  
  
    `Provider=OraOLEDB.Oracle;Data Source=MyOracleDB;User Id=myUsername;Password=myPassword;`  
  
    Das folgende Beispiel zeigt eine Oracle-Client-Verbindungszeichenfolge, die die integrierte Sicherheit verwendet:  
  
    `Data Source=MyOracleDB;Integrated Security=yes;`  
  
    Weitere Informationen finden Sie unter [auf Oracle Verbinden &#40;OracleToSQL&#41;](../../ssma/oracle/connect-to-oracle-oracletosql.md).  
  
## <a name="reconnecting-to-oracle"></a>Erneutes Herstellen einer Verbindung mit Oracle  
Die Verbindung mit dem Datenbankserver bleibt aktiv, bis Sie das Projekt schließen. Wenn Sie das Projekt erneut öffnen, müssen Sie neu, wenn eine aktive Verbindung mit der Datenbank verwendet werden soll. Sie können offline arbeiten, bis Sie verwenden möchten, aktualisieren Sie Metadaten an, und laden die Datenbankobjekte in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], und Daten migrieren.  
  
## <a name="refreshing-oracle-metadata"></a>Aktualisieren von Metadaten für Oracle  
Metadaten für die Oracle-Datenbank wird nicht automatisch aktualisiert. Die Metadaten in Oracle-Metadaten-Explorer wird eine Momentaufnahme der Metadaten, wenn Sie zuerst eine Verbindung hergestellt oder der letzten, dass Sie manuell die Metadaten aktualisiert werden. Sie können die Metadaten für alle Schemas, ein einzelnes Schema oder einzelne Datenbankobjekte manuell aktualisieren.  
  
**Aktualisieren von Metadaten**  
  
1.  Stellen Sie sicher, dass Sie mit der Datenbank verbunden sind.  
  
2.  Wählen Sie in Oracle-Metadaten-Explorer das Kontrollkästchen neben jedem Schema oder Datenbank-Objekt, das Sie aktualisieren möchten.  
  
3.  Mit der rechten Maustaste **Schemas**, einzelnes Schema oder eine Datenbank-Objekt, und wählen Sie dann **aus der Datenbank aktualisieren**.  
  
    SSMA wird angezeigt, wenn Sie nicht über eine aktive Verbindung verfügen, die **Connect to Oracle** Dialogfeld, sodass Sie eine Verbindung herstellen können.  
  
4.  Geben Sie die zu aktualisierenden Objekte in die Aktualisierung über Datenbank-Dialogfeld.  
  
    -   Um ein Objekt zu aktualisieren, klicken Sie auf die **Active** Feld neben dem Objekt, bis ein Pfeil angezeigt wird.  
  
    -   Um zu verhindern, dass ein Objekt aktualisiert wird, klicken Sie auf die **Active** Feld neben solange ein **X** angezeigt wird.  
  
    -   Klicken Sie zum Aktualisieren oder Ablehnen einer Kategorie von Objekten, auf die **Active** Feld neben der Kategorieordner.  
  
    Um die Definitionen der Farbcode anzuzeigen, klicken Sie auf die **Legende** Schaltfläche.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok_md.md)]  
  
## <a name="next-step"></a>Nächster Schritt  
  
-   Der nächste Schritt des Migrationsvorgangs besteht darin [Herstellen einer Verbindung mit einer Instanz von SQL Server](http://msdn.microsoft.com/en-us/1b2a8059-1829-4904-a82f-9c06de1e245f).  
  
## <a name="see-also"></a>Siehe auch  
[Migrieren von Oracle-Datenbanken zu SQLServer &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
