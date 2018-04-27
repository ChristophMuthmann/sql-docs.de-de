---
title: Überprüfen (Dialogfeld) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: service
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a42c5eb2e6fcf7a620eb91c5b3f242a37119b14d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="validate-dialog-box"></a>Dialogfeld 'Überprüfen'
  Verwenden Sie das Dialogfeld **Überprüfen** , um nach häufigen Problemen in einem Projekt oder Paket von [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] zu suchen.  
  
 Wenn ein Problem vorliegt, wird eine Meldung am oberen Rand des Dialogfelds angezeigt. Andernfalls wird "Bereit" oben angezeigt.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Dialogfelds "Überprüfen"](#open_dialog)  
  
-   [Festlegen der Optionen auf der Seite "Allgemein"](#general)  
  
##  <a name="open_dialog"></a> Öffnen des Dialogfelds "Überprüfen"  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server her.  
  
     Sie stellen eine Verbindung mit der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz her, die die SSISDB-Datenbank hostet.  
  
2.  Erweitern Sie im Objekt-Explorer die Struktur, um den Knoten **Integration Services-Kataloge** anzuzeigen.  
  
3.  Erweitern Sie den **SSISDB** -Knoten.  
  
4.  Erweitern Sie den Ordner mit dem Projekt oder Paket, das Sie überprüfen möchten.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Projekt oder Paket, und wählen Sie **Überprüfen**aus.  
  
##  <a name="general"></a> Festlegen der Optionen auf der Seite "Allgemein"  
 **Umgebung**  
 Wählen Sie die Umgebung aus, die Sie verwenden möchten, um das Projekt oder Paket zu überprüfen.  
  
 **32-Bit-Laufzeit**  
 Wählen Sie eine 32-Bit-Laufzeit aus, um ein Paket auszuführen.  
  
 Auf der Registerkarte **Parameter** werden die Parameterwerte aufgelistet, die Sie zum Überprüfen des Projekts oder Pakets verwenden. Im Folgenden finden Sie die Optionen der Registerkarte Parameter.  
  
 **Container**  
 Listet das Objekt auf, das den Parameter enthält.  
  
 **Parameter**  
 Listet den Namen des Parameters auf.  
  
 **ReplTest1**  
 Listet den Parameterwert auf.  
  
 Auf der Registerkarte **Verbindungs-Manager** werden die Verbindungs-Manager-Eigenschaften aufgelistet, die Sie zum Überprüfen des Projekts oder Pakets verwenden.  
  
 Im Folgenden finden Sie die Optionen der Registerkarte **Verbindungs-Manager** .  
  
 **Container**  
 Listet das Objekt auf, das den Verbindungs-Manager enthält.  
  
 **Name**  
 Listet den Namen des Verbindungs-Managers auf.  
  
 **Eigenschaftsname**  
 Listet den Namen der Verbindungs-Manager-Eigenschaft auf.  
  
 **ReplTest1**  
 Listet den Wert auf, der der Verbindungs-Manager-Eigenschaft zugewiesen ist.  
  
  
