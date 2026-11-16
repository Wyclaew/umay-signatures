<div align="center">

# Umay Signatures

**Daily, signed threat intelligence for the Umay anti-malware engine.**

[English](#english) · [Türkçe](#türkçe)

</div>

---

## English

This repository is the download point for Umay's signature bundle. It holds
no source code. A scheduled pipeline rebuilds the bundle once a day and
replaces the single commit on the [`dist`](../../tree/dist) branch.

### What is in the bundle

| Content | Purpose |
| --- | --- |
| Detection rules | First-party Umay rules plus vetted community YARA rules |
| Malware domains | Sites that host or control malware |
| Phishing domains | Fake login pages, fake shops, scams |
| Ad and tracker domains | Used by the optional ad and tracker blocking |
| Command-and-control addresses | Used by the network monitor |

Domain lists are stored as truncated hashes, not as readable names.

### How it is checked before release

- Every community rule is compiled on its own. A rule the engine cannot
  compile is dropped instead of breaking the rest.
- Every community rule is run against a corpus of known-clean system
  programs. A rule that matches any of them is dropped.
- A feed that fails to download stops the build. An incomplete bundle is
  never published.

### Why you can trust a download

The bundle is signed with an Ed25519 key whose public half is compiled into
Umay. The app verifies the signature before it reads a single byte of the
contents, and refuses any bundle older than the one already installed. A
tampered or replayed file is rejected even if this repository or the network
in between were compromised.

| File | Role |
| --- | --- |
| `umay-bundle.tar.gz` | The bundle |
| `umay-bundle.tar.gz.sig` | Detached Ed25519 signature (hex) |
| `version.txt` | Build time; lets the app skip a download it already has |

Public key: `e6c6f72c7c25597a7cc631a87a64e87c005db57beff44b53af6b439e09932342`

### Sources and licences

Umay redistributes these feeds under their own terms. Thank you to the
people who maintain them.

| Source | Used for | Licence |
| --- | --- | --- |
| [YARA Forge](https://github.com/YARAHQ/yara-forge) (core set) | Detection rules | Per-rule licences, kept in each rule's metadata |
| [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists) | Ads, trackers, threat domains and addresses | GPL-3.0 |
| [Phishing.Database](https://github.com/Phishing-Database/Phishing.Database) | Phishing domains | MIT |
| [abuse.ch Feodo Tracker](https://feodotracker.abuse.ch/) | Botnet command-and-control addresses | CC0 |

The bundle as a whole is distributed under GPL-3.0.

### Reporting a false alarm

If Umay blocks a site or flags a file that is safe, open an issue here with
the domain or the file's SHA-256 hash. Do not attach the file itself.

---

## Türkçe

Bu depo, Umay'ın imza paketinin indirildiği yerdir. İçinde kaynak kod yoktur.
Zamanlanmış bir hat paketi günde bir kez yeniden üretir ve
[`dist`](../../tree/dist) dalındaki tek kaydı yenisiyle değiştirir.

### Pakette ne var

| İçerik | Ne işe yarar |
| --- | --- |
| Tespit kuralları | Umay'ın kendi kuralları ve elenmiş topluluk YARA kuralları |
| Zararlı yazılım alan adları | Zararlı yazılım barındıran veya yöneten siteler |
| Oltalama alan adları | Sahte giriş sayfaları, sahte mağazalar, dolandırıcılık siteleri |
| Reklam ve izleyici alan adları | İsteğe bağlı reklam ve izleyici engelleme için |
| Komuta-kontrol adresleri | Ağ izleyicisi için |

Alan adı listeleri okunabilir adlar olarak değil, kısaltılmış özetler olarak
saklanır.

### Yayından önce nasıl denetlenir

- Her topluluk kuralı tek başına derlenir. Motorun derleyemediği kural,
  diğerlerini bozmak yerine atılır.
- Her topluluk kuralı, temiz olduğu bilinen sistem programları üzerinde
  çalıştırılır. Bunlardan herhangi biriyle eşleşen kural atılır.
- İndirilemeyen bir kaynak derlemeyi durdurur. Eksik paket hiçbir zaman
  yayınlanmaz.

### İndirdiğiniz dosyaya neden güvenebilirsiniz

Paket, açık yarısı Umay'ın içine gömülü olan bir Ed25519 anahtarıyla
imzalanır. Uygulama, içeriğin tek baytını okumadan önce imzayı doğrular ve
kurulu olandan eski bir paketi reddeder. Bu depo ya da aradaki ağ ele
geçirilmiş olsa bile değiştirilmiş veya eski bir dosya kabul edilmez.

| Dosya | Görevi |
| --- | --- |
| `umay-bundle.tar.gz` | Paket |
| `umay-bundle.tar.gz.sig` | Ayrı Ed25519 imzası (hex) |
| `version.txt` | Üretim zamanı; uygulama elindeki paketi yeniden indirmez |

Açık anahtar: `e6c6f72c7c25597a7cc631a87a64e87c005db57beff44b53af6b439e09932342`

### Kaynaklar ve lisanslar

Umay bu kaynakları kendi lisans koşullarıyla yeniden dağıtır. Bunları
sürdüren herkese teşekkürler.

| Kaynak | Kullanım | Lisans |
| --- | --- | --- |
| [YARA Forge](https://github.com/YARAHQ/yara-forge) (core) | Tespit kuralları | Kural başına lisans, her kuralın üst verisinde korunur |
| [HaGeZi DNS Blocklists](https://github.com/hagezi/dns-blocklists) | Reklam, izleyici, tehdit alan adları ve adresleri | GPL-3.0 |
| [Phishing.Database](https://github.com/Phishing-Database/Phishing.Database) | Oltalama alan adları | MIT |
| [abuse.ch Feodo Tracker](https://feodotracker.abuse.ch/) | Botnet komuta-kontrol adresleri | CC0 |

Paketin bütünü GPL-3.0 ile dağıtılır.

### Yanlış alarm bildirme

Umay güvenli bir siteyi engelliyor ya da güvenli bir dosyayı işaretliyorsa,
alan adını veya dosyanın SHA-256 özetini yazarak burada bir kayıt açın.
Dosyanın kendisini eklemeyin.
