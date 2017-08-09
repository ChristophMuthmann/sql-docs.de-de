---
title: "Konfigurieren und Verwalten von Verschlüsselungsschlüsseln (SSRS-Konfigurations-Manager) | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 1433e2532fc1deeb8abe5ac0ca71de69956730e0
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="ssrs-encryption-keys---manage-encryption-keys"></a>Verschlüsselungsschlüssel für SSRS - Verwalten von Verschlüsselungsschlüsseln
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] verwendet Verschlüsselungsschlüssel, um Anmelde- und Verbindungsinformationen zu sichern, die in einer Berichtsserver-Datenbank gespeichert sind. Die Verschlüsselung in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]besteht aus einer Kombination von öffentlichen, privaten und symmetrischen Schlüsseln, die zum Schutz sensibler Daten verwendet werden. Der symmetrische Schlüssel wird bei der Initialisierung des Berichtsservers erstellt, wenn Sie den Berichtsserver installieren oder konfigurieren. Er wird vom Berichtsserver verwendet, um sensible Daten zu verschlüsseln, die auf dem Berichtsserver gespeichert sind. Öffentliche und private Schlüssel werden vom Betriebssystem erstellt und zum Schutz des symmetrischen Schlüssels verwendet. Ein Paar aus einem privaten und einem öffentlichen Schlüssel wird für jede Berichtsserverinstanz erstellt, die sensible Daten in einer Berichtsserver-Datenbank speichert.  
  
 Zur Verwaltung der Verschlüsselungsschlüssel gehört das Erstellen einer Sicherungskopie des symmetrischen Schlüssels und das Wissen darüber, wann und wie die Schlüssel wiederhergestellt, gelöscht oder geändert werden müssen. Wenn Sie eine Berichtsserverinstallation migrieren oder eine Bereitstellung für dezentrales Skalieren konfigurieren, benötigen Sie eine Sicherungskopie des symmetrischen Schlüssels, sodass Sie ihn auf die neue Installation anwenden können.  
  
> [!IMPORTANT]  
>  Aus Sicherheitsgründen empfiehlt es sich, den Reporting Services-Verschlüsselungsschlüssel in regelmäßigen Abständen zu ändern. Ein guter Zeitpunkt, um den Schlüssel zu ändern, liegt direkt im Anschluss an ein größeres Versionsupgrade von Reporting Services. Indem der Schlüssel nach einem Upgrade geändert wird, lassen sich zusätzliche Dienstunterbrechungen, die durch eine Änderung des Reporting Services-Verschlüsselungsschlüssels außerhalb des Upgradezyklus verursacht würden, minimieren.  
  
 Symmetrische Schlüssel können mithilfe des Reporting Services-Konfigurationstools oder des Hilfsprogramms **rskeymgmt** verwaltet werden. Die in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] enthaltenen Tools werden nur zum Verwalten des symmetrischen Schlüssels verwendet (private und öffentliche Schlüssel werden vom Betriebssystem verwaltet). Sowohl das Reporting Services-Konfigurationstool als auch das Hilfsprogramm **rskeymgmt** unterstützen folgende Aufgaben:  
  
-   Erstellen einer Sicherungskopie des symmetrischen Schlüssels, sodass er zum Wiederherstellen einer Berichtsserverinstallation oder im Rahmen einer geplanten Migration verwendet werden kann.  
  
-   Wiederherstellen eines zuvor gespeicherten symmetrischen Schlüssels in einer Berichtsserver-Datenbank, sodass eine neue Berichtsserverinstanz auf die vorhandenen Daten zugreifen kann, die ursprünglich nicht von ihr verschlüsselt wurden.  
  
-   Löschen der verschlüsselten Daten in einer Berichtsserver-Datenbank in dem unwahrscheinlichen Fall, dass Sie nicht mehr auf die verschlüsselten Daten zugreifen können.  
  
-   Erneues Erstellen symmetrischer Schlüssel und erneutes Verschlüsseln von Daten in dem unwahrscheinlichen Fall, dass der symmetrische Schlüssel nicht mehr sicher ist. Eine bewährte Sicherheitsmethode ist die regelmäßige Neuerstellung des symmetrischen Schlüssels (z. B. alle paar Monate), um die Berichtsserver-Datenbank vor Angriffen aus dem Internet zu schützen, bei denen versucht wird, den Schlüssel zu entschlüsseln.  
  
-   Hinzufügen oder Entfernen einer Berichtsserverinstanz aus einer Berichtsserverbereitstellung für dezentrales Skalieren, bei der mehrere Berichtsserver eine einzige Berichtsserver-Datenbank und den symmetrischen Schlüssel, der für diese Datenbank die umkehrbare Verschlüsselung bereitstellt, gemeinsam nutzen.  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
 [Initialisieren eines Berichtsservers &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
 Erläutert das Erstellen von Verschlüsselungsschlüsseln.  
  
 [Sichern und Wiederherstellen von Reporting Services-Verschlüsselungsschlüsseln](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 Erläutert das Sichern von Verschlüsselungsschlüsseln und das Wiederherstellen dieser Schlüssel, um eine Berichtsserverinstallation wiederherzustellen oder zu migrieren.  
  
 [Speichern verschlüsselter Berichtsserverdaten &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 Beschreibt die Verschlüsselung auf einem Berichtsserver.  
  
 [Löschen und erneutes Erstellen von Verschlüsselungsschlüsseln &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 Erläutert das Ersetzen eines symmetrischen Schlüssels durch eine neue Version und das erneute Erstellen, wenn die symmetrischen Schlüssel nicht überprüft werden können.  
  
 [Hinzufügen und Entfernen von Verschlüsselungsschlüsseln für die Bereitstellung für horizontales Skalieren &#40;SSRS-Konfigurations-Manager&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 Beschreibt das Hinzufügen und Entfernen von Verschlüsselungsschlüsseln, um zu steuern, welche Berichtsserver Teil der Bereitstellung für dezentrales Skalieren sind.  
  
## <a name="see-also"></a>Siehe auch  
[Reporting Services-Konfigurations-Manager (einheitlicher Modus)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)

