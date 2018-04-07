---
title: Herstellen einer Verbindung mit DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 27b590cbfefdbc01e67e4049ffa3d920afd08b1f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/06/2018
---
# <a name="connect-to-db2-db2tosql"></a>Connect To DB2 (DB2ToSQL)
Verwenden der **Herstellen einer Verbindung mit DB2** Dialogfeld Verbindung mit der DB2-Datenbank, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Herstellen einer Verbindung mit DB2**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung mit DB2**.  
  
## <a name="options"></a>enthalten  
**Provider**  
Auswählen der Datenzugriffsanbieter für die Verbindung mit der DB2-Datenbank. Verfügbare Anbieter sind der DB2-Client-Anbieter und der OLE DB-Anbieter. Der Standardwert ist DB2-Client-Anbieter.  
  
**Mode**  
Wählen Sie entweder Standard, TNSNAME oder Verbindungszeichenfolge-Modus.  
  
-   Im Modus "Standard" Geben Sie ein oder wählen Sie Werte für den Anbieter, Servername, ServerPort, DB2-SID, Benutzername und Kennwort.  
  
-   Im TNSNAME-Modus geben Sie die Connect-Bezeichner (TNS Alias) von der DB2-Datenbank, Benutzername und Kennwort.  
  
-   Stellen Sie eine Verbindungszeichenfolge bereit, in der Verbindungszeichenfolge-Modus.  
  
    > [!IMPORTANT]  
    > Wir empfehlen nicht, dass die Verbindungszeichenfolge Modus verwenden, da der Text Kennwörter enthalten kann und wird als Klartext gesendet.  
  
Der Standardwert ist Modus "Standard".  
  
**Servername**  
Geben Sie den Namen des DB2-Servers ein. Der Standardservername entspricht dem Namen des Computers. Dies ist ein Modus "Standard"-Option.  
  
**Serverport**  
Wenn Sie eine Portnummer als 1521 (Standard) für Verbindungen mit DB2 verwenden, geben Sie die Portnummer. Dies ist ein Modus "Standard"-Option.  
  
**Verbinden Sie Bezeichner**  
Geben Sie ein DB2 Bezeichner verbinden. Dies ist der Alias der Datenbank, wie in der Datei tnsnames.ora lokalen definiert.  
  
Dies ist eine TNSNAME-Modus-Option.  
  
**DB2 SID**  
Geben Sie die SID für die Datenbank ein. Die SID ist ein Bezeichner, der die DB2-Datenbank auf einem Computer unterscheidet. Der Standard-SID für eine Datenbank ist die ersten acht Zeichen des Datenbanknamens.  
  
Dies ist ein Modus "Standard"-Option.  
  
**Benutzername**  
Geben Sie den Benutzernamen, den SSMA für die Verbindung mit der DB2-Datenbank verwenden.  
  
**Kennwort**  
Geben Sie das Kennwort für den Benutzernamen ein.  
  
**Verbindungszeichenfolge**  
> [!IMPORTANT]  
> Wir empfehlen nicht, dass die Verbindungszeichenfolge Modus verwenden, da der Text Kennwörter enthalten kann und wird als Klartext gesendet.  
  
Wenn Sie den Modus für die Verbindungszeichenfolge verwenden, geben Sie die vollständige Verbindungszeichenfolge für die Verbindung mit DB2.  
  
Verbindungszeichenfolgen werden von Name-Wert-Paaren bestehen.  
  
-   OLE DB-Verbindungszeichenfolgen-Informationen finden Sie unter [Microsoft OLE DB-Anbieter für DB2](http://go.microsoft.com/fwlink/?LinkId=85640) Artikel in der MSDN Library.  
  
Beziehen Sie immer für SSMA-Verbindungszeichenfolgen die Anbieter-Parameter. Stellen Sie außerdem sicher, dass Sie den Port-Parameter, beim Herstellen einer Verbindung mit DB2 enthalten.  
  
