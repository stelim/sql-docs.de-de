---
title: "Zugreifen auf WMI-Anbieter für die Konfigurationsverwaltung mit WQL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2055cb2f38ea35c3ae4123c0bf8f1f8501dcc4e1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>Zugreifen auf WMI-Anbieter für die Konfigurationsverwaltung mit WQL
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]In diesem Abschnitt wird beschrieben, wie auszuführende [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Management Instrumentation Query Language (WQL)-Anweisungen für die WMI-Anbieter für die Computerverwaltung.  
  
 Im Beispiel wird ein WQL-Editor, WBEMtest.exe, zum Ausführen von WQL-Abfragen für den WMI-Anbieter verwendet, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienste, -Netzwerkprotokolle und -Aliasnamen aufzuzählen.  
  
### <a name="querying-services-using-wbemtest"></a>Abfragen von Diensten mit WBEMtest  
  
1.  Aus der **starten** Menü klicken Sie auf **ausführen**, und geben Sie dann **WBEMtest**.  
  
2.  Das Dialogfeld WBEMtest.exe wird angezeigt. Klicken Sie auf **Verbinden**.  
  
3.  Geben Sie im ersten Textfeld den Namespace für den WMI-Anbieter für die Computerverwaltung ein: root\Microsoft\SqlServer\ComputerManagement11. Klicken Sie auf **Verbinden**.  
  
4.  Klicken Sie auf **Abfrage**. Geben Sie eine Abfrage, die die aktuellen Dienste zur Ausführung auf dem lokalen Computer zurückgibt: **wählen \* aus SqlService.** Klicken Sie auf **Anwenden**.  
  
5.  Verfeinern Sie die Abfrage durch Hinzufügen von **, in denen ServiceName = "MSSQLSERVER"**.  
  
  