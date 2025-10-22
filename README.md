# Zabbix Template – SolarEdge SE17K (Modbus + Telegraf)

Template completo para monitoramento de inversores **SolarEdge SE17K** utilizando **Modbus TCP** com coleta via **Telegraf** (input Prometheus) e integração com o **Zabbix**.

O objetivo é fornecer visibilidade completa da performance do inversor solar, eficiência energética, tensão/corrente AC e DC, temperatura e condições operacionais, com alertas pré-configurados e macros ajustáveis.

---

## 🧩 Estrutura do Template

**Nome no Zabbix:** `Template SolarEdge SE17K - Prometheus e telegraf`  
**Grupo:** `Inversores`  
**Coleta de dados:** `HTTP Agent` (Telegraf Prometheus endpoint)

### 🔍 Principais Métricas Monitoradas

| Categoria | Item | Unidade | Descrição |
|------------|------|----------|------------|
| **AC** | `ac.power.w` | W | Potência AC total (ajustada pelo scaling factor) |
| | `ac.v12.v`, `ac.v23.v`, `ac.v31.v` | V | Tensões entre fases |
| | `ac.freq.hz` | Hz | Frequência da rede |
| **DC** | `dc.power.w`, `dc.current.a`, `dc.voltage.v` | W / A / V | Potência, corrente e tensão DC do inversor |
| **Energia** | `energy.total.wh` | Wh | Energia total acumulada |
| | `ac.energy.today.v` | kWh | Produção do dia (calculada) |
| **Temperatura** | `inv.temp.c`, `inv.temp.f` | °C / °F | Temperatura interna do inversor |
| **Status** | `i.status` | - | Estado do inversor (Off, MPPT, Fault, etc.) |
| **Eficiência** | `sum.ac.power.raw.sf / dc.power.w` | % | Relação AC/DC calculada com alarmes configuráveis |

---

## ⚙️ Pré-requisitos

1. **Telegraf** configurado com o input `modbus` e o output `prometheus_client`.
2. Endpoint Prometheus disponível (exemplo):  
