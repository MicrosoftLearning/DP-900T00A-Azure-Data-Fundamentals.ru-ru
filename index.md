---
title: Инструкции, размещенные в Интернете
permalink: index.html
layout: home
ms.openlocfilehash: 928f59a9cdc6a3f70d5ad651fb1b5a45b405cee8
ms.sourcegitcommit: 1117342052bce0bbd5a703bd1f763862b9129807
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/16/2022
ms.locfileid: "140682430"
---
# <a name="azure-data-fundamentals-exercises"></a>Основы данных Azure: упражнения

Используйте приведенные ниже ссылки для выполнения практических занятий по курсу [DP-900 *Microsoft Azure Data Fundamentals*](https://docs.microsoft.com/learn/certifications/courses/dp-900t00).

Для выполнения этих упражнений вам понадобится подписка Microsoft Azure. Если ваш инструктор не предоставил вам такую подписку, можете зарегистрироваться для получения бесплатной пробной версии на сайте [https://azure.microsoft.com](https://azure.microsoft.com).

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Модуль | Лаборатория |
| --- | --- | 
{% за активность на лабораторных работах  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
