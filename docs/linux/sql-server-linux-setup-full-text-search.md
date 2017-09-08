---
title: Installieren von SQL Server-Volltextsuche unter Linux | Microsoft Docs
description: Dieses Thema beschreibt, wie SQL Server-Volltextsuche unter Linux zu installieren.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: bb42076f-e823-4cee-9281-cd3f83ae42f5
ms.translationtype: MT
ms.sourcegitcommit: e4a6157cb56c6db911406585f841046a431eef99
ms.openlocfilehash: a542817a861f968cebf3a66f91cfb016d2a685b8
ms.contentlocale: de-de
ms.lasthandoff: 08/16/2017

---
# <a name="install-sql-server-full-text-search-on-linux"></a>Installieren von SQL Server-Volltextsuche unter Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Installieren Sie die folgenden Schritte [SQL Server-Volltextsuche](https://msdn.microsoft.com/library/ms142571.aspx) (**Mssql-Server-Fts**) unter Linux. Volltextsuche können Sie Volltextabfragen für zeichenbasierte Daten in SQL Server-Tabellen ausgeführt. Bekannte Probleme in dieser Version finden Sie unter der [Release Notes](sql-server-linux-release-notes.md).

> [!NOTE]
> Vor der Installation von SQL Server-Volltext-Suchdienst, zuerst [Installieren von SQL Server](sql-server-linux-setup.md#platforms). Konfiguriert, um die Schlüssel und Repositorys, die Sie verwenden, bei der Installation der **Mssql-Server-Fts** Paket.

Installieren Sie SQL Server-Volltextsuche für Ihre Plattform:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Installieren Sie auf dem RHEL</a>

Verwenden Sie die folgenden Befehle zum Installieren der **Mssql-Server-Fts** unter Red Hat Enterprise Linux. 

```bash
sudo yum update
sudo yum install -y mssql-server-fts
```

Falls Sie noch **Mssql-Server-Fts** installiert haben, können Sie auf die neueste Version mit den folgenden Befehlen aktualisieren:

```bash
sudo yum check-update
sudo yum update mssql-server-fts
```

Eine offline-Installation, suchen Sie nach der Paketdownload "Volltextsuche" in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte in diesem Thema beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Installieren Sie auf Ubuntu</a>

Verwenden Sie die folgenden Befehle zum Installieren der **Mssql-Server-Fts** auf Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts
```

Falls Sie noch **Mssql-Server-Fts** installiert haben, können Sie auf die neueste Version mit den folgenden Befehlen aktualisieren:

```bash
sudo apt-get update 
sudo apt-get install -y mssql-server-fts 
```

Eine offline-Installation, suchen Sie nach der Paketdownload "Volltextsuche" in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte in diesem Thema beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Installieren Sie auf SLES</a>

Verwenden Sie die folgenden Befehle zum Installieren der **Mssql-Server-Fts** für SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-fts
```

Falls Sie noch **Mssql-Server-Fts** installiert haben, können Sie auf die neueste Version mit den folgenden Befehlen aktualisieren:

```bash
sudo zypper refresh
sudo zypper update mssql-server-fts
```

Eine offline-Installation, suchen Sie nach der Paketdownload "Volltextsuche" in der [Anmerkungen zu dieser Version](sql-server-linux-release-notes.md). Verwenden Sie die gleichen Offlineinstallation Schritte in diesem Thema beschriebenen [Installieren von SQL Server](sql-server-linux-setup.md#offline).

## <a name="supported-languages"></a>Unterstützte Sprachen

Volltext-Suchdienst verwendet [wörtertrennungen](https://msdn.microsoft.com/library/ms142509.aspx) feststellen, dass einzelne Wörter, die basierend auf Sprache identifizieren. Sie erhalten eine Liste der registrierten wörtertrennungen durch Abfragen der **Sys. fulltext_languages** -Katalogsicht angezeigt. Wörtertrennungen für die folgenden Sprachen sind mit SQL Server 2017 RC2 installiert:

| Sprache | Sprach-ID |
|---|---|
| Neutral | 0 |
| Arabisch | 1025 |
| Bangla (Indien) | 1093 |
| Bokmål | 1044 |
| Brasilianisch | 1046 |
| Englisch (britisch) | 2057 |
| Bulgarisch | 1026 |
| Katalanisch | 1027 |
| Chinesisch (Hongkong SAR, VR China) | 3076 |
| Chinesisch (Macao SAR) | 5124 |
| Chinesisch (Singapur) | 4100 |
| Kroatisch | 1050 |
| Tschechisch | 1029 |
| Dänisch | 1030 |
| Niederländisch | 1043 |
| Englisch | 1033 |
| Französisch | 1036 |
| Deutsch | 1031 |
| Griechisch | 1032 |
| Gujarati | 1095 |
| Hebräisch | 1037 |
| Hindi | 1081 |
| Isländisch | 1039 |
| Indonesisch | 1057 |
| Italienisch | 1040 |
| Japanisch | 1041 |
| Kannada | 1099 |
| Koreanisch | 1042 |
| Lettisch | 1062 |
| Litauisch | 1063 |
| Malaiisch (Malaysia) | 1086 |
| Malayalam | 1100 |
| Marathi | 1102 |
| Polnisch | 1045 |
| Portugiesisch | 2070 |
| Punjabi | 1094 |
| Rumänisch | 1048 |
| Russisch | 1049 |
| Serbisch (Kyrillisch) | 3098 |
| Serbisch (Lateinisch) | 2074 |
| Chinesisch (vereinfacht) | 2052 |
| Slowakisch | 1051 |
| Slowenisch | 1060 |
| Spanisch | 3082 |
| Schwedisch | 1053 |
| Tamil | 1097 |
| Telugu | 1098 |
| Thai | 1054 |
| Chinesisch (traditionell) | 1028 |
| Türkisch | 1055 |
| Ukrainisch | 1058 |
| Urdu | 1056 |
| Vietnamesisch | 1066 |

## <a id="filters"></a>Filter

Volltextsuche funktioniert auch mit Text in binäre Dateien gespeichert. Aber in diesem Fall ein installierten Filter zum Verarbeiten der Datei erforderlich ist. Weitere Informationen zu Filtern finden Sie unter [konfigurieren und Verwalten von Filtern für die Suche](https://msdn.microsoft.com/library/ms142499.aspx).

Sie erhalten eine Liste der installierten Filter durch Aufrufen von **Sp_help_fulltext_system_components 'Filter'**. Für SQL Server 2017 RC2 werden die folgenden Filter installiert:

| Komponentenname | Klassen-ID | Version |
|---|---|---|
|ein | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ans | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ASC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ascx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|ASM | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|ASP | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|aspx | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.asx | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|BAS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|BAT | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|bcp | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|c | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|sql_Dateiname | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|CLS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|".cmd" | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|cpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|cs | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.CSA | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|CSS | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|CSV | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.cxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.DBS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|DEF | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|".dic" | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.DOS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|DSP | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|dsw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ext | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.FAQ | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.fky | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|h | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.HHC | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hpp | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|HTA | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|HTML | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htt | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.htw | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|HTX | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.hxx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|trägt | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.ibq | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|ICS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.idl | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.IDQ | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|Inc | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|INF | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|INI | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.Inl | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.INX | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|".jav" | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.Java | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.js | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.KCI | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.lgN | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.log | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|lst | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|. m3u | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|MAK | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.mk | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ODC | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.odh | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|ODL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|PKGDEF | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.pkgundef | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|PL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.PRC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|RC | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|RC2 | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.rct | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|REG | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|RGS | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|RTF | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|RUL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.s | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.SCC | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.shtm | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|sHTML | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|Snippet | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.SOL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.Sor | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.srf | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|STM | E0CA5340-4534-11CF-B952-00AA0051FE20 | 12.0.6828.0 |
|.TAB | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TDL | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TLH | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TLI | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|TRG | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|".txt" | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|UDF | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.UDT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|URL | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|usr | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|".vbs" | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|.viw | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|VSCT | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsixlangpack | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|vsixmanifest | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vspscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vsscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.vssscc | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wri | C1243CA0-BF96-11CD-B579-08002B30BFEB | 12.0.6828.0 |
|.wtx | C7310720-AC80-11D1-8DF3-00C04FB6EF4F | 12.0.6828.0 |
|*.xml | 41B9BE05-B3AF-460C-BF0B-2CDD44A093B1 | 12.0.9735.0 |

## <a name="semantic-search"></a>Semantische Suche
[Semantische Suche](https://msdn.microsoft.com/library/gg492075.aspx) baut auf die Volltext-Suchfunktion zu extrahieren und zu indizieren, die für statistisch *Schlüsselausdrücke*. Dadurch können Sie die Bedeutung von Dokumenten in der Datenbank abzufragen. Die Lösung schützt auch Dokumente zu identifizieren, die ähnlich sind.

Um die semantische Suche zu verwenden, müssen Sie zuerst herunter, und fügen Sie der [semantische sprachstatistikdatenbank](https://msdn.microsoft.com/library/gg509085.aspx).

1. Auf einem Windows-Computer [Herunterladen der. MSI-Datei für die semantische sprachstatistikdatenbank](https://www.microsoft.com/download/details.aspx?id=54277).

    > [!NOTE]
    > Auf dieser Zeit den Download für die Datenbank ein. MSI-Datei, ein Windows-Computer für diesen Schritt erforderlich ist.

2. Führen Sie die. MSI-Datei extrahieren der Datenbank und Protokolldateien.

3. Verschieben Sie die Datenbank und-Protokolldateien an Ihren Linux SQL Server-Computer.

    > [!TIP]
    > Anleitungen zum Verschieben von Dateien aus Windows auf Linux finden Sie unter [übertragen Sie eine Datei auf Linux](sql-server-linux-migrate-restore-database.md#scp).

4. Führen Sie den folgenden Transact-SQL-Befehl für Ihre Linux SQL Server-Instanz die sprachstatistikdatenbank angefügt.

    ```tsql
    CREATE DATABASE semanticsdb  
            ON ( FILENAME = N'var/opt/mssql/data/semanticsdb.mdf' )  
            LOG ON ( FILENAME = N'var/opt/mssql/data/semanticsdb_log.ldf' )  
            FOR ATTACH;  
    GO  
    ```

5. Führen Sie den folgenden Transact-SQL-Befehl, um die semantische sprachstatistikdatenbank zu registrieren.

    ```tsql
    EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = N'semanticsdb';  
    GO  
    ```

## <a name="next-steps"></a>Nächste Schritte

Informationen zur Volltextsuche finden Sie unter [SQL Server-Volltextsuche](../relational-databases/search/full-text-search.md). 

