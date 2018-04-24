---
title: Zertifikatbereitstellung - Analytics Platform System | Microsoft Docs
description: Zertifikatbereitstellung in Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 82907692bbba3ad92e796e8ecc8bb99e3141cb1a
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Zertifikatbereitstellung in Analyseplattformsystem
Die **PDW Zertifikatbereitstellung** auf der Seite das Analytics Platform System**Configuration Manager** importiert oder von PDW verwendeten Zertifikats entfernt. 

Verwenden, kann ein Zertifikat zum Verschlüsseln von Verbindungen sicheren Kommunikation mit dem Steuerungsknoten über SQL Server-Clients, Tools, mit denen die SQL Server PDW-Treiber unterstützen die [Admin Console](monitor-the-appliance-by-using-the-admin-console.md), und lädt Sie Integration Services. 
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Vor dem Installieren des Zertifikats an, führen Sie folgende Schritte aus:  
  
1.  Ein gesichertes Zertifikat zu erhalten. Wenn Sie weitere Informationen zum Abrufen eines sicheren Zertifikats benötigen, wenden Sie sich an Microsoft Support.  
  
2.  Das Zertifikat mit dem Steuerungsknoten in einer kennwortgeschützten PFX-Datei gespeichert.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Aus Gründen der Sicherheit erhalten Sie ein vertrauenswürdiges Zertifikat  
SQL Server PDW unterstützt, mit einem Zertifikat zum Verschlüsseln von Verbindungen mit dem Steuerungsknoten; Verbindungen, einschließlich der **Admin Console**.  
  
Wird standardmäßig die **Admin Console** enthält ein selbst signiertes Zertifikat, das Datenschutz, aber keine Serverauthentifizierung bereitstellt. Diese lassen Kommunikation anfällig für Man-in-the-Middle-Angriffe. Wenn ein Benutzer mit der Verwaltungskonsole verbunden ist mithilfe des selbstsignierten Zertifikats, Internet Explorer wird der Fehler zurückgegeben: "Es besteht ein Problem mit dem Sicherheitszertifikat dieser Website".  
  
Obwohl in-Flight-Daten zwischen dem Client und dem Server die Verbindung über ein selbst signiertes Zertifikat verschlüsselt wird, wird die Verbindung immer noch durch Angriffe gefährdet.  
  
> [!WARNING]  
> Appliance-Administratoren sollten sofort ein Zertifikat erwerben, ist mit einer vertrauenswürdigen Zertifizierungsstelle, die von Clients, um über eine sichere Verbindung verfügen, und entfernen den Fehler, den Internet Explorer meldet erkannt verkettet.  
  
Zertifizierungspfad muss den vollqualifizierten Domänennamen, der den Knoten "Zugriffssteuerung" (empfohlen) IP-Clusteradresse zugeordnet oder der Name, der in ihren Browser Adresse Balken den Zugriff auf die Benutzer eingeben enthalten die **Admin Console**.  
  
Verwenden Sie das Analytics Platform System**Configuration Manager** hinzufügen oder entfernen das vertrauenswürdige Zertifikat. Direkt mit dem Microsoft Windows HTTP-Dienste Zertifikat-Konfigurationstool (**winHttpCertCfg.exe**) zum Verwalten des Zertifikats werden nicht unterstützt.  
  
## <a name="import-or-remove-the-certificate"></a>Importieren Sie oder entfernen Sie das Zertifikat  
Die folgenden Anweisungen zeigen, wie zum Importieren oder entfernen das Zertifikat für die Appliance.  
  
### <a name="to-import-the-certificate"></a>Um das Zertifikat zu importieren.  
  
1.  Starten Sie die **Configuration Manager**.  
Weitere Informationen finden Sie unter [Starten des Konfigurations-Managers &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md).  

2.  Im linken Bereich des der **Configuration Manager**, erweitern Sie **Parallel Data Warehouse-Topologie**, und klicken Sie dann auf **Zertifikate**.  
  
3.  Wählen Sie **ein Zertifikat zu importieren und konfigurieren Sie die Einheit für den Einsatz**, und klicken Sie dann auf **Durchsuchen** danach suchen, und wählen Sie die Zertifikatdatei.  
  
4.  Geben Sie das Kennwort für das Zertifikat in der **Kennwort** Feld.  
  
5.  Klicken Sie auf **übernehmen** so konfigurieren Sie das Zertifikat für die Anwendung.  
  
SQL Server PDW aktuellen Verbindung wird nicht anhand des importierten Zertifikats verschlüsselt, sondern verwenden Sie das Zertifikat wird für neue Verbindungen.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>So entfernen Sie die zuvor importierte Zertifikat  
  
1.  Starten Sie die **Configuration Manager**. 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  Im linken Bereich des der **Configuration Manager**, erweitern Sie **Parallel Data Warehouse-Topologie**, und klicken Sie dann auf **Zertifikate**.  
  
3.  Wählen Sie **entfernen Sie alle Zertifikate in der Einheit bereitgestellt**.  
  
4.  Klicken Sie auf **übernehmen** zuvor importierte Zertifikat auf dem Gerät zu entfernen.  
  
SQL Server PDW wird zum Verschlüsseln von aktuellen Verbindungen fortgesetzt, aber das Zertifikat entfernte wird nicht für neue Verbindungen verwenden.  
  
![DWConfig-Anwendung PDW-Zertifikat](media/dwconfig-appl-pdw-cert.png "DWConfig Appliance PDW-Zertifikat")  
  
## <a name="see-also"></a>Siehe auch  
[Starten Sie den Konfigurations-Manager &#40;Analyseplattformsystem&#41;](launch-the-configuration-manager.md)  
