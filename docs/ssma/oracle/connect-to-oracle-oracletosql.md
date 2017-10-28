---
title: Herstellen einer Verbindung mit Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d685be15fb8d0c6fea21d539e3370b3377316324
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-oracle-oracletosql"></a>Herstellen einer Verbindung mit Oracle (OracleToSQL)
Verwenden der **Connect to Oracle** Dialogfeld Verbindung mit der Oracle-Datenbank, die Sie migrieren möchten.  
  
Zum Zugriff auf dieses Dialogfeld, in dem **Datei** klicken Sie im Menü **Connect to Oracle**. Wenn Sie zuvor eine Verbindung hergestellt haben, wird der Befehl ist **eine erneute Verbindung mit Oracle**.  
  
## <a name="options"></a>enthalten  
**Provider**  
Auswählen der Datenzugriffsanbieter für die Verbindung mit der Oracle-Datenbank. Verfügbare Anbieter sind die Oracle-Client-Anbieter und der OLE DB-Anbieter. Der Standardwert ist die Oracle-Client-Anbieter.  
  
**Mode**  
Wählen Sie entweder Standard, TNSNAME oder Verbindungszeichenfolge-Modus.  
  
-   Im Modus "Standard" Geben Sie ein oder wählen Sie Werte für den Anbieter, Servername, ServerPort, Oracle SID, Benutzername und Kennwort.  
  
-   Im TNSNAME-Modus geben Sie den Connect-Bezeichner (TNS Alias), der die Oracle-Datenbank, Benutzername und Kennwort.  
  
-   Stellen Sie eine Verbindungszeichenfolge bereit, in der Verbindungszeichenfolge-Modus.  
  
    > [!IMPORTANT]  
    > Wir empfehlen nicht, dass die Verbindungszeichenfolge Modus verwenden, da der Text Kennwörter enthalten kann und wird als Klartext gesendet.  
  
Der Standardwert ist Modus "Standard".  
  
**Servername**  
Geben Sie den Oracle-Servernamen ein. Der Standardservername entspricht dem Namen des Computers. Dies ist ein Modus "Standard"-Option.  
  
**Serverport**  
Wenn Sie eine Portnummer als 1521 (Standard) für Verbindungen mit Oracle verwenden, geben Sie die Portnummer. Dies ist ein Modus "Standard"-Option.  
  
**Verbinden Sie Bezeichner**  
Geben Sie die Oracle Bezeichner verbinden. Dies ist der Alias der Datenbank, wie in der Datei tnsnames.ora lokalen definiert.  
  
Dies ist eine TNSNAME-Modus-Option.  
  
**Oracle SID**  
Geben Sie die SID für die Datenbank ein. Die SID ist ein Bezeichner, der die Oracle-Datenbank auf einem Computer unterscheidet. Der Standard-SID für eine Datenbank ist die ersten acht Zeichen des Datenbanknamens.  
  
Dies ist ein Modus "Standard"-Option.  
  
**Benutzername**  
Geben Sie den Benutzernamen, den SSMA für die Verbindung zur Oracle-Datenbank verwenden.  
  
**Kennwort**  
Geben Sie das Kennwort für den Benutzernamen ein.  
  
**Verbindungszeichenfolge**  
> [!IMPORTANT]  
> Wir empfehlen nicht, dass die Verbindungszeichenfolge Modus verwenden, da der Text Kennwörter enthalten kann und wird als Klartext gesendet.  
  
Wenn Sie den Modus für die Verbindungszeichenfolge verwenden, geben Sie die vollständige Verbindungszeichenfolge für die Verbindung zu Oracle.  
  
Verbindungszeichenfolgen werden von Name-Wert-Paaren bestehen.  
  
-   OLE DB-Verbindungszeichenfolgen-Informationen finden Sie unter [Microsoft OLE DB-Anbieter für Oracle](http://go.microsoft.com/fwlink/?LinkId=85640) Artikel in der MSDN Library.  
  
Beziehen Sie immer für SSMA-Verbindungszeichenfolgen die Anbieter-Parameter. Stellen Sie außerdem sicher, dass Sie den Port-Parameter, beim Herstellen einer Verbindung mit Oracle enthalten.  
  

