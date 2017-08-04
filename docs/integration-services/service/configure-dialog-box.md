---
title: Dialogfeld "konfigurieren" | Microsoft Docs
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
- sql13.dts.designer.configure.f1
- sql13.SSIS.SSMS.ISPROJECTPROP.REFERENCES.F1
- sql13.SSIS.SSMS.ISPROJECTPROP.PARAMETERS.F1
ms.assetid: 10183c8d-b1be-420f-972a-96ea97d4f4d8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f9587abfb97ec048985ac28de0e7dc585e2bea61
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="configure-dialog-box"></a>Konfigurieren (Dialogfeld)
  Verwenden Sie das Dialogfeld **Konfigurieren** , um Parameter, Verbindungs-Manager und Umgebungsverweise für Pakete und Projekte zu konfigurieren.  
  
 **Was möchten Sie tun?**  
  
-   [Öffnen des Dialogfelds 'Konfigurieren'](#open_dialog)  
  
-   [Festlegen der Optionen auf der Seite 'Parameter'](#parameter)  
  
-   [Festlegen der Optionen auf der Seite 'Verweise'](#references)  
  
##  <a name="open_dialog"></a> Öffnen des Dialogfelds 'Konfigurieren'  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]eine Verbindung zum [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server her.  
  
     Sie stellen eine Verbindung mit der [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] -Instanz her, die die SSISDB-Datenbank hostet.  
  
2.  Erweitern Sie im Objekt-Explorer die Struktur, um den Knoten **Integration Services-Kataloge** anzuzeigen.  
  
3.  Erweitern Sie den **SSISDB** -Knoten.  
  
4.  Erweitern Sie den Ordner mit dem Paket oder Projekt, das Sie konfigurieren möchten.  
  
5.  Klicken Sie mit der rechten Maustaste auf das Paket oder Projekt, und klicken Sie anschließend auf **Konfigurieren**.  
  
##  <a name="parameter"></a> Festlegen der Optionen auf der Seite 'Parameter'  
 Verwenden Sie die Seite **Parameter** , um Parameternamen und Werte anzuzeigen und die Werte zu ändern.  
  
 Wählen Sie den Bereich der Parameter aus, der in den Registerkarten **Parameter** und **Verbindungs-Manager** in der Dropdownliste **Bereich** angezeigt wird.  
  
 Im Folgenden finden Sie eine Liste der Optionen auf der Registerkarte **Parameter** .  
  
 **Container**  
 Listet das Objekt auf, das den Parameter enthält.  
  
 **Name**  
 Listet den Namen des Parameters auf.  
  
 **Wert**  
 Listet den Parameterwert auf. Klicken Sie auf die Schaltfläche mit den Auslassungspunkten, um den Wert im Dialogfeld **Parameterwert festlegen** zu ändern.  
  
 Im Folgenden finden Sie eine Liste der Optionen auf der Registerkarte **Verbindungs-Manager** . Sie verwenden diese Registerkarte, um Werte für Eigenschaften des Verbindungs-Managers zu ändern. Parameter für die Eigenschaften werden automatisch auf dem SSIS-Server generiert.  
  
 **Container**  
 Listet das Objekt auf, das den Verbindungs-Manager enthält.  
  
 **Name**  
 Listet den Namen des Verbindungs-Managers auf.  
  
 **Eigenschaftsname**  
 Listet den Namen der Verbindungs-Manager-Eigenschaft auf.  
  
 **Wert**  
 Listet den Wert auf, der der Verbindungs-Manager-Eigenschaft zugewiesen ist. Klicken Sie auf die Schaltfläche mit den Auslassungspunkten, um den Wert im Dialogfeld **Parameterwert festlegen** zu ändern. Sie können einen Literalwert eingeben, eine Umgebungsvariable mit dem zu verwendenden Wert zuordnen oder den Standardwert aus dem Paket verwenden.  
  
##  <a name="references"></a> Festlegen der Optionen auf der Seite 'Verweise'  
 Verwenden Sie die Seite **Verweise** , um Umgebungsverweise hinzuzufügen und zu entfernen und um auf Umgebungseigenschaften zuzugreifen.  
  
 In einer Umgebung werden Laufzeitwerte für Pakete festgelegt, die in den auf dem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Server bereitgestellten Projekten enthalten sind.  
  
 **Umgebung**  
 Listet die Umgebung auf.  
  
 **Umgebungsordner**  
 Listet den Ordner auf, der die Umgebung enthält.  
  
 **Öffnen**  
 Klicken Sie hierauf, um das Dialogfeld **Umgebungseigenschaften** zu öffnen.  
  
 **Hinzufügen**  
 Klicken Sie auf diese Schaltfläche, um einen Verweis auf eine Umgebung hinzuzufügen. Klicken Sie im Dialogfeld **Umgebungen durchsuchen** auf eine Umgebung, und klicken Sie dann auf **OK**.  
  
 Sie können jede in einem Projektordner unter dem **SSISDB** -Knoten enthaltene Umgebung auswählen.  
  
 **Entfernen**  
 Klicken Sie auf eine im Bereich **Verweise** aufgeführte Umgebung und anschließend auf **Entfernen**.  
  
  
