---
title: Architektur | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1328a346dd9852cba349e38204b49faf32573611
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="architecture-overview-for-machine-learning-services-with-python"></a>Übersicht über die Architektur für Machine Learning-Dienste mit Python

Dieses Thema enthält einen Überblick darüber, wie Python in SQL Server, einschließlich des Sicherheitsmodells, die Komponenten in das Datenbankmodul, die Ausführung externer Skripts unterstützen, und neue Komponenten, mit denen die Interoperabilität von Python mit SQL Server integriert ist. Weitere Informationen finden Sie in den verknüpften Themen.

> [!IMPORTANT]
> Unterstützung für Python wird ab SQL Server 2017 CTP-Version 2.0. Diese Vorabversion Funktion unterliegt.

## <a name="python-interoperability"></a>Python-Interoperabilität

SQL Server Machine Learning-Services (Datenbankintern) installiert die Anaconda-Verteilung von Python und 3.5 Python-Laufzeit und Interpreter. Dadurch wird sichergestellt, dass nahezu vollständige Kompatibilität mit standard-Python-Lösungen. Python wird in einem separaten Prozess ausgeführt, von SQL Server, um sicherzustellen, dass die Datenbankvorgänge nicht gefährdet sind.

Weitere Informationen zur Interaktion von SQL Server mit Python finden Sie unter [Python-Interoperabilität](../../advanced-analytics/python/python-interoperability.md)

## <a name="components-that-support-python-integration"></a>Komponenten, die Unterstützung der Python-integration

Das in SQL Server 2016 jetzt eingeführte Extensibility Framework unterstützt die Ausführung von Python-Skript, durch das Hinzufügen von neuen sprachspezifische Komponenten. Diese Komponenten verbessern Data Exchange Geschwindigkeit und Komprimierung, und bietet eine sichere, leistungsstarke Plattform für die Ausführung externer Skripts.

Ausführliche Beschreibung der Komponenten, die z. B. Python, unterstützen die [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] und PythonLauncher, finden Sie unter [neue Komponenten](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md).

## <a name="security"></a>Sicherheit

Python-Aufgaben werden außerhalb der SQL Server-Prozess, um Sicherheit und bessere Verwaltung zu ermöglichen.

Alle Vorgänge werden von Windows-Auftragsobjekte oder SQL Server-Sicherheit gesichert. Daten werden innerhalb der Begrenzung des Kompatibilität beibehalten, durch das Durchsetzen von SQL Server-Sicherheit auf die Tabelle, Datenbank- und Instanzebene. Der Datenbankadministrator kann steuern, wer hat die Möglichkeit zum Ausführen von Python-Aufträgen, Überwachen der Verwendung von Python-Skripts von Benutzern und Anzeigen der Ressourcen verbraucht.

Weitere Informationen finden Sie unter [Sicherheit für Python](../../advanced-analytics/python/security-overview-sql-server-python-services.md)

## <a name="resource-governance"></a>Die Ressourcenkontrolle

In SQL Server Enterprise Edition können Sie die Ressourcenkontrolle verwenden, verwalten und Überwachen der Ressourcenverwendung des externen Skripts-Vorgänge, einschließlich R-Skript und Python-Skripts.

Weitere Informationen finden Sie unter [Ressourcenkontrolle für R](../../advanced-analytics/r/resource-governance-for-r-services.md).

## <a name="next-steps"></a>Nächste Schritte

[Ausführen von Python mit T-SQL](../tutorials/run-python-using-t-sql.md)