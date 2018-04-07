---
title: Installieren von SQL Server Migration Assistant für Access (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0b60003c1d9c7c266d57f6c0fc583b977561be72
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>Installieren von SQL Server Migration Assistant für Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant (SSMA) für den Zugriff ist mithilfe ein Windows Installer-basierten Assistenten installiert. Dieses Thema enthält Informationen über Installationsvoraussetzungen, einen Link auf die neueste Version von SSMA und Anweisungen zum Installieren, Lizenzierung, deinstallieren und Aktualisieren von SSMA.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Bevor Sie SSMA installiert haben, stellen Sie sicher, dass Ihr System die folgenden Anforderungen erfüllt:  
  
-   Windows 7 oder höher oder Windows Server 2008 oder höher.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 oder höher.  
  
-   Die [!INCLUDE[msCoName](../../includes/msconame_md.md)] Version von .NET Framework 4.0 oder höher. .NET Framework, Version 4.0 wird über die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Produkt-CD, und mithilfe der Informationen in der [Handbuch für Microsoft .NET](https://docs.microsoft.com/en-us/dotnet/framework/).
  
-   Zugriff auf sowie ausreichende Berechtigungen auf dem Computer, der die Zielinstanz des hostet [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SQL Azure-Datenbank zu dem Sie Datenbankobjekte und Daten migrieren.  
  
-   Microsoft Data Access Objekt (DAO) Anbieterversion 12.0 oder 14.0. Sie können die DAO-Anbieter von Microsoft Office 2010/2007-Produkt installieren oder Microsoft-Website herunterladen.  
  
-   Der SQL Server Native Access Client (SNAC) Version 10.5 und höher für die Migration zu SQL Azure. Sie erhalten die neueste Version der SNAC aus [Microsoft® SQL Server® 2008 R2 Feature Pack](http://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4 GB RAM (empfohlen).  
  
## <a name="installing-ssma"></a>Installieren SSMA  
SSMA ist ein Webdownload. Informationen zum Herunterladen der neuesten Version finden Sie unter der [Downloadseite für SQL Server Migration Assistant](http://aka.ms/ssmaforaccess).  
  
Nachdem Sie die neueste Version heruntergeladen haben, müssen Sie die Installationsdateien aus dem Extrahieren, vor der Installation von SSMA.

> [!IMPORTANT]  
> -   Deinstallieren Sie alle vorherige Versionen von SSMA für Access vor der Installation der neuen Version ein.  
  
**So installieren Sie SSMA**  
  
1.  Doppelklicken Sie auf SSMA für Access *n*MSI-Datei, wobei *n* Nummer des Builds.  
  
2.  Klicken Sie auf der Seite "Willkommen" auf **Weiter**.  
  
    Wenn Sie nicht die erforderlichen Komponenten installiert haben, wird eine Meldung, der angibt, dass Sie zuerst die erforderlichen Komponenten installieren müssen. Stellen Sie sicher, dass Sie alle erforderlichen Komponenten installiert haben, und führen Sie das Installationsprogramm erneut aus.  
  
3.  Lesen Sie den Endbenutzer-Lizenzvertrag. Wenn Sie zustimmen, aktivieren **ich stimme die Vereinbarung**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf der Seite "Installationstyp auswählen" auf **typisch**.  
  
5.  Klicken Sie auf **Installieren**.  
  
Der Standardinstallationspfad lautet c:\Programme\Microsoft c:\Programme\Microsoft SQL Server Migration Assistant für Access.  
  
## <a name="uninstalling-ssma-for-access"></a>Deinstallieren von SSMA für Access  
Deinstallieren Sie SSMA mit **Software** in der Systemsteuerung. Denken Sie daran, dass die Deinstallation des Programms nicht löschen SSMA-Projektdateien oder Protokolldateien.  
  
**So deinstallieren Sie SSMA**  
  
1.  Klicken Sie auf **starten**, klicken Sie auf **Systemsteuerung**, und klicken Sie dann auf **Software**.  
  
2.  Wählen Sie **Microsoft SQL Server Migration Assistant für Access**, und klicken Sie dann auf **entfernen**.  
  
## <a name="upgrading-to-a-later-version"></a>Upgrade auf eine höhere version  
Wenn Sie auf eine höhere Version von SSMA für Access aktualisieren möchten, müssen Sie zuerst deinstallieren SSMA für Access und dann die neuere Version installieren. Befolgen Sie die Anweisungen in der Deinstallation von SSMA für Access-Abschnitt, um diesen Vorgang abzuschließen.  
  
Wenn Sie ein in einer früheren Version von SSMA für Access erstelltes Projekt öffnen, werden Sie SSMA gefragt, ob Sie das Projekt auf die neuere Version konvertieren möchten. Klicken Sie auf **Ja** bei dem Projekt in der neueren Version von SSMA ordnungsgemäß funktionieren.  
  
## <a name="see-also"></a>Siehe auch  
[Access-Datenbanken vorbereitet für die Migration.](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
[Migrieren von Access-Datenbanken zu SQLServer](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Verknüpfen von Access-Anwendungen mit SQLServer](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
