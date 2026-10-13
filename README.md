# simple-ru-routing

**Минималистичная маршрутизация для России на основе v2fly, refilter и antifilter-community**

---

## 🎯 Цель

Создать компактный и эффективный роутинг-файл объёмом не более **5–8 МБ**, который обеспечивает точную маршрутизацию трафика.

Поможем провайдерам в эпоху дефицита сетевого оборудования, заблокируем самостоятельно ресурсы и, таким образом, снизим нагрузку на их оборудование!

Зарубежные сервисы пусть знают, что их ресурсы никому не нужны и мы сами у себя их блокируем!

---

## Happ Routing
[Роутинг с AdGuard DNS](https://raw.githubusercontent.com/ihavealotofguap/simple-ru-routing/refs/heads/master/ADGUARD-ROUTING)

[Роутинг с Cloudflare DNS](https://raw.githubusercontent.com/ihavealotofguap/simple-ru-routing/refs/heads/master/CF-ROUTING)

[AdGuard JSON Routing пример](https://raw.githubusercontent.com/ihavealotofguap/simple-ru-routing/refs/heads/master/JSON-EXAMPLE)

**Используя AdGuard DNS будьте готовы к тому, что некоторые сайты будут работать некорректно**
---

## 📦 Описание
**Списки можно посмотреть здесь -> [GEOSITE](https://github.com/ihavealotofguap/simple-ru-geosite) - [GEOIP](https://github.com/ihavealotofguap/simple-ru-geoip)**

Проект реализует маршрутизацию на базе следующих источников:
- **[v2fly/domain-list-community](https://github.com/v2fly/domain-list-community)** — список российских доменов;
- **[v2fly/geoip](https://github.com/v2fly/geoip)** — список российских IP-адресов;
- **[refilter](https://github.com/1andrevich/Re-filter-lists)** — список заблокированных российских ресурсов.
- **[antifilter-community](https://community.antifilter.download/)** — дополнительный список заблокированных российских доменов;
- **Автоматически собирается из актуальных данных каждую неделю.**
---

### 🔧 Логика маршрутизации

- Трафик к российским сайтам (по списку `category-ru`) направляется через `direct`.
- Чтобы избежать попадания заблокированных ресурсов в прямой маршрут, используются списки:
  - **antifilter-community**
  - **refilter**
- Эти списки проходят:
  - **дедупликацию**;
  - **фильтрацию** — остаются только домены в зонах `.ru`, `.su`, `.рф` и аналогичных.
- Добавлены списки Apple и Youtube для корректной работы
---

### 📊 Результат

- ✅ Все легальные российские сайты → `direct`
- 🚫 Заблокированные сайты в российских доменных зонах → `proxy`
- 🌍 Всё остальное (зарубежные сайты и сервисы) → `proxy`

---

## 📌 Замечания

- Конфигурация **не включает** полные списки для `.com`, `.net` и других международных доменов — они **по умолчанию** идут через `proxy`.
- Конфигурация **не включает** полный список antifilter, потому что в нём 700+ тысяч доменов. По большей части они мусорные и никак не поместятся на IOS устройствах.
