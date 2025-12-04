# Sensor de Luz e Movimento

## Hardware

- **ESP32**: Microcontrolador principal
- **PIR**: Sensor de movimento (detecção de presença)
- **LDR**: Fotoresistor para medir luminosidade

### Conexões
- PIR → GPIO 26
- LDR → GPIO 34 (ADC)

## Funcionamento

1. Leitura contínua do sensor PIR para detectar presença
2. Leitura do LDR para medir intensidade de luminosidade
3. Geração de um JSON com os valores atuais
4. Envio dos dados via MQTT para o servidor (ex.: Node-RED)

## Comunicação MQTT

### Tópico
```
iot/movimento/luz
```

### Formato JSON
```json
{
  "ambiente_id": "sala",
  "movimento": 1,
  "luz": 1234,
  "timestamp": "2024-01-01T12:00:00Z"
}
```

### Parâmetros
- **ambiente_id**: Nome do ambiente monitorado
- **movimento**: 1 = movimento detectado, 0 = sem movimento
- **luz**: Nível de luminosidade (0–4095)
- **timestamp**: Data/hora da leitura no formato ISO 8601

## Integração com Node-RED

O servidor Node-RED pode:
1. Receber dados via MQTT
2. Identificar ambientes escuros com presença detectada
3. Acionar iluminação automaticamente
4. Registrar histórico de luminosidade
5. Enviar alertas ou notificações
6. Criar dashboards com gráficos e indicadores

## Configuração

### Bibliotecas Necessárias
- WiFi
- PubSubClient (MQTT)

## Extensões Futuras

- Timestamp automático via NTP
- Envio apenas quando houver mudança nos valores
- Acionamento de lâmpadas com relé
- Dashboard completo no Node-RED
- Integração com sensor de temperatura
