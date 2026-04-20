# Референсные источники

## Списки доменов и IP

**Курированные списки сервисов РФ**

- [itdoginfo/allow-domains](https://github.com/itdoginfo/allow-domains) — курированные списки по регионам (inside/outside, Ukraine) и категориям;
  text/dnsmasq/clash/dat/srs/mrs
- [dartraiden/no-russia-hosts](https://github.com/dartraiden/no-russia-hosts) — домены сервисов, ограничивающих доступ с российских IP (enterprise, DevOps,
  semiconductors); hosts / hosts-wildcard / mihomo-wildcard
- [1andrevich/Re-filter-lists](https://github.com/1andrevich/Re-filter-lists) — домены и IP, ограниченные в РФ, плюс self-censorship; dat/srs/db/text +
  публичный BGP-сервер

**Полные агрегаты geosite / geoip**

- [Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) — расширенные geoip.dat/geosite.dat с категориями (Cloudflare, Netflix,
  Telegram, GFWList, ads); ежедневная пересборка
- [Loyalsoldier/geoip](https://github.com/Loyalsoldier/geoip) — генератор GeoIP в dat/mmdb/srs/mrs/clash/surge; кастомные категории по крупным сервисам
- [v2fly/domain-list-community](https://github.com/v2fly/domain-list-community) — исходные данные сообщества для geosite.dat, upstream для большинства
  производных
- [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat) — официальный набор geoip/geosite для mihomo (dat/mrs/mmdb/db), ежедневные релизы
- [SagerNet/sing-geosite](https://github.com/SagerNet/sing-geosite) — geosite-база для sing-box (srs)
- [SagerNet/sing-geoip](https://github.com/SagerNet/sing-geoip) — geoip-база для sing-box (srs)
- [runetfreedom/russia-v2ray-rules-dat](https://github.com/runetfreedom/russia-v2ray-rules-dat) — автогенерируемые geoip.dat/geosite.dat по блокировкам РФ,
  обновление каждые 6 часов (inside/refilter/outside)
- [runetfreedom/russia-blocked-geosite](https://github.com/runetfreedom/russia-blocked-geosite) — geosite.dat с доменами из реестра РКН, плюс ads и
  Windows-телеметрия
- [runetfreedom/russia-blocked-geoip](https://github.com/runetfreedom/russia-blocked-geoip) — geoip/mmdb/srs/mrs/clash/surge/nginx по адресам и подсетям из
  блокировок РФ, обновление каждые 6 часов

**Парсеры реестра РКН**

- [zapret-info/z-i](https://github.com/zapret-info/z-i) — официальные дампы реестра (CSV), upstream для большинства производных списков
- [antifilter.download](https://antifilter.download) — агрегированные выгрузки реестра (домены, IP, subnets) в plain text

**Тематические / DNS-блоклисты**

- [hagezi/dns-blocklists](https://github.com/hagezi/dns-blocklists) — крупный DNS-блоклист (ads, трекеры, malware, NRD); уровни Light/Normal/Pro/Pro++/Ultimate
- [MiHomoer/MiHomo-Hagezi](https://github.com/MiHomoer/MiHomo-Hagezi) — конвертация Hagezi Pro/Pro+/Ultimate в формат mihomo mrs
- [nickspaargaren/no-google](https://github.com/nickspaargaren/no-google) — блоклист доменов Google и связанных сервисов
- [legiz-ru/mihomo-rule-sets](https://github.com/legiz-ru/mihomo-rule-sets) — готовые rule sets для mihomo (mrs/yaml): ru-bundle (itdoginfo + no-russia-hosts +
  antifilter), OISD, re:filter, torrents, Discord voice IPs

## Проверка актуальности блокировок

- [OONI Explorer](https://explorer.ooni.org/country/RU) — объективные измерения блокировок
- [reestr.rublacklist.net](https://reestr.rublacklist.net) — зеркало реестра РКН
- Wikipedia «List of websites blocked in Russia»
- [Freedom on the Net](https://freedomhouse.org/country/russia/freedom-net) — годовые отчёты

## BGP и IP-диапазоны

- [bgp.he.net](https://bgp.he.net) — поиск ASN, `_prefixes` и `_prefixes6` по AS
- [core.telegram.org/resources/cidr.txt](https://core.telegram.org/resources/cidr.txt) — официальные CIDR Telegram
- [www.cloudflare.com/ips/](https://www.cloudflare.com/ips/) — официальные CIDR Cloudflare
- [ip-ranges.amazonaws.com/ip-ranges.json](https://ip-ranges.amazonaws.com/ip-ranges.json) — AWS
- [gstatic.com/ipranges/goog.json](https://www.gstatic.com/ipranges/goog.json) — Google
- [GhostRooter0953/discord-voice-ips](https://github.com/GhostRooter0953/discord-voice-ips) — Discord voice IP; репозиторий заархивирован 9 марта 2026,
  использовать как исторический референс
