---
title: "Dialogfeld \"Überprüfen\" | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d7ff51208136b767dfb6260e6cfc07e67615531e
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

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
  
 **Wert**  
 Listet den Parameterwert auf.  
  
 Auf der Registerkarte **Verbindungs-Manager** werden die Verbindungs-Manager-Eigenschaften aufgelistet, die Sie zum Überprüfen des Projekts oder Pakets verwenden.  
  
 Im Folgenden finden Sie die Optionen der Registerkarte **Verbindungs-Manager** .  
  
 **Container**  
 Listet das Objekt auf, das den Verbindungs-Manager enthält.  
  
 **Name**  
 Listet den Namen des Verbindungs-Managers auf.  
  
 **Eigenschaftsname**  
 Listet den Namen der Verbindungs-Manager-Eigenschaft auf.  
  
 **Wert**  
 Listet den Wert auf, der der Verbindungs-Manager-Eigenschaft zugewiesen ist.  
  
  

