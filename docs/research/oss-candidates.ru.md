# VLP: каталог OSS-кандидатов и протокольных ориентиров

[English overview](oss-candidates.md) · [Машиночитаемый каталог](oss-candidates.json)

Дата исследования: **2026-10-19**. Репозиторий: [VLP-Protocol-Core](https://github.com/a91602788-jpg/VLP-Protocol-Core).

**Research Gate: NOT_EVALUATED. Все 16 кандидатов: NOT_ADOPTED.** Это исследовательский каталог; выбор runtime dependencies и разрешение реализации остаются отдельными решениями.

## Что проверено и что означает ревизия

Через GitHub plugin прочитаны repository metadata, наблюдаемый commit default branch, root/component listings и перечисленные LICENSE/manifest/README по точному commit SHA. Для протокольных ориентиров открыты первичные источники IETF, Noise, NIST и WireGuard.

Наблюдаемый SHA даёт воспроизводимую ссылку на изученный материал. Он **не является pinned dependency**, утверждённым release, результатом проверки подписи релиза или разрешением запуска. Source version из manifest может отличаться от опубликованного и подходящего для внедрения release; development HEAD автоматически не выбирается.

Зависимости, runtime code, vendored source, lockfile и SBOM не создавались. Полный транзитивный граф, release signatures, advisories, практическая совместимость, build, benchmark и аудит безопасности не проверялись. Отсутствие флага archived в repository metadata не доказывает достаточное сопровождение.

Лицензионные наблюдения относятся только к перечисленным файлам. Они не являются общим юридическим заключением о конкретной сборке, модификации, способе распространения или совместимости всех зависимостей. До любого reuse нужны отдельные license/compatibility, maintenance/security и target-platform reviews. Предлагаемая лицензия VLP не изменяет лицензии upstream.

## Как читать классификацию

- **Кандидат на reuse:** компонент может решать отдельную инженерную задачу, если пройдёт проверки и будет принят архитектурой.
- **Reference:** изучается существующее решение; source code в VLP не переносится. Это не утверждение о юридическом запрете всякого reuse.
- **Reference / точечный reuse:** основной интерес — поведение существующего протокола; отдельный компонент можно рассмотреть только после конкретного review.
- **Только экспериментальный benchmark:** не предлагается как production runtime dependency; даже лабораторное выполнение на этом этапе не проводилось.

## Сводная таблица

| ID | Кандидат | Классификация | Наблюдаемая лицензия | Ревизия | Статус |
| --- | --- | --- | --- | --- | --- |
| OSS-001 | [snow](https://github.com/mcginty/snow) | Кандидат на reuse | Apache-2.0 OR MIT | [8ac60f51cfe3](https://github.com/mcginty/snow/commit/8ac60f51cfe3e010c84f0a454cc575ad9204fa12) | NOT_ADOPTED |
| OSS-002 | [RustCrypto AEADs: chacha20poly1305, aes-gcm](https://github.com/RustCrypto/AEADs) | Кандидат на reuse | Apache-2.0 OR MIT | [f90367cf0728](https://github.com/RustCrypto/AEADs/commit/f90367cf07286ab5db652970e8268fbeab62a682) | NOT_ADOPTED |
| OSS-003 | [RustCrypto hkdf](https://github.com/RustCrypto/KDFs) | Кандидат на reuse | MIT OR Apache-2.0 | [19a0df65a558](https://github.com/RustCrypto/KDFs/commit/19a0df65a558feefed0722dd0de73ef4b966d79f) | NOT_ADOPTED |
| OSS-004 | [x25519-dalek](https://github.com/dalek-cryptography/curve25519-dalek) | Кандидат на reuse | BSD-3-Clause | [97a020d18597](https://github.com/dalek-cryptography/curve25519-dalek/commit/97a020d185970839ed1d3f3a5c22aca816631786) | NOT_ADOPTED |
| OSS-005 | [rustls](https://github.com/rustls/rustls) | Кандидат на reuse | Apache-2.0 OR ISC OR MIT | [bb2165fa87ef](https://github.com/rustls/rustls/commit/bb2165fa87ef23fb7d12a28c086f078b4f5d412a) | NOT_ADOPTED |
| OSS-006 | [Quinn](https://github.com/quinn-rs/quinn) | Кандидат на reuse | MIT OR Apache-2.0 | [ecc0dcfdeaec](https://github.com/quinn-rs/quinn/commit/ecc0dcfdeaec996d276da31d836f965753b66ea4) | NOT_ADOPTED |
| OSS-007 | [quiche](https://github.com/cloudflare/quiche) | Кандидат на reuse | BSD-2-Clause | [acf560f2e4a3](https://github.com/cloudflare/quiche/commit/acf560f2e4a3d9254a1b668a50af0e114c84fe6f) | NOT_ADOPTED |
| OSS-008 | [s2n-quic](https://github.com/aws/s2n-quic) | Кандидат на reuse | Apache-2.0 | [8c1fca6a3e38](https://github.com/aws/s2n-quic/commit/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea) | NOT_ADOPTED |
| OSS-009 | [Pion ICE](https://github.com/pion/ice) | Кандидат на reuse | MIT | [5fdc5b169d4a](https://github.com/pion/ice/commit/5fdc5b169d4a06927409f01544fe38f8b3eecd3a) | NOT_ADOPTED |
| OSS-010 | [Pion STUN](https://github.com/pion/stun) | Кандидат на reuse | MIT | [d39c70b1e859](https://github.com/pion/stun/commit/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c) | NOT_ADOPTED |
| OSS-011 | [Pion TURN](https://github.com/pion/turn) | Кандидат на reuse | MIT | [b1bcca91802d](https://github.com/pion/turn/commit/b1bcca91802dffac8070b12ce0bee5bf244ffef1) | NOT_ADOPTED |
| OSS-012 | [liboqs](https://github.com/open-quantum-safe/liboqs) | Только экспериментальный benchmark | MIT (general library; component-specific exceptions) | [fd44469daeff](https://github.com/open-quantum-safe/liboqs/commit/fd44469daeffe6b28f031f54f9bb66cbae69a572) | NOT_ADOPTED |
| OSS-013 | [Xray-core / VLESS reference](https://github.com/XTLS/Xray-core) | Reference | MPL-2.0 | [92ccc939aaf4](https://github.com/XTLS/Xray-core/commit/92ccc939aaf4f8965f369cf0b142e005aeaa11d5) | NOT_ADOPTED |
| OSS-014 | [Hysteria 2](https://github.com/HyNetworks/hysteria) | Reference / точечный reuse | MIT | [ca8fbd874fd6](https://github.com/HyNetworks/hysteria/commit/ca8fbd874fd6ca82413948de6dc5924405e103e1) | NOT_ADOPTED |
| OSS-015 | [AmneziaWG Go](https://github.com/amnezia-vpn/amneziawg-go) | Reference / точечный reuse | MIT | [b5928efb6ca1](https://github.com/amnezia-vpn/amneziawg-go/commit/b5928efb6ca19f0153958460c3d141f04abc5c2e) | NOT_ADOPTED |
| OSS-016 | [wireguard-go](https://github.com/WireGuard/wireguard-go) | Reference / точечный reuse | MIT | [2631ce99a06f](https://github.com/WireGuard/wireguard-go/commit/2631ce99a06f27120d581611cf125d68bc6aa565) | NOT_ADOPTED |

## Инженерные границы выбора

1. **Noise handshake и primitive crates не нужно автоматически включать одновременно.** Если выбранный provider уже решает задачу, второй ручной key schedule увеличивает область проверки.
2. **Quinn, quiche и s2n-quic — альтернативные реализации QUIC.** Использование одной из них как carrier не превращает QUIC в новый native UDP transport. Требуется разделить responsibility за recovery, pacing, congestion control и flow control.
3. **rustls не заменяет DTLS или формальную TLS/UDP-интеграцию.** Собственный transport с TLS handshake потребует отдельной спецификации взаимодействия.
4. **Pion ICE/STUN/TURN — Go-компоненты для отдельного traversal/relay-сценария.** P2P ещё не утверждён; обычный клиент с публично доступным сервером не требует автоматического включения всего набора.
5. **X25519 — key agreement, а не цифровая подпись.** Выбор identity authentication и authorization не закрывается одним primitive.
6. **liboqs — только исследовательский кандидат.** Его upstream README не рекомендует полагаться на библиотеку в production или для защиты sensitive data; это рекомендация upstream, а не юридический запрет.
7. **Xray, Hysteria, AmneziaWG и WireGuard — существующие решения.** Форк или перенос их transport/handshake не доказывает самостоятельность и новизну VLP.

## Карточки кандидатов

### OSS-001. snow

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [mcginty/snow](https://github.com/mcginty/snow).

**Наблюдаемая ревизия:** [`8ac60f51cfe3e010c84f0a454cc575ad9204fa12`](https://github.com/mcginty/snow/commit/8ac60f51cfe3e010c84f0a454cc575ad9204fa12), branch `main`, commit time `2026-03-25T20:18:15Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/mcginty/snow/branches/main). Это не dependency pin.

**Предлагаемая роль:** Кандидат на исполнение неизменённого Noise handshake в будущем Rust-ядре; не готовый UDP-транспорт.

**Лицензия:** Apache-2.0 OR MIT. Прочитанные основания: [Cargo.toml](https://github.com/mcginty/snow/blob/8ac60f51cfe3e010c84f0a454cc575ad9204fa12/Cargo.toml); [LICENSE-APACHE](https://github.com/mcginty/snow/blob/8ac60f51cfe3e010c84f0a454cc575ad9204fa12/LICENSE-APACHE); [LICENSE-MIT](https://github.com/mcginty/snow/blob/8ac60f51cfe3e010c84f0a454cc575ad9204fa12/LICENSE-MIT).

**Технические источники:** [README.md](https://github.com/mcginty/snow/blob/8ac60f51cfe3e010c84f0a454cc575ad9204fa12/README.md); [Cargo.toml](https://github.com/mcginty/snow/blob/8ac60f51cfe3e010c84f0a454cc575ad9204fa12/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- README на наблюдаемой ревизии прямо сообщает об отсутствии формального аудита; это существенное ограничение кандидата.
- Потребуются отдельная спецификация replay window, packet framing, state machine, key update и привязки negotiation к transcript.
- Не включать risky-raw-split, экспериментальные PQ-возможности или дополнительные cipher suites без отдельного review.
- Согласовать фактический crypto provider и его транзитивные зависимости; наличие snow не требует параллельного самостоятельного handshake из primitives.

**Дополнительные наблюдения:**

- В Cargo.toml наблюдается версия 0.10.0 и rust-version 1.85; опубликованный релиз для внедрения не выбран.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-07-06T08:14:33Z`; [источник](https://api.github.com/repos/mcginty/snow). Полный maintenance review и security assessment не завершены.

### OSS-002. RustCrypto AEADs: chacha20poly1305, aes-gcm

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [RustCrypto/AEADs](https://github.com/RustCrypto/AEADs).

**Наблюдаемая ревизия:** [`f90367cf07286ab5db652970e8268fbeab62a682`](https://github.com/RustCrypto/AEADs/commit/f90367cf07286ab5db652970e8268fbeab62a682), branch `master`, commit time `2026-09-14T14:05:12Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/RustCrypto/AEADs/branches/master). Это не dependency pin.

**Предлагаемая роль:** AEAD primitives для обоснованного record layer либо провайдера handshake, если выбранная библиотека не закрывает этот слой.

**Лицензия:** Apache-2.0 OR MIT. Прочитанные основания: [chacha20poly1305/Cargo.toml](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/chacha20poly1305/Cargo.toml); [chacha20poly1305/LICENSE-APACHE](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/chacha20poly1305/LICENSE-APACHE); [chacha20poly1305/LICENSE-MIT](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/chacha20poly1305/LICENSE-MIT); [aes-gcm/Cargo.toml](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/aes-gcm/Cargo.toml); [aes-gcm/LICENSE-APACHE](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/aes-gcm/LICENSE-APACHE); [aes-gcm/LICENSE-MIT](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/aes-gcm/LICENSE-MIT).

**Технические источники:** [README.md](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/README.md); [chacha20poly1305/Cargo.toml](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/chacha20poly1305/Cargo.toml); [aes-gcm/Cargo.toml](https://github.com/RustCrypto/AEADs/blob/f90367cf07286ab5db652970e8268fbeab62a682/aes-gcm/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- AEAD не выполняет handshake, аутентификацию устройства, replay protection и authorization самостоятельно.
- Уникальность nonce, направление, generation keys, authenticated headers и лимиты использования должны быть определены в VLP.
- Не складывать ChaCha20-Poly1305 и AES-GCM последовательно ради заявленного усиления; выбор cipher suite требует обоснования и аутентифицированного согласования.
- Проверять конкретные crates, features, target CPU и provider; общий monorepo не является одной зависимостью.

**Дополнительные наблюдения:**

- Лицензии проверены на уровне двух component directories, поскольку общей root LICENSE в просмотренном root listing нет.
- Наблюдаемые manifests: chacha20poly1305 0.11.0, aes-gcm 0.11.1; это не выбранные версии зависимостей.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-13T04:55:12Z`; [источник](https://api.github.com/repos/RustCrypto/AEADs). Полный maintenance review и security assessment не завершены.

### OSS-003. RustCrypto hkdf

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [RustCrypto/KDFs](https://github.com/RustCrypto/KDFs).

**Наблюдаемая ревизия:** [`19a0df65a558feefed0722dd0de73ef4b966d79f`](https://github.com/RustCrypto/KDFs/commit/19a0df65a558feefed0722dd0de73ef4b966d79f), branch `master`, commit time `2026-06-23T17:38:47Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/RustCrypto/KDFs/branches/master). Это не dependency pin.

**Предлагаемая роль:** Реализация HKDF для специфицированного key schedule или отдельного исследовательского сравнения; не замена дизайну key schedule.

**Лицензия:** MIT OR Apache-2.0. Прочитанные основания: [hkdf/Cargo.toml](https://github.com/RustCrypto/KDFs/blob/19a0df65a558feefed0722dd0de73ef4b966d79f/hkdf/Cargo.toml); [hkdf/LICENSE-APACHE](https://github.com/RustCrypto/KDFs/blob/19a0df65a558feefed0722dd0de73ef4b966d79f/hkdf/LICENSE-APACHE); [hkdf/LICENSE-MIT](https://github.com/RustCrypto/KDFs/blob/19a0df65a558feefed0722dd0de73ef4b966d79f/hkdf/LICENSE-MIT).

**Технические источники:** [README.md](https://github.com/RustCrypto/KDFs/blob/19a0df65a558feefed0722dd0de73ef4b966d79f/README.md); [hkdf/Cargo.toml](https://github.com/RustCrypto/KDFs/blob/19a0df65a558feefed0722dd0de73ef4b966d79f/hkdf/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- Состав input key material, labels, salt и context должен следовать выбранной конструкции; собственное произвольное смешивание ключей не утверждено.
- Не использовать HKDF вместо password hashing либо аутентифицированного обмена ключами.
- Не дублировать вручную внутренний key schedule snow/rustls без необходимости и отдельного review.

**Дополнительные наблюдения:**

- Лицензия проверена в component hkdf; manifest содержит 0.13.0 и rust-version 1.85, но dependency selection не выполнен.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-09-21T16:52:51Z`; [источник](https://api.github.com/repos/RustCrypto/KDFs). Полный maintenance review и security assessment не завершены.

### OSS-004. x25519-dalek

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [dalek-cryptography/curve25519-dalek](https://github.com/dalek-cryptography/curve25519-dalek).

**Наблюдаемая ревизия:** [`97a020d185970839ed1d3f3a5c22aca816631786`](https://github.com/dalek-cryptography/curve25519-dalek/commit/97a020d185970839ed1d3f3a5c22aca816631786), branch `main`, commit time `2026-09-24T14:03:36Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/dalek-cryptography/curve25519-dalek/branches/main). Это не dependency pin.

**Предлагаемая роль:** X25519 Diffie–Hellman key agreement, если выбранному провайдеру нужен этот primitive; X25519 не является цифровой подписью.

**Лицензия:** BSD-3-Clause. Прочитанные основания: [x25519-dalek/Cargo.toml](https://github.com/dalek-cryptography/curve25519-dalek/blob/97a020d185970839ed1d3f3a5c22aca816631786/x25519-dalek/Cargo.toml); [x25519-dalek/LICENSE](https://github.com/dalek-cryptography/curve25519-dalek/blob/97a020d185970839ed1d3f3a5c22aca816631786/x25519-dalek/LICENSE).

**Технические источники:** [x25519-dalek/README.md](https://github.com/dalek-cryptography/curve25519-dalek/blob/97a020d185970839ed1d3f3a5c22aca816631786/x25519-dalek/README.md); [x25519-dalek/Cargo.toml](https://github.com/dalek-cryptography/curve25519-dalek/blob/97a020d185970839ed1d3f3a5c22aca816631786/x25519-dalek/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- Сам по себе DH не аутентифицирует удалённую сторону; требуется стандартный authenticated handshake.
- Проверить генерацию ephemeral secrets, отсутствие их повторного использования, уничтожение секретов и обработку недопустимых входов согласно выбранному профилю.
- Не смешивать API и лицензии x25519-dalek с соседними crates monorepo.

**Дополнительные наблюдения:**

- Актуальный изученный component расположен в monorepo curve25519-dalek/x25519-dalek.
- Manifest содержит 3.0.0; эта source version не названа принятой или установленной.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-09-24T14:03:37Z`; [источник](https://api.github.com/repos/dalek-cryptography/curve25519-dalek). Полный maintenance review и security assessment не завершены.

### OSS-005. rustls

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [rustls/rustls](https://github.com/rustls/rustls).

**Наблюдаемая ревизия:** [`bb2165fa87ef23fb7d12a28c086f078b4f5d412a`](https://github.com/rustls/rustls/commit/bb2165fa87ef23fb7d12a28c086f078b4f5d412a), branch `main`, commit time `2026-10-16T15:00:52Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/rustls/rustls/branches/main). Это не dependency pin.

**Предлагаемая роль:** Кандидат на TLS для carrier / QUIC-интеграции и контрольную архитектуру с TLS 1.3.

**Лицензия:** Apache-2.0 OR ISC OR MIT. Прочитанные основания: [LICENSE](https://github.com/rustls/rustls/blob/bb2165fa87ef23fb7d12a28c086f078b4f5d412a/LICENSE); [rustls/Cargo.toml](https://github.com/rustls/rustls/blob/bb2165fa87ef23fb7d12a28c086f078b4f5d412a/rustls/Cargo.toml).

**Технические источники:** [README.md](https://github.com/rustls/rustls/blob/bb2165fa87ef23fb7d12a28c086f078b4f5d412a/README.md); [Cargo.toml](https://github.com/rustls/rustls/blob/bb2165fa87ef23fb7d12a28c086f078b4f5d412a/Cargo.toml); [rustls/Cargo.toml](https://github.com/rustls/rustls/blob/bb2165fa87ef23fb7d12a28c086f078b4f5d412a/rustls/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- TLS record layer нельзя объявлять готовым протоколом для произвольного ненадёжного UDP; собственная интеграция требует самостоятельного анализа.
- Проверить выбор crypto provider, certificate validation, trust anchors, client authentication и транзитивные лицензии.
- Наблюдаемый rustls/Cargo.toml имеет version 0.24.0-dev.2; development HEAD не должен автоматически становиться runtime dependency.

**Дополнительные наблюдения:**

- Root LICENSE разрешает выбор одной из трёх перечисленных лицензий; проверена также license expression компонента.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-16T15:10:56Z`; [источник](https://api.github.com/repos/rustls/rustls). Полный maintenance review и security assessment не завершены.

### OSS-006. Quinn

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [quinn-rs/quinn](https://github.com/quinn-rs/quinn).

**Наблюдаемая ревизия:** [`ecc0dcfdeaec996d276da31d836f965753b66ea4`](https://github.com/quinn-rs/quinn/commit/ecc0dcfdeaec996d276da31d836f965753b66ea4), branch `main`, commit time `2026-10-18T02:09:37Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/quinn-rs/quinn/branches/main). Это не dependency pin.

**Предлагаемая роль:** Кандидат на настоящий QUIC carrier и baseline benchmark; не готовое самостоятельное native UDP-ядро VLP.

**Лицензия:** MIT OR Apache-2.0. Прочитанные основания: [Cargo.toml](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/Cargo.toml); [quinn/Cargo.toml](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/quinn/Cargo.toml); [LICENSE-APACHE](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/LICENSE-APACHE); [LICENSE-MIT](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/LICENSE-MIT).

**Технические источники:** [README.md](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/README.md); [Cargo.toml](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/Cargo.toml); [quinn/Cargo.toml](https://github.com/quinn-rs/quinn/blob/ecc0dcfdeaec996d276da31d836f965753b66ea4/quinn/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- Определить владельца retransmission, congestion control, pacing и flow control, чтобы не получить два конфликтующих транспортных контура.
- Различать QUIC streams и datagrams; нельзя обещать сохранение дейтаграммных свойств при переносе на reliable stream.
- Согласовать async runtime, crypto provider и версии.
- В README наблюдается MSRV 1.80.0, в workspace manifest rust-version 1.88.0: перед внедрением разрешить расхождение на конкретном релизе.

**Дополнительные наблюдения:**

- Workspace license наследуется компонентом quinn; оба manifest проверены.
- Manifest quinn содержит 0.12.0; версия для внедрения не выбрана.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-18T02:11:33Z`; [источник](https://api.github.com/repos/quinn-rs/quinn). Полный maintenance review и security assessment не завершены.

### OSS-007. quiche

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [cloudflare/quiche](https://github.com/cloudflare/quiche).

**Наблюдаемая ревизия:** [`acf560f2e4a3d9254a1b668a50af0e114c84fe6f`](https://github.com/cloudflare/quiche/commit/acf560f2e4a3d9254a1b668a50af0e114c84fe6f), branch `master`, commit time `2026-10-16T14:41:09Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/cloudflare/quiche/branches/master). Это не dependency pin.

**Предлагаемая роль:** Альтернативный QUIC / HTTP/3 carrier и независимый baseline реализации.

**Лицензия:** BSD-2-Clause. Прочитанные основания: [COPYING](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/COPYING); [Cargo.toml](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/Cargo.toml); [quiche/Cargo.toml](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/quiche/Cargo.toml).

**Технические источники:** [README.md](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/README.md); [Cargo.toml](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/Cargo.toml); [quiche/Cargo.toml](https://github.com/cloudflare/quiche/blob/acf560f2e4a3d9254a1b668a50af0e114c84fe6f/quiche/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- Оценить event loop и socket integration, TLS backend, native build chain, memory/resource ownership и поддержку целевых платформ.
- Лицензия root COPYING не заменяет проверку включённых сторонних компонентов и выбранного TLS backend.
- Не извлекать из QUIC отдельные recovery/crypto части без анализа их инвариантов.

**Дополнительные наблюдения:**

- Компонент наследует BSD-2-Clause из workspace; manifest содержит 0.30.0 и rust-version 1.88.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-16T14:43:34Z`; [источник](https://api.github.com/repos/cloudflare/quiche). Полный maintenance review и security assessment не завершены.

### OSS-008. s2n-quic

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [aws/s2n-quic](https://github.com/aws/s2n-quic).

**Наблюдаемая ревизия:** [`8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea`](https://github.com/aws/s2n-quic/commit/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea), branch `main`, commit time `2026-10-16T23:00:18Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/aws/s2n-quic/branches/main). Это не dependency pin.

**Предлагаемая роль:** Альтернативная реализация QUIC для carrier и сравнения транспортного поведения.

**Лицензия:** Apache-2.0. Прочитанные основания: [LICENSE](https://github.com/aws/s2n-quic/blob/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea/LICENSE).

**Технические источники:** [README.md](https://github.com/aws/s2n-quic/blob/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea/README.md); [Cargo.toml](https://github.com/aws/s2n-quic/blob/8c1fca6a3e3861b5fc6c570e384cc454fbbde8ea/Cargo.toml).

**Риски интеграции и обязательные проверки:**

- README описывает provider architecture и TLS-интеграции; для VLP нужно отдельно выбрать и проверить конкретный backend.
- Размер графа зависимостей, поддержка платформ, binding/FFI и операционная сложность зависят от конфигурации.
- Заявления upstream о testing/compliance не являются подтверждением безопасности VLP или независимым аудитом выбранной сборки.

**Дополнительные наблюдения:**

- Root LICENSE прочитан; transitive license inventory не выполнен.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-17T03:36:56Z`; [источник](https://api.github.com/repos/aws/s2n-quic). Полный maintenance review и security assessment не завершены.

### OSS-009. Pion ICE

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [pion/ice](https://github.com/pion/ice).

**Наблюдаемая ревизия:** [`5fdc5b169d4a06927409f01544fe38f8b3eecd3a`](https://github.com/pion/ice/commit/5fdc5b169d4a06927409f01544fe38f8b3eecd3a), branch `main`, commit time `2026-10-16T17:43:31Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/pion/ice/branches/main). Это не dependency pin.

**Предлагаемая роль:** Кандидат на отдельный Go-компонент ICE/NAT traversal либо interoperability harness при подтверждённой потребности P2P.

**Лицензия:** MIT. Прочитанные основания: [LICENSE](https://github.com/pion/ice/blob/5fdc5b169d4a06927409f01544fe38f8b3eecd3a/LICENSE).

**Технические источники:** [README.md](https://github.com/pion/ice/blob/5fdc5b169d4a06927409f01544fe38f8b3eecd3a/README.md); [go.mod](https://github.com/pion/ice/blob/5fdc5b169d4a06927409f01544fe38f8b3eecd3a/go.mod).

**Риски интеграции и обязательные проверки:**

- Go library не становится непосредственной Rust dependency; выбрать границу отдельного процесса/сервиса либо иной адаптер.
- Не требуется по умолчанию для обычного client → public server; необходимость P2P ещё не утверждена.
- Проверить signaling authorization, candidate exposure, resource limits и поведение при смене сети.

**Дополнительные наблюдения:**

- Наблюдаемое module path github.com/pion/ice/v5; license review также должен охватить каталог LICENSES и transitive dependencies.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-19T03:30:24Z`; [источник](https://api.github.com/repos/pion/ice). Полный maintenance review и security assessment не завершены.

### OSS-010. Pion STUN

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [pion/stun](https://github.com/pion/stun).

**Наблюдаемая ревизия:** [`d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c`](https://github.com/pion/stun/commit/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c), branch `main`, commit time `2026-10-05T06:45:03Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/pion/stun/branches/main). Это не dependency pin.

**Предлагаемая роль:** STUN-компонент для будущего traversal harness / отдельного Go-сервиса.

**Лицензия:** MIT. Прочитанные основания: [LICENSE](https://github.com/pion/stun/blob/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c/LICENSE).

**Технические источники:** [README.md](https://github.com/pion/stun/blob/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c/README.md); [go.mod](https://github.com/pion/stun/blob/d39c70b1e859fabb0e3f937e94d3c7e25fe56c1c/go.mod).

**Риски интеграции и обязательные проверки:**

- STUN не заменяет relay и защищённый транспорт VLP.
- Проверить transaction validation, authentication по применяемому режиму, retry budget и ограничения ответов.
- Согласовать процессную границу Go/Rust; не добавлять отдельный STUN слой без утверждённого сценария.

**Дополнительные наблюдения:**

- Наблюдаемое module path github.com/pion/stun/v4; root license не завершает проверку LICENSES/transitive graph.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-17T01:47:24Z`; [источник](https://api.github.com/repos/pion/stun). Полный maintenance review и security assessment не завершены.

### OSS-011. Pion TURN

**Статус:** NOT_ADOPTED. **Классификация:** Кандидат на reuse.

**Репозиторий:** [pion/turn](https://github.com/pion/turn).

**Наблюдаемая ревизия:** [`b1bcca91802dffac8070b12ce0bee5bf244ffef1`](https://github.com/pion/turn/commit/b1bcca91802dffac8070b12ce0bee5bf244ffef1), branch `main`, commit time `2026-10-05T06:41:58Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/pion/turn/branches/main). Это не dependency pin.

**Предлагаемая роль:** Кандидат на авторизованный relay для подтверждённых P2P-сценариев или controlled test harness.

**Лицензия:** MIT. Прочитанные основания: [LICENSE](https://github.com/pion/turn/blob/b1bcca91802dffac8070b12ce0bee5bf244ffef1/LICENSE).

**Технические источники:** [README.md](https://github.com/pion/turn/blob/b1bcca91802dffac8070b12ce0bee5bf244ffef1/README.md); [go.mod](https://github.com/pion/turn/blob/b1bcca91802dffac8070b12ce0bee5bf244ffef1/go.mod).

**Риски интеграции и обязательные проверки:**

- Обязательны allocation lifetime, quotas, разрешения адресов назначения и ограничения расходов на bandwidth.
- Не допускать превращения relay в неограниченный публичный ретранслятор; права клиента проверяются сервером.
- Go runtime и формат интеграции требуют отдельного архитектурного решения.

**Дополнительные наблюдения:**

- Наблюдаемое module path github.com/pion/turn/v5; license review должен охватить LICENSES и транзитивные модули.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-13T17:11:51Z`; [источник](https://api.github.com/repos/pion/turn). Полный maintenance review и security assessment не завершены.

### OSS-012. liboqs

**Статус:** NOT_ADOPTED. **Классификация:** Только экспериментальный benchmark.

**Репозиторий:** [open-quantum-safe/liboqs](https://github.com/open-quantum-safe/liboqs).

**Наблюдаемая ревизия:** [`fd44469daeffe6b28f031f54f9bb66cbae69a572`](https://github.com/open-quantum-safe/liboqs/commit/fd44469daeffe6b28f031f54f9bb66cbae69a572), branch `main`, commit time `2026-10-08T17:43:53Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/open-quantum-safe/liboqs/branches/main). Это не dependency pin.

**Предлагаемая роль:** Только кандидат на изолированные измерения PQ-алгоритмов, размеров handshake и interoperability после разрешения лабораторных работ.

**Лицензия:** MIT (general library; component-specific exceptions). Прочитанные основания: [LICENSE.txt](https://github.com/open-quantum-safe/liboqs/blob/fd44469daeffe6b28f031f54f9bb66cbae69a572/LICENSE.txt).

**Технические источники:** [README.md](https://github.com/open-quantum-safe/liboqs/blob/fd44469daeffe6b28f031f54f9bb66cbae69a572/README.md).

**Риски интеграции и обязательные проверки:**

- README прямо не рекомендует опираться на библиотеку в production или для защиты sensitive data; применение в runtime VLP не предлагается.
- Root LICENSE.txt предупреждает об иных лицензиях отдельных сторонних subfolders.
- Нужны отдельные review hybrid construction, KEM authentication/binding, C/FFI boundary, выбранного algorithm set и параметров.
- Наличие ML-KEM не доказывает безопасность всего нового handshake.

**Дополнительные наблюдения:**

- Даже experimental benchmark сейчас не запущен; только исследовательский кандидат.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-18T02:25:08Z`; [источник](https://api.github.com/repos/open-quantum-safe/liboqs). Полный maintenance review и security assessment не завершены.

### OSS-013. Xray-core / VLESS reference

**Статус:** NOT_ADOPTED. **Классификация:** Reference.

**Репозиторий:** [XTLS/Xray-core](https://github.com/XTLS/Xray-core).

**Наблюдаемая ревизия:** [`92ccc939aaf4f8965f369cf0b142e005aeaa11d5`](https://github.com/XTLS/Xray-core/commit/92ccc939aaf4f8965f369cf0b142e005aeaa11d5), branch `main`, commit time `2026-10-17T15:23:56Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/XTLS/Xray-core/branches/main). Это не dependency pin.

**Предлагаемая роль:** Изучение существующих proxy/transport boundaries, VLESS и operational integration; baseline существующего продукта.

**Лицензия:** MPL-2.0. Прочитанные основания: [LICENSE](https://github.com/XTLS/Xray-core/blob/92ccc939aaf4f8965f369cf0b142e005aeaa11d5/LICENSE).

**Технические источники:** [README.md](https://github.com/XTLS/Xray-core/blob/92ccc939aaf4f8965f369cf0b142e005aeaa11d5/README.md); [go.mod](https://github.com/XTLS/Xray-core/blob/92ccc939aaf4f8965f369cf0b142e005aeaa11d5/go.mod).

**Риски интеграции и обязательные проверки:**

- Xray-core не является библиотекой нового native UDP transport VLP; большая кодовая база и Go runtime не должны переноситься целиком по умолчанию.
- Повторное использование конкретного файла допускается к рассмотрению только после отдельного анализа MPL-2.0, notices, производных изменений и способа распространения.
- Нельзя автоматически перелицензировать upstream code в предлагаемую для VLP Apache-2.0.
- Observed go.mod содержит go 1.27; toolchain/release compatibility перед любым выполнением требует отдельной проверки.

**Дополнительные наблюдения:**

- REFERENCE_ONLY — текущее архитектурное решение каталога, а не утверждение о запрете любого reuse по MPL-2.0.
- Новые функции текущего Xray нельзя выводить только из исторического описания VLESS; поведение изучать по конкретной версии.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-19T00:20:51Z`; [источник](https://api.github.com/repos/XTLS/Xray-core). Полный maintenance review и security assessment не завершены.

### OSS-014. Hysteria 2

**Статус:** NOT_ADOPTED. **Классификация:** Reference / точечный reuse.

**Репозиторий:** [HyNetworks/hysteria](https://github.com/HyNetworks/hysteria). Исторические адреса: [https://github.com/apernet/hysteria](https://github.com/apernet/hysteria).

**Наблюдаемая ревизия:** [`ca8fbd874fd6ca82413948de6dc5924405e103e1`](https://github.com/HyNetworks/hysteria/commit/ca8fbd874fd6ca82413948de6dc5924405e103e1), branch `master`, commit time `2026-10-05T04:00:22Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/HyNetworks/hysteria/branches/master). Это не dependency pin.

**Предлагаемая роль:** Reference QUIC-based proxy; кандидат на точечное изучение и reuse отдельных компонентов после review, но не готовое самостоятельное UDP-ядро VLP.

**Лицензия:** MIT. Прочитанные основания: [LICENSE.md](https://github.com/HyNetworks/hysteria/blob/ca8fbd874fd6ca82413948de6dc5924405e103e1/LICENSE.md).

**Технические источники:** [README.md](https://github.com/HyNetworks/hysteria/blob/ca8fbd874fd6ca82413948de6dc5924405e103e1/README.md); [PROTOCOL.md](https://github.com/HyNetworks/hysteria/blob/ca8fbd874fd6ca82413948de6dc5924405e103e1/PROTOCOL.md); [core/go.mod](https://github.com/HyNetworks/hysteria/blob/ca8fbd874fd6ca82413948de6dc5924405e103e1/core/go.mod); [app/go.mod](https://github.com/HyNetworks/hysteria/blob/ca8fbd874fd6ca82413948de6dc5924405e103e1/app/go.mod).

**Риски интеграции и обязательные проверки:**

- PROTOCOL.md требует QUIC RFC 9000 и DATAGRAM extension; перенос core сохраняет зависимость от архитектуры Hysteria/QUIC.
- Проверить dependencies и notices по реально используемым core/extras/app компонентам; MIT в root не доказывает единый license profile всей сборки.
- Маркетинговые заявления о неотличимости трафика не являются результатом независимого тестирования VLP.
- Наблюдаемая source revision использует Go module paths с apernet и fork quic-go; перенос repository не равен смене module path.

**Дополнительные наблюдения:**

- Исторический https://api.github.com/repos/apernet/hysteria вернул Moved Permanently; новый canonical repository HyNetworks/hysteria подтверждён API, repository id 257434373.
- core/go.mod содержит github.com/apernet/hysteria/core/v2 и go 1.26.0; выбранного release/pin нет.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-13T18:17:44Z`; [источник](https://api.github.com/repos/HyNetworks/hysteria). Полный maintenance review и security assessment не завершены.

### OSS-015. AmneziaWG Go

**Статус:** NOT_ADOPTED. **Классификация:** Reference / точечный reuse.

**Репозиторий:** [amnezia-vpn/amneziawg-go](https://github.com/amnezia-vpn/amneziawg-go).

**Наблюдаемая ревизия:** [`b5928efb6ca19f0153958460c3d141f04abc5c2e`](https://github.com/amnezia-vpn/amneziawg-go/commit/b5928efb6ca19f0153958460c3d141f04abc5c2e), branch `master`, commit time `2026-08-28T15:48:27Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/amnezia-vpn/amneziawg-go/branches/master). Это не dependency pin.

**Предлагаемая роль:** Изучение модификаций WireGuard-Go, packet obfuscation и userspace integration; точечный reuse возможен только как отдельное решение.

**Лицензия:** MIT. Прочитанные основания: [LICENSE](https://github.com/amnezia-vpn/amneziawg-go/blob/b5928efb6ca19f0153958460c3d141f04abc5c2e/LICENSE).

**Технические источники:** [README.md](https://github.com/amnezia-vpn/amneziawg-go/blob/b5928efb6ca19f0153958460c3d141f04abc5c2e/README.md); [go.mod](https://github.com/amnezia-vpn/amneziawg-go/blob/b5928efb6ca19f0153958460c3d141f04abc5c2e/go.mod).

**Риски интеграции и обязательные проверки:**

- Рассматривается именно amneziawg-go, а не весь Amnezia client или kernel implementation с иной лицензионной областью.
- README называет upstream fork WireGuard-Go; замена внешних байтов не доказывает новизну или camouflage safety VLP.
- Проверить сохранение copyright/notices, транзитивные зависимости и допустимость переноса Go/device code в выбранную архитектуру.
- Обещания DPI-resistance не принимаются без воспроизводимых испытаний по собственной threat model.

**Дополнительные наблюдения:**

- Наблюдаемое module path github.com/amnezia-vpn/amneziawg-go/v3 и go 1.25.0; root LICENSE сохраняет copyright WireGuard LLC.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-09-20T08:43:42Z`; [источник](https://api.github.com/repos/amnezia-vpn/amneziawg-go). Полный maintenance review и security assessment не завершены.

### OSS-016. wireguard-go

**Статус:** NOT_ADOPTED. **Классификация:** Reference / точечный reuse.

**Репозиторий:** [WireGuard/wireguard-go](https://github.com/WireGuard/wireguard-go).

**Наблюдаемая ревизия:** [`2631ce99a06f27120d581611cf125d68bc6aa565`](https://github.com/WireGuard/wireguard-go/commit/2631ce99a06f27120d581611cf125d68bc6aa565), branch `master`, commit time `2026-10-06T16:45:05Z`. Источник наблюдения: [GitHub branch API](https://api.github.com/repos/WireGuard/wireguard-go/branches/master). Это не dependency pin.

**Предлагаемая роль:** Reference userspace WireGuard, ограничения системной интеграции и жизненного цикла туннеля; не универсальная библиотека собственного VLP wire format.

**Лицензия:** MIT. Прочитанные основания: [LICENSE](https://github.com/WireGuard/wireguard-go/blob/2631ce99a06f27120d581611cf125d68bc6aa565/LICENSE).

**Технические источники:** [README.md](https://github.com/WireGuard/wireguard-go/blob/2631ce99a06f27120d581611cf125d68bc6aa565/README.md); [go.mod](https://github.com/WireGuard/wireguard-go/blob/2631ce99a06f27120d581611cf125d68bc6aa565/go.mod).

**Риски интеграции и обязательные проверки:**

- GitHub repository обозначен как mirror; перед выбором версии сверять provenance с официальным upstream git.zx2c4.com.
- Перенос handshake/device/packet частей может сохранить семантику WireGuard; новизна VLP не следует из форка.
- Лицензия именно wireguard-go не переносится автоматически на kernel WireGuard, tools и платформенные модули.
- Нужны review транзитивных зависимостей, системных привилегий, TUN lifecycle и целевых ОС.

**Дополнительные наблюдения:**

- Официальный upstream https://git.zx2c4.com/wireguard-go/ открыт; текущая запись фиксирует наблюдаемую GitHub mirror revision, а не подтверждённое равенство всех upstream refs.
- Наблюдаемое module path golang.zx2c4.com/wireguard.

**Сопровождение:** archived = `false`, последний push repository metadata — `2026-10-06T16:53:18Z`; [источник](https://api.github.com/repos/WireGuard/wireguard-go). Полный maintenance review и security assessment не завершены.

## Протокольные ориентиры для Research Gate

Эти документы — **reference**, а не автоматически принятые нормативные требования VLP. Их использование как источника идей не разрешает без проверки перенос code components или текстов; исходники стандартов и implementations имеют самостоятельные условия использования.

| ID | Первичный источник | Наблюдаемая редакция | Зачем сравнивать |
| --- | --- | --- | --- |
| BASE-001 | [Noise Protocol Framework](https://noiseprotocol.org/noise.html) | Revision 34, 2018-07-11; страница обозначена official/unstable | Сравнение authenticated key exchange и transcript binding. Framework не задаёт весь UDP transport VLP. |
| BASE-002 | [RFC 8446 — TLS 1.3](https://www.rfc-editor.org/rfc/rfc8446) | RFC 8446 | Контрольный стандарт handshake, key schedule, certificate authentication и ограничений early data. |
| BASE-003 | [RFC 9147 — DTLS 1.3](https://datatracker.ietf.org/doc/html/rfc9147) | RFC 9147 | Контрольный защищённый datagram channel: record epochs, replay handling и handshake retransmission. |
| BASE-004 | [RFC 9000 — QUIC Transport](https://www.rfc-editor.org/rfc/rfc9000) | RFC 9000 | Сравнение packet numbers, streams, connection migration, path validation и ограничения amplification. |
| BASE-005 | [RFC 9001 — Using TLS to Secure QUIC](https://datatracker.ietf.org/doc/html/rfc9001) | RFC 9001 | Изучение отдельной TLS/QUIC интеграции; это не готовая схема TLS records поверх произвольного UDP. |
| BASE-006 | [RFC 9002 — QUIC Loss Detection and Congestion Control](https://www.rfc-editor.org/rfc/rfc9002) | RFC 9002 | Baseline recovery, RTT/PTO, congestion control и различения packet retransmission от логической доставки. |
| BASE-007 | [RFC 9221 — QUIC DATAGRAM](https://www.rfc-editor.org/rfc/rfc9221) | RFC 9221 | Сравнение ненадёжных сообщений с QUIC streams для carrier; смысл reliability должен задаваться явно. |
| BASE-008 | [RFC 8445 — ICE](https://www.rfc-editor.org/rfc/rfc8445) | RFC 8445 | Ориентир NAT traversal для возможного отдельного P2P-сценария; P2P не утверждён как обязательная функция VLP. |
| BASE-009 | [RFC 8489 — STUN](https://www.rfc-editor.org/rfc/rfc8489) | RFC 8489 | Ориентир STUN transaction processing; не замена data plane и его аутентификации. |
| BASE-010 | [RFC 8656 — TURN](https://www.rfc-editor.org/rfc/rfc8656) | RFC 8656 | Ориентир relay allocation, permission и lifetime при принятии relay-сценария. |
| BASE-011 | [NIST FIPS 203 — ML-KEM](https://csrc.nist.gov/pubs/fips/203/final) | FIPS 203, Final publication 2024-08-13; профиль VLP не задан | Стандарт KEM для отдельного PQ research; наличие KEM не даёт готового authenticated hybrid handshake. |
| BASE-012 | [WireGuard — Protocol & Cryptography](https://www.wireguard.com/protocol/) | Веб-страница наблюдалась 2026-10-19; immutable revision не предоставлена | Первичный protocol reference для handshake, dataplane и сопоставления с userspace implementation. |

## Что требуется до принятия зависимости

- Выбрать архитектурную роль и показать, какую задачу компонент закрывает без дублирования других слоёв.
- Прочитать лицензии выбранной версии и конкретных включаемых файлов, copyright/NOTICE, component exceptions и транзитивных зависимостей; проверить предполагаемые изменения и распространение.
- Проверить release provenance, policy сопровождения, advisories и открытые ограничения; отсутствие обнаруженной проблемы не считать независимым аудитом.
- Согласовать language/runtime, target OS/architecture, toolchain, crypto provider и разрешённые features.
- После разрешения реализации выбрать release/revision, создать реальный dependency manifest/lockfile и затем SBOM по фактической сборке.
- Проверить interoperability, resource bounds и protocol invariants в разрешённой тестовой среде; не выводить безопасность VLP из репутации upstream.

**Переход к реализации требует отдельного разрешения после Research Gate и проверки спецификаций.** Каталог не закрывает Research Gate и не является результатом security audit.

