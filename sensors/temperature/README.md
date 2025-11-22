# Sensor de Temperatura

## Hardware

- **ESP32**: Microcontrolador principal
- **DHT22**: Sensor de temperatura e umidade
- **Conexão**: Pino digital do ESP32

## Funcionamento

1. Leitura contínua dos dados do sensor DHT22
2. Processamento local dos valores de temperatura e umidade
3. Envio dos dados via MQTT para o servidor Node-RED

## Comunicação MQTT

### Tópico
```
iot/unisinos/temperatura
```

### Formato JSON
```json
{
  "ambiente_id": "sala",
  "temperatura": 25.5,
  "umidade": 60.2,
  "timestamp": "2024-01-01T12:00:00Z"
}
```

### Parâmetros
- **ambiente_id**: Identificador único do ambiente monitorado
- **temperatura**: Valor em graus Celsius
- **umidade**: Percentual de umidade relativa
- **timestamp**: Data/hora da leitura no formato ISO 8601

## Integração com Node-RED

O servidor Node-RED:
1. Recebe os dados via MQTT
2. Aplica regras configuráveis de temperatura (padrão: >35°C ou <10°C)
3. Aciona automaticamente o ar condicionado quando necessário
4. Envia notificações para familiares em casos extremos

## Configuração

### Bibliotecas Necessárias
- WiFi
- PubSubClient (MQTT)
- DHT sensor library
