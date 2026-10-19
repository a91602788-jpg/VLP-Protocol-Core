# Requirements and research-topic register

**220 source topics · 7 engineering cores · 220 OPEN records**

The owner-provided list is preserved as `VLP-REQ-001` through `VLP-REQ-220`. Its 14 subject groups and the seven engineering cores are different views of the work. All original numbers and Russian titles remain available; English titles support international review.

These entries are topics to investigate, refine, and decide. They are not 220 approved normative requirements, an implementation checklist for one release, or completed work. A primary core coordinates a topic; other cores can contribute. Related IDs indicate overlap, not equivalence.

[Machine-readable register](requirements.json) · [Engineering cores](../architecture/engineering-cores.md) · [Decision process](../process/decision-process.md) · [Specification index](../specifications/README.md)

## How to close a topic

Record the selected semantics or explicit disposition, a reviewed decision reference, primary evidence, affected specification sections, validation obligations, and remaining risks. Deferral or exclusion needs a reason and must preserve the ID. No row is closed in this foundation change. A planned test is not a passed test.

Before normative specification work, resolve alternatives such as native UDP versus an existing transport, authentication modes, optional carriers, P2P, multipath, early data, and post-quantum requirements. Source wording such as “retransmission of packets” or “frame and packet encryption” must be clarified, not mechanically implemented.

## Core legend

| Core | Responsibility owner |
| --- | --- |
| 01 | Protocol Core |
| 02 | Transport |
| 03 | Cryptography |
| 04 | Handshake |
| 05 | Camouflage |
| 06 | Data Plane |
| 07 | Security |

## Planning-track legend

| Track | Meaning |
| --- | --- |
| R | Research a required design topic; no design or implementation is approved. |
| D | Evaluate alternatives or optional capabilities and record the scope decision. |
| I | Specify the property now; implementation work remains behind its approval gate. |
| V | Plan evidence now; execute only at the authorized stage and record actual results. |
| S | Track document coverage; formal specifications follow the Research Gate. |

Tracks are provisional organization labels. They do not grant approval, change the threat model, or remove any source topic from consideration. All records currently have status `OPEN`.

## 01. Architecture

Архитектура протокола (Core) · source topics 1–12.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-001 | Назначение протокола и сценарии использования. | Protocol purpose and use cases. | 01 | R |
| VLP-REQ-002 | Самостоятельный протокол или расширение существующего транспорта. | Independent protocol or extension of an existing transport. | 01 | D |
| VLP-REQ-003 | Модель взаимодействия клиент — сервер — узел — узел. | Client-server and node-to-node interaction model. | 01 | D |
| VLP-REQ-004 | Одноранговые (P2P) соединения. | Peer-to-peer connections. | 01 | D |
| VLP-REQ-005 | Архитектура Control Plane и Data Plane. | Control Plane and Data Plane architecture. | 01 | R |
| VLP-REQ-006 | Машина состояний соединения. | Connection state machine. | 01 | R |
| VLP-REQ-007 | Формат пакетов (Wire Format). | Packet wire format. | 01 | R |
| VLP-REQ-008 | Типы сообщений и их назначение. | Message types and their purpose. | 01 | R |
| VLP-REQ-009 | Управление сессиями. | Session management. | 01 | R |
| VLP-REQ-010 | Версионирование протокола. | Protocol versioning. | 01 | R |
| VLP-REQ-011 | Расширяемость и совместимость версий. | Extensibility and version compatibility. | 01 | R |
| VLP-REQ-012 | Согласование возможностей сторон. | Peer capability negotiation. | 01 | R |

## 02. Transport Layer

Transport Layer — транспорт · source topics 13–30.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-013 | Передача поверх UDP. | Transport over UDP. | 02 | D |
| VLP-REQ-014 | Передача поверх TCP. | Transport over TCP. | 02 | D |
| VLP-REQ-015 | Собственный механизм надёжной доставки поверх UDP. | A protocol-specific reliable-delivery mechanism over UDP. | 02 | D |
| VLP-REQ-016 | Поддержка потоков (Streams). | Stream support. | 02 | D |
| VLP-REQ-017 | Поддержка датаграмм (Datagrams). | Datagram support. | 02 | D |
| VLP-REQ-018 | Мультиплексирование соединений. | Connection multiplexing. | 02 | D |
| VLP-REQ-019 | Управление потоком (Flow Control). | Flow control. | 02 | R |
| VLP-REQ-020 | Управление перегрузкой (Congestion Control). | Congestion control. | 02 | R |
| VLP-REQ-021 | Повторная передача потерянных пакетов. | Retransmission of lost packets. | 02 | R |
| VLP-REQ-022 | Контроль порядка доставки. | Delivery ordering. | 02 | R |
| VLP-REQ-023 | Обнаружение потерь. | Loss detection. | 02 | R |
| VLP-REQ-024 | Управление MTU и размером пакетов. | MTU and packet-size management. | 02 | R |
| VLP-REQ-025 | Фрагментация и сборка данных. | Data fragmentation and reassembly. | 02 | D |
| VLP-REQ-026 | Миграция соединения между сетями. | Connection migration between networks. | 02 | D |
| VLP-REQ-027 | NAT Traversal. | NAT traversal. | 02 | D |
| VLP-REQ-028 | Multipath — несколько сетевых путей. | Multipath support. | 02 | D |
| VLP-REQ-029 | Keepalive и определение доступности. | Keepalive and reachability detection. | 02 | R |
| VLP-REQ-030 | Управление задержками, джиттером и пропускной способностью. | Latency, jitter, and bandwidth management. | 02 | R |

## 03. Cryptography

Cryptography — шифрование · source topics 31–52.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-031 | Модель криптографической защиты. | Cryptographic protection model. | 03 | D |
| VLP-REQ-032 | Выбор проверенных криптографических алгоритмов. | Selection of established cryptographic algorithms. | 03 | D |
| VLP-REQ-033 | Симметричное шифрование. | Symmetric encryption. | 03 | R |
| VLP-REQ-034 | Асимметричная криптография. | Asymmetric cryptography. | 03 | D |
| VLP-REQ-035 | AEAD — шифрование с проверкой подлинности. | Authenticated encryption with associated data. | 03 | R |
| VLP-REQ-036 | Обмен ключами (Key Exchange). | Key exchange. | 03 | D |
| VLP-REQ-037 | ECDH / ECDHE. | ECDH and ECDHE. | 03 | D |
| VLP-REQ-038 | HKDF и получение производных ключей. | HKDF and key derivation. | 03 | R |
| VLP-REQ-039 | Forward Secrecy. | Forward secrecy. | 03 | R |
| VLP-REQ-040 | Post-Compromise Security — восстановление защищённости после компрометации. | Post-compromise security. | 03 | D |
| VLP-REQ-041 | Post-Quantum Cryptography. | Post-quantum cryptography. | 03 | D |
| VLP-REQ-042 | Гибридный классический и постквантовый обмен ключами. | Hybrid classical and post-quantum key exchange. | 03 | D |
| VLP-REQ-043 | Ротация ключей (Key Rotation). | Key rotation. | 03 | R |
| VLP-REQ-044 | Разделение ключей по направлениям передачи. | Directional key separation. | 03 | R |
| VLP-REQ-045 | Управление Nonce и IV. | Nonce and IV management. | 03 | R |
| VLP-REQ-046 | Защита от повторного использования Nonce. | Nonce-reuse prevention. | 03 | R |
| VLP-REQ-047 | Криптографическая случайность. | Cryptographic randomness. | 03 | I |
| VLP-REQ-048 | Domain Separation. | Domain separation. | 03 | R |
| VLP-REQ-049 | Шифрование полезной нагрузки. | Payload encryption. | 03 | R |
| VLP-REQ-050 | Защита метаданных и заголовков. | Metadata and header protection. | 03 | R |
| VLP-REQ-051 | Контроль целостности сообщений. | Message integrity. | 03 | R |
| VLP-REQ-052 | Безопасное уничтожение ключевого материала. | Secure destruction of key material. | 03 | I |

## 04. Handshake

Handshake — установка соединения · source topics 53–68.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-053 | Собственный протокол рукопожатия. | Protocol-specific handshake. | 04 | D |
| VLP-REQ-054 | Взаимная аутентификация сторон. | Mutual authentication. | 04 | D |
| VLP-REQ-055 | Подтверждение владения ключами. | Proof of key possession. | 04 | R |
| VLP-REQ-056 | Односторонняя и двусторонняя аутентификация. | One-way and mutual authentication modes. | 04 | D |
| VLP-REQ-057 | PSK / Public Key / Certificate Authentication. | PSK, public-key, and certificate authentication. | 04 | D |
| VLP-REQ-058 | Согласование криптографических алгоритмов. | Cryptographic algorithm negotiation. | 04 | D |
| VLP-REQ-059 | Защита согласования параметров от подмены. | Integrity of parameter negotiation. | 04 | R |
| VLP-REQ-060 | Защита от Downgrade Attack. | Downgrade-attack resistance. | 04 | R |
| VLP-REQ-061 | Защита от MITM. | Man-in-the-middle resistance. | 04 | R |
| VLP-REQ-062 | Защита от Replay Attack. | Replay-attack resistance. | 04 | R |
| VLP-REQ-063 | 0-RTT / 1-RTT с учётом рисков повторного воспроизведения. | 0-RTT and 1-RTT with replay risks considered. | 04 | D |
| VLP-REQ-064 | Session Resumption. | Session resumption. | 04 | D |
| VLP-REQ-065 | Защита начального обмена. | Initial-exchange protection. | 04 | R |
| VLP-REQ-066 | Минимизация раскрываемых данных до аутентификации. | Minimization of pre-authentication disclosure. | 04 | R |
| VLP-REQ-067 | Защита от подмены идентичности. | Identity-impersonation resistance. | 04 | R |
| VLP-REQ-068 | Тайм-ауты и безопасное завершение Handshake. | Handshake timeouts and safe termination. | 04 | R |

## 05. Camouflage

Camouflage — маскировка · source topics 69–87.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-069 | Маскировка структуры сетевого трафика. | Traffic-structure camouflage. | 05 | R |
| VLP-REQ-070 | Обфускация пакетов. | Packet obfuscation. | 05 | D |
| VLP-REQ-071 | Маскировка Handshake. | Handshake camouflage. | 05 | R |
| VLP-REQ-072 | Сокрытие характерных сигнатур протокола. | Reduction of characteristic protocol signatures. | 05 | R |
| VLP-REQ-073 | Уменьшение распознаваемости по размерам пакетов. | Reduction of packet-size fingerprinting. | 05 | R |
| VLP-REQ-074 | Packet Padding. | Packet padding. | 05 | R |
| VLP-REQ-075 | Адаптивный Padding. | Adaptive padding. | 05 | D |
| VLP-REQ-076 | Traffic Shaping. | Traffic shaping. | 05 | R |
| VLP-REQ-077 | Маскировка временных характеристик передачи. | Camouflage of transmission timing. | 05 | R |
| VLP-REQ-078 | Управление Burst-передачами. | Burst management. | 05 | R |
| VLP-REQ-079 | Рандомизация допустимых параметров протокола. | Randomization of permitted protocol parameters. | 05 | D |
| VLP-REQ-080 | Согласованность внешнего поведения с выбранным транспортом. | Consistency of observable behavior with the selected transport. | 05 | D |
| VLP-REQ-081 | Защита от пассивного Fingerprinting. | Passive-fingerprinting resistance. | 05 | R |
| VLP-REQ-082 | Устойчивость к активному Fingerprinting. | Active-fingerprinting resistance. | 05 | R |
| VLP-REQ-083 | Устойчивость к Active Probing. | Active-probing resistance. | 05 | R |
| VLP-REQ-084 | Анализ распознаваемости с помощью DPI. | DPI detectability analysis. | 05 | R |
| VLP-REQ-085 | Анализ статистического распознавания трафика. | Statistical traffic-classification analysis. | 05 | R |
| VLP-REQ-086 | Анализ корреляции входящих и исходящих потоков. | Incoming/outgoing traffic correlation analysis. | 05 | R |
| VLP-REQ-087 | Баланс маскировки, задержки и накладных расходов. | Camouflage, latency, and overhead trade-offs. | 05 | R |

## 06. Data Plane

Data Plane — передача данных · source topics 88–104.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-088 | Формат заголовков. | Header format. | 06 | R |
| VLP-REQ-089 | Идентификаторы соединений. | Connection identifiers. | 06 | R |
| VLP-REQ-090 | Идентификаторы потоков. | Stream identifiers. | 06 | R |
| VLP-REQ-091 | Packet Number. | Packet number. | 06 | R |
| VLP-REQ-092 | Sequence Number. | Sequence number. | 06 | R |
| VLP-REQ-093 | Frame Types. | Frame types. | 06 | R |
| VLP-REQ-094 | Packet Framing. | Packet framing. | 06 | R |
| VLP-REQ-095 | Шифрование отдельных фреймов и пакетов. | Frame-level and packet-level encryption. | 03 | D |
| VLP-REQ-096 | Механизм подтверждений ACK. | Acknowledgment mechanism. | 02 | R |
| VLP-REQ-097 | Обработка дубликатов. | Duplicate handling. | 06 | R |
| VLP-REQ-098 | Разделение данных и управляющих сообщений. | Separation of data and control messages. | 06 | R |
| VLP-REQ-099 | Приоритеты потоков. | Stream priorities. | 02 | R |
| VLP-REQ-100 | Ограничение буферизации. | Buffering limits. | 06 | R |
| VLP-REQ-101 | Backpressure. | Backpressure. | 06 | R |
| VLP-REQ-102 | Передача больших объёмов данных. | Bulk data transfer. | 06 | R |
| VLP-REQ-103 | Передача небольших сообщений. | Small-message transfer. | 06 | R |
| VLP-REQ-104 | Работа с нестабильными соединениями. | Operation over unstable connections. | 02 | R |

## 07. Security

Security — защита протокола · source topics 105–125.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-105 | Threat Model — модель угроз. | Threat model. | 07 | R |
| VLP-REQ-106 | Защита от MITM. | Man-in-the-middle resistance. | 07 | R |
| VLP-REQ-107 | Replay Protection. | Replay protection. | 07 | R |
| VLP-REQ-108 | Anti-Replay Window. | Anti-replay window. | 07 | R |
| VLP-REQ-109 | Защита от подмены пакетов. | Packet-forgery resistance. | 07 | R |
| VLP-REQ-110 | Защита от изменения порядка сообщений, если это критично. | Protection of message ordering where required. | 07 | R |
| VLP-REQ-111 | Защита от Session Hijacking. | Session-hijacking resistance. | 07 | R |
| VLP-REQ-112 | Защита от Connection Injection. | Connection-injection resistance. | 07 | R |
| VLP-REQ-113 | Защита от Downgrade. | Downgrade resistance. | 07 | R |
| VLP-REQ-114 | Защита от Reflection и Amplification. | Reflection and amplification resistance. | 07 | R |
| VLP-REQ-115 | Защита от DoS на уровне протокола. | Protocol-level denial-of-service resistance. | 07 | R |
| VLP-REQ-116 | Rate Limiting до аутентификации. | Pre-authentication rate limiting. | 07 | R |
| VLP-REQ-117 | Ограничение расходования CPU и памяти. | CPU and memory limits. | 07 | R |
| VLP-REQ-118 | Защита от исчерпания состояния сессий. | Session-state exhaustion resistance. | 07 | R |
| VLP-REQ-119 | Защита от Timing Side Channels. | Timing side-channel resistance. | 07 | I |
| VLP-REQ-120 | Защита от ошибок криптографической реализации. | Prevention of cryptographic implementation errors. | 07 | I |
| VLP-REQ-121 | Безопасное поведение при сбоях (Fail Closed). | Fail-closed behavior. | 07 | R |
| VLP-REQ-122 | Изоляция контекстов и сессий. | Context and session isolation. | 07 | R |
| VLP-REQ-123 | Защита от некорректных и специально сформированных пакетов. | Malformed and adversarial packet handling. | 07 | R |
| VLP-REQ-124 | Предотвращение утечек через сообщения об ошибках. | Prevention of error-message leakage. | 07 | R |
| VLP-REQ-125 | Безопасное восстановление после разрыва соединения. | Safe recovery after disconnection. | 07 | R |

## 08. Privacy

Privacy — конфиденциальность · source topics 126–136.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-126 | Минимизация открытых метаданных. | Minimization of exposed metadata. | 07 | R |
| VLP-REQ-127 | Сокрытие идентичности участников там, где это возможно. | Participant identity hiding where feasible. | 04 | R |
| VLP-REQ-128 | Защита идентификаторов соединений от отслеживания. | Reduction of connection-identifier tracking. | 07 | R |
| VLP-REQ-129 | Уменьшение возможностей связывания разных сессий. | Reduction of cross-session linkability. | 07 | R |
| VLP-REQ-130 | Защита от Traffic Analysis. | Traffic-analysis resistance. | 05 | R |
| VLP-REQ-131 | Защита от Session Correlation. | Session-correlation resistance. | 05 | R |
| VLP-REQ-132 | Устойчивость к пассивному наблюдению. | Passive-observation resistance. | 05 | R |
| VLP-REQ-133 | Управление раскрытием адресов назначения. | Control of destination-address disclosure. | 07 | R |
| VLP-REQ-134 | Политика обработки DNS, если протокол передаёт имена. | DNS handling policy when names are carried. | 07 | D |
| VLP-REQ-135 | Минимизация долговременных идентификаторов. | Minimization of long-lived identifiers. | 07 | R |
| VLP-REQ-136 | Устранение утечек через управляющие пакеты. | Prevention of control-packet leakage. | 07 | R |

## 09. Connection Management

Connection Management — управление соединением · source topics 137–148.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-137 | Создание соединения. | Connection creation. | 01 | R |
| VLP-REQ-138 | Аутентификация нового соединения. | Authentication of a new connection. | 04 | R |
| VLP-REQ-139 | Повторное подключение. | Reconnection. | 01 | R |
| VLP-REQ-140 | Восстановление сессии. | Session recovery. | 04 | D |
| VLP-REQ-141 | Тайм-ауты неактивности. | Idle timeouts. | 02 | R |
| VLP-REQ-142 | Heartbeat / Keepalive. | Heartbeat and keepalive. | 02 | R |
| VLP-REQ-143 | Обнаружение смены IP-адреса. | IP-address change detection. | 02 | R |
| VLP-REQ-144 | Смена сетевого маршрута. | Network-path change. | 02 | R |
| VLP-REQ-145 | Защита от подмены адреса при миграции. | Address-spoofing resistance during migration. | 07 | R |
| VLP-REQ-146 | Завершение соединения. | Connection termination. | 01 | R |
| VLP-REQ-147 | Обработка одностороннего разрыва. | One-sided disconnection handling. | 01 | R |
| VLP-REQ-148 | Обработка потери пакетов и недоступности узла. | Packet loss and peer unavailability handling. | 02 | R |

## 10. Performance

Performance — производительность · source topics 149–162.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-149 | Минимизация Handshake RTT. | Handshake round-trip minimization. | 04 | R |
| VLP-REQ-150 | Минимизация Packet Overhead. | Packet overhead minimization. | 02 | R |
| VLP-REQ-151 | Минимизация криптографических накладных расходов. | Cryptographic overhead minimization. | 03 | R |
| VLP-REQ-152 | Оптимизация обработки пакетов. | Packet-processing optimization. | 06 | I |
| VLP-REQ-153 | Zero-Copy как возможность реализации. | Zero-copy as an implementation option. | 06 | I |
| VLP-REQ-154 | Работа на слабом оборудовании. | Operation on resource-constrained hardware. | 06 | I |
| VLP-REQ-155 | Работа в мобильных сетях. | Operation on mobile networks. | 02 | R |
| VLP-REQ-156 | Работа при высокой задержке. | Operation on high-latency networks. | 02 | R |
| VLP-REQ-157 | Работа при потере пакетов. | Operation under packet loss. | 02 | R |
| VLP-REQ-158 | Работа в сетях с низкой пропускной способностью. | Operation on low-bandwidth networks. | 02 | R |
| VLP-REQ-159 | Оптимизация мультиплексирования. | Multiplexing optimization. | 06 | I |
| VLP-REQ-160 | Справедливость распределения пропускной способности. | Bandwidth-allocation fairness. | 02 | R |
| VLP-REQ-161 | Энергозатраты протокола. | Protocol energy cost. | 02 | I |
| VLP-REQ-162 | Масштабируемость по количеству соединений. | Connection-count scalability. | 06 | I |

## 11. Protocol Evolution

Protocol Evolution — развитие · source topics 163–173.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-163 | Независимое версионирование Wire Format. | Independent wire-format versioning. | 01 | D |
| VLP-REQ-164 | Обратная совместимость. | Backward compatibility. | 01 | D |
| VLP-REQ-165 | Расширения протокола. | Protocol extensions. | 01 | D |
| VLP-REQ-166 | Регистрация типов сообщений. | Message-type registration. | 01 | R |
| VLP-REQ-167 | Согласование расширений. | Extension negotiation. | 01 | R |
| VLP-REQ-168 | Криптографическая гибкость без небезопасного Downgrade. | Cryptographic agility without unsafe downgrade. | 03 | D |
| VLP-REQ-169 | Удаление устаревших алгоритмов. | Removal of obsolete algorithms. | 03 | D |
| VLP-REQ-170 | Зарезервированные поля и коды. | Reserved fields and code points. | 01 | R |
| VLP-REQ-171 | Обработка неизвестных типов сообщений. | Unknown-message handling. | 01 | R |
| VLP-REQ-172 | Формальное описание состояний. | Formal state description. | 01 | R |
| VLP-REQ-173 | Совместимость независимых реализаций. | Compatibility of independent implementations. | 01 | R |

## 12. Reliability

Reliability — устойчивость · source topics 174–184.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-174 | Корректность при потере пакетов. | Correctness under packet loss. | 02 | R |
| VLP-REQ-175 | Корректность при дублировании пакетов. | Correctness under packet duplication. | 02 | R |
| VLP-REQ-176 | Корректность при изменении порядка. | Correctness under reordering. | 02 | R |
| VLP-REQ-177 | Корректность при частичной доставке. | Correctness under partial delivery. | 02 | R |
| VLP-REQ-178 | Обработка повреждённых сообщений. | Corrupted-message handling. | 07 | R |
| VLP-REQ-179 | Восстановление после сетевого сбоя. | Recovery after network failure. | 02 | R |
| VLP-REQ-180 | Защита от бесконечных циклов повторной передачи. | Prevention of unbounded retransmission loops. | 02 | R |
| VLP-REQ-181 | Ограничение очередей. | Queue limits. | 06 | R |
| VLP-REQ-182 | Контроль переполнения буферов. | Buffer-overflow control. | 07 | I |
| VLP-REQ-183 | Предсказуемая обработка ошибок. | Predictable error handling. | 01 | R |
| VLP-REQ-184 | Устойчивость при высокой нагрузке. | Resilience under high load. | 06 | R |

## 13. Protocol Validation

Protocol Validation — проверка протокола · source topics 185–200.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-185 | Сравнение с VLESS, Shadowsocks, Hysteria 2, WireGuard, AmneziaWG, QUIC, TLS 1.3 и Noise. | Comparison with VLESS, Shadowsocks, Hysteria 2, WireGuard, AmneziaWG, QUIC, TLS 1.3, and Noise. | 07 | V |
| VLP-REQ-186 | Формальная модель угроз. | Formal threat model. | 07 | V |
| VLP-REQ-187 | Криптографический анализ. | Cryptographic analysis. | 03 | V |
| VLP-REQ-188 | Формальная проверка Handshake. | Formal handshake verification. | 04 | V |
| VLP-REQ-189 | Анализ безопасности Wire Format. | Wire-format security analysis. | 06 | V |
| VLP-REQ-190 | Проверка машин состояний. | State-machine verification. | 01 | V |
| VLP-REQ-191 | Тестирование на Replay и Downgrade. | Replay and downgrade testing. | 07 | V |
| VLP-REQ-192 | Fuzz Testing парсера пакетов. | Packet-parser fuzz testing. | 06 | V |
| VLP-REQ-193 | Property-Based Testing. | Property-based testing. | 01 | V |
| VLP-REQ-194 | Interoperability Testing. | Interoperability testing. | 01 | V |
| VLP-REQ-195 | Наборы тестовых векторов. | Test-vector sets. | 03 | V |
| VLP-REQ-196 | Анализ устойчивости к DPI. | DPI-resistance analysis. | 05 | V |
| VLP-REQ-197 | Анализ обнаруживаемости сетевого поведения. | Network-behavior detectability analysis. | 05 | V |
| VLP-REQ-198 | Нагрузочные испытания. | Load testing. | 06 | V |
| VLP-REQ-199 | Измерение задержки, скорости и потерь. | Latency, throughput, and loss measurement. | 02 | V |
| VLP-REQ-200 | Анализ безопасности независимыми специалистами. | Independent specialist security analysis. | 07 | V |

## 14. Specification

Specification — документация нового протокола · source topics 201–220.

| ID | Исходный пункт | English title | Core | Track |
| --- | --- | --- | --- | --- |
| VLP-REQ-201 | Architecture Specification. | Architecture specification. | 01 | S |
| VLP-REQ-202 | Threat Model. | Threat model document. | 07 | S |
| VLP-REQ-203 | Transport Specification. | Transport specification. | 02 | S |
| VLP-REQ-204 | Packet Wire Format. | Packet wire-format specification. | 06 | S |
| VLP-REQ-205 | Cryptographic Specification. | Cryptographic specification. | 03 | S |
| VLP-REQ-206 | Handshake Specification. | Handshake specification. | 04 | S |
| VLP-REQ-207 | Authentication Specification. | Authentication specification. | 04 | S |
| VLP-REQ-208 | Key Management Specification. | Key-management specification. | 03 | S |
| VLP-REQ-209 | Camouflage Specification. | Camouflage specification. | 05 | S |
| VLP-REQ-210 | Data Plane Specification. | Data-plane specification. | 06 | S |
| VLP-REQ-211 | Connection State Machine. | Connection state-machine specification. | 01 | S |
| VLP-REQ-212 | Congestion & Flow Control Specification. | Congestion and flow-control specification. | 02 | S |
| VLP-REQ-213 | Error Handling Specification. | Error-handling specification. | 01 | S |
| VLP-REQ-214 | Version Negotiation Specification. | Version-negotiation specification. | 04 | S |
| VLP-REQ-215 | Security Considerations. | Security considerations. | 07 | S |
| VLP-REQ-216 | Privacy Considerations. | Privacy considerations. | 07 | S |
| VLP-REQ-217 | Protocol Test Vectors. | Protocol test vectors. | 03 | S |
| VLP-REQ-218 | Interoperability Requirements. | Interoperability requirements. | 01 | S |
| VLP-REQ-219 | Performance Benchmarks. | Performance benchmarks. | 02 | S |
| VLP-REQ-220 | Security Audit Requirements. | Security-audit requirements. | 07 | S |

## Clarifications requiring explicit decisions

The following clarifications preserve the original wording and make the review question explicit. They are not approved protocol behavior.

- **VLP-REQ-002:** A protocol over QUIC can still be a distinct protocol. A native UDP transport adds responsibilities and needs a recorded justification.
- **VLP-REQ-003:** Define roles, trust boundaries, relays, and key-termination endpoints; node-to-node interaction is not automatically a P2P topology.
- **VLP-REQ-004:** P2P is a scope candidate; discovery, admission, NAT traversal, relay fallback, and peer privacy need a joint decision.
- **VLP-REQ-014:** TCP carriage requires an explicit mapping of stream/datagram semantics and a review of head-of-line blocking and fallback policy.
- **VLP-REQ-015:** If an existing reliable carrier is selected, justify any additional reliability layer instead of duplicating it automatically.
- **VLP-REQ-018:** Distinguish multiplexed application channels from separate transport connections; ownership and limits must remain explicit.
- **VLP-REQ-021:** The original wording is preserved. Resending a cached, byte-identical encoded packet is distinct from encrypting a new packet. A new AEAD encryption must satisfy the selected construction's nonce-uniqueness rules, even when the plaintext is unchanged; changing authenticated headers does not permit reuse of the same key/nonce pair. Specify how retransmitted logical data receives fresh packet numbers and nonces.
- **VLP-REQ-025:** Bound fragment count, total reassembly memory, lifetime, and pre-authentication work. Decide whether fragmentation is required for the selected IP profile.
- **VLP-REQ-027:** NAT rebinding, hole punching, ICE-style traversal, discovery, and relays are different mechanisms; select only the applicable ones.
- **VLP-REQ-028:** Separate migration with one active path from simultaneous multipath; review congestion fairness and packet-number/key contexts.
- **VLP-REQ-039:** State whose compromise is considered, when it occurs, which data is protected, and which secrets must have been erased.
- **VLP-REQ-040:** A one-way update derived from a compromised traffic secret does not by itself restore secrecy. Specify attacker access, fresh secret contributions, and identity-key recovery.
- **VLP-REQ-041:** A post-quantum primitive does not imply an authenticated post-quantum protocol. Evaluate the complete profile and its threat assumptions.
- **VLP-REQ-042:** Review the exact hybrid construction, transcript binding, identity authentication, confirmation, size, and fragmentation requirements.
- **VLP-REQ-045:** Nonce namespaces must account for directions, generations, retries, paths, restarts, and snapshot restoration.
- **VLP-REQ-046:** No network failure, migration, or restored snapshot may silently reset a counter under a reused key.
- **VLP-REQ-052:** Specify implementation and platform limits; do not promise universal erasure of registers, copies, swap, or crash dumps.
- **VLP-REQ-053:** A protocol-specific handshake specification may integrate an existing reviewed construction; this is not a requirement to invent new cryptography.
- **VLP-REQ-054:** Record whether mutual authentication is mandatory for the initial use case, rather than assuming that every optional mode is equivalent.
- **VLP-REQ-056:** Authentication modes are alternatives requiring explicit policy. A failed stronger mode must not silently select a weaker mode.
- **VLP-REQ-057:** Separate PSKs, identifiers, public keys, certificates, enrollment credentials, and authorization; one mode need not support all others.
- **VLP-REQ-058:** Keep the mandatory initial profile small and bind any negotiation to authenticated context.
- **VLP-REQ-063:** Early application data is a scope decision with replay and side-effect analysis; planning 0-RTT is not permission to enable it.
- **VLP-REQ-064:** Define ticket/key lifecycle, peer identity, replay handling, expiry, and multi-node state before introducing resumption.
- **VLP-REQ-070:** Obfuscation is not payload confidentiality, authentication, or evidence of indistinguishability.
- **VLP-REQ-079:** Randomize only permitted values. Authentication, parse bounds, protocol invariants, and negotiated minimum policy still apply.
- **VLP-REQ-080:** A native UDP format with a similar prefix is not a standards-compliant HTTP/3 carrier. Specify each profile honestly.
- **VLP-REQ-086:** State observer placement and capabilities; a successful classifier experiment does not establish global unlinkability.
- **VLP-REQ-087:** Count padding, headers, control traffic, and retransmissions in applicable network and resource budgets.
- **VLP-REQ-091:** A packet number is distinct from a stream offset or message ID; define its scope and authenticated interpretation.
- **VLP-REQ-092:** Define sequence-number purpose and namespace; do not introduce a redundant counter without a semantic need.
- **VLP-REQ-095:** Frame-level and packet-level protection are design alternatives or explicitly composed layers, not a requirement for redundant encryption.
- **VLP-REQ-096:** Transport acknowledgment does not prove application processing or exactly-once execution across reconnections.
- **VLP-REQ-099:** A client-provided priority is a request. The enforcing peer determines its allowed class and resource share.
- **VLP-REQ-110:** Ordering is required only for the negotiated semantics; an unreliable datagram profile must not silently become a reliable stream.
- **VLP-REQ-114:** Validate return reachability and bound responses; account for retry and camouflage bytes before authentication.
- **VLP-REQ-121:** Security-policy failure must not disable authentication. Dropping one unauthenticated forged packet must not let an outsider terminate a valid session.
- **VLP-REQ-125:** Recovery must preserve identity and authorization and avoid restoring traffic secrets with lost nonce/replay state.
- **VLP-REQ-127:** Specify identity-disclosure properties for each handshake flight, including future compromise of long-lived keys.
- **VLP-REQ-128:** Connection IDs route packets; possession of an ID is not authentication. Rotation alone does not remove all linkability.
- **VLP-REQ-134:** If names are carried, decide who resolves them, trust and egress policy, destination disclosure, and handling of address changes.
- **VLP-REQ-140:** Distinguish application recovery, reconnection, transport resumption, and restore from a local snapshot.
- **VLP-REQ-149:** Measure cryptographic establishment separately from channel acceptance and application readiness.
- **VLP-REQ-153:** Zero-copy is an implementation option, not a wire-level security or correctness guarantee.
- **VLP-REQ-163:** A separate wire-version scheme is a candidate; minimize independent version axes and bind compatibility negotiation.
- **VLP-REQ-164:** Compatibility must not keep a prohibited security mode usable after retirement.
- **VLP-REQ-168:** Algorithm agility requires authenticated negotiation and a clear minimum policy; it is not trial-and-error fallback.
- **VLP-REQ-171:** Differentiate ignorable extensions from mandatory unknown semantics and bound parsing work.
- **VLP-REQ-185:** Compare like-for-like functions and configurations: proxy protocols, transports, cryptographic frameworks, and applications are different layers.
- **VLP-REQ-195:** Later vectors must be synthetic, versioned, and cover negative cases; a vector file is not a completed independent audit.
- **VLP-REQ-200:** Record reviewer identity, independence, scope, revision, findings, and limitations. Author self-review is not an independent audit.
- **VLP-REQ-217:** Only publish actual generated or independently derived vectors after the applicable approved work; no placeholder output may look like a passed vector.
- **VLP-REQ-219:** Publish reproducible conditions, baselines, useful throughput, latency percentiles, overhead, and uncertainty; no benchmark has run at this stage.

## Updating this register

Keep the JSON and this readable view in the same change. Preserve source numbers and Russian titles; add clarifications rather than overwriting source intent. Record decisions and evidence only when they exist. New requirements receive new IDs through maintainer review and do not renumber 001–220.
